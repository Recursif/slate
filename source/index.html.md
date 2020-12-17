---
title: API Reference

language_tabs: 
  - shell
  - javascript

toc_footers:

includes:
  - references

search: true

code_clipboard: true
---

# Get Started

Welcome to the Linkcy's API!

Before starting, make sure that you have created your CLIENT_ID and CLIENT_SECRET as they will be used across all the documentation. You can generate them in the configuration page in the dashboard.

By the end of this section, you will be able to register a new customer and issue him bank account and cards using Linkcy services.


## Register a new customer

```shell
curl -X POST 'https://api.linkcy.io/entities/' \
  -u CLIENT_ID:CLIENT_SECRET | jq
```

```javascript
const axios = require("axios");
const config = {
  auth: { username: "CLIENT_ID", password: "CLIENT_SECRET" },
  headers: {
    Accept: "application/vnd.api+json",
    "Content-Type": "application/vnd.api+json",
  },
};

const entity = {
  firstName: "firstName",
  lastName: "lastName",
  mail: "mail",
  phone: "phone"
}

axios.post("https://api.linkcy.io/entities/", entity, config)

/* return */

return {
  entityId: "4dd0a464-131e-4571-8bae-c1fc865071b1"
  firstName: "firstName",
  lastName: "lastName",
  mail: "mail",
  phone: "phone"
  ...
}

```


Before issuing bank account and cards to your customers, you'll need to register your customers into our system.

<aside class="notice">
  Make sure to replace `CLIENT_ID` & `CLIENT_SECRET` with your API key.
</aside>


## Issue a Bank account to a customer

```shell
curl -X POST 'https://api.linkcy.io/bank/accounts/' \
  -u CLIENT_ID:CLIENT_SECRET | jq
```

```javascript
const axios = require("axios");
const config = {
  auth: { username: "CLIENT_ID", password: "CLIENT_SECRET" },
  headers: {
    Accept: "application/vnd.api+json",
    "Content-Type": "application/vnd.api+json",
  },
};

const entityId = "4dd0a464-131e-4571-8bae-c1fc865071b1"

axios.post("https://api.linkcy.io/bank/accounts/", entityId, config)

/* return */

return {
  accountId: "aae6accf-8338-4174-908a-0d5642b9db6c"
  entityId: "4dd0a464-131e-4571-8bae-c1fc865071b1",
  iban: "GB84 TEST 1191 1608 1377 51",
  bic: "TESTGB21",
  ...
}


```

This endpoint allow you to bank account to your customer.

<aside class="success">
  Your customer will be able to fund their account using the IBAN and BIC prodived in the response!
</aside>

## Issue a Card to a customer

```shell
curl -X POST 'https://api.linkcy.io/cards/' \
  -u CLIENT_ID:CLIENT_SECRET | jq
```


```javascript
const axios = require("axios");
const config = {
  auth: { username: "CLIENT_ID", password: "CLIENT_SECRET" },
  headers: {
    Accept: "application/vnd.api+json",
    "Content-Type": "application/vnd.api+json",
  },
};

const accountId = "aae6accf-8338-4174-908a-0d5642b9db6c"

axios.post("https://api.linkcy.io/cards/", accountId, config)

/* return */

return {
  cardId: "8ace41a9-3b8f-4ae4-88f4-69a818ba238e"
}

```

This endpoint allow you to issue a card to your customer.

<aside class="success">
  Your customer will receive his new card within 4 to 14 days!
</aside>


# Entities

## Get a Customer

```shell
curl -X POST 'https://api.linkcy.io/entities/:entityId' \
  -u CLIENT_ID:CLIENT_SECRET | jq
```


```javascript
const axios = require("axios");
const config = {
  auth: { username: "CLIENT_ID", password: "CLIENT_SECRET" },
  headers: {
    Accept: "application/vnd.api+json",
    "Content-Type": "application/vnd.api+json",
  },
};
axios.post("https://api.linkcy.io/entities/:entityId", null, config)
```

This endpoint retrieves a customer by it's id.

## Get all your Customers

```shell
curl -X GET 'https://api.linkcy.io/entities/' \
  -u CLIENT_ID:CLIENT_SECRET | jq
```


```javascript
const axios = require("axios");
const config = {
  auth: { username: "CLIENT_ID", password: "CLIENT_SECRET" },
  headers: {
    Accept: "application/vnd.api+json",
    "Content-Type": "application/vnd.api+json",
  },
};
axios.get("https://api.linkcy.io/entities/", null, config)
```

This endpoint retrieves all your customers registred on Linkcy Services.


# Bank Accounts

## Get all transactions of one customer's bank account 

```shell
curl -X POST 'https://api.linkcy.io/ledgers/:entityId' \
  -u CLIENT_ID:CLIENT_SECRET | jq
```


```javascript
const axios = require("axios");
const config = {
  auth: { username: "CLIENT_ID", password: "CLIENT_SECRET" },
  headers: {
    Accept: "application/vnd.api+json",
    "Content-Type": "application/vnd.api+json",
  },
};
axios.post("https://api.linkcy.io/ledgers/:entityId", null, config)
```

This endpoint retrieves all transactions from a customer's bank account.


# Cards

## Get your customer's card details

```shell
curl -X POST 'https://api.linkcy.io/cards/details/:entityId' \
  -u CLIENT_ID:CLIENT_SECRET | jq
```


```javascript
const axios = require("axios");
const config = {
  auth: { username: "CLIENT_ID", password: "CLIENT_SECRET" },
  headers: {
    Accept: "application/vnd.api+json",
    "Content-Type": "application/vnd.api+json",
  },
};
axios.post("https://api.linkcy.iocards/details/:entityId", null, config)

```

This endpoint retrieves your customer's card details.

## Get the PIN of your customer's card

```shell
curl -X GET 'https://api.linkcy.io/cards/pin/:entityId' \
  -u CLIENT_ID:CLIENT_SECRET | jq
```


```javascript
const axios = require("axios");
const config = {
  auth: { username: "CLIENT_ID", password: "CLIENT_SECRET" },
  headers: {
    Accept: "application/vnd.api+json",
    "Content-Type": "application/vnd.api+json",
  },
};
axios.get("https://api.linkcy.io/cards/pin/:entityId", null, config)

```

This endpoint retrieves the pin of your customer's card.

## Reset the PIN of your customer's card

```shell
curl -X POST 'https://api.linkcy.io/cards/pin/:entityId' \
  -u CLIENT_ID:CLIENT_SECRET | jq
```


```javascript
const axios = require("axios");
const config = {
  auth: { username: "CLIENT_ID", password: "CLIENT_SECRET" },
  headers: {
    Accept: "application/vnd.api+json",
    "Content-Type": "application/vnd.api+json",
  },
};
axios.post("https://api.linkcy.io/cards/pin/:entityId", null, config)

```

This endpoint reset your customer's card pin code.


## Suspend your customer's card

```shell
curl -X POST 'https://api.linkcy.io/cards/suspend' \
  -u CLIENT_ID:CLIENT_SECRET | jq
```


```javascript
const axios = require("axios");
const config = {
  auth: { username: "CLIENT_ID", password: "CLIENT_SECRET" },
  headers: {
    Accept: "application/vnd.api+json",
    "Content-Type": "application/vnd.api+json",
  },
};
axios.post("https://api.linkcy.io/cards/suspend", null, config)

```

This endpoint allows you to enable or disable your customer's card.




