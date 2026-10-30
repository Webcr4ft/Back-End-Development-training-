# How to Install Specific Versions and Manage Dependencies

## The Big Idea

Keeping your dependencies up to date is important for keeping your project stable. It helps you avoid unexpected bugs, and it gives you more control when new versions of packages are released.

In this lesson, you'll learn how to:

1. Install a specific version of a package
2. Check which versions exist
3. See which packages are out of date
4. Update one package or all of them
5. Install the newest major version

---

## Installing a Specific Version

Use this format:

```bash
npm install package@version-number
```

For example, if your project needs an older version of Express, such as `4.21.2`:

```bash
npm install express@4.21.2
```

> **What if I don't include a version number?**
> npm automatically installs the **latest** version available.

| Command | What you get |
|---------|--------------|
| `npm install express` | The latest version of Express |
| `npm install express@4.21.2` | Exactly version `4.21.2` |

---

## Checking Which Versions Exist

Not sure which versions are available? Use:

```bash
npm view package-name versions
```

For example:

```bash
npm view express versions
```

This prints a list of every version of Express that has been published. You can then pick the one you want and install it with `@version-number`.

---

## Finding Out-of-Date Packages

Before updating anything, it helps to see which packages have newer versions. Run:

```bash
npm outdated
```

You'll see output similar to this:

```text
Package  Current  Wanted  Latest  Location              Depended by
chalk      5.5.0   5.5.0   5.6.2  node_modules/chalk    install-spec-version
cleave     1.0.1   1.0.1   1.0.2  node_modules/cleave   install-spec-version
express   4.21.2  4.21.2   5.2.1  node_modules/express  install-spec-version
```

### How to read the table

| Column | What it means |
|--------|---------------|
| **Package** | The name of the package |
| **Current** | The version you have installed right now |
| **Wanted** | The highest version your `package.json` range allows |
| **Latest** | The newest version published on npm |
| **Location** | Where the package is installed |
| **Depended by** | Which project uses it |

> **Tip:** If **Wanted** and **Latest** are different, the newest version is outside your allowed range. This often means a new **major** version with possible breaking changes.

In the example above, `express` is on `4.21.2`, but the latest is `5.2.1`. That's a new major version, so it needs extra care.

---

## Updating Packages

Once you know what's outdated, you can start updating.

### Update one package

```bash
npm update package-name
```

For example:

```bash
npm update express
```

This updates the package **only within the version range allowed by your `package.json`**.

For example, if you have `"express": "^4.21.2"`, npm can update to `4.22.0`, but it will not jump to `5.0.0`.

### Update all packages

```bash
npm update
```

This updates every dependency, but again, only within the ranges your `package.json` allows.

> **Why doesn't npm update to a new major version?**
> Major versions often contain **breaking changes**. So if your `package.json` doesn't allow a new major version, `npm update` won't install it automatically. (This is the semantic versioning idea from the earlier lesson.)

---

## Installing the Newest Version (Even a New Major One)

If you **do** want the newest release, even if it's a new major version, run:

```bash
npm install package-name@latest
```

For example:

```bash
npm install express@latest
```

This ignores the version range in your `package.json` and installs the most recent release.

> ⚠️ **Be careful.** A new major version can break your code. Check the package's documentation or changelog before upgrading, and test your project afterward.

---

## `npm update` vs. `npm install package@latest`

| | `npm update` | `npm install package@latest` |
|---|---|---|
| **Respects your version range?** | Yes | No |
| **Can install a new major version?** | No (unless your range allows it) | Yes |
| **Safety** | Safer | Riskier |
| **Use it when...** | You want safe, routine updates | You want the newest release on purpose |

---

## Suggested Workflow

1. Run `npm outdated` to see what's behind.
2. Run `npm update` for safe updates within your ranges.
3. For packages with a new major version, read the docs first.
4. If you decide to upgrade, run `npm install package-name@latest`.
5. Test your project to make sure nothing broke.

---

## Quick Reference

| I want to... | Command |
|--------------|---------|
| Install a specific version | `npm install package@version-number` |
| Install the latest version | `npm install package` |
| See all versions of a package | `npm view package-name versions` |
| See which packages are outdated | `npm outdated` |
| Update one package (within range) | `npm update package-name` |
| Update all packages (within range) | `npm update` |
| Install the newest version, ignoring the range | `npm install package-name@latest` |
