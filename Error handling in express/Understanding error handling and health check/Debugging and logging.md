# Debugging and Logging in Express (Simple Version)

## The Big Idea

Sometimes your Express app breaks and you have no idea why. **Debugging** and **logging** let you see what's happening behind the scenes so you can find problems faster.

- **Debugging** = a detailed view of how Express works internally (routes, middleware). Mostly for development.
- **Logging** = a record of what requests your app receives. Useful in development and production.

---

## 1. Debugging with `debug`

Express already includes a debugging tool called `debug`. **No install needed.**

To turn it on, set the `DEBUG` environment variable when you start your app:

```bash
DEBUG=express:* node index.js
```

The `express:*` part means "show me all Express debug messages." You'll see output like:

```
express:router:route dispatching GET /
express:router:layer processing GET /
```

This lets you trace how a request moves through your routes and middleware.

### Want less noise?

Narrow it down to just one area, like the router:

```bash
DEBUG=express:router node index.js
```

### Windows users

The syntax is different depending on your terminal.

**PowerShell:**

```powershell
$env:DEBUG = "express:*"; node index.js
```

**CMD:**

```cmd
set DEBUG=express:* && node index.js
```

Same idea, just a different way of setting the environment variable.

---

## 2. Logging Requests with `morgan`

`morgan` is a popular middleware that logs every incoming request.

**Step 1: Install it**

```bash
npm install morgan
```

**Step 2: Add it to your app**

```js
const express = require('express');
const morgan = require('morgan');
const app = express();

app.use(morgan('dev'));
```

Now every request shows up in your terminal with:

- The HTTP method (GET, POST, etc.)
- The URL
- The status code
- The response time

---

## Why Both Matter

| Tool | What it shows you | Best for |
|------|-------------------|----------|
| **debug** | How Express handles requests internally | Understanding the flow while developing |
| **morgan (logging)** | A record of requests coming in | Tracking bugs, traffic, and issues early |

Debugging keeps you informed without cluttering your production logs, and logging gives you a history of what happened.

## Summary

Use `DEBUG=express:*` to see what Express is doing internally, and use `morgan` to log every request. Together, they make problems much easier to spot and fix.
