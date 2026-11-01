# Middleware in Express

## What is Middleware?

Middleware is a function that runs **between** the moment a request arrives and the moment your route sends a response.

Think of it as a checkpoint. Every request passes through it before reaching your route.

Each middleware function receives three things:

- `req`: the incoming request
- `res`: the response you'll send back
- `next`: a function that passes control to the next step

Common uses:

- Logging requests
- Parsing incoming data (like JSON)
- Checking if a user is logged in
- Serving static files
- Handling errors

## How Does It Work?

Middleware runs **in the order you add it**.

1. A request is sent to the server.
2. The first middleware processes it.
3. If it calls `next()`, the request moves on to the next middleware or route handler.
4. If it does **not** call `next()` (and doesn't send a response), the request hangs and never finishes.

## Example

```js
const express = require('express')
const app = express()

// Middleware: logs info about every request
app.use((req, res, next) => {
  console.log('Request URL:', req.url)
  console.log('Request Method:', req.method)
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

### What happens when you visit `http://localhost:3000`?

1. The request hits the middleware, which logs the URL and method.
2. The middleware calls `next()`.
3. The `app.get('/')` route runs and sends "Hello World!".

## Key Points

- `app.use()` adds middleware to your **whole app**, so it runs on every request.
- Middleware can **read and modify** `req` and `res` before your routes see them.
- Always call `next()` unless you're sending a response yourself.
- Order matters: middleware placed after a route won't run for that route.
