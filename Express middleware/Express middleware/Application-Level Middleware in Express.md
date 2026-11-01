# Application-Level Middleware in Express

## What is it?

Application-level middleware is middleware **attached to your Express app** (the `app` object you create with `express()`).

It's the most common type of middleware. Use it when you need the same logic to run across **many or all routes**, instead of repeating code in each one.

## How do you add it?

You register it with:

- `app.use()`: runs for every request (or every request matching a path)
- `app.get()`, `app.post()`, etc.: runs only for that specific route and method

## Example

```js
const express = require('express')
const app = express()

// Application-level middleware: logs every incoming request
app.use((req, res, next) => {
  console.log('Request received at:', new Date())
  next() // Pass control to the next step
})

// Route handler
app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(3000, () => {
  console.log('Server running on http://localhost:3000')
})
```

### What happens when someone visits `/`?

1. The request arrives at the server.
2. The `app.use()` middleware logs the current date and time.
3. It calls `next()`, passing control onward.
4. The `app.get('/')` route sends "Hello World!".

The same logging would happen for **any** route (`/about`, `/contact`, etc.), because the middleware isn't tied to a specific path.

## When should you use it?

- **Logging**: record every request
- **Authentication**: check the user is logged in before reaching protected routes
- **Error handling**: catch problems from any route
- **Parsing data**: read JSON or form data on all requests

## Key Points

- `app.use()` without a path runs on **every request**.
- Always call `next()` unless you're sending a response yourself.
- Order matters: middleware must be added **before** the routes you want it to affect.
