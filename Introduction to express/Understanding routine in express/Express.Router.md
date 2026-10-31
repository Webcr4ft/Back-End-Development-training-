# How Does `express.Router` Work?

## What Is `express.Router()`?

`express.Router()` helps you organize your routes into **smaller, modular pieces**. This becomes very useful as your application grows.

Instead of defining every route in one large file, you can split them into separate files using **routers**. This keeps your code easier to read, maintain, and scale.

A **router** works like a **mini Express application**. It can handle its own routes and middleware, but it is not a full Express app. Once you define routes on a router, you **mount** it in your main app using `app.use()`.

> **Think of it this way:** A router is like a department in a company. The main app is the front desk that receives every request and sends it to the right department.

---

## Benefits of Using Routers

| Benefit | What It Means |
|---------|---------------|
| **Separation of concerns** | Routes live in separate files, which improves organization and readability |
| **Code reusability** | Routers can be reused in different parts of an app, or even across projects |
| **Cleaner main file** | Your main `app.js` or `server.js` stays focused on configuration and setup |

---

## Example: Routing Requests for `/users`

This example uses two files.

### File 1: `app.js` (the main app)

```js
const express = require("express");
const app = express();
const port = 3000;

// Importing the user routes
const userRoutes = require("./userRoutes");

// Using the userRoutes router for /users path
app.use("/users", userRoutes);

app.listen(port, () => {
  console.log(`Server running at http://localhost:${port}`);
});
```

### File 2: `userRoutes.js` (the router)

```js
const express = require("express");
const router = express.Router();

// GET request for /users
router.get("/", (req, res) => {
  res.send("List of users");
});

// POST request for /users
router.post("/", (req, res) => {
  res.send("Creating a new user");
});

// GET request for /users/:id
router.get("/:id", (req, res) => {
  const userId = req.params.id;
  res.send(`User details for user with id: ${userId}`);
});

module.exports = router;
```

---

## How the Example Works

### In `app.js`

1. `express` is imported and an app instance is created and stored in `app`.
2. The router is imported from `userRoutes.js` with `require("./userRoutes")`.
3. `app.use("/users", userRoutes)` **mounts** the router. This tells Express: *"If a request path starts with `/users`, pass it to the `userRoutes` router."*

### In `userRoutes.js`

1. A new router is created with `express.Router()`.
2. Routes are defined with `router.get()` and `router.post()`.
3. The router is exported with `module.exports = router` so `app.js` can use it.

---

## Paths Are Relative to the Mount Point

Because the router is mounted at `/users`, the paths inside it are **relative** to `/users`:

| Route in `userRoutes.js` | Full URL | Response |
|--------------------------|----------|----------|
| `router.get("/")` | `GET /users` | List of users |
| `router.post("/")` | `POST /users` | Creating a new user |
| `router.get("/:id")` | `GET /users/:id` | User details for the given ID |

```
Request: GET /users/42
        ↓
app.use("/users", userRoutes)   ← path starts with /users, so pass to the router
        ↓
router.get("/:id")              ← remaining path is "/42", so id = "42"
        ↓
res.send("User details for user with id: 42")
```

---

## Organizing Larger Applications

Using `express.Router()` keeps your main file clean and focused on configuration. All user-related routes are grouped together in `userRoutes.js`.

As your app grows, you can add more routers for other sections, such as `/products`, `/orders`, or `/auth`:

```
my-app/
├── app.js
├── userRoutes.js
├── productRoutes.js
├── orderRoutes.js
└── authRoutes.js
```

```js
app.use("/users", userRoutes);
app.use("/products", productRoutes);
app.use("/orders", orderRoutes);
app.use("/auth", authRoutes);
```

Each section stays organized in its own file, which makes the application easier to maintain and scale.

---

## Summary

- `express.Router()` creates a **modular, mini app** for grouping related routes.
- Define routes on the router with `router.get()`, `router.post()`, and so on.
- Export the router with `module.exports = router`.
- **Mount** it in the main app with `app.use("/path", router)`.
- Router paths are **relative** to the mount path.
- Routers keep your code **organized, reusable, and easy to scale**.
