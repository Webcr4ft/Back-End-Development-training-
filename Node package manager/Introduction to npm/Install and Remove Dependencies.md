# How to Install and Remove Dependencies

## The Big Idea

npm lets you add packages to your project with one command, and remove them with another. npm updates your `package.json` for you each time.

## Installing a Dependency

```bash
npm install dependencyName
```

Shortcut: `i` works the same as `install`.

```bash
npm i dependencyName
```

### What happens after you install?

1. npm adds a `dependencies` section to `package.json` (if it isn't there yet) and lists your package.
2. Two new things appear in your project's root folder:

| New item | What it is |
|----------|------------|
| `node_modules/` | A folder holding the actual code of the packages you installed |
| `package-lock.json` | A file recording the exact versions installed, including each package's own dependencies (more in a later lesson) |

Example: after running `npm install chalk`, `package.json` includes:

```json
"dependencies": {
  "chalk": "^5.6.2"
}
```

## Installing Several Packages at Once

List the package names with spaces between them:

```bash
npm install express lodash bcrypt
```

npm updates `package.json`, `package-lock.json`, and `node_modules` for all of them:

```json
"dependencies": {
  "bcrypt": "^6.0.0",
  "chalk": "^5.6.2",
  "express": "^5.1.0",
  "lodash": "^4.17.21"
}
```

## Installing a devDependency

Add the `--save-dev` flag, or the shorter `-D`:

```bash
npm i nodemon -D
```

npm puts it under `devDependencies`:

```json
"devDependencies": {
  "nodemon": "^3.1.10"
}
```

## Reading the Install Message

After each install, npm prints a summary. A successful one looks like this:

```text
added 72 packages, and audited 74 in 8s

17 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
```

| Line | Meaning |
|------|---------|
| `added 72 packages` | How many packages were installed (including the packages' own dependencies) |
| `audited 74` | How many packages npm checked |
| `looking for funding` | Some package authors accept donations (you can ignore this) |
| `found 0 vulnerabilities` | No known security problems |

## Removing a Dependency

```bash
npm uninstall dependencyName
```

Example: remove `chalk`.

```bash
npm uninstall chalk
```

Remove several at once:

```bash
npm uninstall express lodash bcrypt
```

npm prints a message to confirm it worked:

```text
removed 70 packages, and audited 31 in 1s

found 0 vulnerabilities
```

Your `package.json` is updated automatically. After removing everything except `nodemon`:

```json
"devDependencies": {
  "nodemon": "^3.1.10"
}
```

## Removing a devDependency

```bash
npm uninstall nodemon
```

> **No `-D` needed.** npm finds the package and removes it from the right section on its own.

Your `package.json` is now clean again, with no `dependencies` or `devDependencies` sections.

## Quick Reference

| I want to... | Command |
|--------------|---------|
| Install a package | `npm install name` or `npm i name` |
| Install several packages | `npm i express lodash bcrypt` |
| Install a dev-only package | `npm i name -D` |
| Remove a package | `npm uninstall name` |
| Remove several packages | `npm uninstall name1 name2` |
| Remove a dev-only package | `npm uninstall name` (no flag) |
