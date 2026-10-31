# What Are the Different Response Methods in Express?

## What Are Response Methods?

In Express, the **`res` (response) object** is used to send a reply back to the client after a request has been processed.

Express provides several built-in **response methods** for different kinds of replies. You can:

- Send plain text
- Send JSON data
- Set a status code
- Redirect to another URL
- Render a template

---

## 1. `res.send()`

One of the most commonly used response methods. It can send **plain text, HTML, JSON, or even binary data**.

```js
app.get("/text", (req, res) => {
  res.send("Hello, World!");
});
```

When a client visits `/text`, the server responds with:

```
Hello, World!
```

---

## 2. `res.json()`

Sends a **JSON response** to the client. It's especially useful when building **APIs**, where you often return structured data like objects or arrays.

Express automatically converts a JavaScript object into a JSON-formatted string.

```js
app.get("/user", (req, res) => {
  res.json({ name: "John Doe", age: 30 });
});
```

When a client requests `/user`, the server responds with:

```json
{
  "name": "John Doe",
  "age": 30
}
```

---

## 3. `res.status()`

Sets the **HTTP status code** of the response. It's usually **chained** with another response method like `res.send()` or `res.json()`.

```js
app.get("/notfound", (req, res) => {
  res.status(404).send("Not Found");
});
```

Here, the server sets the status code to `404` and sends back the message `Not Found`.

---

## 4. `res.redirect()`

Sends the user to a **different URL**.

```js
app.get("/oldpage", (req, res) => {
  res.redirect("/newpage");
});
```

When a client visits `/oldpage`, they are automatically redirected to `/newpage`.

---

## 5. `res.render()`

Used with **template engines** such as **Pug, EJS, or Handlebars**. It renders a view template and sends the resulting HTML to the client.

```js
app.get("/profile", (req, res) => {
  res.render("profile", { username: "john_doe" });
});
```

Here, the server renders the `profile` view and passes in a `username` variable, which the template can display in the HTML.

---

## Quick Comparison

| Method | What It Does | Typical Use |
|--------|--------------|-------------|
| `res.send()` | Sends text, HTML, JSON, or binary data | Simple responses |
| `res.json()` | Sends a JSON response | APIs |
| `res.status()` | Sets the HTTP status code | Errors, success codes (chain it with another method) |
| `res.redirect()` | Sends the user to another URL | Moved pages, after form submissions |
| `res.render()` | Renders a template and sends HTML | Server-rendered web pages |

---

## Summary

- The **`res` object** is how your app sends responses to the client.
- Use **`res.send()`** for text, HTML, or other simple data.
- Use **`res.json()`** to return structured data from an API.
- Use **`res.status()`** to control the status code, and chain it with `send()` or `json()`.
- Use **`res.redirect()`** to send users to a different URL.
- Use **`res.render()`** to display a template with dynamic data.

Whether you're sending text, JSON, or redirecting the client, Express gives you a flexible set of tools to handle it.
