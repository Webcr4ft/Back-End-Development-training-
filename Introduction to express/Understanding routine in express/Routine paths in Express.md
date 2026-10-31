# What Are Route Paths in Express?

## What Is a Route Path?

A **route path** is the URL pattern that tells Express how to respond to an incoming request.

When a user requests a URL, Express matches it to a route path and runs the corresponding **handler** function.

Route paths are defined inside route methods like `app.get()` and `app.post()`. There are two types:

| Type | Description | Example |
|------|-------------|---------|
| **Static** | A fixed path that never changes | `/home` |
| **Dynamic** | A path with parameters that capture values from the URL | `/user/:id` |

> In this lesson, we focus on **static routes**. Dynamic routes are covered in the next lesson.

---

## Example 1: A Simple Static Route

```js
// Static route
app.get("/home", (req, res) => {
  res.send("Welcome to the homepage!");
});
```

The server listens for **GET** requests to `/home` and responds with a simple message.

### Breaking It Down

`app.get()` takes two arguments:

| Argument | What It Does |
|----------|--------------|
| `"/home"` | The **static route path** (URL) the server listens for |
| `(req, res) => { ... }` | A **callback function** that runs when a GET request is made to that path |

Inside the callback, `res.send()` sends a response back to the client. Here, it sends the text `Welcome to the homepage!`, which shows up in the browser.

```
Browser visits http://localhost:3000/home
        ↓
Express matches app.get("/home")
        ↓
res.send("Welcome to the homepage!")
        ↓
Browser displays "Welcome to the homepage!"
```

---

## Example 2: A Nested Static Route

```js
// Static route
app.get("/menu/drinks", (req, res) => {
  res.send("Welcome to the drinks menu!");
});
```

Here, the server listens for GET requests to `/menu/drinks` and sends back a message when that URL is requested.

Paths can have multiple parts separated by `/`. This is useful for grouping related pages under a common path.

---

## Organizing Routes with Common Paths

A restaurant website could group its menu pages like this:

```
/menu/food
/menu/drinks
/menu/desserts
```

And the matching routes:

```js
app.get("/menu/food", (req, res) => {
  res.send("Welcome to the food menu!");
});

app.get("/menu/drinks", (req, res) => {
  res.send("Welcome to the drinks menu!");
});

app.get("/menu/desserts", (req, res) => {
  res.send("Welcome to the desserts menu!");
});
```

### Why This Is Helpful

- URLs stay **clear and meaningful**
- Routes are **easier to organize** as your app grows
- Your app is **easier to maintain**

---

## Summary

- A **route path** is the URL pattern Express matches against incoming requests.
- **Static routes** use fixed paths like `/home` or `/menu/drinks`.
- `app.get()` takes a **path** and a **callback function**.
- Grouping related pages under a common path keeps your app organized.
- **Next lesson:** dynamic route paths with parameters, like `/user/:id`.
