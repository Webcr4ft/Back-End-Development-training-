# What Are Route Parameters?

## What Is a Route Parameter?

A **route parameter** is a dynamic value inside the URL path. It lets your app capture the part of a URL that changes with each request.

This is useful for building dynamic pages, like showing a specific user, blog post, or product based on the URL.

> **Think of it this way:** A route parameter is a blank to be filled in. The route says `/post/___`, and each request fills in a different value.

---

## Example 1: A Route with a Parameter

```js
// Route with a parameter in the path
app.get("/post/:postId", (req, res) => {
  const postId = req.params.postId;
  res.send(`Viewing post with ID: ${postId}`);
});
```

### Breaking It Down

| Part | Meaning |
|------|---------|
| `/post/:postId` | The route path. It listens for GET requests to URLs like `/post/42` |
| `:postId` | The **route parameter**, a placeholder that gets replaced by a real value. The colon `:` marks it as a parameter |
| `req.params` | An object that holds **all** route parameters |
| `req.params.postId` | The value captured from the URL (for example, `42`) |
| `res.send()` | Sends a response back to the client |

### How It Works

```
Browser visits http://localhost:3000/post/42
        ↓
Express matches the route /post/:postId
        ↓
postId is set to "42"
        ↓
res.send("Viewing post with ID: 42")
        ↓
Browser displays "Viewing post with ID: 42"
```

Route parameters make your routes flexible. You don't need a separate route for every possible value.

---

## Example 2: Dynamic Menu Routes

In the last lesson, we made a separate static route for each menu:

```js
app.get("/menu/food", ...);
app.get("/menu/drinks", ...);
app.get("/menu/desserts", ...);
```

With route parameters, **one route** can handle them all:

```js
app.get("/menu/:category", (req, res) => {
  const category = req.params.category;
  res.send(`You are viewing the ${category} menu!`);
});
```

### Step-by-Step

1. A user visits `http://localhost:3000/menu/drinks`.
2. The server matches the route `/menu/:category` and captures `category` as `drinks`.
3. The server responds with:

```
You are viewing the drinks menu!
```

### Same Route, Different URLs

| URL | `category` Value | Response |
|-----|------------------|----------|
| `/menu/drinks` | `drinks` | You are viewing the drinks menu! |
| `/menu/food` | `food` | You are viewing the food menu! |
| `/menu/desserts` | `desserts` | You are viewing the desserts menu! |

---

## Static vs. Dynamic Routes

| | Static Route | Dynamic Route |
|---|---|---|
| **Path** | `/menu/drinks` | `/menu/:category` |
| **Matches** | Only `/menu/drinks` | Any value after `/menu/` |
| **Routes needed** | One per page | One for all pages |

---

## Summary

- A **route parameter** is a dynamic placeholder in a URL path, written with a colon (like `:postId`).
- Use **`req.params`** to access the captured values.
- Each parameter is available as **`req.params.parameterName`**.
- One dynamic route can replace many static routes, which keeps your code shorter and more flexible.
