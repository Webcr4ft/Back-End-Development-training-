# Node.js Process Module: A Simple Guide

## What Is the Process Module?

`process` is one of the most important parts of Node.js. It gives you **information about the running program** and lets you **control it** while it runs.

### What Is a "Process"?

When you type `node script.js` in the terminal, Node.js starts a **process**. A process is a running copy of Node that executes your file. It has its own memory, environment, and execution context.

### No Import Needed

`process` is **global**, so you can use it anywhere without `require()`.

---

## Reading Environment Info: `process.env`

`process.env` is an object holding information about the **environment** your app runs in. It's usually a giant object, so you normally pick out just the values you need.

```js
// Get ALL environment variables
console.log(process.env);

// Current mode (like 'development' or 'production')
console.log(process.env.NODE_ENV); // development

// The shell program running Node
console.log(process.env.SHELL); // /bin/bash

// Where the system looks for executable programs
console.log(process.env.PATH); // /usr/local/bin:/usr/bin:/bin

// The folder the process was started from
console.log(process.env.PWD); // /Users/johndoe/projects/myapp

// The username of the person running the process
console.log(process.env.USER); // johndoe
```

| Variable | What it tells you |
| --- | --- |
| `NODE_ENV` | Mode: development or production |
| `SHELL` | Which shell is running Node |
| `PATH` | Where executables are searched for |
| `PWD` | Folder the process started from |
| `USER` | Current username |

---

## Reading Command-Line Arguments: `process.argv`

`process.argv` is an **array** of everything typed in the terminal when the app was started.

```js
console.log(process.argv);
/*
[
  '/Users/user/.nvm/versions/node/v22.17.0/bin/node',
  '/Users/user/Desktop/fCC/script-code/node/node-process/script.js',
  '--watch'
]
*/
```

How to read it:

| Position | What it is |
| --- | --- |
| `argv[0]` | Path to the Node program |
| `argv[1]` | Path to your script file |
| `argv[2]` and on | Extra arguments you typed (like `--watch`) |

---

## Current Folder: `process.cwd()`

`cwd()` means **current working directory**. It returns the folder the process is running from.

```js
console.log(process.cwd());
```

---

## Process Events

Events let your app **react to key moments** in its life, like when it's about to exit, hits an error, or gets a warning. You listen for them with `process.on()`.

### `exit`: When the Process Ends

Runs right before the process finishes. The `code` tells you how it ended (`0` means success).

```js
process.on("exit", (code) => {
  console.log(`Process exiting with code: ${code}`);
});

// Process exiting with code: 0
```

### `uncaughtException`: Catching Unhandled Errors

Runs when an error happens that **nothing in your code caught**. It can help prevent a crash.

```js
process.on("uncaughtException", (err) => {
  console.error("Uncaught error:", err.message);
});
```

### `warning`: When Node Gives a Warning

Runs when Node.js emits a warning.

```js
process.on("warning", (warning) => {
  console.warn("Warning name:", warning.name);
  console.warn("Warning message:", warning.message);
});
```

You can create your own warning with `emitWarning()`:

```js
process.emitWarning("This is a custom warning message", "CustomWarning");

/*
  Warning name: CustomWarning
  Warning message: This is a custom warning message
*/
```

---

## Quick Summary

| Goal | Use |
| --- | --- |
| Read environment info | `process.env` |
| Read command-line arguments | `process.argv` |
| Get the current folder | `process.cwd()` |
| Run code when the app exits | `process.on("exit", ...)` |
| Handle uncaught errors | `process.on("uncaughtException", ...)` |
| Listen for warnings | `process.on("warning", ...)` |
| Trigger a custom warning | `process.emitWarning()` |

**Remember:** `process` is global, so you can use it anywhere without importing it.
