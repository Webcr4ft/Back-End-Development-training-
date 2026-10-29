# Node.js Path Module: A Simple Guide

## What Is the Path Module?

`path` is a core module built into Node.js. It helps you work with **file and directory paths**. It can join, clean up, and break apart paths, and it handles differences between operating systems for you (for example, `/` on Mac/Linux and `\` on Windows).

## Importing Path

```js
const path = require("path");
```

---

## Before You Start: Key Concepts

### Global Variables: `__filename` and `__dirname`

These are built-in "CommonJS" variables. You **don't need the path module** to use them.

| Variable | What it gives you |
| --- | --- |
| `__filename` | Full path of the **current file** |
| `__dirname` | Full path of the **folder** containing the current file |

Example, working in a file called `script.js`:

```js
console.log(__filename);
// /Users/user/Desktop/fCC/script-code/node/node-path/script.js

console.log(__dirname);
// /Users/user/Desktop/fCC/script-code/node/node-path
```

### Relative vs. Absolute Paths

| Type | Meaning | Example |
| --- | --- | --- |
| **Relative** | Starts from your current working directory | `./assets/src/text-files` |
| **Absolute** | Complete address from the root of your system | `/Users/johndoe/projects/app/assets/src/text-files` |

---

## Getting Parts of a Path

### `basename()`: The Filename

Returns the last part of a path, which is the filename:

```js
console.log(path.basename(__filename)); // script.js
```

### `dirname()`: The Folder Name

Returns the directory part of a path:

```js
console.log(path.dirname(__dirname)); // node-path
```

### `extname()`: The File Extension

Returns the extension of a file:

```js
console.log(path.extname(__filename)); // .js
```

You can also check a different file:

```js
console.log(path.extname("text-files/text1.txt")); // .txt
```

---

## Building Paths

### `join()`: Combine Path Pieces

Takes multiple path segments and joins them into **one clean path**. Useful for combining files and folders.

```js
const joinedPath = path.join("src", "assets", "text-files");
console.log(joinedPath); // src/assets/text-files
```

> On Windows, the result uses backslashes: `src\assets\text-files`

`join()` also **fixes bad slashes** and removes extra ones:

```js
const wrongPath = path.join("/src//", "assets", "text-files");
console.log(wrongPath); // /src/assets/text-files
```

### `resolve()`: Get an Absolute Path

Turns path segments into a **full absolute path**.

How it works:

1. It reads the segments from **right to left** until it builds an absolute path
2. If it reaches the start without getting one, it uses the **current working directory**

```js
const absolutePath = path.resolve("assets", "src", "text-files");
console.log(absolutePath);
// /Users/user/Desktop/fCC/script-code/node/node-path/assets/src/text-files
```

### `join()` vs. `resolve()`

| Method | Result |
| --- | --- |
| `join()` | Joins and cleans segments. Can return a **relative or absolute** path |
| `resolve()` | **Always** returns an absolute path |

---

## Breaking Down and Rebuilding Paths

### `parse()`: Path to Object

Breaks a path into an object with its parts:

```js
const parsedFile = path.parse(__filename);

console.log(parsedFile);
/*
{
 root: '/',
 dir: '/Users/user/Desktop/fCC/script-code/node/node-path',
 base: 'script.js',
 ext: '.js',
 name: 'script'
}
*/
```

| Property | Meaning |
| --- | --- |
| `root` | The system root |
| `dir` | The folder path |
| `base` | Full filename with extension |
| `ext` | The file extension |
| `name` | Filename without extension |

### `format()`: Object to Path

The opposite of `parse()`. It builds a path from an object:

```js
const formattedDirectory = path.format({
  dir: "/users/johndoe/docs",
  name: "file",
  ext: ".txt",
});

console.log(formattedDirectory); // /users/johndoe/docs/file.txt
```

---

## Quick Summary

| Goal | Method |
| --- | --- |
| Get the filename | `basename()` |
| Get the folder | `dirname()` |
| Get the extension | `extname()` |
| Combine path pieces | `join()` |
| Get a full absolute path | `resolve()` |
| Split a path into parts | `parse()` |
| Build a path from parts | `format()` |

**Tip:** always use `path.join()` or `path.resolve()` instead of typing slashes by hand. Your code will then work on every operating system.
