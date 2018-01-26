# API Reference

<aside class="warning">
The api endpoints listed here are for demonstration purpose only. The real life APIs will be subject for change according to specific integration requirements.
</aside>

## Customers

> Sample request

```shell
curl -X GET
     -H "Authorization: Bearer access_token"
     http://api.pentamic.com/api/customers?orderBy=name
```

> Sample response

```json
[
    {
        "id": 102568,
        "name": "Nguyen Van Thanh",
        "taxCode": 0106459932,
        "address": "Phuong Dong Hoa, Di An, Binh Duong",
        "phone": "0123456789"
    }
]
```

### Get list of customers

Get a list of customers with specific filters.

#### Request

`GET http://api.pentamic.com/api/customers/`

#### Query Parameters

| Parameter | Required | Default | Description                                                   |
| --------- | -------- | ------- | ------------------------------------------------------------- |
| orderBy   | `false`  | `null`  | Field name to order the list. Add `desc` to order descending. |

#### Response

List of customers in JSON format.

### Create a customer

> Sample request

```shell
curl -X POST
     -H "Authorization: Bearer access_token"
     -H "Content-Type: application/json"
     -d '{"name":"Nguyen Van Thanh","taxCode":0106459932,"address":"Phuong Dong Hoa, Di An, Binh Duong","phone":"0123456789"}'
     http://api.pentamic.com/api/customers
```

#### Request

`POST http://api.pentamic.com/api/customers/`

#### Request body

| Field     | Data type | Required | Description                  |
| --------- | --------- | -------- | ---------------------------- |
| `name`    | string    | `true`   | Name of the customer         |
| `taxCode` | int       | `true`   | Tax code of the customer     |
| `address` | string    | `false`  | Address of the customer      |
| `phone`   | string    | `false`  | Phone number of the customer |

#### Response

Return HTTP response code 200 and the customer when the customer is successfully created.
Return HTTP response code 403 and the error code in the body if the creating process failed.

#### Errors

> Error response body

```json
{
    "error": "errorCode"
}
```

| Error           | Description                        |
| --------------- | ---------------------------------- |
| `NAME_REQUIRED` | The name field has been missing    |
| `TAXC_REQUIRED` | The taxCode field has been missing |
| `TAXC_INVALID`  | The taxCode value is invalid       |

### Update a customer

> Sample request

```shell
curl -X PUT
     -H "Authorization: Bearer access_token"
     -H "Content-Type: application/json"
     -d '{"name":"Nguyen Van Thanh","taxCode":0106459932,"address":"Phuong Dong Hoa, Di An, Binh Duong","phone":"0123456789"}'
     http://api.pentamic.com/api/customers/102568
```

#### Request

`PUT http://api.pentamic.com/api/customers/{id}`

#### URL Parameters

| Field | Data type | Required | Description                     |
| ----- | --------- | -------- | ------------------------------- |
| `id`  | int       | `true`   | ID of the customer to be update |

#### Request body

| Field     | Data type | Required | Description                  |
| --------- | --------- | -------- | ---------------------------- |
| `name`    | string    | `true`   | Name of the customer         |
| `taxCode` | int       | `true`   | Tax code of the customer     |
| `address` | string    | `false`  | Address of the customer      |
| `phone`   | string    | `false`  | Phone number of the customer |

#### Response

Return HTTP response code 200 and the customer when the customer is successfully updated.
Return HTTP response code 403 and the error code in the body if the updating process failed.

#### Errors

> Error response body

```json
{
    "error": "errorCode"
}
```

| Error           | Description                                      |
| --------------- | ------------------------------------------------ |
| `ID_NOTFOUND`   | The customer with the provided ID does not exist |
| `NAME_REQUIRED` | The name field has been missing                  |
| `TAXC_REQUIRED` | The taxCode field has been missing               |
| `TAXC_INVALID`  | The taxCode value is invalid                     |

### Delete a customer

> Sample request

```shell
curl -X DELETE
     -H "Authorization: Bearer access_token"
     http://api.pentamic.com/api/customers/102568
```

#### Request

`DELETE http://api.pentamic.com/api/customers/{id}`

#### URL Parameters

| Field | Data type | Required | Description                     |
| ----- | --------- | -------- | ------------------------------- |
| `id`  | int       | `true`   | ID of the customer to be update |

#### Response

Return HTTP response code 200 when the customer is successfully deleted.
Return HTTP response code 403 and the error code in the body if the deleting process failed.

#### Errors

> Error response body

```json
{
    "error": "errorCode"
}
```

| Error         | Description                                      |
| ------------- | ------------------------------------------------ |
| `ID_NOTFOUND` | The customer with the provided ID does not exist |

### Get a customer's invoices

> Sample request

```shell
curl -X GET
     -H "Authorization: Bearer access_token"
     http://api.pentamic.com/api/customers/102568/invoices
```

#### Request

`GET http://api.pentamic.com/api/customers/{id}/invoices`

#### Response

Return HTTP response code 200 and the customer invoices if request successful.
Return HTTP response code 403 and the error code in the body if the request error.

#### Errors

> Error response body

```json
{
    "error": "errorCode"
}
```

| Error         | Description                                      |
| ------------- | ------------------------------------------------ |
| `ID_NOTFOUND` | The customer with the provided ID does not exist |
