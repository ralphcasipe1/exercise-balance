# Introduction

Your task is to implement an API service based on the given GraphQL schema.

An optional `X-Request-ID` header may be set. If `X-Request-ID` is set, then the request must be idempotent. Requests with the same `X-Request-ID` will be treated as retry instances of a single request. Idempotency is valid only within the 24 hour period since the first request was received.

# Schema

## Account

Object representing the user account.

### Fields

| Field              | Description                                                      |
| ------------------ | ---------------------------------------------------------------- |
| `id`               | Unique ID of user.                                               |
| `balance`          | Balance currently held by the user.                              |
| `reservedBalance`  | Reserved balance held by the user for a specific context.        |
| `virtualBalance`   | Virtual balance held by the user for a specific context.         |
| `availableBalance` | Total available balance held by the user for a specific context. |

## Query

### Fields

| Field     | Description   |
| --------- | ------------- |
| `account` | User account. |

## Mutation

### Fields

| Field                    | Description                                                                                                                                                                                                                                                                          |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `updateBalance`          | Update the user's current balance.                                                                                                                                                                                                                                                   |
| `createReservedBalance`  | Take a portion of the user's current balance and create a reserved balance for the given context. If the reserved balance already exists for the given context, then the resulting reserved will be the sum of the existing reserved balance and the newly created reserved balance. |
| `updateReservedBalance`  | Update the reserved balance for the given context.                                                                                                                                                                                                                                   |
| `releaseReservedBalance` | Take the reserved balance and add it into the user's current balance.                                                                                                                                                                                                                |
| `updateVirtualBalance`   | Update the virtual balance for the given context.                                                                                                                                                                                                                                    |
| `cancelVirtualBalance`   | Reset the virtual balance for the given context to zero.                                                                                                                                                                                                                             |
| `commitVirtualBalance`   | Take the virtual balance and add it into the user's current balance.                                                                                                                                                                                                                 |

