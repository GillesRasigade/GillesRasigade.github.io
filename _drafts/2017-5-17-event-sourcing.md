---
layout: post
title: Practical Event Sourcing
---

## Principle

A command must be processed. This command is a transaction and when is finished, it produces one or several events. These events are stored into a reliable database and are the history of the overall system. Its state must be rebuilt from the events.

### Example - The marketplace

A marketplace is defined as a multi-actors transaction place. The sellers are offering crafts or services. The buyers are looking for such services and buy them.

Scenario: a buyer is buying a one place service. The critical part is the following,  a single place is available and two different users must not buy the service in same time.

In the near past, the seller created the service on the platform. This command inserted into a transaction compatible database an object with available quantity (ie. `quantiy=1`).

Two users are buying the  service in same time. The commands are handled by 2 different servers into different world locations (replications problem).

The database  request is:

```javascript
// Mongo
db.collection('services')
.findOneAndUpdate({
	service_id: "service_id",
	quantity: 1
}, {
	quantity: 0
}, {
	w: 'majority',
	wtimeout: 5000 // ms
});
```

The most important part is the atomic search and update. This is ensuring that 2 different processes can not decrease the document quantity in same time. One of them will lose. The Mongo write concerns `majority` is validating the replication and ensures that the document update has been replicated in a majority of replicas (and is thus the truth).

After these 2 commands, one will succeed, one will fail. Both of them will produce an event. A command always lead to at least one event: failure or success. The process is as following:

## Modelization

An event is a single document giving all necessary information about a past fact: Alice registerd, Alice booked a room, Bernard signed off, etc. The minimal document is thus of the following shape:

```json
{
	"type": "USER_REGISTERED",
	...
}
```

All the events attached to a user will have his own identification key:

```json
{
	"type": "USER_REGISTERED",
	"user_id": "user_id",
	...
}
```

An event attached to multiple objects must embed the ids:

```json
{
	"type": "SERVICE_BOUGHT",
	"service_id": "service_id",
	"buyer_id": "buyer_id",
	...
}
```

These definitions are allowing us to reduce these events into different collections, following the Event-Sourcing pattern.

## Reduction

The `events` are reduced into a single document. As the process is repeated each
time new events are stored into the database, how do we know which events have
to be reduced ?

The solution is versioning.

Each event reduction will lead to a unitary increment of the resulting document.
By consequence, each time an event is stored then reduced, the consolidated
document has his version incremented of 1.

The process is then:

1. Retrieve all events until the last reduction
2. Reduce each event on the state in the same order as they have been stored
3. Store the resulting document with incremented version only if the version in
   database is greater than or equal.

```javascript
/**
 * Main events reduction function (pure function)
 * @see http://redux.js.org/docs/introduction/ThreePrinciples.html
 *
 * @param {object} [state={ version: 0 }] The state to reduce events on
 * @param {number} state.version=0        The current state version
 * @param {object} event                  The event to reduce
 * @returns {object}
 */
function reduce(state = { version: 0 }, event) {
  state.version++;
  /**
   * Logical stuff here as well obviously !
   */
  return state;
}

/**
 * List of events to reduce from scratch
 */
const events = [
  { type: 'signin' },
  { type: 'update_profile' },
  { type: 'quote' },
  { type: 'order' }
]

let state;
for (const event of events) {
  state = reduce(state, event);
}

console.log('State restored from scratch\t', state);

// New events stored into the collection:
events.push({ type: 'pay' }, { type: 'signoff' });

// Reduce events from the last state version:
for (const event of events.slice(state.version)) {
  state = reduce(state, event);
}

console.log('State updated after new events\t', state);
```

## Snapshots

As you might guess, your `events` database will grow quickly with very little
atomic docummnts. These documents are volatile and are not supposed to exist for
a long time period (I mean several months).

In order to keep the Event-Sourcing process working, we have to build snapshots.
The events are reduced into consolidated or agregated documents. These last
documents can thus be rebuild from scratch thanks to the list of events present
into the `events` collection.

But if some events are removed, this history is changed and the resulting
consolidated documents as well. To keep track of partial states, we use snapshots
synced with events.

