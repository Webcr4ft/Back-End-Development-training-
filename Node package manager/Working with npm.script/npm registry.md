# How to Publish a Package to the npm Registry

## The Big Idea

The **npm registry** is a database of public and private packages. Developers and organizations publish packages there to share their tools with their teams, their communities, and often with all Node.js developers.

> **Think of it like publishing an app to an app store.** You build it once, upload it, and anyone can install it with one command.

| Package type | Who can access it |
|--------------|-------------------|
| **Public** | Anyone |
| **Private** | Only specific users or members of an organization |

---

## The Steps at a Glance

1. Create an account
2. Log in from your terminal
3. Create a `package.json` file
4. Create a `README.md`
5. Set up `.npmignore`
6. Publish your package
7. (Optional) Install your package

---

## Step 1: Create an Account

1. Go to [npmjs.com/signup](https://www.npmjs.com/signup).
2. Fill in the form: **username**, **email**, and **password**.

> ⚠️ **Heads up:** Your email address is added to the metadata of packages you publish, so it may be seen publicly.

---

## Step 2: Log In

In your terminal, run:

```bash
npm login
```

Then authenticate with your account information.

---

## Step 3: Create a package.json File

If your project already has a `package.json`, skip to Step 4. Otherwise, run:

```bash
npm init
```

You'll be asked for these details:

| Field | What to enter |
|-------|---------------|
| `name` | Usually your project or directory name. For a public package, it must be **unique** (unless you use a scope, explained below) |
| `version` | Start with the default, `1.0.0`. Update it as you make changes |
| `main` | The entry point of your project. Default: `index.js` |
| `author` | Your name or preferred handle |
| `license` | For example, `MIT` or `ISC` |
| `description` | A brief summary of your package |

### Check that your package name is available

Go to this URL, replacing the placeholder with your package name:

```text
https://www.npmjs.com/package/<your-package-name>
```

- **No package at that URL?** The name is available. Use it.
- **A package already exists?** The name is taken. If you still want it, use a **scope**.

### Scopes

When you create a user or organization account, you get a **scope** that matches your username or organization name.

A scope helps you avoid name conflicts. You can publish under your scope even if another package has the same name.

A scoped package name looks like this in `package.json`:

```json
"name": "@<scope-name>/<your-package-name>"
```

For example, if your username is `kolade` and your package is `my-tool`:

```json
"name": "@kolade/my-tool"
```

You can edit this directly in the file, or add the scope from the start:

```bash
npm init --scope=@<scope-name>
```

The scope name is your **username** (personal account) or your **organization's name** (organization account).

---

## Step 4: Create a README.md

The README is a Markdown file that explains what your package does and how to use it.

Things you may want to include:

- Its purpose
- How to install it
- Important dependencies and considerations
- How to get started
- Sample code snippets
- Contribution guidelines (if you accept contributions)
- A link to a changelog file that tracks changes in each version

The structure is flexible. Adapt it to fit your needs.

---

## Step 5: Set Up .npmignore

The `.npmignore` file tells npm **which files to leave out** when publishing. This is very important for avoiding the sharing of sensitive information like private keys, passwords, and personal data.

In this file, you write patterns for files, directories, and file types to ignore. It uses the same pattern rules as `.gitignore`.

### How it relates to .gitignore

> According to the npm documentation, if there's no `.npmignore` file but there is a `.gitignore` file, npm ignores whatever `.gitignore` matches.

Also, npm looks for `.npmignore` and `.gitignore` files in **all subdirectories**, not just the root.

### Ignored by default

You don't need to add these to `.npmignore`:

```text
.*.swp
._*
.DS_Store
.git
.gitignore
.hg
.npmignore
.npmrc
.lock-wscript
.svn
.wafpickle-*
config.gypi
CVS
npm-debug.log
```

The `node_modules` directory is also ignored, except for bundled dependencies.

---

## Step 6: Publish Your Package

### Test it first

Before publishing, test your package locally:

```bash
npm install <full-path-to-package-directory>
```

### Then publish

The command depends on whether your package is scoped or unscoped.

| Package type | Command | Result |
|--------------|---------|--------|
| **Unscoped** | `npm publish` | Published publicly |
| **Scoped** | `npm publish` | Published as **private** by default (if available in your account) |
| **Scoped, made public** | `npm publish --access public` | Published publicly |

Example for a scoped public package:

```bash
npm publish --access public
```

### See your package

Visit:

```text
https://npmjs.com/package/<your-package-name>
```

Below the package name, you'll see whether it is **public** or **private**.

---

## Step 7 (Optional): Install Your Package

Test it in any Node.js project:

```bash
npm install <your-package-name>
```

---

## Updating Your Package

To change your package after publishing, update the **version** in `package.json`, then publish again. Follow semantic versioning:

| Release type | What to do | Example |
|--------------|------------|---------|
| **First release** | Start at `1.0.0` | `1.0.0` |
| **Patch** | Increase the third digit | `1.0.0` → `1.0.1` |
| **Minor** | Increase the middle digit, reset the last to zero | `1.0.0` → `1.1.0` |
| **Major** | Increase the first digit, reset the middle and last to zero | `1.1.0` → `2.0.0` |

---

## Publishing Checklist

- [ ] I have an npm account and I'm logged in (`npm login`)
- [ ] My `package.json` has a unique name, version, main, author, license, and description
- [ ] My package name is available (or I'm using a scope)
- [ ] I wrote a `README.md`
- [ ] My `.npmignore` keeps sensitive files out
- [ ] I tested my package with `npm install <path>`
- [ ] I ran `npm publish` (or `npm publish --access public` for a public scoped package)

---

## Quick Reference

| I want to... | Command |
|--------------|---------|
| Log in | `npm login` |
| Create a `package.json` | `npm init` |
| Create one with a scope | `npm init --scope=@scope-name` |
| Test my package locally | `npm install <full-path-to-package-directory>` |
| Publish an unscoped package | `npm publish` |
| Publish a scoped package publicly | `npm publish --access public` |
| Install my published package | `npm install <your-package-name>` |
