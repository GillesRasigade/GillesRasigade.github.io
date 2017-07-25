# Metrics documentation

Today, metrics are sent with the following code:

```js
const metrics = require('chpr-metrics');

metrics.increment('hit.ride.ride_create');
```

The question is: how can we document this metrics in order to build Grafana
dashboards by a third part without any doubt ?

The following proposals are discussed:

## 1. Create a document `docs/metrics.md`

Key | Comment |
--- | --- |
`hit.ride.ride_create` | Sent each time the route `ride_create` on API-Node is called
`routine.${name}.failure` | Sent each time API-Node is answering with a status code higher or equal to 500 <br/> `name` is the operation name (ie. `ride_create`)

Notes:
- desynchronization between the current code implementation and the documentation
- already formated

## 2. Add a description in the metrics call

```js
const metrics = require('chpr-metrics');

metrics.increment('hit.ride.ride_create', 'The route `ride_create` has been called');
```

Notes:
- modify the overall metrics methods signatures
- hard to give complex description
- require a parser to consolidate all definitions

## 3. Add a jsdoc tag

Add a *jsdoc* tag above the metrics call

```js
const metrics = require('chpr-metrics');

/**
 * @metric
 * Sent each time API-Node is answering with a status code higher or equal to 500
 * - `name` is the operation name (ie. `ride_create`
 */
metrics.increment(`routine.${name}.failure`);
```

Notes:
- pptional so possibly not documented
- non obtrusive so the call is staying clean
- complex documentation is possible
- closer to the code so more reliable
- require a parser to consolidate all definitions

## 4. Other

Your proposal