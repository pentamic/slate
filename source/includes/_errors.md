# Errors

Pentamic Accouting APIs use the following standard HTTP response errors: 

Error Code | Error Text | Description
---------- | ---------- | -----------
400 | Bad Request | Your request is invalid. Check the request parameter.
401 | Unauthorized | The client is not authenticated. Check [Authentication section](#authentication)
403 | Forbidden | You are authenticated but not allowed to access the resource.
404 | Not Found | The resource you request cannot be found. Check the url.
405 | Method Not Allowed | The HTTP method (GET,POST,PUT,DELETE) does not allowed for the current resource.
500 | Internal Server Error | We had a problem with our server. Try again later.
503 | Service Unavailable | The services are temporarily offline for maintenance. Please try again later.
