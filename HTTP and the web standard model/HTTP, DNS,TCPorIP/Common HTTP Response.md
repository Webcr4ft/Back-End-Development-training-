# What Are Some Common HTTP Response Codes?

Let's learn about common HTTP response codes.

**HTTP response codes** are three-digit numerical codes that web servers use to communicate with clients to let them know what happened with their requests.

They provide information about whether the request was handled successfully or if there was an error while handling the request.

We'll cover some of the most common ones in this lecture.

## Quick Overview

| Range | Category | Meaning |
| ----- | -------- | ------- |
| `2xx` | Success | The request was handled successfully |
| `3xx` | Redirection | The resource moved, or the client must take extra steps |
| `4xx` | Client errors | The client seems to have made an error |
| `5xx` | Server errors | The server had a problem processing the request |

---

## Success Codes

Let's start with success codes. These codes start with the number **2**.

### `200 OK`

The code **200 OK** is the most common HTTP response code. It means that the request was successful and the server returned the information requested by the client.

### `201 Created`

The code **201 Created** is returned by the server when the client requests creating a resource and the process is completed successfully. For example, if a new user account is created successfully, the server returns this response code to the client.

### `204 No Content`

The code **204 No Content** is returned when the request has been handled successfully but the server has no content to return. This can be used for processes that delete or update a resource in a database but have no data to return.

---

## Redirection Codes

Now let's talk about redirection codes.

These codes are returned by the server when the resource requested by the client has been moved to a different location or when the client needs to take additional steps to complete the request.

These codes start with the number **3**.

### `301 Moved Permanently`

The code **301 Moved Permanently** is returned when the resource requested by the client has been moved permanently to another location. In this case, the server should include a URL to the new location in the response and once the client receives the response, the user should be redirected to this URL.

### `302 Found`

The code **302 Found** indicates that the resource requested by the client has been temporarily moved to another location. The server should provide the new URL in the response and the client should redirect the user to this URL. However, the original URL might be available in the future since the change is temporary. That is the main difference between the response codes 301 and 302.

| Code | Move type | Original URL in the future? |
| ---- | --------- | --------------------------- |
| `301` | Permanent | No, the resource has moved for good |
| `302` | Temporary | Possibly, since the change is temporary |

### `304 Not Modified`

The code **304 Not Modified** is returned by the server to tell the client that the resource requested has not been modified since the last time it was requested. The server sends this code to avoid sending data that has already been sent if the content has not changed. It's a **performance optimization technique**.

---

## Client Error Codes

Now we'll start diving into error codes.

Errors can be caused by the client and by the server. We'll talk about client error codes first.

A **4xx** response indicates that the client seems to have made an error.

These error codes start with the number **4**.

### `400 Bad Request`

The **400 Bad Request** code is returned when the server could not understand the request sent by the client. This can occur when the client sends a request with incorrect syntax, with invalid parameters, or invalid data.

### `401 Unauthorized`

The **401 Unauthorized** code is related to **authentication**. It indicates that the client has to provide certain authentication credentials to access the resource that is being requested. These credentials may include a username and a password.

### `403 Forbidden`

The **403 Forbidden** code is returned when the client is not authorized to access the requested resource. The difference between 401 and 403 is that in 403, the client doesn't have the necessary permissions for the particular resource it's requesting, even if it has valid authentication credentials.

| Code | Problem |
| ---- | ------- |
| `401` | The client needs to provide authentication credentials |
| `403` | The client lacks permission for this resource, even with valid credentials |

### `404 Not Found`

The **404 Not Found** code is returned when the resource could not be found on the server. Maybe it was deleted or there is a typo in the URL that prevents the server from finding the resource. A 404 response does not indicate whether the condition is temporary or permanent.

---

## Server Error Codes

Next, we have server error codes. These codes are returned by the server when the request could not be processed because of an issue on the server's end.

### `500 Internal Server Error`

The **500 Internal Server Error** code indicates that there was an unexpected error on the server. This error could be caused by a wide range of issues, ranging from configuration issues to temporary issues.

### `502 Bad Gateway`

The **502 Bad Gateway** error code is returned when the server was trying to communicate with another server but received an invalid response from that server. There is a wide range of causes for this type of error.

### `503 Service Unavailable`

The **503 Service Unavailable** error code indicates that the server will not be able to handle the request temporarily, so the client should try again later. Common causes for this error include maintenance tasks and a high volume of requests that the server is currently unable to handle.

---

## Summary Table of All Codes Covered

| Code | Name | Category | Short description |
| ---- | ---- | -------- | ----------------- |
| `200` | OK | Success | Request succeeded and the requested info was returned |
| `201` | Created | Success | A resource was created successfully |
| `204` | No Content | Success | Request succeeded, but there is no content to return |
| `301` | Moved Permanently | Redirection | Resource moved permanently to a new URL |
| `302` | Found | Redirection | Resource moved temporarily to a new URL |
| `304` | Not Modified | Redirection | Resource unchanged since last requested |
| `400` | Bad Request | Client error | Server could not understand the request |
| `401` | Unauthorized | Client error | Authentication credentials are required |
| `403` | Forbidden | Client error | Client lacks permission for the resource |
| `404` | Not Found | Client error | Resource could not be found |
| `500` | Internal Server Error | Server error | Unexpected error on the server |
| `502` | Bad Gateway | Server error | Invalid response from another server |
| `503` | Service Unavailable | Server error | Server temporarily unable to handle the request |

---

## Wrapping Up

HTTP response codes are essential for understanding the communication between clients and web servers. By understanding these codes, you can troubleshoot and debug your web applications.
