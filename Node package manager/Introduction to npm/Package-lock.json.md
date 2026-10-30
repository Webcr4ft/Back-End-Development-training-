# What Is the package-lock.json File?

## The Big Idea

The **package-lock.json** file records the **exact versions** of every package installed in your project, so everyone working on it gets the same setup.

> **Think of it as a receipt.** `package.json` is your shopping list ("I want lodash, any 4.x version is fine"). `package-lock.json` is the receipt ("I bought exactly lodash 4.17.21").

---

## The Problem It Solves

When you run `npm install`, npm reads `package.json` to see which packages your project needs. Each dependency has a version number like this:

```json
"lodash": "^4.17.21"
```

As you learned earlier, the caret (`^`) lets npm install newer **minor and patch** versions, like `4.18.0` or `4.17.22`. That flexibility is helpful, but it can cause trouble:

- Developer A runs `npm install` today and gets `4.17.21`.
- Developer B runs `npm install` next month and gets `4.18.0`.

Even small differences between versions can cause bugs or unexpected behavior. Now the same project behaves differently on two machines.

---

## The Solution

`package-lock.json` fixes this.

- It is **created automatically** the first time you run `npm install`.
- It **locks the exact version** of every dependency that was installed.
- It also locks all **child dependencies** (the dependencies *of* your dependencies).

This guarantees that everyone gets the **same versions every time**, no matter when they run `npm install`.

---

## Example: `package.json` vs. `package-lock.json`

Here's a simple `package.json` with lodash as a dependency:

```json
{
  "name": "package-lock-json",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "type": "commonjs",
  "dependencies": {
    "lodash": "^4.17.21"
  }
}
```

And here is the matching section from `package-lock.json`:

```json
"node_modules/lodash": {
  "version": "4.17.21",
  "resolved": "https://registry.npmjs.org/lodash/-/lodash-4.17.21.tgz",
  "integrity": "sha512-v2kDEe57..."
}
```

Notice the difference:

| File | How lodash is written | What it means |
|------|-----------------------|---------------|
| `package.json` | `^4.17.21` | A **flexible** rule (a range of versions is allowed) |
| `package-lock.json` | `4.17.21` | **Pinned** to one exact version |

### What the lock file entry contains

| Field | What it means |
|-------|---------------|
| `version` | The exact version that was installed |
| `resolved` | The URL the package was downloaded from |
| `integrity` | A checksum that confirms the downloaded code hasn't been changed or corrupted |

---

## Child Dependencies

The lock file also pins **child dependencies**: packages that your dependencies need internally to work.

Here's part of the `package-lock.json` for a project that uses Express:

```json
{
  "name": "package-lock-json-file",
  "version": "1.0.0",
  "lockfileVersion": 3,
  "requires": true,
  "packages": {
    "": {
      "name": "package-lock-json-file",
      "version": "1.0.0",
      "license": "ISC",
      "dependencies": {
        "express": "^5.2.1"
      }
    },
    ...
    "node_modules/etag": {
      "version": "1.8.1",
      "resolved": "https://registry.npmjs.org/etag/-/etag-1.8.1.tgz",
      "integrity": "sha512-aIL5Fx7mawVa300al2BnEE4iNvo1qETxLrPI/o05L7z6go7fCw1J6EQmbK4FmJ2AS7kgVF/KEZWufBfdClMcPg==",
      "license": "MIT",
      "engines": {
        "node": ">= 0.6"
      }
    },
    "node_modules/express": {
      "version": "5.2.1",
      "resolved": "https://registry.npmjs.org/express/-/express-5.2.1.tgz",
      "integrity": "sha512-hIS4idWWai69NezIdRt2xFVofaF4j+6INOpJlVOLDO8zXGpUVEVzIYk12UUi2JzjEzWL3IOAxcTubgz9Po0yXw==",
      "license": "MIT",
      "dependencies": {
        "accepts": "^2.0.0",
        "body-parser": "^2.2.1",
        "content-disposition": "^1.0.0",
        "content-type": "^1.0.5",
        "cookie": "^0.7.1",
        "cookie-signature": "^1.2.1",
        "debug": "^4.4.0",
        "depd": "^2.0.0",
        "encodeurl": "^2.0.0",
        "escape-html": "^1.0.3",
        "etag": "^1.8.1",
        "finalhandler": "^2.1.0",
        "fresh": "^2.0.0",
        "http-errors": "^2.0.0",
        "merge-descriptors": "^2.0.0",
        "mime-types": "^3.0.0",
        "on-finished": "^2.4.1",
        "once": "^1.4.0",
        "parseurl": "^1.3.3",
        "proxy-addr": "^2.0.7",
        "qs": "^6.14.0",
        "range-parser": "^1.2.1",
        "router": "^2.2.0",
        "send": "^1.1.0",
        "serve-static": "^2.2.0",
        "statuses": "^2.0.1",
        "type-is": "^2.0.1",
        "vary": "^1.1.2"
      },
      "engines": {
        "node": ">= 18"
      },
      "funding": {
        "type": "opencollective",
        "url": "https://opencollective.com/express"
      }
    },
    ...others
  }
}
```

*(The `...` marks parts that were left out to keep the example short.)*

### What to notice

Besides Express itself, the file lists many other packages, such as `accepts`, `mime-types`, and `negotiator`. These are **child dependencies**: packages Express depends on internally to work.

Also look closely at the version rules:

- Inside the `node_modules/express` entry, its dependencies still use **caret ranges** (like `"etag": "^1.8.1"`). These are the rules Express asks for.
- But the separate entry for each child, like `node_modules/etag`, is **pinned to one exact version** (`1.8.1`). That is the version npm actually installed.

```text
Express asks for:   "etag": "^1.8.1"   (a range)
Lock file records:  etag 1.8.1         (an exact version)
```

---

## Why It Matters

The `package-lock.json` file keeps everyone on the same page. It ensures consistency across:

- Developer machines
- CI servers
- Deployments
- Other environments

---

## Best Practices

| Do | Don't |
|----|-------|
| ✅ **Commit** `package-lock.json` to Git so your whole team shares the same setup | ❌ **Edit** `package-lock.json` by hand |

npm updates the file **automatically** whenever your dependencies change, so you never need to touch it yourself.

---

## Quick Summary

| | `package.json` | `package-lock.json` |
|---|---|---|
| **Purpose** | Lists the packages your project needs | Records the exact versions installed |
| **Versions** | Flexible ranges (`^4.17.21`) | Exact versions (`4.17.21`) |
| **Includes child dependencies?** | No, only your direct ones | Yes, every one |
| **Who edits it?** | You (and npm commands) | npm only, automatically |
| **Commit to Git?** | Yes | Yes |
