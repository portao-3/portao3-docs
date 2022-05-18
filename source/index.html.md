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

# Users

User management to every passenger, card holder or company employee that have access to the platform.

## Retrieve Users

> **GET** https://api.portao3.com.br/organization/users

```shell
curl -X GET https://api.portao3.com.br/organization/users \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
```

> **200** Response

```json
[
  {
    "uid": "B9InbYzWM3bBGSwX2M5muYbLkAv1",
    "firstName": "John",
    "lastName": "Doe",
    "email": "john@doe.com",
    "admin": true,
    "avatar": "https://app.portao3.com.br/johndoe.png",
    "birthdate": "31/12/1990",
    "companyId": "000001",
    "role": "Diretor",
    "mobilePhoneNumber": "(99) 99999-9999",
    "gender": "MALE",
    "documents": {
      "cnh": {
        "number": "12345678",
        "validUntil": "31/12/2025"
      },
      "cpf": {
        "number": "111.111.111-11"
      },
      "passport": {
        "country": "BR",
        "number": "NT12345",
        "validUntil": "31/12/2025",
      },
      "rg": {
        "emitter": "SSPMG",
        "number": "15683942",
      }
    },
    "project": {
      "id": "sT9OPjOnetwj4Q6q776t",
      "name": "Apple"
    },
    "costCenter": {
      "id": "DtG2lWrblX1yLx9Z2c7L",
      "name": "Finance",
    },
    "status": "ACTIVE",
  },
  {
    ...
  }
]
```

This will retrieve the users for an organization.

## Create a User

> **POST** https://api.portao3.com.br/organization/users

```shell
curl -X POST https://api.portao3.com.br/organization/users \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}' \
  -D '{
    "firstName": "John",
    "lastName": "Doe",
    "email": "john@doe.com",
    "birthdate": "31/12/1990",
    "companyId": "000001",
    "role": "Diretor",
    "mobilePhoneNumber": "(99) 99999-9999",
    "gender": "MALE",
    "documents": {
      "cnh": {
        "number": "12345678",
        "validUntil": "31/12/2025"
      },
      "cpf": {
        "number": "111.111.111-11"
      },
      "passport": {
        "country": "BR",
        "number": "NT12345",
        "validUntil": "31/12/2025"
      },
      "rg": {
        "emitter": "SSPMG",
        "number": "15683942"
      }
    },
    "project": {
      "id": "sT9OPjOnetwj4Q6q776t",
      "name": "Apple"
    },
    "costCenter": {
      "id": "DtG2lWrblX1yLx9Z2c7L",
      "name": "Finance"
    }
  }'
```

> **201** Response

```json
{
  "uid": "B9InbYzWM3bBGSwX2M5muYbLkAv1",
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@doe.com",
  "admin": true,
  "avatar": "https://app.portao3.com.br/johndoe.png",
  "birthdate": "31/12/1990",
  "companyId": "000001",
  "role": "Diretor",
  "mobilePhoneNumber": "(99) 99999-9999",
  "gender": "MALE",
  "documents": {
    "cnh": {
      "number": "12345678",
      "validUntil": "31/12/2025"
    },
    "cpf": {
      "number": "111.111.111-11"
    },
    "passport": {
      "country": "BR",
      "number": "NT12345",
      "validUntil": "31/12/2025"
    },
    "rg": {
      "emitter": "SSPMG",
      "number": "15683942"
    }
  },
  "project": "sT9OPjOnetwj4Q6q776t",
  "costCenter": "DtG2lWrblX1yLx9Z2c7L",
  "status": "ACTIVE"
}
```

This will create a new user for the organization

### Parameters

#### firstName **REQUIRED**

The first name of the person, this should be equal to the name in a government ID as to make issuing travel and credit cards for the user a breeze.

#### lastName **REQUIRED**

The last names of the person, this should be equal to the name in a government ID as to make issuing travel and credit cards for the user a breeze.

#### email **REQUIRED**

The email address for the user.

#### birthdate **REQUIRED**

The birth date for the user, using the format DD/MM/YYYY. This should be equal to the name in a government ID as to make issuing travel and credit cards for the user a breeze.

#### companyId

The ID for the user inside the organization. Usefull for integrating our solution with other third party systems in HR.

#### role

The role for the user inside the organization. Usefull for creating policies based on the role for the person.

#### mobilePhoneNumber

The mobile phone number for the user, using the format (99) 99999-9999. Altough we will try to match other formats to this one, sending it correctly guarantees the integration works always the best way possible. It is not required, but usefull in case someone on our team needs to get ahold of the passenger to send additional information about a reservation.

#### gender

The gender for the user, it should be either "MALE" or "FEMALE". Altough we, as a company, value every human that identifies with every gender, this is unfortunately standard while issuing air tickets for other countries or managing hotel reservations where sharing rooms are directed with specific laws for each country.

#### documents.cnh.number

The number for the user's Brazilian driver license. Although it is not required, it may be usefull to fill it out if a user ever needs to rent a car.

#### documents.cnh.validUntil

The expiration for the user's Brazilian driver license, using the format DD/MM/YYYY. Although it is not required, it may be usefull to fill it out if a user ever needs to rent a car.

#### documents.cpf.number **REQUIRED**

The government ID for the user, using the format 999.999.999-99 and a valid verification code. It is used whenever we have to issue reservations or credit cards for a user.

#### documents.passport.country

The country ID according to [ISO 3166](https://www.iso.org/iso-3166-country-codes.html) for the user's passport. It is a two digit string. Although it is not required, it is used whenever we have to issue reservations to other countries for a user.

#### documents.passport.number

The number of the passport for the user's passport. Although it is not required, it is used whenever we have to issue reservations to other countries for a user.

#### documents.passport.validUntil

The expiration for the user's Brazilian driver license, using the format DD/MM/YYYY. Although it is not required, it is used whenever we have to issue reservations to other countries for a user.

#### documents.rg.emitter

The government ID issuer for the user. Although it is not required, it may be used while issuing some hotel stays for a user.

#### documents.rg.number

The government ID number for the user. Although it is not required, it may be used while issuing some hotel stays for a user.

#### project

The project ID related to the user. Should be a valid ID from a project created inside the platform. Although it is not required, it will auto-fill the information whenever a user requests a travel or a budget.

#### costCenter

The cost center ID related to the user. Should be a valid ID from a cost center created inside the platform. Although it is not required, it will auto-fill the information whenever a user requests a travel or a budget.

## Update a User

> **PUT** https://api.portao3.com.br/organization/users/{id}

```shell
curl -X PUT https://api.portao3.com.br/organization/users/{id} \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}' \
  -D '{
    "firstName": "John",
    "lastName": "Doe",
    "email": "john@doe.com",
    "birthdate": "31/12/1990",
    "companyId": "000001",
    "role": "Diretor",
    "mobilePhoneNumber": "(99) 99999-9999",
    "gender": "MALE",
    "documents": {
      "cnh": {
        "number": "12345678",
        "validUntil": "31/12/2025"
      },
      "cpf": {
        "number": "111.111.111-11"
      },
      "passport": {
        "country": "BR",
        "number": "NT12345",
        "validUntil": "31/12/2025"
      },
      "rg": {
        "emitter": "SSPMG",
        "number": "15683942"
      }
    },
    "project": {
      "id": "sT9OPjOnetwj4Q6q776t",
      "name": "Apple"
    },
    "costCenter": {
      "id": "DtG2lWrblX1yLx9Z2c7L",
      "name": "Finance"
    }
  }'
```

> **201** Response

```json
{
  "uid": "B9InbYzWM3bBGSwX2M5muYbLkAv1",
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@doe.com",
  "admin": true,
  "avatar": "https://app.portao3.com.br/johndoe.png",
  "birthdate": "31/12/1990",
  "companyId": "000001",
  "role": "Diretor",
  "mobilePhoneNumber": "(99) 99999-9999",
  "gender": "MALE",
  "documents": {
    "cnh": {
      "number": "12345678",
      "validUntil": "31/12/2025"
    },
    "cpf": {
      "number": "111.111.111-11"
    },
    "passport": {
      "country": "BR",
      "number": "NT12345",
      "validUntil": "31/12/2025"
    },
    "rg": {
      "emitter": "SSPMG",
      "number": "15683942"
    }
  },
  "project": "sT9OPjOnetwj4Q6q776t",
  "costCenter": "DtG2lWrblX1yLx9Z2c7L",
  "status": "ACTIVE"
}
```

This will update a user for the organization

### Parameters

#### firstName **REQUIRED**

The first name of the person, this should be equal to the name in a government ID as to make issuing travel and credit cards for the user a breeze.

#### lastName **REQUIRED**

The last names of the person, this should be equal to the name in a government ID as to make issuing travel and credit cards for the user a breeze.

#### email **REQUIRED**

The email address for the user.

#### birthdate **REQUIRED**

The birth date for the user, using the format DD/MM/YYYY. This should be equal to the name in a government ID as to make issuing travel and credit cards for the user a breeze.

#### companyId

The ID for the user inside the organization. Usefull for integrating our solution with other third party systems in HR.

#### role

The role for the user inside the organization. Usefull for creating policies based on the role for the person.

#### mobilePhoneNumber

The mobile phone number for the user, using the format (99) 99999-9999. Altough we will try to match other formats to this one, sending it correctly guarantees the integration works always the best way possible. It is not required, but usefull in case someone on our team needs to get ahold of the passenger to send additional information about a reservation.

#### gender

The gender for the user, it should be either "MALE" or "FEMALE". Altough we, as a company, value every human that identifies with every gender, this is unfortunately standard while issuing air tickets for other countries or managing hotel reservations where sharing rooms are directed with specific laws for each country.

#### documents.cnh.number

The number for the user's Brazilian driver license. Although it is not required, it may be usefull to fill it out if a user ever needs to rent a car.

#### documents.cnh.validUntil

The expiration for the user's Brazilian driver license, using the format DD/MM/YYYY. Although it is not required, it may be usefull to fill it out if a user ever needs to rent a car.

#### documents.cpf.number **REQUIRED**

The government ID for the user, using the format 999.999.999-99 and a valid verification code. It is used whenever we have to issue reservations or credit cards for a user.

#### documents.passport.country

The country ID according to [ISO 3166](https://www.iso.org/iso-3166-country-codes.html) for the user's passport. It is a two digit string. Although it is not required, it is used whenever we have to issue reservations to other countries for a user.

#### documents.passport.number

The number of the passport for the user's passport. Although it is not required, it is used whenever we have to issue reservations to other countries for a user.

#### documents.passport.validUntil

The expiration for the user's Brazilian driver license, using the format DD/MM/YYYY. Although it is not required, it is used whenever we have to issue reservations to other countries for a user.

#### documents.rg.emitter

The government ID issuer for the user. Although it is not required, it may be used while issuing some hotel stays for a user.

#### documents.rg.number

The government ID number for the user. Although it is not required, it may be used while issuing some hotel stays for a user.

#### project

The project ID related to the user. Should be a valid ID from a project created inside the platform. Although it is not required, it will auto-fill the information whenever a user requests a travel or a budget.

#### costCenter

The cost center ID related to the user. Should be a valid ID from a cost center created inside the platform. Although it is not required, it will auto-fill the information whenever a user requests a travel or a budget.

## Delete a User

> **DELETE** https://api.portao3.com.br/organization/users/{id}

```shell
curl -X DELETE https://api.portao3.com.br/organization/users/{id} \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
```

> **204** Response

```text
NO CONTENT
```

This will delete a User.
