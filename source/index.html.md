---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

The Portão 3 API is organized around [REST](https://www.w3.org/TR/2004/NOTE-ws-arch-20040211/#relwwwrest). Our API has predictable resource-oriented URLs, accepts form-encoded request bodies, returns JSON-encoded responses, and uses standard HTTP response codes, authentication, and verbs.

# Identity

## Authentication

> **POST** https://api.identity.v2.portao3.com.br/auth/sign-in

```shell
curl -X POST https://api.identity.v2.portao3.com.br/auth/sign-in \
  -H 'Content-Type: application/json' \
  -D '{
    "email": "",
    "password": ""
  }'
```

> **200** Response

```json
{
  "accessToken": "Your_Access_Token_Will_Show_Up_Here",
  "refreshToken": "Your_Refresh_Token_Will_Show_Up_Here"
}
```

In order to ensure that only authorized users and applications are allowed access to the API, we make use of the [OAuth 2.0 authorization framework](https://tools.ietf.org/html/rfc6749).

OAuth 2 provides several grant types for different use cases. For server-side integration, we will use the Client Credentials Grant.

With Client Credentials Grant (defined in RFC 6749, section 4.4) an application can directly request an Access Token from the Authorization Server by using its Client Credentials (a Client Id and a Client Secret).

You can create new credentials and manage existing ones in your account dashboard.

<!-- ## Realm

### Retrieve a Realm

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
      "number": "21",
      "state": "MG",
      "street": "Av. dos Vinhedos",
      "zipCode": "38411-694",
      "cnpj": "28.352.868/0001-70"
    },
    "corporateName": "PORTAO 3 VIAGENS LTDA",
    "name": "Portão 3",
    "status": "ACTIVE"
  }
}
```

This will retrieve the users' organization information. -->

# Banking

## Account

### List Organization Accounts

> **GET** /realms/:realmId/organizations/:organizationId/accounts

```shell
curl -X GET :url/realms/:realmId/organizations/:organizationId/accounts \
-H 'Authorization: Bearer :token'
```

> **200** Response

```json
[
  {
    "_id": "652d22af362a51d216112f9e",
    "legalName": "PORTAO 3 VIAGENS LTDA",
    "tradingName": "PORTAO 3",
    "foundingDate": "2021-01-01",
    "document": "28352868000170",
    "businessType": "LTDA",
    "email": "financeiro@portao3.com.br",
    "mainActivity": "99999",
    "phoneNumber": "55999999999",
    "address": {
      "city": "UBERLANDIA",
      "complement": "ANDAR 4",
      "neighborhood": "JARDIM SUL",
      "number": "70",
      "postalCode": "38411694",
      "state": "MG",
      "street": "AV DOS VINHEDOS"
    },
    "shareholders": [
      {
        "address": {
          "city": "UBERLANDIA",
          "complement": "ANDAR 4",
          "neighborhood": "JARDIM SUL",
          "number": "70",
          "postalCode": "38411694",
          "state": "MG",
          "street": "AV DOS VINHEDOS"
        },
        "birthDate": "1990-12-31",
        "document": "99999999999",
        "email": "financeiro@portao3.com.br",
        "firstName": "JOHN",
        "lastName": "DOE",
        "motherName": "MOTHER DOE",
        "phoneNumber": "55999999999",
        "_id": "64fa1412d3b438e3eb3fe6c8"
      }
    ],
    "status": [
        {
            "status": "OPEN",
            "environment": "LIVE",
            "updatedAt": "2023-09-07T18:20:53.670Z",
            "analysisResult": [],
            "_id": "64fa1485096102607170c4bc",
            "defaultWalletId": "652d87b1362a51d216112fa6"
        },
        {
            "status": "OPEN",
            "environment": "TEST",
            "updatedAt": "2023-09-07T18:20:55.389Z",
            "analysisResult": [],
            "_id": "64fa14878bc3af88503299f4"
        }
    ],
    "createdAt": "2023-09-07T18:20:50.996Z",
    "updatedAt": "2023-09-07T18:20:55.403Z",
    "organizationId": "9d63955d-ce87-45d7-9bc8-5a87894acba2",
    "realmId": "97025c3c-84ea-47a8-8e1c-bcc3ef43f45b"
  },
  ...
]
```

### Retrieve an Account

> **GET** /realms/:realmId/organizations/:organizationId/accounts/:accountId

```shell
curl -X GET :url/realms/:realmId/organizations/:organizationId/accounts/:accountId \
-H 'Authorization: Bearer :token'
```

> **200** Response

```json
{
  "_id": "652d22af362a51d216112f9e",
  "legalName": "PORTAO 3 VIAGENS LTDA",
  "tradingName": "PORTAO 3",
  "foundingDate": "2021-01-01",
  "document": "28352868000170",
  "businessType": "LTDA",
  "email": "financeiro@portao3.com.br",
  "mainActivity": "99999",
  "phoneNumber": "55999999999",
  "address": {
    "city": "UBERLANDIA",
    "complement": "ANDAR 4",
    "neighborhood": "JARDIM SUL",
    "number": "70",
    "postalCode": "38411694",
    "state": "MG",
    "street": "AV DOS VINHEDOS"
  },
  "shareholders": [
    {
      "address": {
        "city": "UBERLANDIA",
        "complement": "ANDAR 4",
        "neighborhood": "JARDIM SUL",
        "number": "70",
        "postalCode": "38411694",
        "state": "MG",
        "street": "AV DOS VINHEDOS"
      },
      "birthDate": "1990-12-31",
      "document": "99999999999",
      "email": "financeiro@portao3.com.br",
      "firstName": "JOHN",
      "lastName": "DOE",
      "motherName": "MOTHER DOE",
      "phoneNumber": "55999999999",
      "_id": "64fa1412d3b438e3eb3fe6c8"
    }
  ],
  "status": [
    {
      "status": "OPEN",
      "environment": "LIVE",
      "updatedAt": "2023-09-07T18:20:53.670Z",
      "analysisResult": [],
      "_id": "64fa1485096102607170c4bc",
      "defaultWalletId": "652d87b1362a51d216112fa6"
    },
    {
      "status": "OPEN",
      "environment": "TEST",
      "updatedAt": "2023-09-07T18:20:55.389Z",
      "analysisResult": [],
      "_id": "64fa14878bc3af88503299f4"
    }
  ],
  "createdAt": "2023-09-07T18:20:50.996Z",
  "updatedAt": "2023-09-07T18:20:55.403Z",
  "organizationId": "9d63955d-ce87-45d7-9bc8-5a87894acba2",
  "realmId": "97025c3c-84ea-47a8-8e1c-bcc3ef43f45b"
}
```

## Wallet

### Create a Wallet

> **POST** /realms/:realmId/organizations/:organizationId/accounts/:accountId/wallets

```shell
curl -X POST :url/realms/:realmId/organizations/:organizationId/accounts/:accountId/wallets \
  -H 'Authorization: Bearer :token' \
  -H 'Environment: LIVE' \
  -H 'Content-Type: application/json' \
  -D '{
    "currency": "986",
    "customFields": {
        "key": "value"
    }
  }'
```

> **201** Response

```json
{
  "realmId": "97025c3c-84ea-47a8-8e1c-bcc3ef43f45b",
  "organizationId": "9d63955d-ce87-45d7-9bc8-5a87894acba2",
  "accountId": "652d86af362a51d216112f9e",
  "environment": "LIVE",
  "currency": "986",
  "customFields": {
    "key": "value"
  },
  "status": "PENDING",
  "role": "CHECKING",
  "_id": "65516cbe6a73fae8ae4377d9",
  "createdAt": "2023-11-13T00:24:30.152Z",
  "updatedAt": "2023-11-13T00:24:30.152Z"
}
```

### Retrieve a Wallet

> **GET** /realms/:realmId/organizations/:organizationId/accounts/:accountId/wallets/:walletId

```shell
curl -X GET :url/realms/:realmId/organizations/:organizationId/accounts/:accountId/wallets/:walletId \
  -H 'Authorization: Bearer :token' \
  -H 'Environment: LIVE'
```

> **200** Response

```json
{
  "_id": "65516cbe6a73fae8ae4377d9",
  "realmId": "97025c3c-84ea-47a8-8e1c-bcc3ef43f45b",
  "organizationId": "9d63955d-ce87-45d7-9bc8-5a87894acba2",
  "accountId": "652d86af362a51d216112f9e",
  "environment": "LIVE",
  "currency": "986",
  "customFields": {
    "key": "value"
  },
  "status": "ACTIVE",
  "role": "CHECKING",
  "createdAt": "2023-11-13T00:24:30.152Z",
  "updatedAt": "2023-11-13T00:24:34.683Z",
  "totalBalance": 100000,
  "balances": [
    {
      "category": "TRAVEL",
      "amount": 0
    },
    {
      "category": "MOBILITY",
      "amount": 50000
    },
    {
      "category": "ADS",
      "amount": 0
    },
    {
      "category": "SAAS",
      "amount": 0
    },
    {
      "category": "AIRLINES",
      "amount": 0
    },
    {
      "category": "TOLL",
      "amount": 0
    },
    {
      "category": "GAS",
      "amount": 0
    },
    {
      "category": "FLEX_INTERNATIONAL",
      "amount": 50000
    },
    {
      "category": "FLEX_NATIONAL",
      "amount": 0
    },
    {
      "category": "HOTEL",
      "amount": 0
    },
    {
      "category": "FOOD",
      "amount": 0
    }
  ]
}
```

### List Account Wallets

> **GET** /realms/:realmId/organizations/:organizationId/accounts/:accountId/wallets

```shell
curl -X GET :url/realms/:realmId/organizations/:organizationId/accounts/:accountId/wallets \
  -H 'Authorization: Bearer :token' \
  -H 'Environment: LIVE'
```

> **200** Response

```json
[
  {
  "_id": "6515902dec2d9822bf1c4852",
  "accountId": "652d86af362a51d216112f9e",
  "environment": "LIVE",
  "currency": "986",
  "customFields": {
    "key": "value"
  },
  "status": "BLOCKED",
  "role": "CHECKING",
  "createdAt": "2023-09-28T14:39:41.975Z",
  "updatedAt": "2023-11-06T12:26:21.649Z",
  "organizationId": "9d63955d-ce87-45d7-9bc8-5a87894acba2",
  "realmId": "97025c3c-84ea-47a8-8e1c-bcc3ef43f45b"
  },
  ...
]
```

## Card

### Create a Card

> **POST** /realms/:realmId/organizations/:organizationId/accounts/:accountId/wallets/:walletId/cards

```shell
curl -X POST :url/realms/:realmId/organizations/:organizationId/accounts/:accountId/wallets/:walletId/cards \
  -H 'Authorization: Bearer :token' \
  -H 'Environment: LIVE' \
  -H 'Content-Type: application/json' \
  -D '{
    "type": "VIRTUAL",
    "singleUse": false,
    "customFields": {
        "key": "value"
    }
  }'
```

> **201** Response

```json
{
  "realmId": "97025c3c-84ea-47a8-8e1c-bcc3ef43f45b",
  "organizationId": "9d63955d-ce87-45d7-9bc8-5a87894acba2",
  "accountId": "652d86af362a51d216112f9e",
  "walletId": "65516cbe6a73fae8ae4377d9",
  "environment": "LIVE",
  "panMasked": "524674******0521",
  "expiryDate": "11/2029",
  "tokenisationPermitted": true,
  "singleUse": false,
  "type": "VIRTUAL",
  "status": "ACTIVE",
  "customFields": {
    "key": "value"
  },
  "cardLimitIds": [],
  "_id": "65516f8094a4e95ffbb43886",
  "createdAt": "2023-11-13T00:36:16.848Z",
  "updatedAt": "2023-11-13T00:36:16.848Z"
}
```

### Retrieve a Card

> **GET** /realms/:realmId/organizations/:organizationId/accounts/:accountId/wallets/:walletId/cards/:cardId

```shell
curl -X GET :url/realms/:realmId/organizations/:organizationId/accounts/:accountId/wallets/:walletId/cards/:cardId \
  -H 'Authorization: Bearer :token' \
  -H 'Environment: LIVE'
```

> **200** Response

```json
{
  "_id": "65516f8094a4e95ffbb43886",
  "realmId": "97025c3c-84ea-47a8-8e1c-bcc3ef43f45b",
  "organizationId": "9d63955d-ce87-45d7-9bc8-5a87894acba2",
  "accountId": "652d86af362a51d216112f9e",
  "walletId": "65516cbe6a73fae8ae4377d9",
  "environment": "LIVE",
  "panMasked": "524674******0521",
  "expiryDate": "11/2029",
  "tokenisationPermitted": true,
  "singleUse": false,
  "type": "VIRTUAL",
  "status": "ACTIVE",
  "customFields": {
    "key": "value"
  },
  "cardLimitIds": [],
  "createdAt": "2023-11-13T00:36:16.848Z",
  "updatedAt": "2023-11-13T00:36:16.848Z"
}
```

### Retrieve Card Details

> **GET** /realms/:realmId/organizations/:organizationId/accounts/:accountId/wallets/:walletId/cards/:cardId/details

```shell
curl -X GET :url/realms/:realmId/organizations/:organizationId/accounts/:accountId/wallets/:walletId/cards/:cardId/details \
  -H 'Authorization: Bearer :token' \
  -H 'Environment: LIVE'
```

> **200** Response

```json
{
  "_id": "65516f8094a4e95ffbb43886",
  "realmId": "97025c3c-84ea-47a8-8e1c-bcc3ef43f45b",
  "organizationId": "9d63955d-ce87-45d7-9bc8-5a87894acba2",
  "accountId": "652d86af362a51d216112f9e",
  "walletId": "65516cbe6a73fae8ae4377d9",
  "environment": "LIVE",
  "panMasked": "524674******0521",
  "expiryDate": "11/2029",
  "tokenisationPermitted": true,
  "singleUse": false,
  "type": "VIRTUAL",
  "status": "ACTIVE",
  "customFields": {
    "key": "value"
  },
  "cardLimitIds": [],
  "createdAt": "2023-11-13T00:36:16.848Z",
  "updatedAt": "2023-11-13T00:36:16.848Z",
  "pan": "5246742051160521",
  "cvv": "571"
}
```

### List Wallet Cards

> **GET** /realms/:realmId/organizations/:organizationId/accounts/:accountId/wallets/:walletId/cards

```shell
curl -X GET :url/realms/:realmId/organizations/:organizationId/accounts/:accountId/wallets/:walletId/cards \
  -H 'Authorization: Bearer :token' \
  -H 'Environment: LIVE'
```

> **200** Response

```json
[
  {
    "_id": "65516f8094a4e95ffbb43886",
    "realmId": "97025c3c-84ea-47a8-8e1c-bcc3ef43f45b",
    "organizationId": "9d63955d-ce87-45d7-9bc8-5a87894acba2",
    "accountId": "652d86af362a51d216112f9e",
    "walletId": "65516cbe6a73fae8ae4377d9",
    "environment": "LIVE",
    "panMasked": "524674******0521",
    "expiryDate": "11/2029",
    "tokenisationPermitted": true,
    "singleUse": false,
    "type": "VIRTUAL",
    "status": "ACTIVE",
    "customFields": {
      "key": "value"
    },
    "cardLimitIds": [],
    "createdAt": "2023-11-13T00:36:16.848Z",
    "updatedAt": "2023-11-13T00:36:16.848Z",
  },
  ...
]
```

### List Account Cards

> **GET** /realms/:realmId/organizations/:organizationId/accounts/:accountId/cards

```shell
curl -X GET :url/realms/:realmId/organizations/:organizationId/accounts/:accountId/cards \
  -H 'Authorization: Bearer :token' \
  -H 'Environment: LIVE'
```

> **200** Response

```json
[
  {
    "_id": "65516f8094a4e95ffbb43886",
    "realmId": "97025c3c-84ea-47a8-8e1c-bcc3ef43f45b",
    "organizationId": "9d63955d-ce87-45d7-9bc8-5a87894acba2",
    "accountId": "652d86af362a51d216112f9e",
    "walletId": "65516cbe6a73fae8ae4377d9",
    "environment": "LIVE",
    "panMasked": "524674******0521",
    "expiryDate": "11/2029",
    "tokenisationPermitted": true,
    "singleUse": false,
    "type": "VIRTUAL",
    "status": "ACTIVE",
    "customFields": {
      "key": "value"
    },
    "cardLimitIds": [],
    "createdAt": "2023-11-13T00:36:16.848Z",
    "updatedAt": "2023-11-13T00:36:16.848Z",
  },
  ...
]
```

## Pix Payment

## Boleto Payment
