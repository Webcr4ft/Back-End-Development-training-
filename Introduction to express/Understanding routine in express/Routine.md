# What Is Routing and How Do Route Methods Work in Express?

## What Is Routing?

In Express, **routing** is how you define the **endpoints** of your web application.

> **Think of it this way:** Routes are rules that tell your app how to respond when a user visits a specific URL.

---

## Recap: Our Basic App

```js
const express = require("express");
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`);
});
```

This app defines one route for the root URL (`/`). When a client sends a **GET** request to that path, the server responds with `Hello World!`. The app then listens for requests on port `3000`.

---

## Route Methods

Express lets you handle different types of HTTP requests using different **route methods**. The most common ones are:

| Method | Purpose | Example |
|--------|---------|---------|
| `app.get()` | Retrieve data | Load a list of users |
| `app.post()` | Create new data | Submit a sign-up form |
| `app.put()` | Update existing data | Edit a user's profile |
| `app.delete()` | Delete data | Remove a user |

Each method defines how your app should respond to a specific **HTTP method** at a specific **URL path**.

---

## Examples

```js
app.post("/submit", (req, res) => {
  res.send("Form submitted!");
});

app.put("/update", (req, res) => {
  res.send("Item updated!");
});

app.delete("/delete", (req, res) => {
  res.send("Item deleted!");
});
```

### How Each Route Is Built

Every route follows the same pattern:

```js
app.METHOD(PATH, HANDLER);
```

| Part | Meaning |
|------|---------|
| `METHOD` | The HTTP method to listen for (`get`, `post`, `put`, `delete`) |
| `PATH` | The URL path, such as `/submit` |
| `HANDLER` | The function `(req, res) => { ... }` that runs when a request matches |

When a request arrives, Express checks its **method** and **path**. If both match a route, it runs that route's handler and sends back a response.

```
Request: POST /submit
        ↓
Express finds app.post("/submit")
        ↓
Handler runs: res.send("Form submitted!")
        ↓
Client receives: "Form submitted!"
```

---

## How to Test Your Routes

Browsers can only send **GET** requests when you type a URL, so you'll need a tool to test POST, PUT, and DELETE routes. Two popular options are:

- **Postman**: a visual app for sending HTTP requests
- **curl**: a command-line tool

Example with `curl`:

```bash
curl -X POST http://localhost:3000/submit
curl -X PUT http://localhost:3000/update
curl -X DELETE http://localhost:3000/delete
```

Expected responses:

```
Form submitted!
Item updated!
Item deleted!
```

---

## Summary

- **Routing** is defining how your app responds to different requests.
- A route is made of an **HTTP method**, a **path**, and a **handler function**.
- The most common methods are `get`, `post`, `put`, and `delete`.
- Use **Postman** or **curl** to test routes that a browser can't send.
