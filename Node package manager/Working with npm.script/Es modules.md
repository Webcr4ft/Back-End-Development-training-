# How Do Imports and Exports Work with ES Modules?

## The Big Idea

**ES modules (ESM)**, short for ECMAScript modules, are the official, standardized module format for JavaScript. They use `import` and `export` statements instead of `require()` and `module.exports`.

In Node.js, ES modules load **asynchronously**, which is more efficient than CommonJS's synchronous loading.

> **Quick comparison with what you already know:** CommonJS uses `require()`. ES modules use `import`.

---

## When Does Node Treat a File as an ES Module?

1. Files with a `.mjs` extension.
2. Files with a `.js` extension when the nearest parent `package.json` has `"type": "module"`.

```json
{
  "type": "module"
}
```

---

## Named Exports

Here is the same `multiply` function from before, now using ESM. In these examples, both files use the `.mjs` extension.

### Way 1: Export with curly braces

Use the `export` keyword, followed by the names you want to export inside curly braces:

```js
// math.mjs
function multiply(a, b) {
  return a * b;
}

export { multiply };
```

### Way 2: Export directly in the declaration

Put `export` before the function:

```js
// math.mjs
export function multiply(a, b) {
  return a * b;
}
```

Both ways are called **named exports**. You can have **multiple named exports** in one module.

---

## Importing a Module

Use the `import` keyword, curly braces, the `from` keyword, and the relative path to the module:

```js
import { multiply } from './math.mjs';

console.log(multiply(6, 7)); // 42
```

Inside the curly braces, write the name of the function, variable, or object you want to import. Here, it's `multiply`.

> **Key difference:** ES modules use `import`, not `require()`.

---

## Default Exports

Each ES module can have **one default export**. When you import a default export, you **don't need curly braces**.

```js
// math.mjs
export default function multiply(a, b) {
  return a * b;
}
```

```js
import multiply from './math.mjs';
```

The function is imported and assigned by default.

### Named vs. default exports

| | Named export | Default export |
|---|--------------|----------------|
| **How many per module?** | Many | Only one |
| **Export syntax** | `export function multiply() {}` or `export { multiply }` | `export default function multiply() {}` |
| **Import syntax** | `import { multiply } from './math.mjs'` | `import multiply from './math.mjs'` |
| **Curly braces on import?** | Yes | No |

---

## How Node Detects the Module System

If you don't use a file extension or `package.json` to tell Node which system you want, Node **inspects your source code**.

- It finds ES module syntax (`import` / `export`)? It runs the file as an **ES module**.
- It doesn't? It runs the file as **CommonJS**.

---

## CommonJS vs. ES Modules

| | CommonJS | ES Modules |
|---|----------|------------|
| **Import** | `require('./math')` | `import { multiply } from './math.mjs'` |
| **Export** | `module.exports = { multiply }` | `export { multiply }` or `export default multiply` |
| **Loading** | Synchronous | Asynchronous |
| **File extension** | `.cjs` (or `.js` by default) | `.mjs` (or `.js` with `"type": "module"`) |
| **`package.json` setting** | `"type": "commonjs"` (or no `"type"`) | `"type": "module"` |

---

## Summary

- ES modules are the official JavaScript standard.
- Use `export` to share code and `import ... from` to use it.
- **Named exports**: many per module, imported with curly braces.
- **Default export**: one per module, imported without curly braces.
- Node uses the file extension, the `package.json` `"type"` field, or the code's syntax to decide which system to use.
- CommonJS was the default in Node's early days, but developers increasingly use ESM for its efficiency and compatibility with modern JavaScript. It's important to know both.

## Quick Reference

| I want to... | Code |
|--------------|------|
| Export one named item | `export { multiply };` |
| Export directly in the declaration | `export function multiply() {}` |
| Export a default | `export default function multiply() {}` |
| Import a named export | `import { multiply } from './math.mjs';` |
| Import a default export | `import multiply from './math.mjs';` |
