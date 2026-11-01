# Router-Level Middleware in Express

## What is it?

Router-level middleware works just like application-level middleware, but it is attached to a **router** (`express.Router()`) instead of the main `app`.

A router is a mini-app for a group of related routes. Middleware attached to it only runs for **that group**, not your whole app.

## Why use it?

- Split a big app into smaller, organized files (menu routes, user routes, admin routes)
- Apply middleware to **only some routes**
- Keep code cleaner and easier to maintain

## Example

```js
const express = require('express')
const app = express()
const router = express.Router()

// Router-level middleware: runs only for routes in this router
router.use((req, res, next) => {
  console.log('Request made to /menu route')
  next() // Pass control to the next step
})

// Route inside the router
router.get('/drinks', (req, res) => {
  res.send('Welcome to the drinks menu!')
})

// Mount the router at /menu
app.use('/menu', router)

app.listen(3000, () => {
  console.log('Server running on http://localhost:3000')
})
```

### What happens when someone visits `/menu/drinks`?

1. `app.use('/menu', router)` sends the request into the router.
2. The router's middleware logs "Request made to /menu route".
3. It calls `next()`.
4. The `/drinks` route sends "Welcome to the drinks menu!".

### What about `/about` or `/`?

The router's middleware does **not** run, because those paths don't start with `/menu`.

## Application-level vs Router-level

| | Application-level | Router-level |
|---|---|---|
| Attached to | `app` | `router` |
| Runs for | All routes (by default) | Only routes in that router |
| Best for | Logging, parsing, global auth | Grouping related routes |

## Key Points

- `router.use()` adds middleware to **one router only**.
- `app.use('/menu', router)` sets the URL prefix, so `/drinks` becomes `/menu/drinks`.
- Always call `next()` unless you're sending a response.
