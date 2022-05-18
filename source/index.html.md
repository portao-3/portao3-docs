---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:

includes:
  - transactionStatus
  - errors

search: true

code_clipboard: true
---

# Introduction

The Portão 3 API is organized around [REST](https://www.w3.org/TR/2004/NOTE-ws-arch-20040211/#relwwwrest). Our API has predictable resource-oriented URLs, accepts form-encoded request bodies, returns JSON-encoded responses, and uses standard HTTP response codes, authentication, and verbs.

# Authentication

> **POST** https://api.portao3.com.br/auth

```shell
curl -X POST https://api.portao3.com.br/auth \
  -H 'Content-Type: application/json' \
  -D '{
    "client_id": "",
    "client_secret": ""
  }'
```

> **200** Response

```json
{
  "access_token": "Your_Access_Token_Will_Show_Up_Here",
  "expires_in": 86400,
  "token_type": "Bearer"
}
```

In order to ensure that only authorized users and applications are allowed access to the API, we make use of the [OAuth 2.0 authorization framework](https://tools.ietf.org/html/rfc6749).

OAuth 2 provides several grant types for different use cases. For server-side integration, we will use the Client Credentials Grant.

With Client Credentials Grant (defined in RFC 6749, section 4.4) an application can directly request an Access Token from the Authorization Server by using its Client Credentials (a Client Id and a Client Secret).

You can create new credentials and manage existing ones in your account dashboard.

# Organization

## Retrieve an Organization

> **GET** https://api.portao3.com.br/organization

```shell
curl -X GET https://api.portao3.com.br/organization \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
```

> **200** Response

```json
{
  "id": "zkIAT5N3g69FAl6OUMnd",
  "organization": {
    "address": {
      "city": "Uberlândia",
      "district": "Jardim Sul",
      "number": "126",
      "state": "MG",
      "street": "Al. Tuim",
      "zipCode": "38411-694",
      "cnpj": "28.352.868/0001-70"
    },
    "corporateName": "PORTAO 3 VIAGENS LTDA",
    "name": "Portão 3",
    "status": "ACTIVE"
  }
}
```

This will retrieve the users' organization information.

# Cost Centers

Cost centers are a way to categorize travel and budget expenses inside the platform.

## Retrieve Cost Centers

> **GET** https://api.portao3.com.br/organization/cost_centers

```shell
curl -X GET https://api.portao3.com.br/organization/cost_centers \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
```

> **200** Response

```json
[
  {
    "id": "0ZkEadksC0y8VW5DOKAY",
    "name": "Finance",
    "externalId": "12345",
    "status": "ACTIVE",
    "created_at": 1624047780
  },
  {
    ...
  }
]
```

This will retrieve the users' organization active cost centers.

## Create a Cost Center

> **POST** https://api.portao3.com.br/organization/cost_centers

```shell
curl -X POST https://api.portao3.com.br/organization/cost_centers \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}' \
  -D '{
    "name": "",
    "externalId": "",
  }'
```

> **201** Response

```json
{
  "id": "0ZkEadksC0y8VW5DOKAY",
  "name": "",
  "externalId": "",
  "status": "ACTIVE",
  "created_at": 1624047780
}
```

This will create a new cost center for the organization

### Parameters

#### name **REQUIRED**

The name for the Cost Center on all the information that is displayed to a user.

#### externalId

This represents an ID for the Cost Center in other systems. Usefull for migrating data, or making sure the data we export is backwards compatible to other systems.

## Update a Cost Center

> **PUT** https://api.portao3.com.br/organization/cost_centers/{id}

```shell
curl -X PUT https://api.portao3.com.br/organization/cost_centers/{id} \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}' \
  -D '{
    "name": "",
    "externalId": "",
  }'
```

> **200** Response

```json
{
  "id": "0ZkEadksC0y8VW5DOKAY",
  "name": "",
  "externalId": "",
  "status": "ACTIVE",
  "created_at": 1624047780
}
```

This will update a center for the organization

### Parameters

#### name **REQUIRED**

The name for the Cost Center on all the information that is displayed to a user.

#### externalId

This represents an ID for the Cost Center in other systems. Usefull for migrating data, or making sure the data we export is backwards compatible to other systems.

## Delete a Cost Center

> **DELETE** https://api.portao3.com.br/organization/cost_centers/{id}

```shell
curl -X DELETE https://api.portao3.com.br/organization/cost_centers/{id} \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
```

> **204** Response

```text
NO CONTENT
```

This will delete a Cost Center.

# Projects

Projects are a way to categorize travel and budget expenses inside the platform.

## Retrieve Projects

> **GET** https://api.portao3.com.br/organization/projects

```shell
curl -X GET https://api.portao3.com.br/organization/projects \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
```

> **200** Response

```json
[
  {
    "id": "Mt4ILqGbuJNGfRqxULjr",
    "name": "ERP Implementation",
    "externalId": "0987",
    "status": "ACTIVE",
    "created_at": 1624047780
  },
  {
    ...
  }
]
```

This will retrieve the users' organization active projects.

## Create a Project

> **POST** https://api.portao3.com.br/organization/projects

```shell
curl -X POST https://api.portao3.com.br/organization/projects \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}' \
  -D '{
    "name": "",
    "externalId": "",
  }'
```

> **201** Response

```json
{
  "id": "Mt4ILqGbuJNGfRqxULjr",
  "name": "",
  "externalId": "",
  "status": "ACTIVE",
  "created_at": 1624047780
}
```

This will create a new project for the organization

### Parameters

#### name **REQUIRED**

The name for the Project on all the information that is displayed to a user.

#### externalId

This represents an ID for the Project in other systems. Usefull for migrating data, or making sure the data we export is backwards compatible to other systems.

## Update a Project

> **PUT** https://api.portao3.com.br/organization/projects/{id}

```shell
curl -X PUT https://api.portao3.com.br/organization/projects/{id} \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}' \
  -D '{
    "name": "",
    "externalId": "",
  }'
```

> **200** Response

```json
{
  "id": "Mt4ILqGbuJNGfRqxULjr",
  "name": "",
  "externalId": "",
  "status": "ACTIVE",
  "created_at": 1624047780
}
```

This will update a project for the organization

### Parameters

#### name **REQUIRED**

The name for the Project on all the information that is displayed to a user.

#### externalId

This represents an ID for the Project in other systems. Usefull for migrating data, or making sure the data we export is backwards compatible to other systems.

## Delete a Project

> **DELETE** https://api.portao3.com.br/organization/projects/{id}

```shell
curl -X DELETE https://api.portao3.com.br/organization/projects/{id} \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
```

> **204** Response

```text
NO CONTENT
```

This will delete a Project.

# Motivations

Motivations are a way to categorize travel and budget expenses inside the platform.

## Retrieve Motives

> **GET** https://api.portao3.com.br/organization/motives

```shell
curl -X GET https://api.portao3.com.br/organization/motives \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
```

> **200** Response

```json
[
  {
    "id": "Mt4ILqGbuJNGfRqxULjr",
    "name": "Client Visit",
    "externalId": "4576",
    "status": "ACTIVE",
    "created_at": 1624047780
  },
  {
    ...
  }
]
```

This will retrieve the users' organization active motives.

## Create a Motive

> **POST** https://api.portao3.com.br/organization/motives

```shell
curl -X POST https://api.portao3.com.br/organization/motives \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}' \
  -D '{
    "name": "",
    "externalId": "",
  }'
```

> **201** Response

```json
{
  "id": "vqsj85qzi6E7uJMhgKbP",
  "name": "",
  "externalId": "",
  "status": "ACTIVE",
  "created_at": 1624047780
}
```

This will create a new motive for the organization

### Parameters

#### name **REQUIRED**

The name for the Motive on all the information that is displayed to a user.

#### externalId

This represents an ID for the Motive in other systems. Usefull for migrating data, or making sure the data we export is backwards compatible to other systems.

## Update a Motive

> **PUT** https://api.portao3.com.br/organization/motives/{id}

```shell
curl -X PUT https://api.portao3.com.br/organization/motives/{id} \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}' \
  -D '{
    "name": "",
    "externalId": "",
  }'
```

> **200** Response

```json
{
  "id": "vqsj85qzi6E7uJMhgKbP",
  "name": "",
  "externalId": "",
  "status": "ACTIVE",
  "created_at": 1624047780
}
```

This will update a motive for the organization

### Parameters

#### name **REQUIRED**

The name for the Motive on all the information that is displayed to a user.

#### externalId

This represents an ID for the Motive in other systems. Usefull for migrating data, or making sure the data we export is backwards compatible to other systems.

## Delete a Motive

> **DELETE** https://api.portao3.com.br/organization/motives/{id}

```shell
curl -X DELETE https://api.portao3.com.br/organization/motives/{id} \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
```

> **204** Response

```text
NO CONTENT
```

This will delete a Motive.

# Tags

Tags are a way to categorize travel and budget expenses inside the platform.

## Retrieve Tags

> **GET** https://api.portao3.com.br/organization/tags

```shell
curl -X GET https://api.portao3.com.br/organization/tags \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
```

> **200** Response

```json
[
  {
    "id": "Mt4ILqGbuJNGfRqxULjr",
    "name": "International Expense",
    "externalId": "9273",
    "status": "ACTIVE",
    "created_at": 1624047780
  },
  {
    ...
  }
]
```

This will retrieve the users' organization active tags.

## Create a Tag

> **POST** https://api.portao3.com.br/organization/tags

```shell
curl -X POST https://api.portao3.com.br/organization/tags \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}' \
  -D '{
    "name": "",
    "externalId": "",
  }'
```

> **201** Response

```json
{
  "id": "GobatSjVRwp9aBrOuSg9",
  "name": "",
  "externalId": "",
  "status": "ACTIVE",
  "created_at": 1624047780
}
```

This will create a new tag for the organization

### Parameters

#### name **REQUIRED**

The name for the Tag on all the information that is displayed to a user.

#### externalId

This represents an ID for the Tag in other systems. Usefull for migrating data, or making sure the data we export is backwards compatible to other systems.

## Update a Tag

> **PUT** https://api.portao3.com.br/organization/tags/{id}

```shell
curl -X PUT https://api.portao3.com.br/organization/tags/{id} \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}' \
  -D '{
    "name": "",
    "externalId": "",
  }'
```

> **200** Response

```json
{
  "id": "GobatSjVRwp9aBrOuSg9",
  "name": "",
  "externalId": "",
  "status": "ACTIVE",
  "created_at": 1624047780
}
```

This will update a tag for the organization

### Parameters

#### name **REQUIRED**

The name for the Tag on all the information that is displayed to a user.

#### externalId

This represents an ID for the Tag in other systems. Usefull for migrating data, or making sure the data we export is backwards compatible to other systems.

## Delete a Tag

> **DELETE** https://api.portao3.com.br/organization/tags/{id}

```shell
curl -X DELETE https://api.portao3.com.br/organization/tags/{id} \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
```

> **204** Response

```text
NO CONTENT
```

This will delete a Tag.

# Cards

## Create a Card

> **POST** https://api.portao3.com.br/cards

```shell
curl -X POST https://api.portao3.com.br/cards \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}' \
  -D '{
    "amount": "",
    "type": "",
    "currency": "",
    "maxPercentageApproval": "",
    "minPercentageApproval": "",
    "activatesAt": "",
    "cancelsAt": "",
    "custom_fields": {
      "": ""
    },
  }'
```

> **201** Response

```json
{
  "id": "8frftfw3zZLyNqjzALTr",
  "number": "5285326537172425",
  "expiration": "07/22",
  "cvv": "345",
  "amount": 100,
  "type": "DEFAULT",
  "currency": "986",
  "maxPercentageApproval": 1,
  "minPercentageApproval": 0,
  "activatesAt": "2021-07-01",
  "cancelsAt": "2021-08-10",
  "custom_fields": {
    "cost_center": "HR"
  }
}
```

This will issue a new virtual card number.

For security reasons, this will be the only response we are able to show you the virtual card number information, so please make sure you do all required treatments with this information on your side at this time.

### Parameters

#### amount **REQUIRED**

The amount for which the card should be generated, in cents.

#### type

Defines what kind of merchant will be able to use this card. Needs to be one of our pre-defined types: DEFAULT, HOTEL, FLIGHT, NATIONAL or INTERNATIONAL. Defaults to DEFAULT.

#### currency

The currency that the card will be transacted. Use [ISO 4217](https://pt.wikipedia.org/wiki/ISO_4217) codes as reference. Defaults to 986.

#### maxPercentageApproval

The maximum authorization amount that will be available for approval. Should be a number greater than 0. Defaults to 1.

#### minPercentageApproval

The minimum authorization amount that will be available for approval. Should be a number between 0 and 1. Defaults to 0.

#### activatesAt **REQUIRED**

The date for which the card will be activated. Should be greater or equal than today.

#### cancelsAt **REQUIRED**

The date for which the card will be cancelled automatically. Should be greater than activation date.

#### custom_fields

Any custom fields you could use for future referral.

## Retrieve a Card

> **GET** https://api.portao3.com.br/cards/{id}

```shell
curl -X GET https://api.portao3.com.br/cards/{id} \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
```

> **200** Response

```json
{
  "id": "8frftfw3zZLyNqjzALTr",
  "env": "live",
  "number": "231024******6688",
  "expiration": "11/2022",
  "amount": 100,
  "type": "DEFAULT",
  "currency": "986",
  "balance": 100,
  "maxPercentageApproval": 1,
  "minPercentageApproval": 0,
  "activatesAt": "2021-07-01",
  "cancelsAt": "2021-08-10",
  "status": "ACTIVE",
  "custom_fields": {
    "cost_center": "HR"
  }
}
```

This will retrieve a virtual card parameters.

Please notice that this service will not return the virtual card information (such as number, expiration and cvv). This information is only shown once, when you create a new card.

### Parameters

#### id **REQUIRED**

Card ID

## Update a Card

> **PUT** https://api.portao3.com.br/cards/{id}

```shell
curl -X PUT https://api.portao3.com.br/cards/{id} \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
  -D '{
    "amount": "",
    "type": "",
    "currency": "",
    "maxPercentageApproval": "",
    "minPercentageApproval": "",
    "activatesAt": "",
    "cancelsAt": "",
    "custom_fields": {
      "": ""
    },
  }'
```

> **200** Response

```json
{
  "id": "8frftfw3zZLyNqjzALTr",
  "amount": 100,
  "type": "DEFAULT",
  "currency": "986",
  "maxPercentageApproval": 1,
  "minPercentageApproval": 0,
  "activatesAt": "2021-07-01",
  "cancelsAt": "2021-08-10",
  "custom_fields": {
    "cost_center": "HR"
  }
}
```

Will update a virtual card parameters.

While updating a credit card information, you are able to change all the usage parameters, including amounts, dates, and custom fields.

By changing the dates or the amounts of an active card, we will move any funds or change the status for this card as required, so it automatically reflect's the new information you provided.

### Parameters

#### amount **REQUIRED**

The amount for which the card should be generated, in cents.

#### type

Defines what kind of merchant will be able to use this card. Needs to be one of our pre-defined types: DEFAULT, HOTEL, FLIGHT, NATIONAL or INTERNATIONAL. Defaults to DEFAULT.

#### currency

The currency that the card will be transacted. Use [ISO 4217](https://pt.wikipedia.org/wiki/ISO_4217) codes as reference. Defaults to 986.

#### maxPercentageApproval

The maximum authorization amount that will be available for approval. Should be a number greater than 0. Defaults to 1.

#### minPercentageApproval

The minimum authorization amount that will be available for approval. Should be a number between 0 and 1. Defaults to 0.

#### activatesAt **REQUIRED**

The date for which the card will be activated. Should be greater or equal than today.

#### cancelsAt **REQUIRED**

The date for which the card will be cancelled automatically. Should be greater than activation date.

#### custom_fields

Any custom fields you could use for future referral.

## Delete a Card

> **DELETE** https://api.portao3.com.br/cards/{id}

```shell
curl -X DELETE https://api.portao3.com.br/cards/{id} \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
```

> **204** Response

```text
NO CONTENT
```

This will delete a virtual card and return any funds associated with it.

When deleting a card, we make sure that it is no longer available to receive transactions. If it was already active, we will move any funds associated with it to the main account.

## List all cards

> **GET** https://api.portao3.com.br/cards

```shell
curl -G https://api.portao3.com.br/cards \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
  -D 'status=""'
  -D 'startsActivationAt=""'
  -D 'endsActivationAt=""'
  -D 'page=""'
  -D 'page_size=""'
```

> **200** Response

```json
{
  "data": [
    {
      "id":"8frftfw3zZLyNqjzALTr",
      "amount": 100,
      "type": "DEFAULT",
      "currency": "986",
      "maxPercentageApproval": 1,
      "minPercentageApproval": 0,
      "activatesAt": "2021-07-01",
      "cancelsAt": "2021-08-10",
      "status": "ACTIVE",
      "custom_fields": {
        "cost_center": "HR"
      }
    },
    {...},
    {...}
  ],
  "page": 1,
  "records": 20
}
```

Returns a list of cards you’ve previously issued. The cards are returned in sorted order, with the earlier activation date appearing first.

### Parameters

#### status

Filter by the status for the cards you are looking for.

#### startsActivationAt

Filter for the initial date a card is expected to be activated.

#### endsActivationAt

Filter for the end date a card is expected to be activated.

#### page

Page number you are retrieving. Defaults to 1.

#### page_size

Number of results you want in each page. Defaults to 20.

## List attached transactions

> **GET** https://api.portao3.com.br/cards/{id}/transactions

```shell
curl -G https://api.portao3.com.br/cards/{id}/transactions \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
  -D 'response_code=""'
  -D 'page=""'
  -D 'page_size=""'
```

> **200** Response

```json
{
  "data": [
    {
      "id": "U0RPiQB8XcYnyEu6Kput",
      "date_time": 1598274503,
      "merchant_name": "ibis",
      "merchant_city": "São Paulo",
      "merchant_country": "Brasil",
      "mcc": "7011",
      "amount": 100,
      "currency": "986",
      "auth_code": "123456",
      "response_code": 0
    },
    {...},
    {...}
  ],
  "page": 1,
  "records": 3
}
```

Fetch a list of transactions that are associated to a card.

### Parameters

#### status

Filter by the status for the transactions you are looking for.

#### page

Page number you are retrieving. Defaults to 1.

#### page_size

Number of results you want in each page. Defaults to 20.
