# Passport.js (Simple Version)

## The Big Idea

Building authentication yourself means writing a lot of manual logic: reading headers, extracting cookies, verifying signatures, handling errors. It's great for learning, but time-consuming and easy to get wrong in production.

**Passport.js** is authentication middleware for Node.js. It handles the low-level details so you can focus on your app's logic.

The core idea: every app logs users in differently, but the **authentication flow stays the same**. Passport makes that possible with plugins called **Strategies**.

---

## 1. Strategies

Instead of writing custom code for each login method, you install the **strategy** you need. There are 500+ available.

| Strategy | What it does |
|----------|--------------|
| `passport-local` | Username and password login against your own database |
| `passport-jwt` | Protects API endpoints by validating JSON Web Tokens |
| `passport-google-oauth20` | "Log in with Google" |
| `passport-facebook` | "Log in with Facebook" (OAuth 2.0) |
| `passport-github2` | "Log in with GitHub" |

**Why this is useful:** Start with username/password today, then add "Log in with Google" next month. You don't rewrite your auth code. You just install the Google strategy and plug it in.

---

## 2. Setting Up Passport

Install the core package plus the strategy you want:

```bash
npm install passport passport-local
```

Then wire it into your Express app. This must happen **before you define your routes**:

```js
const express = require('express');
const passport = require('passport');
const LocalStrategy = require('passport-local').Strategy;

const app = express();

// initialize Passport middleware
app.use(passport.initialize());

// configure Passport to use the Local Strategy
passport.use(new LocalStrategy((username, password, done) => {
    // your database look-up and password verification logic goes here
}));
```

---

## 3. Authenticating Requests

Passport works as normal Express middleware. Add it to your login route:

```js
app.post('/login', passport.authenticate('local'), (req, res) => {
  // if this function runs, then authentication was successful
  res.send(`Welcome back, ${req.user.username}!`);
});
```

**What happens:**

1. The user submits their credentials to `/login`.
2. Passport intercepts the request.
3. It passes the data to your configured strategy.
4. It evaluates the result.

---

## 4. What Passport Does Automatically

When the strategy successfully verifies the user, Passport handles two things for you:

1. **Session management:** It stores a small piece of user data in the session cookie.
2. **Request decoration:** It attaches the authenticated user to the request as `req.user`.

Once `req.user` is set, any later middleware or route can see who is logged in and make **authorization** decisions.

```
Login request → Passport → Strategy verifies → req.user set → Your route runs
```

---

## Easy Way to Remember

- **Passport = a security desk** that standardizes how people get checked in.
- **Strategies = the different ID types** it accepts (password, Google, GitHub, JWT).

---

## Summary

- Passport.js is authentication middleware that saves you from writing low-level auth code.
- **Strategies** are plugins for each login method.
- Install `passport` plus a strategy, call `passport.initialize()`, and configure it with `passport.use()`.
- Use `passport.authenticate('local')` on routes to protect them.
- On success, Passport manages the session and sets `req.user`.
