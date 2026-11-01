# The REST Architecture

## What is REST?

**REST** stands for **Representational State Transfer**. It is a set of guidelines that describe how web clients and servers should communicate over the internet.

Clients (browsers, mobile apps, other APIs) talk to a server using standard HTTP methods like `GET`, `POST`, `PUT`, `PATCH`, and `DELETE`.

## Core Concepts

### 1. Statelessness

Each request is handled **independently**. The server does not remember previous requests.

So every request must include **everything the server needs**. For example, if a user is logged in, their authentication token must be sent with **every** request.

### 2. Resources

Everything in REST is a **resource**: a piece of data that can be accessed or modified. Each resource has its own URL.

- `/products` : all products
- `/products/1` : the product with ID 1

### 3. HTTP Methods

Methods define the **action** to perform on a resource.

| Method | Action |
|---|---|
| `GET` | Retrieve a resource |
| `POST` | Create a new resource |
| `PUT` / `PATCH` | Update an existing resource |
| `DELETE` | Remove a resource |

### 4. HTTP Status Codes

After processing a request, the server replies with a status code showing the result.

| Code | Meaning |
|---|---|
| `200` OK | The request was successful |
| `201` Created | A new resource was created |
| `400` Bad Request | The client sent invalid data |
| `404` Not Found | The resource does not exist |
| `500` Internal Server Error | Something went wrong on the server |

## How REST Works: Step by Step

### 1. Client sends a request

- Uses an HTTP method like `GET` or `POST`
- Includes a URL identifying the resource
- May include headers, metadata, and a request body

### 2. Server receives the request

- Validates the request format and authentication (if required)
- Identifies the resource from the URL
- Determines the action from the HTTP method
- Checks permissions and access control

### 3. Server performs the action

- `GET`: retrieve the resource
- `POST`: create a new resource
- `PUT` / `PATCH`: update the resource
- `DELETE`: remove the resource
- Runs any other necessary logic

### 4. Server builds the response

- Picks an appropriate status code (`200`, `201`, `404`, etc.)
- Formats the data, usually as JSON
- Adds headers such as `Content-Type` or `Cache-Control`

### 5. Server sends the response

- Includes a status code, headers, and an optional body
- Stores **no client state** (statelessness)

### 6. Client handles the response

- Checks the status code to see if it succeeded
- Processes any data returned

## Example

**Request:**

```http
GET /products/1
Authorization: Bearer <token>
Accept: application/json
```

**Response:**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "name": "Laptop",
  "price": 999
}
```

Notice the token is sent with the request. That is statelessness at work: the server doesn't remember who you are between requests.

## Key Points

- REST is a set of **guidelines**, not a tool or library.
- Everything is a **resource** with a **URL**.
- **HTTP methods** say what to do; **status codes** say what happened.
- The server is **stateless**, so each request must carry all needed information.
