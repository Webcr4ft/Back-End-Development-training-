# dotenv and .env Files

## Overview

A **`.env` file** and the **`dotenv` library** are tools used in modern software development to **separate sensitive configuration data from application code**.

| | **`.env` file** | **`dotenv` package** |
|---|---|---|
| **What it is** | A plain text file | A lightweight module |
| **Role** | Stores settings and secrets as key-value pairs | Reads the file and loads values into your app |
| **Location** | Root of the project directory | Imported in your entry file |

---

## 1. What Is a `.env` File?

A `.env` file is a plain text file at the **root of your project** that stores configuration settings and secrets as **key-value pairs**.

### The problem it solves

Developers should not hardcode these directly in source code:

- API keys
- Database passwords
- Port numbers

If hardcoded code is pushed to a public repository like **GitHub**, those secrets are exposed. Instead, developers store them **locally** in the `.env` file.

### Structure

```env
PORT=3000
DB_HOST=localhost
API_KEY=xyz123secretkey
```

Each line follows the format `KEY=value`.

### Keep it out of Git

Because the file holds highly sensitive keys, it is standard practice to add `.env` to your **`.gitignore`** file so Git never tracks it.

```gitignore
# .gitignore
.env
```

---

## 2. What Is the `dotenv` Package?

`dotenv` **connects the `.env` file to your application**.

### How it works

1. Your program starts.
2. `dotenv` **reads** the `.env` file.
3. It **parses** the keys.
4. It **injects** them into the runtime environment.
5. Your code accesses them through the global **`process.env`** object (in Node.js).

> **Tip:** In a Node.js app, initialize `dotenv` at the **very top of your entry file**, so the variables are available before the rest of your code runs.

---

## 3. Example in Node.js (Express)

```javascript
const express = require('express');
const app = express();

// Initialize and configure dotenv
require('dotenv').config();

// Access the variables securely from the environment
const port = process.env.PORT || 5000;
const apiKey = process.env.API_KEY;

app.get('/', (req, res) => {
  res.send(`Connected successfully using API Key: ${apiKey}`);
});

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

| Line | What it does |
|---|---|
| `require('dotenv').config()` | Loads the `.env` file into `process.env` |
| `process.env.PORT \|\| 5000` | Uses `PORT` from `.env`, or falls back to `5000` if it is missing |
| `process.env.API_KEY` | Reads the secret API key from the environment |

> **Warning:** The example above sends the API key back to the browser. That is fine for a demo, but **never expose real secrets in a response** in a real application.

---

## 4. Two Major Benefits

| Benefit | Explanation |
|---|---|
| **Security** | Private credentials stay **out of source code**, so they are not exposed if the code is shared |
| **Flexibility** | The **same codebase** behaves differently in development, testing, and production. You just swap the `.env` file on each hosting server |

---

## Key Takeaways

- A **`.env` file** stores secrets and settings as `KEY=value` pairs at the project root.
- **Add `.env` to `.gitignore`** so it is never pushed to GitHub.
- **`dotenv`** loads the file and makes values available through **`process.env`**.
- Call `require('dotenv').config()` **at the top** of your entry file.
- Use `process.env.NAME || fallback` to provide **default values**.
- One codebase can run in **development, testing, and production** just by changing the `.env` file.

---

## Questions

*(Add your questions here.)*
