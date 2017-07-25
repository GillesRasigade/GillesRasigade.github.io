---
layout: post
title: Generic market modelization
---

## Principle

The architecture must be error proof, meaning operational and programming. It has
critical and non critical domains. Non critical domains must wake up and resynchronize
to the critical domain state with no pain.

To be reliable, the services must be built with the same systemic approach: the
cell definition. A microservice or program is a cell in a many more complex system.
All its internal logic is unknown of the external world and only interfaces data
exchange can allow an observer to understand its composition.

What does compose a live world cell ? Multiplication ? Persistence ? etc.

The interface is as follow:

- a frontier between the external and internal world: the API
- specific receptors for specific molecules: the authentication + authorization
  mechanism.
- the ADN is the persistence strategy of the cell. How to keep persistence safe ?
  Replication mechanisms
- One component = one function

Questions to answer ?
- How to detect a service is unavailable ?
- How to know for how long a service will be unavailable ?
- What fallback strategy do we have in such situation ?
- How to keep exploitation strategy up to date with the Platform state ?

## Châssis:

- log
- metrics
- models definition: Event Sourcing first
- contracts definitions: commands, errors, events
- REST APi mapping
- tests
- linter

### Architecture:
- src/
  - config/
    index.js
  - helpers/
    - *List of already known helpers (mongodb, i18n, express, etc.)...*
    - mongodb
    - amqp
  - common/
    - constants/
    - schemas/
      - commands/
      - events/
  - models/
    - rider/
      - events.js
      - model.js
      - index.js
  - services/
    - *List of already known services definitions (sdk)*
    - gaia
    - driver-state
- test/
  - mocha.opts
  - index.js
- scripts/
  - commands/
    - index.js
- -------------
- Dockerfile
- package.json
- .eslintrc
- .nvmrc
- .npmrc
- .jsdoc.json
- .istanbul.yaml
- circle.yaml
- Procfile
- README.md
- LICENSE

### Projects

- chassis-project
- chassis-helpers
- chassis-models
- chassis-services
- chassis-eslint

### Implementation

```js
const chassis = require('chassis');

async function main() {
  //
}

main().then(status => {
  chassis.logger.info({ status }, 'Application started successfully');
  process.exit(0);
}).catch(err => {
  chassis.logger.error({ err }, 'An error occured on application startup');
  process.exit(1);
});
```