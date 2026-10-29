# Node.js `fs` Module Guide

A beginner-friendly guide to working with files and folders in Node.js.

## Table of Contents

- [What Is the `fs` Module?](#what-is-the-fs-module)
- [Importing the Module](#importing-the-module)
- [Method Types](#method-types)
- [Sync vs Callback vs Promise](#sync-vs-callback-vs-promise)
- [Common Methods](#common-methods)
  - [writeFile()](#writefile)
  - [appendFile()](#appendfile)
  - [readFile()](#readfile)
  - [unlink()](#unlink)
- [Quick Reference](#quick-reference)

---

## What Is the `fs` Module?

`fs` stands for **file system**. It is a built-in Node.js module that lets you work with files and folders, including:

- Opening and closing files
- Reading and writing files
- Deleting files

## Importing the Module

`fs` is a standard module, so there is nothing to install. If you have Node.js, you have `fs`.

```js
const fs = require("fs");
```

## Method Types

Many `fs` methods come in two forms: **asynchronous** and **synchronous** (the synchronous ones end in `Sync`). A few are asynchronous only.

```js
fs.writeFile()      // Asynchronous file writing
fs.writeFileSync()  // Synchronous file writing

fs.readFile()       // Asynchronous file reading
fs.readFileSync()   // Synchronous file reading

fs.open()           // Asynchronous open
fs.openSync()       // Synchronous open

fs.openAsBlob()     // Asynchronous only, no synchronous version

fs.opendir()        // Asynchronous directory open
fs.opendirSync()    // Synchronous directory open
```

You can use these methods in three styles:

| Style | Example | Best for |
| --- | --- | --- |
| Callbacks | `fs.writeFile()` | Older code, simple cases |
| Promises (`async/await`) | `fs.promises.writeFile()` | Modern, readable code |
| Synchronous | `fs.writeFileSync()` | Quick scripts |

### Callback style

```js
fs.writeFile("filePath", "content", "utf8", (err) => {
  if (err) {
    throw err;
  }
  console.log("File written to!");
});
```

### Promise style

You can import from `fs/promises` or use `fs.promises`.

```js
async function promisesExample() {
  try {
    await fs.promises.writeFile("filePath", "content", "utf8");
    console.log("File written to!");
  } catch (err) {
    console.error("Error:", err);
  }
}

promisesExample();
```

### Synchronous style

```js
try {
  fs.writeFileSync("filePath", "content", "utf8");
  console.log("File written to!");
} catch (err) {
  console.error("Error:", err);
}
```

## Sync vs Callback vs Promise

**Synchronous methods are blocking.** Your program stops and waits for the file operation to finish before running the next line.

- **Good for:** quick scripts, small projects, one-off tasks.
- **Bad for:** real-world apps. Blocking I/O (input/output) can freeze other parts of your app, which slows it down and hurts user experience.

**Asynchronous methods are non-blocking.** The rest of your program keeps running while Node handles the file work in the background.

- **Callbacks** are the traditional approach, but they get messy as your app grows.
- **Promises with `async/await`** are easier to read and maintain.

Both async options are available. Choose based on your needs.

## Common Methods

The examples below use the promise-based API (`fs/promises`).

### `writeFile()`

Writes to a file and **overwrites** any existing content. If the file doesn't exist, it is created. A relative path is resolved from the current working directory.

```js
const fs = require("fs/promises");

async function writeToFile() {
  try {
    await fs.writeFile(
      "article.md",
      "## Node `fs` Module: The Complete Guide",
      "utf8",
    );
    console.log("File written to!");
  } catch (err) {
    console.error("Error writing to file:", err);
  }
}

writeToFile(); // File written to!
```

Content of `article.md` afterward:

```md
## Node `fs` Module: The Complete Guide
```

### `appendFile()`

Adds content to the **end** of a file without erasing what is already there. If the file doesn't exist, it is created.

```js
const fs = require("fs/promises");

async function appendToFile() {
  try {
    await fs.appendFile(
      "article.md",
      "\nIn this article, you will learn all there is to know about the Node fs module...",
      "utf8",
    );
    console.log("File appended to!");
  } catch (err) {
    console.log("Error appending to file:", err);
  }
}

appendToFile(); // File appended to!
```

### `readFile()`

Reads the content of a file.

```js
const fs = require("fs/promises");

async function readFileContent() {
  try {
    const fileContent = await fs.readFile("article.md", "utf8");
    console.log("File content:", fileContent);
  } catch (err) {
    console.error("Error reading file:", err);
  }
}

readFileContent();

/*
File content: ## Node `fs` Module: The Complete Guide

In this article, you will learn all there is to know about the Node fs module...
*/
```

> **Tip:** If you don't specify the `utf8` encoding, you get a **Buffer** (raw bytes) instead of readable text.

```js
async function readFileContent() {
  try {
    const fileContent = await fs.readFile("article.md");
    console.log("File content:", fileContent);
  } catch (err) {
    console.error("Error reading file:", err);
  }
}

readFileContent();

/*
File content: <Buffer 23 23 20 4e 6f 64 65 20 60 66 73 60 20 4d 6f 64 75 6c 65 3a 20 54 68 65 20 43 6f 6d 70 6c 65 74 65 20 47 75 69 64 65 0a 49 6e 20 74 68 69 73 20 61 72 ... 70 more bytes>
*/
```

The next lesson covers how to handle a Buffer with the Node.js `Buffer` module.

### `unlink()`

Deletes a file.

```js
const fs = require("fs/promises");

async function deleteFile() {
  try {
    await fs.unlink("article.md");
    console.log("File deleted successfully!");
  } catch (err) {
    console.error("Error deleting file:", err);
  }
}

deleteFile();
```

If the file does not exist, you get an error like this:

```
Error deleting file: Error: ENOENT: no such file or directory, unlink 'article.md'
```

If it exists, the file is deleted and your success message is printed.

## Quick Reference

| Task | Method | Behavior |
| --- | --- | --- |
| Create or overwrite a file | `writeFile()` | Replaces existing content |
| Add to a file | `appendFile()` | Keeps existing content, adds to the end |
| Read a file | `readFile()` | Returns a string (with `utf8`) or a Buffer |
| Delete a file | `unlink()` | Throws `ENOENT` if the file doesn't exist |
