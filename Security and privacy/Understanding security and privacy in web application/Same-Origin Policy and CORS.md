# Same-Origin Policy and CORS (Simple Version)

## The Big Idea

- **Same-Origin Policy (SOP):** The browser's default rule: "A website can only read data from **itself**, not from other websites."
- **CORS:** A way for a server to say: "I trust that other website. Let it read my data."

**Analogy:** Think of an office building.
- SOP is the **security guard** who only lets employees into their own office.
- CORS is a **guest list**. If your name is on it, the guard lets you in.

---

## 1. Same-Origin Policy

### What is an origin?

An origin is a website's "address," made of **3 parts**:

| Part | Example |
|---|---|
| Protocol | `https` |
| Domain | `example.com` |
| Port | `443` |

Full example: `https://example.com:443`

Two sites have the **same origin** only if **all 3 parts match exactly**.

| Site A | Site B | Same origin? |
|---|---|---|
| `https://example.com` | `https://example.com/page` | ✅ Yes |
| `https://example.com` | `http://example.com` | ❌ No (different protocol) |
| `https://example.com` | `https://other.com` | ❌ No (different domain) |
| `https://example.com` | `https://example.com:8080` | ❌ No (different port) |

> **Note:** Browsers hide standard ports (HTTPS = `443`, HTTP = `80`), but they still check them.

### Why does it exist?

Imagine you have two tabs open:

- **Tab 1:** Your bank account
- **Tab 2:** A malicious website

Without SOP, Tab 2 could secretly read your bank data. **SOP blocks this.**

---

## 2. The Problem

Sometimes websites **need** to share data across origins. For example:

- Your **frontend** is at `https://myapp.com`
- Your **backend** is at `https://api.myapp.com`

These are different origins, so SOP blocks the request, even though it is safe.

**CORS solves this problem.**

---

## 3. CORS (Cross-Origin Resource Sharing)

CORS lets a **server** give permission to specific websites using **headers** (small pieces of info sent with a request or response).

### How it works, step by step

1. **Browser asks:** "Hey server, can I get your data? I'm from `https://myapp.com`." (This is the `Origin` header.)
2. **Server checks:** "Do I trust `https://myapp.com`?"
3. **If yes:** The server replies with a permission header. The browser lets the website read the data. ✅
4. **If no:** The server sends no permission. The browser **blocks** the data, and the website gets an error. ❌

---

## 4. CORS in Code (Node.js)

### Option A: Express with the `cors` package

**For development:** allow everyone (easy, but not safe for real apps).

```javascript
const express = require('express');
const cors = require('cors');
const app = express();

app.use(cors()); // Allows ALL origins
```

**For production:** allow only specific websites.

```javascript
const corsOptions = {
  origin: ['https://yourapp.com', 'https://admin.yourapp.com'],
  credentials: true
};

app.use(cors(corsOptions));
```

### Option B: Raw Node.js (no package)

You must set the headers **by hand on every response**.

```javascript
res.setHeader('Access-Control-Allow-Origin', 'https://example.com');
res.setHeader('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE, OPTIONS');
res.setHeader('Access-Control-Allow-Headers', 'Content-Type, Authorization');
```

**What each header means:**

| Header | Plain English |
|---|---|
| `Access-Control-Allow-Origin` | "This website is allowed in." |
| `Access-Control-Allow-Methods` | "These actions are allowed (GET, POST, etc.)." |
| `Access-Control-Allow-Headers` | "These extra request details are allowed." |

---

## Key Takeaways

- **SOP** = the browser blocks sites from reading each other's data by default.
- **CORS** = the server gives specific sites permission to read its data.
- **Dev:** `cors()` allows everyone. **Production:** list only the sites you trust.

---

## Questions

*(Add your questions here.)*
