---
layout: post
title: Generic market modelization
---

## Principle

A transaction is a contract between several parts. A part is a moral entity and
not necessary a physical people. Thus, the key of a transaction is the contract
itself.

### Transaction definitions

- **WHAT** what service or product is concerned
- **HOW MUCH** how much quantity must be transfered
- **WHEN** when the service
- **WHO** who are the actors around the transaction
- **WHERE** where the service is happening
- **RESTRICTIONS** what restrictions are applying

Example:

- I am selling at €12, 1 hour of piano lesson to people above 12 years old any day of the
week between 4pm and 8pm at the 26 rue Lamblardie, 75012. Payment by cash only.
- I am selling a TV at 25€. Bring it at the 26 rue Lamblardie, 75012 PARIS.
- I am buying a ride from here to there, any price, any car.
- I am selling my services for a ride at the following cost: 2 €/km + 0.2 €/min

### Application #1

Peter is creating an offer to sell 1 hour of piano lesson. He creates a contract
for piano lesson. He is attaching `terms` to the contract: the buyer must be at
least 12 years old.

The terms of a contract are of different types:

- transaction check
- transaction price modificator

### Design patterns

An offer is the first step of a transaction. The sellers are engaged legaly. A
transaction is thus based on the following design patterns:

- `COMMAND`: undo / redo the commands
- `STATE`: the actions available to a transaction are given by its state
- `EVENT`: all objects are emitting and listening events