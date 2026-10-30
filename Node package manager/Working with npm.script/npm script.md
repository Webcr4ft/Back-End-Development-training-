# What Are npm Scripts?

## The Big Idea

**npm scripts** are custom commands you define in your `package.json` file. They let you turn long or repeated commands into short shortcuts.

> **Think of them as keyboard shortcuts for your terminal.** Instead of typing a long chain of commands every time, you type one short command.

They are useful for automating tasks you repeat during development, testing, and deployment, such as:

- Starting your whole development environment with `npm start`
- Checking your code style (linting)
- Running your test suite

---

## Quick Review

| Term | Meaning |
|------|---------|
| **npm** | A command-line tool for installing and managing JavaScript packages |
| **Package** | A directory that groups related code in a logical structure |
| **Script** | A sequence of instructions or commands written in a scripting language |
| **npm script** | A custom command defined in `package.json` |

---

## Where Scripts Live

To create npm scripts, you first need a `package.json` file. It holds your project's metadata, dependencies, and scripts.

To create one, run this in your project's root folder:

```bash
npm init
```

You can type in the details (name, version, description, etc.) or leave them blank to use the defaults. With all defaults, you'll see something like this:

```json
{
  "name": "<project_name>",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "description": ""
}
```

Your scripts go under the `scripts` key. By default there is one script, called `test`.

---

## Script Syntax

```text
"<script_name>": "<commands>"
```

| Side of the colon | What it is |
|-------------------|------------|
| **Left** | The script name, which acts as a shortcut. Common names: `start`, `test`, `build`, `dev`, `lint` |
| **Right** | The actual command(s) that run |

Example:

```json
"scripts": {
  "start": "node app.js"
}
```

---

## Running a Script

```bash
npm run <script_name>
```

For the example above:

```bash
npm run start
```

This runs the underlying command, `node app.js`.

### The shorthand

You can skip the word `run`:

```bash
npm <script_name>
```

> ⚠️ This only works for four script names: `start`, `test`, `stop`, and `restart`.

So `npm start` and `npm run start` do the same thing.

At first, this just replaces `node app.js` with `npm start`. But imagine a script that runs many complex commands in order or at the same time. One short command can run all of them, which saves a lot of time.

### Common scripts

| Command | What it does |
|---------|--------------|
| `npm run <script_name>` | Runs any custom script |
| `npm start` | Starts the main app or development server |
| `npm run lint` | Checks that your code follows style standards and best practices |
| `npm test` | Runs your project's test suite |

### Naming tip

A common convention is to use a **colon** to group related scripts, like `start:server` and `start:ui`.

---

## Running Commands One After Another (Sequentially)

You have two options: `&&` and `;`.

### `&&` (logical AND): stops if something fails

The next command runs **only if the first one succeeds**.

```json
"scripts": {
  "build": "webpack --mode production",
  "start": "npm run build && node server.js"
}
```

Here, `npm start` runs `npm run build` first. Only if the build succeeds does `node server.js` run.

This is very common because it's reliable. It avoids wasting time and resources on later commands that would fail anyway.

### `;` (semicolon): keeps going no matter what

The next command runs **regardless of whether the first one succeeded**.

```json
"scripts": {
  "build": "webpack --mode production",
  "start": "npm run build; node server.js"
}
```

Now `node server.js` **always runs** after `npm run build`, even if the build failed.

> **Note:** The original text says this runs "even if `node server.js` was not successful." That's a small mix-up. The semicolon makes `node server.js` run even if `npm run build` (the *first* command) fails.

### Comparison

| | `&&` | `;` |
|---|------|-----|
| **Runs next command if first succeeds?** | Yes | Yes |
| **Runs next command if first fails?** | No | Yes |
| **Best for** | Steps that depend on each other | Steps that are independent |

---

## Running Commands at the Same Time (Concurrently)

Use the `&` operator to run commands in parallel:

```json
"scripts": {
  "start:server": "node server/index.js",
  "start:client": "npm run build:watch",
  "dev": "npm run start:server & npm run start:client"
}
```

> ⚠️ **Watch out:** This runs the processes in the **background**. In one terminal, you'll see their output mixed together, which can be hard to read.

Other options for running commands concurrently:

- `concurrently`
- `npm-run-all`

### Quick comparison of the three operators

| Operator | Meaning | Example |
|----------|---------|---------|
| `&&` | Run next only if the first succeeds | `npm run build && node server.js` |
| `;` | Run next no matter what | `npm run build; node server.js` |
| `&` | Run both at the same time | `npm run start:server & npm run start:client` |

---

## Passing Arguments to Scripts

To send arguments to the command inside a script, type two hyphens (`--`) followed by the arguments:

```bash
npm run <script_name> -- <argument_1> <argument_2> <argument_3>
```

The `--` tells npm: **"everything after this goes to the underlying command."**

### Example: choosing a port

Say you have this script:

```json
{
  "name": "project-example",
  "scripts": {
    "start": "node app.js"
  }
}
```

To pass a port number:

```bash
npm start -- 8000
```

### Reading the argument in your code

Node.js stores arguments in the `process.argv` array:

```js
process.argv[0] // The path to the node executable
process.argv[1] // The script file being executed
process.argv[2] // The first argument (8000)
```

So you can get the port number anywhere in your code with `process.argv[2]`.

---

## Summary

npm scripts turn complex, repeated command sequences into simple, consistent shortcuts. They are essential tools for simplifying your development workflow.

## Quick Reference

| I want to... | Do this |
|--------------|---------|
| Define a script | `"name": "command"` inside `scripts` |
| Run any script | `npm run name` |
| Run `start`, `test`, `stop`, or `restart` | `npm name` (no `run` needed) |
| Run commands in order, stop on failure | `cmd1 && cmd2` |
| Run commands in order, ignore failure | `cmd1; cmd2` |
| Run commands at the same time | `cmd1 & cmd2` |
| Pass arguments | `npm run name -- arg1 arg2` |
