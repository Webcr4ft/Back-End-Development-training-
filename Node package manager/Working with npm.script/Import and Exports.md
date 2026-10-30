# How Do Imports and Exports Work with CommonJS Modules?

## The Big Idea

A **module** is a self-contained, reusable block of code. In Node.js, **every file is a module**.

> **Think of modules as LEGO bricks.** Each file does one job. You snap them together by importing what you need.

Splitting code into modules makes it easier to maintain, especially in large and complex applications.

---

## Two Module Systems in Node.js

| System | Notes |
|--------|-------|
| **CommonJS** | The original and default system. Uses `require()` |
| **ES Modules** | The newer syntax that is gradually replacing CommonJS |

CommonJS loads modules **synchronously**. That means Node waits for one module to finish loading before it loads the next one or continues running your code.

CommonJS is still widely used, so it's important to understand it.

---

## Exporting: Sharing Code From a File

By default, functions and variables in a Node.js module are **private**. Other files can't use them unless you **export** them.

Say we have a file called `math.js` with a multiplication function:

```js
function multiply(a, b) {
  return a * b;
}
```

Right now, no other file can use `multiply`. To share it, assign a value to `module.exports`.

> `module.exports` is what the module hands back when another file imports it.

```js
function multiply(a, b) {
  return a * b;
}

module.exports = {
  multiply: multiply
};
```

Here, we export an object with a `multiply` property. Its value is a reference to the `multiply` function.

---

## Importing: Using Code From Another File

Use the `require()` function and pass the **relative path** of the file. Store the result in a variable:

```js
const math = require('./math');
```

If you print `math`, you'll see an object with a `multiply` function inside:

```js
console.log(math);
// { multiply: [Function: multiply] }
```

Now call the function:

```js
const math = require('./math');

console.log(math.multiply(6, 7)); // 42
```

The function runs successfully, even though it lives in another file. The import worked.

---

## Ways to Export

### 1. Export an object (as shown above)

```js
module.exports = {
  multiply: multiply
};
```

### 2. Export a single value

If you only need to export one function, variable, or object, assign it directly:

```js
function multiply(a, b) {
  return a * b;
}

module.exports = multiply;
```

### 3. Export multiple functions

Add each one to the object, separated by commas:

```js
function subtract(a, b) {
  return a - b;
}

function multiply(a, b) {
  return a * b;
}

module.exports = {
  subtract: subtract,
  multiply: multiply
};
```

Any file that imports `math.js` can now use both `subtract` and `multiply`.

> **Important:** The way you export affects the way you import. If you export a single function (`module.exports = multiply`), then `require('./math')` gives you the function itself, not an object.

---

## Full vs. Partial Imports

When a module exports several things, you can import **everything** or **only what you need**.

### Full import

You get the whole object:

```js
const math = require('./math');

console.log(math.subtract(6, 7)); // -1
console.log(math.multiply(6, 7)); // 42
```

### Partial import

Put the names you want inside curly braces. This uses **destructuring assignment** to pull properties out of the exported object:

```js
const { multiply } = require('./math');

console.log(multiply(6, 7)); // 42
```

Now you can use `multiply` directly, without `math.` in front of it.

To import several, separate the names with commas:

```js
const { subtract, multiply } = require('./math');
```

### Comparison

| | Full import | Partial import |
|---|-------------|----------------|
| **Syntax** | `const math = require('./math')` | `const { multiply } = require('./math')` |
| **How you call it** | `math.multiply(6, 7)` | `multiply(6, 7)` |
| **Gets** | The whole exported object | Only the names you list |

---

## When Does Node Treat a File as CommonJS?

Node.js treats these as CommonJS modules:

1. Files with a `.cjs` extension.
2. Files with a `.js` extension when the nearest parent `package.json` has `"type": "commonjs"`.
3. Files with a `.js` extension (or no extension) when the nearest parent `package.json` has **no** `"type"` field, or when there is no `package.json` in any parent folder.
4. Files with an extension that is **not** `.mjs`, `.cjs`, `.json`, `.node`, or `.js`.

### Easy way to remember

| File or setting | Module type |
|-----------------|-------------|
| `.cjs` | CommonJS |
| `.js` with no `"type"` in `package.json` | CommonJS (the default) |
| `.js` with `"type": "commonjs"` | CommonJS |

---

## Summary

- Each file in Node.js is a **module**.
- Things in a module are **private** until you export them.
- **Export** with `module.exports`.
- **Import** with `require('./relative-path')`.
- You can import **everything** or **only some properties** using destructuring.
- ES Modules are gradually replacing CommonJS, but CommonJS is still essential for working with existing Node.js codebases and many npm packages.

## Quick Reference

| I want to... | Code |
|--------------|------|
| Export one thing | `module.exports = multiply;` |
| Export several things | `module.exports = { subtract, multiply };` |
| Import everything | `const math = require('./math');` |
| Import specific things | `const { multiply } = require('./math');` |
| Import several specific things | `const { subtract, multiply } = require('./math');` |
