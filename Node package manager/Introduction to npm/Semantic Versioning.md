# What Is Semantic Versioning?

## The Big Idea

**Semantic versioning (SemVer)** is a system that gives version numbers a clear meaning. Just by looking at a version number, you can tell what kind of changes were made.

## The Format

```text
MAJOR.MINOR.PATCH
```

Example: the popular library `lodash` is currently version `4.17.21`.

| Part | Number in 4.17.21 | Change it signals | Example |
|------|-------------------|-------------------|---------|
| **MAJOR** | `4` | Big changes that **break** existing code | Removing or renaming a function |
| **MINOR** | `17` | **New features** that don't break anything | Adding a new function or optional parameter |
| **PATCH** | `21` | **Small fixes** | Fixing a bug or typo |

> **Think of it like this:** MAJOR = "be careful, things changed." MINOR = "new stuff, nothing broke." PATCH = "just a fix."

## Example: How a Version Changes Over Time

Here's how a package called `my-package` might grow:

| Version | What changed |
|---------|--------------|
| `1.0.0` | First stable release |
| `1.1.0` | New optional feature |
| `1.1.1` | Small bug fix |
| `2.0.0` | Breaking changes added |

## Version Symbols in package.json

In your `package.json`, a version can have a symbol in front of it:

```json
"lodash": "^4.17.21"
```

These symbols tell npm **which updates it's allowed to install**.

### The Caret (`^`)

Allows new **minor and patch** updates, but **not** new major versions.

- `^4.17.21` accepts `4.18.0` and `4.17.22`
- `^4.17.21` does **not** accept `5.0.0`

Why? Major updates may include breaking changes.

**Special case:** if the major version is `0`, the caret is stricter, because `0.x` versions are considered less stable.

- `^0.2.3` accepts `0.2.4`
- `^0.2.3` does **not** accept `0.3.0`

### The Tilde (`~`)

Allows **patch** updates only.

- `~1.2.3` accepts `1.2.4` and `1.2.9`
- `~1.2.3` does **not** accept `1.3.0`

### Comparison Operators (`>`, `<`, `>=`, `<=`)

Accept any version within a **range**.

- `>=1.2.3 <2.0.0` means any version from `1.2.3` up to, but not including, `2.0.0`

### The Asterisk (`*`)

Accepts **any version**.

> ⚠️ Only use this for testing. It is not recommended for production.

### No Symbol

Locks the **exact version**.

- `1.2.3` accepts only `1.2.3`

## Quick Summary

| Symbol | Meaning | Example | Accepts |
|--------|---------|---------|---------|
| `^` | Minor + patch updates | `^1.2.3` | `1.x.x` |
| `~` | Patch updates only | `~1.2.3` | `1.2.x` |
| `>`, `<`, `>=`, `<=` | Custom range | `>=1.2.3 <2.0.0` | Anything in the range |
| `*` | Any version | `*` | All versions |
| none | Exact version | `1.2.3` | Only `1.2.3` |

## Easy Way to Remember

- **Most flexible:** `*`
- **Flexible, but safe from breaking changes:** `^`
- **Only bug fixes:** `~`
- **No changes at all:** exact version
