# Getting Started with Express.js

## What is Express.js?

**Express.js** (or just **Express**) is a small, flexible web framework built on top of **Node.js**. It makes it much easier to build web servers and APIs.

Node.js can already create servers with its built-in `http` module, but that takes a lot of repetitive "boilerplate" code. Express removes most of that work, so you can build a working server in just a few lines.

> **Think of it this way:** Node.js is the engine. Express is the steering wheel and pedals that make it easy to drive.

Express is also **unopinionated**, which means it doesn't force a specific project structure or way of doing things. You decide how to organize your app.

---

## Why Developers Love Express

1. **Minimal and fast**
   Express gives you only the essentials. You add extra features only when you need them, using middleware and plugins.

2. **Massive ecosystem**
   There are thousands of ready-made middleware packages and plugins for things like logging, authentication, security, and sessions.

3. **Great for APIs**
   Its simple routing and request-handling model makes it ideal for building **RESTful APIs**.

---

## What Can You Build with Express?

- Web apps
- RESTful APIs
- Backends for Single Page Applications (SPAs)
- Middleware-heavy services
- Anything server-side that uses HTTP

---

## How to Install Express

### Step 1: Check that Node.js and npm are installed

Run these commands in your terminal:

```bash
node -v
npm -v
```

- If you see version numbers, you're ready to go.
- If not, install Node.js first (npm comes with it). See the earlier lesson or the official [Node.js website](https://nodejs.org).

### Step 2: Create a project and install Express

```bash
mkdir my-app        # create a new folder for your project
cd my-app           # move into that folder
npm init -y         # create a package.json file with default settings
npm install express # install Express
```

---

## Key Terms Explained

### Middleware

**Middleware** is code that runs *between* receiving a request and sending back a response.

```
Request  →  Middleware  →  Middleware  →  Route Handler  →  Response
```

It's commonly used for:

- Error handling
- Input validation
- Modifying data in the request or response

You can **chain** several middleware functions together to build flexible, reusable logic for handling requests.

### Plugins

**Plugins** are third-party Node.js modules that add extra features to Express. You install them separately with npm, and most work as middleware, so they only need a little setup.

Instead of writing common features from scratch, you can use a plugin for:

- Logging
- Authentication
- Security best practices

> You'll learn more about both middleware and plugins in future lessons.

---

## Summary

Express is one of the most popular frameworks for server-side development with Node.js. It gives you the building blocks to:

- Quickly start a server
- Handle routes
- Manage middleware
- Build APIs

All with clean, readable code.
