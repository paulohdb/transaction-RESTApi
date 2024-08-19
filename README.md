# RESTful API - Transaction

This is a RESTful API using NodeJs, the interface can make transactions with credit and debit, and validation of user using cookies.

## Contents:
- RESTful
- Validation
- Cookies
- Unit Tests
- Deploy

## Technologies

The technologies used in this application, consists in:

- Typescript (As main language)
- Fastify
- Knex (Query Builder)
- Zod (Validation)
- Vitest (Unit Test - E2E)
- Cookies

# How the API works?

It is a transaction management, where you can register credit transactions and debit transactions.

### Functionalities:

- The User can create a new transaction
- The user can visualize a summary of his account
- The user can list all the transactions made
- The user can visualize a unique transaction
- The transaction can be credit, it will sum the total value, or debit will subtract.
- It can be possible to identify the user between the request
- The user only can visualize transactions which it created.

The transaction consist with some information, as:

- Id - the unique identifier of a transaction
- Title - the title of a transaction
- Amount - the amount of the transaction
- Created_at - When it was created
- Session_Id - Session Id to use with cookies

When a User create their first transaction, it will create a session id as a cookie, giving permission only to see their own transactions.

## Requests

There will be some examples of request we can made.

### POST/transactions

This POST method, will send a body with 3 informations to create a new transaction on DB.

```json
{
    "title": "Example of a Transaction",
    "amount": 2000,
    "type": "credit"
}
```
When it's created, it generates a new session Id.

### GET/transactions

This GET method, will show up all the transactions the user did, with his session id.

```json
{
    "transactions": [
        {
            "id": "18f5f748-ecc1-47cd-a50e-5a8b5304b3cf",
            "title": "Example of a Transaction",
            "amount": 2000,
            "created_at": "2024-08-19 19:11:08",
            *"session_id": "2e4599ca-549e-448a-8c43-753a7116ef3e"*
        },
        {
            "id": "ce83fff4-7770-440e-a7fc-b2c0c8224aba",
            "title": "Another Example with Debit",
            "amount": -500,
            "created_at": "2024-08-19 19:13:50",
            *"session_id": "2e4599ca-549e-448a-8c43-753a7116ef3e"*
        }
    ]
}
```
### GET/transactions/:id

This GET method, will show up a specific transaction using the id.

```json
{
    "transaction": {
        *"id": "18f5f748-ecc1-47cd-a50e-5a8b5304b3cf"*,
        "title": "Example of a Transaction",
        "amount": 2000,
        "created_at": "2024-08-19 19:11:08",
        "session_id": "2e4599ca-549e-448a-8c43-753a7116ef3e"
    }
}
```
### GET/transactions/summary

This GET Method, will show up a summary of user's transactions.

```json
{
    "summary": {
        "amount": 1500
    }
}
```

In this example, the user created a credit transaction with 2000, and a debit transaction with 500, the final amount must be 1500.

## E2E Test

This API has a E2E Test, using vitest to verify all the entries.

<img width="397" alt="image" src="https://github.com/user-attachments/assets/3bfe6320-6386-42ca-836e-7ebb96568016">

You can check the steps of verification in https://github.com/paulohdb/transaction-RESTApi/blob/master/test/transactions.spec.ts

## Deploy

The entire code was written in Typescript, but NodeJs cannot interpretate Typescript, only javascript, so I used the "TSUP" to build the entire application, to deploy in Render as web Service and the DB using Postegres.
