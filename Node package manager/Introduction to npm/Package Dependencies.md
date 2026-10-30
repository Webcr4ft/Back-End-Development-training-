# What Are Package Dependencies?

## The Big Idea

A **dependency** is a piece of code your project needs in order to work.

Most dependencies are **external packages**: code that other developers built and shared on the npm registry.

> **Think of dependencies as ingredients.** Instead of growing your own tomatoes, you buy them and focus on cooking.

Using dependencies saves a lot of time. Packages already exist for common jobs like:

- Creating a web server
- Handling routing
- Fetching data
- Managing authentication

## Where Dependencies Are Listed

In `package.json`, every package your project needs is listed under the `dependencies` key:

```json
{
  "name": "package-dependencies",
  "version": "1.0.0",
  "description": "a demo on how package dependencies work",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": ["Node", "NPM"],
  "author": "Kolade Chris",
  "license": "ISC",
  "dependencies": {
    "chalk": "^5.6.2",
    "lodash": "^4.17.21"
  }
}
```

Here, `chalk` and `lodash` are the project's dependencies. If they aren't installed and listed, any feature that uses them will **break**.

## Two Types of Dependencies

| Type | Needed when... | Examples |
|------|----------------|----------|
| `dependencies` | The app is **running** (production) | chalk, lodash |
| `devDependencies` | You are **building or testing** | Nodemon, Jest, Mocha, ESLint |

Common `devDependencies` and what they do:

- **Nodemon**: restarts your project automatically when files change
- **Jest / Mocha**: test your code
- **ESLint**: checks your code for problems (linting)

Here is the same file with `devDependencies` added:

```json
{
  "dependencies": {
    "chalk": "^5.6.2",
    "lodash": "^4.17.21"
  },
  "devDependencies": {
    "jest": "^30.2.0",
    "nodemon": "^3.1.10"
  }
}
```

*(Other fields like `name` and `version` are hidden here to keep it short.)*

## How to Choose a Good Package

Before you install a package, check these five things:

1. **Security**
   - This comes first. Even one unsafe package can cause problems for your whole project.

2. **Performance**
   - A large or poorly optimized package can slow your project down.

3. **Popularity**
   - Popular packages usually have active communities, good docs, and frequent updates.
   - A quick check: look at the **weekly downloads** on npm. For example, `chalk` gets over 300,000 downloads each week.

4. **Maintenance**
   - Well-maintained packages are updated regularly and work better with new versions of other software.

5. **Documentation**
   - Clear docs make a package easier to use and save you time.

### Quick checklist

- [ ] Is it safe?
- [ ] Is it fast enough?
- [ ] Do lots of people use it?
- [ ] Is it updated regularly?
- [ ] Are the docs clear?
