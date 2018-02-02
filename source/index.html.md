---
title: Pentamic Accounting APIs Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='mailto:info@pentamic.com'>Contact our administrator</a>
  - <a href='http://pentamic.com'>Pentamic Website</a>

includes:
  - api-refrerence
  - errors

search: true
---

# Introduction

## Overview

> This is the code example pane. APIs using examples will display here.

Welcome to the Pentamic Accounting APIs!

The purposes of these APIs are:

* To provide access to Pentamic Accounting centralized server instance from Pentamic Accounting client applications.
* Easily & securely integrating with other applications using widely accepted protocols and standards.

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

* Contact our administrator to get specific APIs informations like URLs, generated clients,...
* Use the Client ID and Client Secret to authenticate with our Authentication services and get an access token.
* Use the access token to interact with the APIs.

# Testing

For testing purpose, the examples in this APIs docs use cURL as a HTTP Client to connect to the APIs.
cURL is a open source command line tool and library for transferring data with URLs.
You can download and learn cURL [here](https://curl.haxx.se/)

> Example HTTP GET Request using cURL

```shell
  curl https://curl.haxx.se
```

# Authentication

Pentamic use separated authentication services to provide authentication to many of our applications.

The authentication services follow the OpenId Connect protocol and can authenticate both applications and users.

For the integration purpose, we only demonstrate application authentications using Client Credentials flow.

## Request token

Contact our administrator and get the specific client information, include:

* Authentication server URL
* Your Client ID and Client Secret
* Your allowed scope

After getting the information, request a token from the authentication services by sending a post request to the token endpoint `/connect/token` with grant type `client_credentials`

> Request token:

```shell
curl -X POST
     -H "Content-Type: application/x-www-form-urlencoded"
     -H "Cache-Control: no-cache"
     -d 'client_id=clientid&scope=allowedscope&client_secret=clientsecret&grant_type=client_credentials'
     "https://identity.pentamic.com/connect/token"
```

> Replace `clientid`, `clientsecret`, `allowedscope` with your Client ID and Secret.

## Token response

### Result

> Success request result:

```json
{
  "access_token": "eyJh...",
  "expires_in": 3600,
  "token_type": "Bearer"
}
```

**Explain:**

| Field          | Meaning                              |
| -------------- | ------------------------------------ |
| `access_token` | The access token string              |
| `token_type`   | Type of the received token           |
| `expires_in`   | Time the token will expire in second |

### Error

> Request error result:

```json
{
  "error": "error_code"
}
```

Possible error code:

| Error                    | Meaning                                                                                 |
| ------------------------ | --------------------------------------------------------------------------------------- |
| `invalid_client`         | The client id or client secret is not correct. Check typo or contact our administrator. |
| `invalid_scope`          | The scope is not correct or the client does not allowed to access this scope            |
| `unsupported_grant_type` | The grant type is not correct. It must be `client_credentials`.                         |

## Making request

Add the access token string you received to future API requests authorization header as following:

`Authorization: {token_type} {access_token}`

> Example using token:

```shell
curl -X Get
     -H "Authorization: Bearer access_token"
     -H "Cache-Control: no-cache"
     "http://api.pentamic.com/api/customers"
```

> Replace and `access_token` with your access token string.

## Refresh token

The client credential authorization flow does not support refresh token so when the token expired, you must request a new one using the methods above.
