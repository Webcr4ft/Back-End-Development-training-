# How Can You Serve Static Files in Express?

## What Is Static File Serving?

**Static files** are assets that don't change dynamically, such as:

- Images
- CSS files
- Client-side JavaScript
- Fonts
- Other resources

**Static file serving** means delivering files directly from the server's file system to the browser, with no extra server-side processing.

For example, when a browser requests `/styles.css`, `/script.js`, or `/images/logo.png`, Express can find those files in a specified folder and send them as they are. Because the files don't need to be generated or modified, they're called *static*.

Express does this with its built-in **`express.static()`** middleware. You don't need to define a route for each file.

> **Think of it this way:** Static files are like items on a shelf. When someone asks for one, Express just grabs it and hands it over without changing anything.

---

## Setting Up Static File Serving

```js
const express = require("express");
const path = require("path");
const app = express();
const port = 3000;

// Serve static files from the "public" directory
app.use(express.static(path.join(__dirname, "public")));

app.get("/", (req, res) => {
  res.send("Welcome to the static file demo!");
});

app.listen(port, () => {
  console.log(`Server running at http://localhost:${port}`);
});
```

### Breaking It Down

| Part | Meaning |
|------|---------|
| `require("express")` | Imports Express to create the server |
| `require("path")` | Imports Node's `path` module, which builds file paths that work on any operating system |
| `express.static(...)` | Middleware that serves files from a folder |
| `path.join(__dirname, "public")` | The full path to the `public` folder, starting from the current file's directory |
| `app.use(...)` | Registers the middleware, so every file in `public` becomes accessible to the browser |
| `app.get("/", ...)` | A normal route, which shows that static serving and dynamic routes can **coexist** |
| `app.listen()` | Starts the server on port `3000` |

---

## Project Structure

You need a folder named `public` to hold your static files:

```
my-app/
│
├── app.js
└── public/
    ├── index.html
    ├── styles.css
    └── image.png
```

### What Happens When a File Is Requested

When a user visits `http://localhost:3000/index.html`:

```
Request: GET /index.html
        ↓
express.static() checks the "public" folder
        ↓
  File exists?
  ├── Yes → Express sends the file to the browser
  └── No  → The request moves on to the next middleware or route
                  ↓
            Nothing else handles it? → Express returns a 404
```

You don't define a route for each file. A request to `http://localhost:3000/styles.css` makes Express look for `public/styles.css` and send it automatically.

| Request URL | File Express Looks For |
|-------------|------------------------|
| `/index.html` | `public/index.html` |
| `/styles.css` | `public/styles.css` |
| `/image.png` | `public/image.png` |

Notice that `public` does **not** appear in the URL. Files are served from the root path.

---

## Serving Files From Multiple Directories

You can also serve files from more than one directory. Imagine this structure:

```
my-app/
│
├── app.js
│
├── public/
│   ├── index.html
│   └── styles.css
│
└── images/
    └── image.png
```

Register both directories like this:

```js
app.use(express.static(path.join(__dirname, "public")));
app.use("/images", express.static(path.join(__dirname, "images")));
```

### How It Works

- **Line 1** serves the `public` directory from the **root path**, just like before.
- **Line 2** passes `"/images"` as the first argument to `app.use()`. This is a **mount path**. It tells Express to only use this middleware when a request **starts with `/images`**. When that happens, `express.static()` looks for the file inside the `images` directory.

### Example Requests

| Request | What Express Does |
|---------|-------------------|
| `GET /styles.css` | Looks in `public` for `styles.css`, finds it, and sends it to the client |
| `GET /images/image.png` | The path starts with `/images`, so Express looks in the `images` directory for `image.png`, finds it, and sends it to the client |

---

## Conclusion

Serving static files with Express is simple and powerful. With `express.static()`, you can easily serve assets like images, stylesheets, and client-side JavaScript.

Keeping static files in a dedicated folder like `public`, or using multiple directories with mount paths, keeps your app **organized, maintainable, and easy to scale**.

---

## Summary

- **Static files** are assets that don't change, such as images, CSS, JavaScript, and fonts.
- `express.static()` is **middleware** that serves files directly from a folder.
- Use `app.use(express.static(path.join(__dirname, "public")))` to serve a `public` folder.
- You **don't need a route for each file**.
- If a file isn't found, the request moves on to the next middleware or route, and Express returns a **404** if nothing handles it.
- Use a **mount path**, like `app.use("/images", ...)`, to serve a directory under a specific URL prefix.
- Static serving and normal routes can **work together** in the same app.
