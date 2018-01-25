---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

## Overview

Welcome to the Pentamic Accounting APIs!

The purposes of these APIs are:

- To provide access to Pentamic Accounting centralized server instance from Pentamic Accounting client applications.
- Easily & securely integrating with other applications using widely accepted protocols and standards.

This document provide technical information and manual for developers who want to interact with the Pentamic Accounting APIs.

## Protocol

Pentamic Accounting APIs are HTTP based APIs. We attempts to design our APIs conform to the RESTful principles. So you can interact with the APIs resources using HTTP Verbs (GET, POST, PUT, DELETE) and receive standard HTTP results.

## Supported format

Pentamic Accounting API supports both XML and JSON format for transferring data.
JSON is the primary and recommended format because it is faster, smaller and easier to read. But we still support XML for older apps that don't understand JSON.

## Security

You can connect to the Pentamic Accouting APIs using HTTP or HTTPS (SSL), but the APIs only use Self-Signed Certificate.

# Basic steps

To connect to Pentamic Accounting APIs, follow these steps:

- Contact our administrator to get specific APIs URLs, Client ID and Client Secret.
- Use the Client ID and Client Secret to authenticate with our Authentication services and get an access token.
- Use the access token to interact with the APIs.

# Testing

For testing purpose, the examples in this APIs docs use cURL as a HTTP Client to connect to the APIs.

# Authentication

Pentamic use separated authentication services to provide authentication to many of our applications.

The authentication services follow the OpenId Connect protocol and can authenticate both applications and users.

For the integration purpose, we only demonstrate application authentications using Client Credentials flow.

## Request token

After getting the Client ID and Client Secret, request a token from the authentication services.

> Request token:

```shell
curl -X POST
     -H "Content-Type: application/x-www-form-urlencoded"
     -H "Cache-Control: no-cache"
     -d 'client_id=clientid&scope=pa-api&client_secret=clientsecret&grant_type=client_credentials'
     "http://identity.pentamic.com.vn/connect/token"
```

> Replace `clientid` and `clientsecret` with your Client ID and Secret.

## Add token to API request header

> Using token:

```shell
curl -X POST
     -H "Content-Type: application/x-www-form-urlencoded"
     -H "Cache-Control: no-cache"
     -d 'client_id=clientid&scope=pa-api&client_secret=clientsecret&grant_type=client_credentials'
     "http://identity.pentamic.com.vn/connect/token"
```

## Get All Kittens


```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

| Parameter    | Default | Description                                                                      |
| ------------ | ------- | -------------------------------------------------------------------------------- |
| include_cats | false   | If set to true, the result will also include cats.                               |
| available    | true    | If set to false, the result will include kittens that have already been adopted. |

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

| Parameter | Description                      |
| --------- | -------------------------------- |
| ID        | The ID of the kitten to retrieve |

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The ID of the kitten to delete |

