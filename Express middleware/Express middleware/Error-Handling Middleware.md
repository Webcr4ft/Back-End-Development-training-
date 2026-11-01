# Error-Handling Middleware in Express

## What is it?

Error-handling middleware is a special middleware that **catches errors** in your app. Instead of crashing or leaving the user with a broken page, it logs the problem and sends a clean response.

It is different from normal middleware in one way: it takes **four parameters** instead of three.

```js
app.use((err, req, res, next) => {
  console.error(err.message)
  res.status(500).send('Internal Server Error')
})
```

| Parameter | Meaning |
|---|---|
| `err` | The error that happened |
| `req` | The incoming request |
| `res` | The response you send back |
| `next` | Passes control onward |

> Express recognizes it as an error handler **because of the four parameters**. Even if you don't use `next`, you must still list it.

## When does it run?

It runs when:

- A route or middleware **throws an error**, or
- You pass an error to `next()`, like `next(new Error('Oops'))`

## Example

```js
const express = require('express')
const app = express()

// Route that throws an error on purpose
app.get('/', (req, res) => {
  throw new Error('Something went wrong!')
})

// Error-handling middleware (placed AFTER all routes)
app.use((err, req, res, next) => {
  console.error(err.stack) // Log the full error details
  res.status(500).send('Something went wrong!')
})

app.listen(3000, () => {
  console.log('Server running on http://localhost:3000')
})
```

### What happens when someone visits `/`?

1. The route throws an error.
2. Express skips all normal middleware and routes.
3. It jumps straight to the error-handling middleware.
4. The error is logged on the server.
5. The user receives a `500` response with a generic message.

## Why use it?

- Users get a **proper response** instead of a crash or hanging request
- You can **log errors** for debugging
- You can **hide technical details** from users (they see a simple message, you see the full stack)

## Key Points

- It must have **four parameters**: `(err, req, res, next)`.
- Place it **at the end**, after all routes and other middleware.
- `res.status(500)` means "server error".
- Use `next(err)` to send errors to it from async code, since thrown errors inside async functions are not always caught automatically in older Express versions.
