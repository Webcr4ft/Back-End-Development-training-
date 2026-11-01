# Built-in and Third-Party Middleware in Express

## Two types

- **Built-in middleware**: comes with Express. No install needed.
- **Third-party middleware**: made by the community. Install it with `npm install` first.

## Built-in middleware

| Middleware | What it does |
|---|---|
| `express.json()` | Reads JSON sent by the client and puts it in `req.body` |
| `express.urlencoded()` | Reads HTML form data and puts it in `req.body` |
| `express.static()` | Serves files like images, CSS, and JavaScript |

```js
app.use(express.json())
app.use(express.urlencoded({ extended: true }))
app.use(express.static('public'))
```

**Notes:**

- With `express.static('public')`, a file at `public/logo.png` is available at `/logo.png`.
- `extended: true` lets form data contain nested objects and arrays.

## Third-party middleware

### cors

Allows your server to accept requests from **other websites or domains** (for example, a frontend on port 5173 calling your API on port 3000). Browsers block these requests by default.

```bash
npm install cors
```

```js
const cors = require('cors')
app.use(cors())
```

### morgan

Logs every HTTP request in your terminal (method, URL, status, response time).

```bash
npm install morgan
```

```js
const morgan = require('morgan')
app.use(morgan('tiny'))
```

## Using them together

```js
const express = require('express')
const cors = require('cors')
const morgan = require('morgan')
const app = express()

app.use(express.json()) // Built-in: parse JSON
app.use(cors())         // Third-party: allow cross-origin requests
app.use(morgan('tiny')) // Third-party: log requests

app.get('/', (req, res) => {
  res.send('Hello, World!')
})

app.listen(3000, () => {
  console.log('Server running on http://localhost:3000')
})
```

### What happens on each request?

1. `express.json()` parses the body if it contains JSON.
2. `cors()` adds the headers that allow cross-origin access.
3. `morgan('tiny')` logs the request.
4. The `app.get('/')` route sends "Hello, World!".

## Key Points

- Middleware runs **in the order you add it** with `app.use()`.
- Add `express.json()` **before** any route that reads `req.body`.
- Third-party middleware must be installed with `npm install` before you `require` it.
- Built-in middleware handles common tasks; third-party middleware adds extra features.
