# Error Handling in Express (Simple Version)

## The Big Idea

Things go wrong in every app: the database is down, a user visits a page that doesn't exist, your code has a bug. **Error handling** means having a plan for those moments so your app doesn't crash and users get a clear message.

In Express, you do this with a special function called an **error-handling middleware**.

---

## 1. The Error Handler

A normal middleware function takes 3 things: `req`, `res`, `next`.

An error handler takes **4**. The extra one, `err`, goes first:

```js
app.use((err, req, res, next) => {
  console.error(err.message);               // log the problem for yourself
  res.status(500).send("Internal Server Error"); // tell the user something went wrong
});
```

**How does Express know it's an error handler?** By the 4 parameters. That's the only signal.

**Where does it go?** At the **very end**, after all your routes.

---

## 2. Async Errors (depends on your Express version)

"Async" code is anything using `await`, like a database call.

### Express 4: you must catch errors yourself

Express 4 does **not** catch errors from async routes. If you don't handle them, your app may crash or show a warning.

The fix: use `try/catch` and pass the error to `next(err)`:

```js
app.get("/user", async (req, res, next) => {
  try {
    const user = await getUserFromDatabase();
    res.send(user);
  } catch (err) {
    next(err); // hands the error to your error handler
  }
});
```

Tired of writing `try/catch` everywhere? Make a helper once:

```js
function asyncHandler(fn) {
  return function (req, res, next) {
    Promise.resolve(fn(req, res, next)).catch(next);
  };
}
```

Then wrap your routes with it:

```js
app.get("/user", asyncHandler(async (req, res) => {
  const user = await getUserFromDatabase();
  res.send(user);
}));
```

### Express 5: it's automatic

Express 5 catches async errors for you and sends them to your error handler. No `try/catch`, no `next(err)`:

```js
app.get("/user", async (req, res) => {
  const user = await getUserFromDatabase();
  res.send(user);
});
```

---

## 3. 404 Errors (Page Not Found)

A 404 isn't a crash. It just means **no route matched** the request. Handle it with a normal middleware:

```js
app.use((req, res, next) => {
  res.status(404).send("Sorry, that route does not exist.");
});
```

**Order matters:** put this **after your routes** but **before your error handler**.

---

## Correct Order in Your File

```js
// 1. Your routes
app.get("/user", ...);

// 2. 404 handler
app.use((req, res, next) => {
  res.status(404).send("Sorry, that route does not exist.");
});

// 3. Error handler (always last)
app.use((err, req, res, next) => {
  console.error(err.message);
  res.status(500).send("Internal Server Error");
});
```

---

## Quick Rules

- Put the error handler **last**.
- Handle 404s **separately**.
- In Express 4, use `next(err)` to pass along async errors.
- In production, **never show stack traces to users**. Log them privately and show a friendly message instead.

## Summary

Error handling is just a safety net: a function at the end of your app that catches problems and responds clearly, so your app never crashes without a backup plan.
