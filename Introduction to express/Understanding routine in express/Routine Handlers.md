# What Are Route Handlers?

## What Is a Route Handler?

A **route handler** is a function that defines what happens when a client sends a request to a specific route. You may also hear it called a **route callback function** or a **controller function**.

A route handler:

1. Receives the incoming request
2. Performs any needed logic (like querying a database or running calculations)
3. Sends a response back to the client

> **Think of it this way:** If a route is the address, the handler is the person at that address who reads your request and replies.

---

## Example

You've actually been using route handlers all along:

```js
app.get("/menu", (req, res) => {
  res.send("Welcome to the menu!");
});
```

### Breaking It Down

| Part | Meaning |
|------|---------|
| `app.get()` | A route method that listens for **GET** requests |
| `"/menu"` | The route path being listened for |
| `(req, res) => { ... }` | The **route handler**. It runs whenever a GET request is sent to `/menu` |
| `req` | The **request** object, with information about the incoming request |
| `res` | The **response** object, used to send a reply to the client |
| `res.send()` | Sends a plain text response to the client |

### What's Inside `req`?

The `req` object can contain things like:

- Route parameters
- Query strings
- Headers
- Body data

### How It Works

```
User visits /menu (or sends a GET request to it)
        ↓
Express matches app.get("/menu")
        ↓
The route handler runs
        ↓
res.send("Welcome to the menu!")
        ↓
Client receives "Welcome to the menu!"
```

---

## Why Route Handlers Matter

Route handlers are the **core of an Express application**. They define how each route of your app responds to requests.

You can add logic inside them, such as:

- Processing form data
- Interacting with databases
- Performing validation

---

## Summary

- A **route handler** is the function that runs when a request matches a route.
- It receives two objects: **`req`** (the request) and **`res`** (the response).
- It processes the request, then sends a response with methods like `res.send()`.
- Route handlers are also called **callback functions** or **controller functions**.

---

## Questions

1. What is a route handler, and what does it do?
2. What are two other names for a route handler?
3. In `app.get("/menu", (req, res) => { ... })`, which part is the route handler?
4. What is the difference between `req` and `res`?
5. What would a client see if they sent a GET request to `/menu` in the example above?
6. Name two things you might do inside a route handler besides sending a response.

### Answers

1. A route handler is a function that runs when a client sends a request to a specific route. It processes the request and sends back a response.
2. Route callback functions and controller functions.
3. `(req, res) => { res.send("Welcome to the menu!"); }`
4. `req` holds information about the incoming request. `res` is used to send a response back to the client.
5. The text `Welcome to the menu!`
6. For example: process form data, query a database, or validate input.
