# What Is a package.json File?

## The Big Idea

Every npm project needs a place to write down important facts about itself: what it's called, what packages it uses, and what commands it can run.

That place is the **package.json** file.

> **Think of it as your project's ID card and shopping list.** It says who the project is and what it needs to work.

It's a simple JSON file made of key-value pairs.

## What It Keeps Track Of

- The project's name and version
- The author
- The first file to run (the "main" file)
- The license
- The repository, keywords, and description
- The packages (dependencies) the project needs

## What One Looks Like

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "description": "A simple NPM project",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "test": "echo \"Running tests...\""
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/username/project.git"
  },
  "keywords": ["fCC", "js"],
  "author": "Kolade Chris",
  "license": "ISC",
  "dependencies": {
    "react": "^19.2.1"
  },
  "devDependencies": {
    "cypress": "^15.7.1"
  }
}
```

## The Important Fields

| Field | What it does |
|-------|--------------|
| `main` | Tells Node.js which file to run first (usually `index.js`) |
| `scripts` | Shortcuts for commands, like `npm start` |
| `license` | Says how others can use, change, and share your code |
| `dependencies` | Packages your app needs to **run** |
| `devDependencies` | Packages you only need while **building** |

### About licenses

Common licenses are MIT, ISC, and GPL. Each has different rules. The default is **ISC**, which is very permissive (it allows almost anything).

### Dependencies vs. devDependencies

When you install a package, npm puts it in one of two sections.

- **`dependencies`**: needed when your app is live.
  - Example: **React**, because your app can't work without it.
- **`devDependencies`**: only needed while you're developing.
  - Example: **Cypress**, a testing tool you use before deploying.

## How to Create a package.json File

Run these commands in the **root folder** of your project.

### Option 1: Answer questions (recommended)

```bash
npm init
```

npm asks you a series of questions, like name, version, description, and author. Your answers fill in the file. If you skip a question, npm uses a default value. For example, leaving the license blank gives you `ISC`.

### Option 2: Skip the questions

```bash
npm init -y
```

or

```bash
npm init --yes
```

This instantly creates the file with default values.

> **Tip:** Use plain `npm init` so you can customize each field.

## Example: What You See When You Run `npm init`

```text
package name: (test) my-app
version: (1.0.0)
description: a description for my-app
entry point: (index.js)
test command:
git repository:
keywords: fCC, JS
author: Kolade Chris
license: (ISC)

About to write to /Users/user/Desktop/fCC/npm/package-json-file/package.json

Is this OK? (yes)
```

The file it creates:

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "description": "a description for my-app",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": ["fCC", "JS"],
  "author": "Kolade Chris",
  "license": "ISC"
}
```

## Why Are Some Fields Missing?

You may notice two things are missing from the file above.

1. **`dependencies` and `devDependencies`**
   - They only appear after you install your first package.

2. **`repository`**
   - npm asks about it, but doesn't fill it in automatically.
   - Commands like `git remote add origin` or `git push` won't update it either.
   - If you want it, add it **manually**.

## Coming Up

In the next lessons, you'll learn how to **install, update, and remove** dependencies in your `package.json`.
