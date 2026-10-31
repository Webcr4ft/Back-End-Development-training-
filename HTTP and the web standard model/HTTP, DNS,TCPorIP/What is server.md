# What Is a Server and How Does It Work? (A High-Level Overview)

## What Is a Server?

Servers are essential for the modern web. They power the online experiences that we rely on every day as users, and they will power most of the experiences that you will create as a developer.

Let's learn more about them.

As you may know, the internet is a global system of interconnected computer networks. Servers are the central components that enable this communication by handling the process of exchanging data.

> **In simple terms:** A server is a computer or computer program that receives requests from other computers and sends data or services to them over the network as a response.

### Two Meanings of "Server"

The word **server** is a dual concept because it can refer to:

1. **Hardware:** The actual physical, powerful computer hardware that is designed to run efficiently and continuously to provide these services. These machines are built and designed for reliability.
2. **Software:** The actual computer software that is running on that physical hardware to provide the services.

The physical computers that we refer to as "servers" are usually stored at **data centers**, which are large and secure facilities with controlled environments.

---

## The Client-Server Model

Servers are an essential part of **The Client-Server Model**.

The Client-Server Model is a **distributed system architecture** where components are either clients or servers.

| Role       | What it is                                                                                         | Example           |
| ---------- | -------------------------------------------------------------------------------------------------- | ----------------- |
| **Client** | The process or application that sends requests to servers for data or services.                    | A web browser     |
| **Server** | The physical device or computer program that handles those requests and returns a response.        | A web server      |

### The Request-Response Cycle

Essentially, the client and the server are part of a **request-response cycle**, where the client sends a request to the server, and the server returns a response to the client.

```
 ┌──────────┐    1. Request     ┌──────────┐
 │  Client  │ ────────────────▶ │  Server  │
 │ (browser)│                   │          │
 │          │ ◀──────────────── │          │
 └──────────┘    2. Response    └──────────┘
```

### Example: Logging In

For example, when you use your browser (the client) to authenticate on an application with your username and password, your information is securely sent to a server. The server then checks if the username and password that you entered match the information that the platform currently has in its database.

- **If there is a match:** the server returns a successful response to the client (your browser), and you are successfully authenticated on the site.
- **If no match is found:** the server returns a failure response to the client, and you'll typically see an error or some sort of feedback explaining why your login attempt was unsuccessful.

All of this authentication logic runs on the server. The server is responsible for:

- Validating credentials
- Interacting with the database
- Deciding how to respond to each request

---

## The HTTP Status Code in a Server Response

Each server response includes an **HTTP status code**, which tells the client what happened. These status codes let the client know whether a request succeeded or failed and why.

For example:

| Code    | Meaning                                       |
| ------- | --------------------------------------------- |
| **200** | Everything was OK.                            |
| **404** | The resource was not found on the server.     |
| **500** | There was an internal server error.           |
| **503** | The server is temporarily unavailable.        |

And so on…

Each status code has its own unique meaning.

---

## Examples of Applications Using Servers

Examples of real-world applications that use servers include:

- E-commerce
- Search engines
- Gaming
- Video streaming
- Cloud storage and collaboration platforms
- Social media platforms
- Financial applications
- And more

If the data is updated dynamically or the application needs some sort of communication with a database, servers are very likely key components of the communication process.

---

## Main Types of Servers

These are some of the main types of servers:

| Type                   | What it does                                                                                                    |
| ---------------------- | --------------------------------------------------------------------------------------------------------------- |
| **Web servers**        | Deliver web content, such as HTML pages, images, and CSS files, to browsers.                                    |
| **Application servers**| Handle business logic, process user input, and coordinate responses.                                           |
| **Database servers**   | Run database management systems and store, retrieve, and manage data.                                           |
| **Mail servers**       | Send, receive, and store email messages.                                                                        |
| **File servers**       | Manage access to files and allow them to be stored and shared across a network.                                 |
| **Proxy servers**      | Act as intermediaries between clients and other servers, often used for caching, security, or traffic control.  |

---

## Why Servers Matter

Servers are the backbone of the powerful online platforms we use every day. They make it possible to:

- Run complex logic
- Store and process large amounts of data
- Support millions of users at the same time

Without servers, the modern digital world we rely on would not exist.
