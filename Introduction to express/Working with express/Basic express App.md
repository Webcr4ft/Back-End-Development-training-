# How Do You Create a Basic Express App?

## Quick Recap

In the previous lesson, you set up your project:

```bash
mkdir my-app        # create a new project folder
cd my-app           # move into the folder
npm init -y         # create a basic package.json file
npm install express # install Express
```

---

## Step 1: Create Your First Server

Open a code editor, create a file named `index.js`, and add this code:

```js
const express = require("express");
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`);
});
```

## Step 2: Run It

In your terminal, run:

```bash
node index.js
```

## Step 3: See the Result

Open your browser and go to [http://localhost:3000](http://localhost:3000). You'll see:

```
Hello World!
```

That's how fast it is to get started with Express!

---

## Code Walkthrough

Let's break the code down piece by piece.

### 1. Load Express

```js
const express = require("express");
```

This loads the Express library and stores it in a variable called `express`.

### 2. Create the App

```js
const app = express();
```

`express` is a **factory function**, meaning that calling it creates and returns a new Express application.

`app` is your main server object. It gives you access to Express methods like `.get()`, `.post()`, and `.listen()`.

### 3. Set the Port

```js
const port = 3000;
```

A **port** is a network endpoint your app listens on. `3000` is a common choice for local development.

### 4. Define a Route

```js
app.get("/", (req, res) => {
  res.send("Hello World!");
});
```

A **route** tells the server how to respond to a specific request. Here is what each part does:

| Part | Meaning |
|------|---------|
| `app.get()` | Handles HTTP **GET** requests (commonly used to retrieve data) |
| `"/"` | The route path. `/` is the root URL of your app |
| `(req, res) => { ... }` | A **callback function** that runs when a request matches this route |
| `req` | The **request** object, with info about the incoming request |
| `res` | The **response** object, used to send a reply to the client |
| `res.send("Hello World!")` | Sends the text "Hello World!" back to the client |

### 5. Start the Server

```js
app.listen(port, () => {
  console.log(`Example app listening on port ${port}`);
});
```

`app.listen()` starts your app and tells Node to listen for incoming HTTP requests on the given port (`3000` here).

Once the server is running, the callback executes and logs this message to the console:

```
Example app listening on port 3000
```

This confirms your app started successfully and is ready to receive requests.

---

## How It All Fits Together

```
Browser visits http://localhost:3000
        ↓
Express receives a GET request for "/"
        ↓
app.get("/") route matches
        ↓
res.send("Hello World!")
        ↓
Browser displays "Hello World!"
```

---

## Summary

- `require("express")` loads the library.
- `express()` creates your app.
- `app.get()` defines how to respond to a route.
- `app.listen()` starts the server on a port.
- `node index.js` runs everything.
