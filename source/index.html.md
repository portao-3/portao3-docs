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

<!-- aaaaaaaaaaaa -->

# Platform

## Wallet

### Create Wallet

> **POST** /realms/:realmId/:organizations/:organizationId/wallets

```json
{
  "settings": {
    "payment": {
      "pix": true,
      "bankSlip": true,
      "card": true
    },
    "notification": {
      "balanceLimit": {
        "amount": 10000,
        "email": true,
        "isActive": true
      }
    }
  }
}
```

```json
{
  customFields: [
		{
			id: "1af48e91-bf83-4467-842b-839acd176c0a",
			label: "label",
			identifier: "identifier",
			values: [
				"value1", "value2",
			]
			version: 1,
		}
  ]
}
```

```json
{
  "shared": [
    {
      "id": "a5ea899d-e45f-464d-8934-aed3d9fd7f40",
      "role": "OWNER"
    }
  ]
}
```

```shell
curl --location 'https://api.platform.v2.portao3.com.br/realms/b7e3ed37-4f6f-46ef-9fe7-baede912a940/organizations/5785e88b-d2ea-453f-99f7-c562db038fbb/wallets' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <TOKEN>' \
--data '{
    "name": "Individual",
    "type": "PERSONAL",
    "settings": {
        "payment": {
            "pix": true,
            "bankSlip": true,
            "card": false
        },
        "notification": {
            "balanceLimit": {
                "amount": 10000,
                "email": true,
                "isActive": true
            }
        }
    },
    "customFields": [
		{
			"id": "1af48e91-bf83-4467-842b-839acd176c0a",
			"label": "label",
			"identifier": "identifier",
			"values": [
				"value1", "value2"
			],
			"version": 1
		}
    ],
    "shared": [
        {
            "id": "937a0b78-c4ab-4aa0-bfae-e58adc9856c0",
            "role": "OWNER"
        }
    ]
}'
```

> RESPONSE
> 200 (OK)

```json
{
  "id": "46d6ce2d-f8bd-4600-9e09-5ed299a019dd",
  "name": "WALLET_NAME",
  "createdBy": "ba2afc7f-4545-49d6-9046-e6268dbadca0",
  "updatedBy": "ba2afc7f-4545-49d6-9046-e6268dbadca0",
  "realm": "b7e3ed37-4f6f-46ef-9fe7-baede912a940",
  "organization": "5785e88b-d2ea-453f-99f7-c562db038fbb",
  "status": "ACTIVE",
  "type": "SHARED",
  "currency": "986",
  "settings": {
    "payment": {
      "bankSlip": true,
      "card": true,
      "pix": true
    }
  },
  "shared": [
    {
      "id": "a5ea899d-e45f-464d-8934-aed3d9fd7f40",
      "role": "OWNER",
      "firstName": "USER_FIRST_NAME",
      "lastName": "USER_LAST_NAME",
      "email": "user@email.com"
    }
  ],
  "customFields": [
    {
      "id": "1af48e91-bf83-4467-842b-839acd176c0a",
      "label": "label",
      "values": ["value1", "value2"],
      "identifier": "identifier",
      "version": 1
    }
  ]
}
```

> 400 (BAD REQUEST)

```json
{
  "code": "BAD_REQUEST",
  "message": "Bad Request: Your request is invalid or incomplete. Please make sure you are requesting with the right fields.",
  "fields": []
}
```

> 404 (FIELD NOT FOUND)

```json
{
  "code": "{FIELD}_NOT_FOUND",
  "traceId": "1-65b270bc-52a8e06e0b6921012c9af55d",
  "origin": "IDENTITY",
  "message": "{FIELD} not found"
}
```

Use this endpoint to create a Wallet.

Path Params

| Field          | Type   | Required |
| -------------- | ------ | -------- |
| realmId        | string | true     |
| organizationId | string | true     |

Body Params

| Field        | Type   | Required | Allowed values                 |
| ------------ | ------ | -------- | ------------------------------ |
| name         | string | true     |                                |
| type         | string | true     | PERSONAL, ORGANIZATION, SHARED |
| settings     | object | false    |                                |
| customFields | array  | false    |                                |
| shared       | array  | true     |                                |

Important information:

The following information must be considered before using this endpoint

Settings:
In the body, the `settings` field is a not required object. But if your body contains the `settings` field, then some fields are required:

| Field    | Type    | Required |
| -------- | ------- | -------- |
| pix      | boolean | true     |
| bankSlip | boolean | true     |
| card     | boolean | true     |
| amount   | number  | false    |
| email    | boolean | false    |
| isActive | boolean | false    |

Custom Fields:
In the body, the `customFields` field is a not required array. But if your body contains the `customFields` field, then some fields are required:

| Field      | Type            | Required |
| ---------- | --------------- | -------- |
| id         | string          | true     |
| label      | string          | false    |
| identifier | string          | false    |
| values     | array of string | true     |

Shared:
Shared is a required field that contains information about who is allowed to use the wallet and his role. Shared must have at least one item whit role OWNER.

| Field | Type             | Required | Allowed values         |
| ----- | ---------------- | -------- | ---------------------- |
| id    | string (user_id) | true     |                        |
| role  | string           | true     | OWNER, USER, READ_ONLY |

### Get Wallets

> **GET** /realms/:realmId/:organizations/:organizationId/wallets

```shell
curl --location --request GET 'https://api.platform.v2.portao3.com.br/realms/e829f181-e8b2-453c-9cde-5554c71d5c8d/organizations/9e020430-487b-4e43-a84b-a58bf5bf98a9/wallets?limit=1&next=657756fcf623d97eca90e752&name=SALES&status=ACTIVE' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <TOKEN>' \
--data ''
```

> RESPONSES
> 200 (OK)

```json
{
  "next": "65b109b430b6b793d1af2552",
  "items": [
    {
      "id": "5389d8f4-de65-4bca-9543-2a2edfde727b",
      "name": "WALLET_NAME",
      "realm": "e829f181-e8b2-453c-9cde-5554c71d5c8d",
      "type": "SHARED",
      "shared": [
        {
          "id": "9edc6a02-91a6-40a1-b71e-1d646e7a1e9d",
          "firstName": "SHARED_USER_NAME",
          "lastName": "SHARED_USER_LASTNAME",
          "email": "user@email.com",
          "role": "OWNER",
          "_id": "65b109b430b6b793d1afx786"
        }
      ],
      "settings": {
        "payment": {
          "pix": true,
          "bankSlip": true,
          "card": true
        }
      },
      "customFields": [],
      "status": "ACTIVE",
      "currency": "986",
      "organization": "9e020430-487b-4e43-a84b-a58bf5bf98a9",
      "balances": [
        {
          "category": "FLEX_INTERNATIONAL",
          "amount": 100
        },
        {
          "category": "FLEX_NATIONAL",
          "amount": 0
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
          "category": "TRAVEL",
          "amount": 0
        },
        {
          "category": "FOOD",
          "amount": 0
        },
        {
          "category": "HOTEL",
          "amount": 0
        },
        {
          "category": "AIRLINES",
          "amount": 0
        },
        {
          "category": "MOBILITY",
          "amount": 0
        },
        {
          "category": "GAS",
          "amount": 0
        },
        {
          "category": "TOLL",
          "amount": 0
        }
      ],
      "totalBalance": 100
    }
  ]
}
```

> 403 - Occurs when a realm or organization is incorrect.

```json
{
  "message": "Forbidden"
}
```

Use this endpoint to get organization's wallets.

Path params

| Field          | Type   | Required |
| -------------- | ------ | -------- |
| realmId        | string | true     |
| organizationId | string | true     |

Query Params

| Field  | Type   | Required | Description                      | Allowed values      |
| ------ | ------ | -------- | -------------------------------- | ------------------- |
| name   | string | false    | Wallet name                      |                     |
| status | string | false    | Wallet status                    | ACTIVE, DEACTIVATED |
| limit  | number | false    | Max wallets to be returned       |                     |
| next   | string | false    | Next wallet \_id to be paginated |                     |

Important information:

- Pagination is supported through the **`next`** token provided in the response.

### Get Wallet

> **GET** /realms/:realmId/organizations/:organizationId/wallets

```shell
curl --location 'https://api.platform.v2.portao3.com.br/realms/d5a27925-6043-4be9-912f-ffc13009855a/organizations/58d649cd-5da8-4b00-ac97-14274f7010d0/wallets/3526bb87-3120-47d3-b396-8dff2a0a2fe5' \
--header 'Authorization: Bearer <TOKEN>'
```

> RESPONSES
> 200 (OK)

```json
{
  "id": "3526bb87-3120-47d3-b396-8dff2a0a2fe5",
  "name": "WALLET_NAME",
  "createdBy": "f0376d72-0e5d-4118-aded-81dfaa0380f4",
  "updatedBy": "f0376d72-0e5d-4118-aded-81dfaa0380f4",
  "realm": "d5a27925-6043-4be9-912f-ffc13009855a",
  "organization": "58d649cd-5da8-4b00-ac97-14274f7010d0",
  "status": "ACTIVE",
  "type": "PERSONAL",
  "currency": "986",
  "settings": {
    "payment": {
      "pix": true,
      "bankSlip": true,
      "card": true
    }
  },
  "shared": [
    {
      "_id": "65b29022cd2fc8c0761a5f58",
      "id": "39215807-d364-430a-ab56-8278e6c01f9c",
      "firstName": "SHARED_FIRST_NAME",
      "lastName": "SHARED_LAST_NAME",
      "email": "user@email.com",
      "role": "OWNER"
    }
  ],
  "customFields": [],
  "totalBalance": 0,
  "balances": [
    {
      "category": "FLEX_NATIONAL",
      "amount": 0
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
      "category": "TRAVEL",
      "amount": 0
    },
    {
      "category": "FOOD",
      "amount": 0
    },
    {
      "category": "HOTEL",
      "amount": 0
    },
    {
      "category": "AIRLINES",
      "amount": 0
    },
    {
      "category": "GAS",
      "amount": 0
    },
    {
      "category": "FLEX_INTERNATIONAL",
      "amount": 0
    },
    {
      "category": "MOBILITY",
      "amount": 0
    },
    {
      "category": "TOLL",
      "amount": 0
    }
  ]
}
```

> 404 (NOT FOUND)

```json
{
  "code": "WALLET_NOT_FOUND",
  "traceId": "1-65b2910b-2a9f8a6d46b0b67f3db68a14",
  "message": "wallet not found"
}
```

> 403 (FORBIDDEN) - Occurs when a realm or organization is incorrect.

```json
{
  "message": "Forbidden"
}
```

Use this endpoint to get a specific wallet.

Path Params

| Field          | Type   | Required | Allowed values |
| -------------- | ------ | -------- | -------------- |
| realmId        | string | true     |                |
| organizationId | string | true     |                |
| walletId       | string | true     | uuid, default  |

Important information:

- If the **`walletId`** parameter is set to `default`, the API returns information about the organization's default wallet.

### Get User Wallet Default

> **GET** /realms/:realmId/organizations/:organizationId/users/:userId/wallets/default

```shell
curl --location --request GET 'https://api.platform.v2.portao3.com.br/realms/b7b4fa83-34d4-45d7-a645-eedb303dfa4e/organizations/16df03a7-12f7-45c2-992c-98f550ec374b/users/b62087db-4a2b-4d07-9752-fcddc92ccf36/wallets/default?details=false' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <TOKEN>' \
```

> RESPONSES
> 200 (OK)

```json
{
  "id": "3ff12a82-25e7-40c8-a468-17f04665a567",
  "name": "WALLET_NAME_DEFAULT",
  "createdBy": "9f958e8c-490d-4ca4-97bb-f70e1d9e503c",
  "updatedBy": "9f958e8c-490d-4ca4-97bb-f70e1d9e503c",
  "realm": "b7b4fa83-34d4-45d7-a645-eedb303dfa4e",
  "organization": "16df03a7-12f7-45c2-992c-98f550ec374b",
  "status": "ACTIVE",
  "type": "PERSONAL",
  "currency": "986",
  "settings": {
    "payment": {
      "pix": true,
      "bankSlip": true,
      "card": true
    }
  },
  "shared": [
    {
      "_id": "65b293e6d082c38bb5138fb8",
      "id": "9f958e8c-490d-4ca4-97bb-f70e1d9e503c",
      "firstName": "USER_FIRST_NAME",
      "lastName": "USER_LAST_NAME",
      "email": "user@email.com",
      "role": "OWNER"
    }
  ],
  "customFields": []
}
```

> 404 (NOT FOUND)

```json
{
  "code": "WALLET_NOT_FOUND",
  "traceId": "1-65b29453-20ce57e361607c1b52fa2af8",
  "message": "wallet not found"
}
```

> 403 (FORBIDDEN)

```json
{
  "message": "Forbidden"
}
```

Use this endpoint to get a user default wallet

Path Params

| Field          | Type   | Required |
| -------------- | ------ | -------- |
| realmId        | string | true     |
| organizationId | string | true     |
| userId         | string | true     |

Query Params

| Field   | Type    | Required |
| ------- | ------- | -------- |
| details | boolean | false    |

Important information:

- The **`details`** query parameter can be used to include additional details from the banking service.

### Block Wallet

> **POST** realms/:realmId/organizations/:organizationId/wallets/:walletId/block

```shell
curl --location --request POST 'https://api.platform.v2.portao3.com.br/realms/fb125845-c001-4e39-af05-a975981c16ea/organizations/502a8142-2b43-401e-994c-1c075f2d6a7f/wallets/fb6252b2-367a-433f-b84b-f17e57d2e9ed/block' \
--header 'Authorization: Bearer <TOKEN>' \
--data ''
```

> RESPONSES
> 204 (NO CONTENT)

```json
{}
```

> 404 (NOT FOUND)

```json
{
  "code": "WALLET_NOT_FOUND",
  "traceId": "1-65b296f0-24c5c74925d243d64e5e82b7",
  "message": "wallet not found"
}
```

> 403 (FORBIDDEN)

```json
{
  "message": "Forbidden"
}
```

Use this endpoint to block a wallet

Path Params

| Field          | Type   | Required |
| -------------- | ------ | -------- |
| realmId        | string | true     |
| organizationId | string | true     |
| walletId       | string | true     |

### Unblock Wallet

> **POST** /realms/:realmId/organizations/:organizationId/wallets/:walletId/unblock

```shell
curl --location --request POST 'https://api.platform.v2.portao3.com.br/realms/a6ed97df-e4a5-4036-9340-2e12108fae3b/organizations/6354d4e4-9902-4245-a156-77a57b76a1c4/wallets/da66fa29-ac17-43e6-be08-c67ac643a7b9/unblock' \
--header 'Authorization: Bearer <TOKEN>' \
--data ''
```

> RESPONSES
> 204 (NO CONTENT)

```json
{}
```

> 404 (NOT FOUND)

```json
{
  "code": "WALLET_NOT_FOUND",
  "traceId": "1-65b296f0-24c5c74925d243d64e5e82b7",
  "message": "wallet not found"
}
```

> 403 (FORBIDDEN) - Occurs when a realm or organization is incorrect.

```json
{
  "message": "Forbidden"
}
```

Use this endpoint to unblock a wallet

Path Params

| Field          | Type   | Required |
| -------------- | ------ | -------- |
| realmId        | string | true     |
| organizationId | string | true     |
| walletId       | string | true     |

### Update Wallet

> **POST** /realms/:realmId/organizations/:organizationId/wallets/:walletId

```json
settings: {
	payment: {
		pix: true,
		bankSlip: true,
		card: true,
	},
	notification: {
		balanceLimit: {
			amount: 10000,
			email: true,
			isActive: true
		}
	}
}
```

```json
{
  customFields: [
		{
			id: "1af48e91-bf83-4467-842b-839acd176c0a",
			label: "label",
			identifier: "identifier",
			values: [
				"value1", "value2",
			]
			version: 1,
		}
  ]
}
```

```json
shared: [
	{
		id: "a5ea899d-e45f-464d-8934-aed3d9fd7f40",
		role: "OWNER",
	}
]
```

```shell
curl --location --request PUT 'https://api.platform.v2.portao3.com.br/realms/b7e3ed37-4f6f-46ef-9fe7-baede912a940/organizations/5785e88b-d2ea-453f-99f7-c562db038fbb/wallets' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <TOKEN>' \
--data '{
    "name": "Individual",
    "type": "PERSONAL",
    "settings": {
        "payment": {
            "pix": true,
            "bankSlip": true,
            "card": false
        },
        "notification": {
            "balanceLimit": {
                "amount": 10000,
                "email": true,
                "isActive": true
            }
        }
    },
    "customFields": [
		{
			"id": "1af48e91-bf83-4467-842b-839acd176c0a",
			"label": "label",
			"identifier": "identifier",
			"values": [
				"value1", "value2"
			],
			"version": 1
		}
    ],
    "shared": [
        {
            "id": "937a0b78-c4ab-4aa0-bfae-e58adc9856c0",
            "role": "OWNER"
        }
    ]
}'
```

> RESPONSE
> 200 (OK)

```json
{
  "id": "46d6ce2d-f8bd-4600-9e09-5ed299a019dd",
  "name": "WALLET_NAME",
  "createdBy": "ba2afc7f-4545-49d6-9046-e6268dbadca0",
  "updatedBy": "ba2afc7f-4545-49d6-9046-e6268dbadca0",
  "realm": "b7e3ed37-4f6f-46ef-9fe7-baede912a940",
  "organization": "5785e88b-d2ea-453f-99f7-c562db038fbb",
  "status": "ACTIVE",
  "type": "SHARED",
  "currency": "986",
  "settings": {
    "payment": {
      "bankSlip": true,
      "card": true,
      "pix": true
    }
  },
  "shared": [
    {
      "id": "a5ea899d-e45f-464d-8934-aed3d9fd7f40",
      "role": "OWNER",
      "firstName": "USER_FIRST_NAME",
      "lastName": "USER_LAST_NAME",
      "email": "user@email.com"
    }
  ],
  "customFields": [
    {
      "id": "1af48e91-bf83-4467-842b-839acd176c0a",
      "label": "label",
      "values": ["value1", "value2"],
      "identifier": "identifier",
      "version": 1
    }
  ]
}
```

> 400 (BAD REQUEST)

```json
{
  "code": "BAD_REQUEST",
  "message": "Bad Request: Your request is invalid or incomplete. Please make sure you are requesting with the right fields.",
  "fields": []
}
```

> 404 (FIELD NOT FOUND)

```json
{
  "code": "{FIELD}_NOT_FOUND",
  "traceId": "1-65b270bc-52a8e06e0b6921012c9af55d",
  "origin": "IDENTITY",
  "message": "{FIELD} not found"
}
```

Use this endpoint to update a wallet.

Path Params

| Field          | Type   | Required |
| -------------- | ------ | -------- |
| realmId        | string | true     |
| organizationId | string | true     |
| walletId       | string | true     |

Body params

| Field        | Type   | Required | Allowed values                 |
| ------------ | ------ | -------- | ------------------------------ |
| name         | string | true     |                                |
| type         | string | true     | PERSONAL, ORGANIZATION, SHARED |
| settings     | object | false    |                                |
| customFields | array  | false    |                                |
| shared       | array  | true     |                                |

Important information:

The following information must be considered before using this endpoint

Settings:
In the body, the settings field is a not required object. But if your body contains the settings field, then some fields are required:

| Field    | Type    | Required |
| -------- | ------- | -------- |
| pix      | boolean | true     |
| bankSlip | boolean | true     |
| card     | boolean | true     |
| amount   | number  | false    |
| email    | boolean | false    |
| isActive | boolean | false    |

Custom Fields:
In the body, the `customFields` field is a not required array. But if your body contains the `customFields` field, then some fields are required:

| Field      | Type            | Required |
| ---------- | --------------- | -------- |
| id         | string          | true     |
| label      | string          | false    |
| identifier | string          | false    |
| values     | array of string | true     |

Shared:
Shared is a required field that contains information about who is allowed to use the wallet and his role. Shared must have at least one item whit role OWNER.

| Field | Type             | Required | Allowed values         |
| ----- | ---------------- | -------- | ---------------------- |
| id    | string (user_id) | true     |                        |
| role  | string           | true     | OWNER, USER, READ_ONLY |

### Clear Wallet Balance

> **POST** /realms/:realmId/organizations/:organizationId/wallets/:walletId/clear-balance

```shell
curl --location --request POST 'https://api.platform.v2.portao3.com.br/realms/8d51a848-605d-4387-b508-dab63039348a/organizations/2e71c89e-25da-4a1a-a3c5-4109e5bb8d03/wallets/266cb22d-b3be-4f94-a502-1ce5f0fc77ad/clear-balance' \
--header 'Authorization: Bearer <TOKEN>'
```

> REPSONSES
> 204 (NO CONTENT)

```json
{}
```

> 403 (INSUFFICIENT PERMISSIONS)

```json
{
  "code": "INSUFFICIENT_PERMISSIONS",
  "message": "insufficient permissions"
}
```

> 403 (FIELD NOT FOUND)

```json
{
  "code": "{FIELD}_NOT_FOUND",
  "traceId": "1-65b270bc-52a8e06e0b6921012c9af55d",
  "origin": "IDENTITY",
  "message": "{FIELD} not found"
}
```

Use this endpoint to clear a wallet balance.

Path Params

| Field          | Type   | Required |
| -------------- | ------ | -------- |
| realmId        | string | true     |
| organizationId | string | true     |
| walletId       | string | true     |

## Card

### Create card

> **POST** realms/:realmId/organizations/:organizationId/wallets/:walletId/cards

```shell
curl --location 'https://api.platform.v2.portao3.com.br/realms/7499fada-8453-49fb-9e4c-ef81c2f2c4f1/organizations/26dfd2a9-f4c5-40ec-afe8-0e26690c0767/wallets/097bf9ad-9149-41a5-baca-2e1cd9867a7d/cards' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <TOKEN>' \
--data '{
    "name": "CARD VIRTUAL",
    "type": "VIRTUAL"
}'
```

> RESPONSES
> 201 (CREATED)

```json
{
  "id": "8fe742b2-faa9-4758-91e1-f35e88912887",
  "name": "CARD VIRTUAL",
  "panMasked": "524524******0876",
  "tokenisationPermitted": true,
  "expiryDate": "01/2030",
  "organization": "26dfd2a9-f4c5-40ec-afe8-0e26690c0767",
  "realm": "7499fada-8453-49fb-9e4c-ef81c2f2c4f1",
  "wallet": "097bf9ad-9149-41a5-baca-2e1cd9867a7d",
  "singleUse": false,
  "createdBy": "0cda8d0c-095e-4cec-91d8-44fbff1bb616",
  "updatedBy": "0cda8d0c-095e-4cec-91d8-44fbff1bb616",
  "type": "VIRTUAL",
  "status": "ACTIVE"
}
```

> 400 (BAD REQUEST)

```json
{
  "code": "BAD_REQUEST",
  "message": "Bad Request: Your request is invalid or incomplete. Please make sure you are requesting with the right fields.",
  "fields": []
}
```

> 403 (INSUFFICIENT PERMISSIONS)

```json
{
  "code": "INSUFFICIENT_PERMISSIONS",
  "message": "insufficient permissions"
}
```

> 403 (FORBIDDEN) - Occurs when a realm or organization is incorrect.

```json
{
  "message": "Forbidden"
}
```

Use this endpoint to create a virtual card.

Path Params

| Field          | Type   | Required |
| -------------- | ------ | -------- |
| realmId        | string | true     |
| organizationId | string | true     |
| walletId       | string | true     |

Body Params

| Field | Type   | Required | Allowed values |
| ----- | ------ | -------- | -------------- |
| name  | string | true     |                |
| type  | string | true     | VIRTUAL        |

### Get Organization Card

> **GET** realms/:realmId/organizations/:organizationId/cards

```shell
curl --location --request GET 'https://api.platform.v2.portao3.com.br/realms/5106eb38-9eca-4da5-8a8f-24e6e558b70a/organizations/db93e224-9e8a-40b6-8feb-876be2763a42/cards' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <TOKEN>' \
```

> RESPONSES
> 200 (OK)

```json
{
  "next": "65b109b430b6b793d1af2552",
  "items": [
    {
      "id": "8fe742b2-faa9-4758-91e1-f35e88912887",
      "name": "CARD VIRTUAL",
      "panMasked": "524524******0876",
      "tokenisationPermitted": true,
      "expiryDate": "01/2030",
      "organization": "26dfd2a9-f4c5-40ec-afe8-0e26690c0767",
      "realm": "7499fada-8453-49fb-9e4c-ef81c2f2c4f1",
      "wallet": "097bf9ad-9149-41a5-baca-2e1cd9867a7d",
      "singleUse": false,
      "createdBy": "0cda8d0c-095e-4cec-91d8-44fbff1bb616",
      "updatedBy": "0cda8d0c-095e-4cec-91d8-44fbff1bb616",
      "type": "VIRTUAL",
      "status": "ACTIVE"
    }
  ]
}
```

> 400 (BAD REQUEST)

```json
{
  "code": "BAD_REQUEST",
  "message": "Bad Request: Your request is invalid or incomplete. Please make sure you are requesting with the right fields.",
  "fields": []
}
```

> 403 (INSUFFICIENT PERMISSIONS)

```json
{
  "code": "INSUFFICIENT_PERMISSIONS",
  "message": "insufficient permissions"
}
```

> 403 (FORBIDDEN) - Occurs when a realm or organization is incorrect.

```json
{
  "message": "Forbidden"
}
```

Use this endpoint to get all organization cards.

Path Params

| Field          | Type   | Required |
| -------------- | ------ | -------- |
| realmId        | string | true     |
| organizationId | string | true     |

Query Params

| Field  | Type   | Required | Description                                      | Allowed values            |
| ------ | ------ | -------- | ------------------------------------------------ | ------------------------- |
| next   | string | false    | Token for paginating to the next set of results. |                           |
| limit  | number | false    | Maximum number of items to return per page.      |                           |
| name   | string | false    | Filter cards by name                             |                           |
| status | string | false    | Filter cards by status                           | ACTIVE, BLOCKED, ARCHIVED |

Important information:

- Pagination is supported through the **`next`** token provided in the response.

### Get Wallet Cards

> **GET** realms/:realmId/organizations/:organizationId/wallets/:walletId/cards

```shell
curl --location --request GET 'https://api.platform.v2.portao3.com.br/realms/5106eb38-9eca-4da5-8a8f-24e6e558b70a/organizations/db93e224-9e8a-40b6-8feb-876be2763a42/wallets/d9b0f72e-d88c-434d-9c52-0bb738498941/cards' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <TOKEN>' \
```

> RESPONSES
> 200 (OK)

```json
{
  "next": "65b109b430b6b793d1af2552",
  "items": [
    {
      "id": "8fe742b2-faa9-4758-91e1-f35e88912887",
      "name": "CARD VIRTUAL",
      "panMasked": "524524******0876",
      "tokenisationPermitted": true,
      "expiryDate": "01/2030",
      "organization": "26dfd2a9-f4c5-40ec-afe8-0e26690c0767",
      "realm": "7499fada-8453-49fb-9e4c-ef81c2f2c4f1",
      "wallet": "097bf9ad-9149-41a5-baca-2e1cd9867a7d",
      "singleUse": false,
      "createdBy": "0cda8d0c-095e-4cec-91d8-44fbff1bb616",
      "updatedBy": "0cda8d0c-095e-4cec-91d8-44fbff1bb616",
      "type": "VIRTUAL",
      "status": "ACTIVE"
    }
  ]
}
```

> 400 (BAD REQUEST)

```json
{
  "code": "BAD_REQUEST",
  "message": "Bad Request: Your request is invalid or incomplete. Please make sure you are requesting with the right fields.",
  "fields": []
}
```

> 403 (INSUFFICIENT PERMISSIONS)

```json
{
  "code": "INSUFFICIENT_PERMISSIONS",
  "message": "insufficient permissions"
}
```

> 403 (FORBIDDEN) - Occurs when a realm or organization is incorrect.

```json
{
  "message": "Forbidden"
}
```

Use this endpoint to get cards from a wallet.

Path params

| Field          | Type   | Required |
| -------------- | ------ | -------- |
| realmId        | string | true     |
| organizationId | string | true     |
| walletId       | string | true     |

Query params

| Field  | Type   | Required | Description                                      | Allowed values            |
| ------ | ------ | -------- | ------------------------------------------------ | ------------------------- |
| next   | string | false    | Token for paginating to the next set of results. |                           |
| limit  | number | false    | Maximum number of items to return per page.      |                           |
| name   | string | false    | Filter cards by name                             |                           |
| status | string | false    | Filter cards by status                           | ACTIVE, BLOCKED, ARCHIVED |

Important information:

- Pagination is supported through the **`next`** token provided in the response.

### Get Card Details

> **GET** /realms/:realmId/organizations/:organizationId/wallets/:walletId/cards/:cardId/details

```shell
curl --location --request GET 'https://api.platform.v2.portao3.com.br/realms/5106eb38-9eca-4da5-8a8f-24e6e558b70a/organizations/db93e224-9e8a-40b6-8feb-876be2763a42/wallets/d9b0f72e-d88c-434d-9c52-0bb738498941/cards/1360241d-1a13-4fea-8325-323dd56d5c4a/details' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <TOKEN>' \
```

> RESPONSES
> 200 (OK)

```json
{
  "id": "1360241d-1a13-4fea-8325-323dd56d5c4a",
  "name": "CARD_NAME",
  "panMasked": "123456******7654",
  "pan": "1234567890987654",
  "cvv": "123",
  "tokenisationPermitted": true,
  "expiryDate": "01/2030",
  "organization": "db93e224-9e8a-40b6-8feb-876be2763a42",
  "realm": "5106eb38-9eca-4da5-8a8f-24e6e558b70a",
  "wallet": "d9b0f72e-d88c-434d-9c52-0bb738498941",
  "singleUse": false,
  "createdBy": "dce54570-7e03-412f-a77f-1e02f18fd868",
  "updatedBy": "dce54570-7e03-412f-a77f-1e02f18fd868",
  "type": "VIRTUAL",
  "status": "ACTIVE"
}
```

> 400 (BAD REQUEST)

```json
{
  "code": "BAD_REQUEST",
  "message": "Bad Request: Your request is invalid or incomplete. Please make sure you are requesting with the right fields.",
  "fields": []
}
```

> 403 (INSUFFICIENT PERMISSIONS)

```json
{
  "code": "INSUFFICIENT_PERMISSIONS",
  "message": "insufficient permissions"
}
```

> 404 (NOT FOUND)

```json
{
  "code": "{FIELD}_NOT_FOUND",
  "traceId": "1-65b270bc-52a8e06e0b6921012c9af55d",
  "origin": "BANKING",
  "message": "{FIELD} not found"
}
```

Use this endpoint to get details from a card.

Path params

| Field          | Type   | Required |
| -------------- | ------ | -------- |
| realmId        | string | true     |
| organizationId | string | true     |
| walletId       | string | true     |
| cardId         | string | true     |

### Block Card

> **POST** /realms/:realmId/organizations/:organizationId/wallets/:walletId/cards/:cardId/block

```shell
curl --location --request GET 'https://api.platform.v2.portao3.com.br/realms/5106eb38-9eca-4da5-8a8f-24e6e558b70a/organizations/db93e224-9e8a-40b6-8feb-876be2763a42/wallets/d9b0f72e-d88c-434d-9c52-0bb738498941/cards/1360241d-1a13-4fea-8325-323dd56d5c4a/block' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <TOKEN>' \
```

> REPONSES
> 200 (OK)

```json
{
  "id": "1360241d-1a13-4fea-8325-323dd56d5c4a",
  "name": "CARD_NAME",
  "panMasked": "123456******7654",
  "pan": "1234567890987654",
  "cvv": "123",
  "tokenisationPermitted": true,
  "expiryDate": "01/2030",
  "organization": "db93e224-9e8a-40b6-8feb-876be2763a42",
  "realm": "5106eb38-9eca-4da5-8a8f-24e6e558b70a",
  "wallet": "d9b0f72e-d88c-434d-9c52-0bb738498941",
  "singleUse": false,
  "createdBy": "dce54570-7e03-412f-a77f-1e02f18fd868",
  "updatedBy": "dce54570-7e03-412f-a77f-1e02f18fd868",
  "type": "VIRTUAL",
  "status": "BLOCKED"
}
```

> 400 (BAD REQUEST)

```json
{
  "code": "BAD_REQUEST",
  "message": "Bad Request: Your request is invalid or incomplete. Please make sure you are requesting with the right fields.",
  "fields": []
}
```

> 403 (INSUFFICIENT PERMISSIONS)

```json
{
  "code": "INSUFFICIENT_PERMISSIONS",
  "message": "insufficient permissions"
}
```

> 403 (FORBIDDEN) - Occurs when a realm or organization is incorrect.

```json
{
  "message": "Forbidden"
}
```

> 404 (FIELD NOT FOUND)

```json
{
  "code": "{FIELD}_NOT_FOUND",
  "traceId": "1-65b270bc-52a8e06e0b6921012c9af55d",
  "origin": "BANKING",
  "message": "{FIELD} not found"
}
```

Use this endpoint to block a card.

Path Params

| Field          | Type   | Required |
| -------------- | ------ | -------- |
| realmId        | string | true     |
| organizationId | string | true     |
| walletId       | string | true     |
| cardId         | string | true     |

## Pix

Use this endpoint to initiate a Pix transaction using the DICT key or EMV of the credited party. To create a Pix payment using the the DICT key, you must perform the following steps:

Step 1 - Initiate the Pix payment using the DICT key of the credited party.

### Initiate Pix

> **POST** /realms/:realmId/organizations/:organizationId/wallets/:walletId/pix

```shell
curl --location 'https://api.platform.v2.portao3.com.br/realms/3db25756-a1ae-4e13-a00b-9cab3cd68dcf/organizations/f9084d72-fd46-4065-80c0-8a4ce4ba35a6/wallets/default/pix' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <TOKEN>' \
--data-raw '{
    "amount": "10000",
    "description": "Pix",
    "key": "someone@dictkey.com",
    "dict": "EMAIL",
    "initiationType": "DICT"
}'
```

> RESPONSE
> 200 (OK)

```json
{
  "environment": "LIVE",
  "realmId": "3db25756-a1ae-4e13-a00b-9cab3cd68dcf",
  "organizationId": "f9084d72-fd46-4065-80c0-8a4ce4ba35a6",
  "accountId": "6500a6968956183d96ed5dr4",
  "walletId": "65031ef0659fd5018a9d3827",
  "txnCurrency": "986",
  "txnAllowAmountChange": false,
  "txnOriginalAmount": 10000,
  "txnDiscountAmount": 0,
  "txnFineAmount": 0,
  "txnInterestAmount": 0,
  "txnPurchaseAmount": 0,
  "txnWithdrawalAmount": 0,
  "txnUpdatedAmount": 10000,
  "creditParty": {
    "bankIspb": "12345678",
    "document": "***.123.456-**",
    "key": "someone@dictkey.com",
    "name": "RECEIVER_NAME",
    "_id": "65b2c5a6fe07df79497d0ac2"
  },
  "debitParty": {
    "bankIspb": "12345678",
    "accountType": "TRAN",
    "document": "83939183000132",
    "name": "PORTÃO 3",
    "_id": "65b2c5a6fe07df79497d0ab2"
  },
  "description": "Pix",
  "receipt": {
    "endToEndId": "E31680151202401252033703NKF9TV4W"
  },
  "initiationType": "DICT",
  "status": "REQUESTED",
  "transactionType": "TRANSFER",
  "confirmedAmount": 0,
  "_id": "65b2c5a6fe07df79497d0abc",
  "additionalInfo": [],
  "createdAt": "2024-01-25T20:33:42.959Z",
  "updatedAt": "2024-01-25T20:33:42.959Z",
  "__v": 0,
  "external": {}
}
```

> 400 (BAD REQUEST)

```json
{
  "code": "BAD_REQUEST",
  "message": "Bad Request: Your request is invalid or incomplete. Please make sure you are requesting with the right fields.",
  "fields": []
}
```

> 403 (INSUFFICIENT PERMISSIONS)

```
{
	"code": "INSUFFICIENT_PERMISSIONS",
	"message": "insufficient permissions"
}
```

> 403 (FORBIDDEN) - Occurs when a realm or organization is incorrect.

```json
{
  "message": "Forbidden"
}
```

> 500 (INTERNAL SERVER ERROR)

```json
{
  "code": "ERR_BAD_REQUEST",
  "traceId": "1-65b2c689-762893851e0f3f505713b2b1",
  "origin": "BANKING",
  "message": "Request failed with status code 400"
}
```

Path Params

| Field          | Type   | Required |
| -------------- | ------ | -------- |
| realmId        | string | true     |
| organizationId | string | true     |
| walletId       | string | true     |

Body params

| Field          | Type   | Required | Allowed values               | Description                                                              |
| -------------- | ------ | -------- | ---------------------------- | ------------------------------------------------------------------------ |
| initiationType | string | true     | DICT, COPY_PASTE             |                                                                          |
| dict           | string | false    | PHONE, EMAIL, CPF, CNPJ, EVP |                                                                          |
| key            | string | false    |                              | The DICT key of the person who will receive the transaction.             |
| emv            | string | false    |                              |                                                                          |
| amount         | number | false    |                              | The amount that will be transferred, in cents. Must be a positive value. |
| description    | string | false    |                              |                                                                          |

Important information:

The following information must be considered before using this endpoint.

Dict:
If `initiationType` is DICT, then `dict` is a required field.

Key:
if `dict` , then `key` is a required field.

Emv:
If `initiationType` is COPY_PAST, then `emv` is a required field.

Amount:
If `initiationType` is DICT, then `amount` is a required field.

Portão 3 will return the details about the key owner (credited party). You must display this information to the user for validation.

Step 2- Confirm the payment

After the user validation, confirm the PIX payment using the Confirm Pix endpoint.

### Confirm Pix

> **POST** /realms/:realmId/organizations/:organizationId/wallets/:walletId/pix/:pidId/confirm

```json
{
  customFields: [
		{
			id: "1af48e91-bf83-4467-842b-839acd176c0a",
			label: "label",
			identifier: "identifier",
			values: [
				"value1", "value2",
			]
			version: 1,
		}
  ]
}
```

```shell
curl --location 'https://api.platform.v2.portao3.com.br/realms/3db25756-a1ae-4e13-a00b-9cab3cd68dcf/organizations/f9084d72-fd46-4065-80c0-8a4ce4ba35a6/wallets/default/pix/65b2c5a6fe07df79497d0abc/confirm' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <TOKEN>' \
--data '{
    "amount": 10000,
    "category": "FLEX_INTERNATIONAL",
    "customFields": [{
        "id": "1af48e91-bf83-4467-842b-839acd176c0a",
        "version": 1,
        "label": "label",
        "identifier": "identifier",
        "values": [ "value1", "value2" ]
    }]
}'
```

> REPONSES
> 200 (OK)

```json
{
		"environment": "LIVE",
    "realmId": "3db25756-a1ae-4e13-a00b-9cab3cd68dcf",
    "organizationId": "f9084d72-fd46-4065-80c0-8a4ce4ba35a6",
    "accountId": "6500a6968956183d96ed5dr4",
    "walletId": "65031ef0659fd5018a9d3827",
    "txnCurrency": "986",
    "txnAllowAmountChange": false,
    "txnOriginalAmount": 10000,
    "txnDiscountAmount": 0,
    "txnFineAmount": 0,
    "txnInterestAmount": 0,
    "txnPurchaseAmount": 0,
    "txnWithdrawalAmount": 0,
    "txnUpdatedAmount": 10000,
    "creditParty": {
        "bankIspb": "12345678",
        "document": "***.123.456-**",
        "key": "someone@dictkey.com",
        "name": "RECEIVER_NAME",
        "_id": "65b2c5a6fe07df79497d0ac2"
    },
    "debitParty": {
        "bankIspb": "12345678",
        "accountType": "TRAN",
        "document": "83939183000132",
        "name": "PORTÃO 3",
        "_id": "65b2c5a6fe07df79497d0ab2"
    },
    "description": "Pix",
    "receipt": {
        "endToEndId": "E31680151202401252033703NKF9TV4W"
    },
    "initiationType": "DICT",
    "status": "REQUESTED",
    "transactionType": "TRANSFER",
    "confirmedAmount": 0,
    "_id": "65b2c5a6fe07df79497d0abc",
    "additionalInfo": [],
    "createdAt": "2024-01-25T20:33:42.959Z",
    "updatedAt": "2024-01-25T20:33:42.959Z",
    "__v": 0,
    "external": {
        "0": {
		        "id": "1af48e91-bf83-4467-842b-839acd176c0a",
		        "version": 1,
		        "label": "label",
		        "identifier": "identifier",
		        "values": [ "value1", "value2" ]
            "_id": "65b2ca68eb6577bf3c968f5d"
        }
    }
}
```

> 400 (BAD REQUEST)

```json
{
  "code": "BAD_REQUEST",
  "message": "Bad Request: Your request is invalid or incomplete. Please make sure you are requesting with the right fields.",
  "fields": []
}
```

> 403 (INSUFFICIENT PERMISSIONS)

```json
{
  "code": "INSUFFICIENT_PERMISSIONS",
  "message": "insufficient permissions"
}
```

> 403 (FORBIDDEN) - Occurs when a realm or organization is incorrect.

```json
{
  "message": "Forbidden"
}
```

> 500 (INTERNAL SERVER ERROR)

```json
{
  "code": "ERR_BAD_REQUEST",
  "traceId": "1-65b2c689-762893851e0f3f505713b2b1",
  "origin": "BANKING",
  "message": "Request failed with status code 400"
}
```

Path Params

| Field          | Type   | Required |
| -------------- | ------ | -------- |
| realmId        | string | true     |
| organizationId | string | true     |
| walletId       | string | true     |
| pixId          | string | true     |

Body Params

| Field        | Type   | Required | Allowed values                              |
| ------------ | ------ | -------- | ------------------------------------------- |
| amount       | number | true     |                                             |
| category     | string | false    | FLEX_INTERNATIONAL (default), FLEX_NATIONAL |
| customFields | array  | false    |                                             |

Important information:

The following information must be considered before using this endpoint.

Custom Fields:
In the body, the `customFields` field is a not required array. But if your body contains the `customFields` field, then some fields are required:

| Field      | Type            | Required |
| ---------- | --------------- | -------- |
| id         | string          | true     |
| label      | string          | false    |
| identifier | string          | false    |
| values     | array of string | true     |
