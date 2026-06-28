# Week 23 — npm & Modules Deep Dive

> **Prerequisites:** Week 22 (Introduction to Node.js), CommonJS basics
> **Goal:** Master npm, manage dependencies professionally, create custom modules, and set up a production-ready Node.js project.

---

## Table of Contents

1. [What is npm?](#1-what-is-npm)
2. [Initializing a Project with `npm init`](#2-initializing-a-project-with-npm-init)
3. [Understanding `package.json`](#3-understanding-packagejson)
4. [Installing Packages](#4-installing-packages)
5. [node_modules and .gitignore](#5-node_modules-and-gitignore)
6. [package-lock.json](#6-package-lockjson)
7. [Semantic Versioning](#7-semantic-versioning)
8. [npm Scripts](#8-npm-scripts)
9. [Creating Custom Modules](#9-creating-custom-modules)
10. [Environment Variables and dotenv](#10-environment-variables-and-dotenv)
11. [Nodemon — Auto-Restart on Changes](#11-nodemon--auto-restart-on-changes)
12. [Summary](#12-summary)

---

## 1. What is npm?

**npm** stands for **Node Package Manager**. It is the world's largest software registry, with over 2 million packages available for free.

> Think of npm as an **app store for developers**. Just like you download apps from Google Play or the App Store instead of building everything from scratch, npm lets you download ready-made code packages that solve common problems — sending emails, hashing passwords, connecting to databases, and more.

### npm Has Three Parts

```
  +-----------------------------------------------------------+
  |                         npm                                |
  +-----------------------------------------------------------+
  |                                                           |
  |  1. WEBSITE (npmjs.com)                                   |
  |     - Browse and search for packages                      |
  |     - Read documentation                                  |
  |     - View download stats                                 |
  |                                                           |
  |  2. CLI (Command Line Interface)                          |
  |     - Install, update, remove packages                    |
  |     - Run scripts                                         |
  |     - Publish your own packages                           |
  |                                                           |
  |  3. REGISTRY (Database)                                   |
  |     - Stores all the packages                             |
  |     - Serves downloads                                    |
  |     - Over 2 million packages                             |
  |                                                           |
  +-----------------------------------------------------------+
```

### Why Use npm?

| Reason                  | Explanation                                                    |
|-------------------------|----------------------------------------------------------------|
| **Do not reinvent the wheel** | Someone already solved that problem. Use their package.    |
| **Save time**           | A validated email package saves days of writing regex.         |
| **Community tested**    | Popular packages are used by millions and battle-tested.       |
| **Easy updates**        | One command updates a package to the latest version.           |
| **Dependency management**| npm tracks what your project needs and installs it all.       |

---

## 2. Initializing a Project with `npm init`

Every Node.js project should start with a `package.json` file. This file is the "identity card" of your project.

### Creating a `package.json`

```bash
# Create a new directory and navigate into it
mkdir my-node-project
cd my-node-project

# Interactive mode (asks questions one by one)
npm init

# Quick mode (accepts all defaults)
npm init -y
```

When you run `npm init -y`, npm creates a `package.json` with default values:

```json
{
  "name": "my-node-project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

---

## 3. Understanding `package.json`

The `package.json` file is the most important file in any Node.js project. It stores metadata about your project and lists all the packages it depends on.

### Field-by-Field Breakdown

```json
{
  "name": "online-store-api",
  "version": "1.0.0",
  "description": "REST API for an online store",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js",
    "test": "jest"
  },
  "keywords": ["api", "store", "nodejs"],
  "author": "Fahad Ahmed",
  "license": "MIT",
  "dependencies": {
    "express": "^4.18.2",
    "mongoose": "^7.6.3"
  },
  "devDependencies": {
    "nodemon": "^3.0.1",
    "jest": "^29.7.0"
  }
}
```

| Field               | Purpose                                                          |
|---------------------|------------------------------------------------------------------|
| `name`              | The name of your project (lowercase, no spaces).                 |
| `version`           | Current version following semantic versioning (e.g., 1.0.0).     |
| `description`       | A short description of what the project does.                    |
| `main`              | The entry point file (what runs when someone imports your package). |
| `scripts`           | Custom commands you can run with `npm run <script-name>`.        |
| `keywords`          | Tags that help people find your package on npmjs.com.            |
| `author`            | Who created the project.                                         |
| `license`           | The legal license (MIT, ISC, Apache-2.0, etc.).                  |
| `dependencies`      | Packages your project needs **in production**.                   |
| `devDependencies`   | Packages needed only **during development**.                     |

### dependencies vs devDependencies

```
  +---------------------------+    +---------------------------+
  |     dependencies          |    |    devDependencies        |
  +---------------------------+    +---------------------------+
  |                           |    |                           |
  |  Needed to RUN the app    |    |  Needed to DEVELOP the    |
  |                           |    |  app (not in production)  |
  |  Examples:                |    |                           |
  |  - express (web server)   |    |  Examples:                |
  |  - mongoose (database)    |    |  - nodemon (auto-restart) |
  |  - bcrypt (passwords)     |    |  - jest (testing)         |
  |  - jsonwebtoken (auth)    |    |  - eslint (code quality)  |
  |                           |    |                           |
  |  Installed with:          |    |  Installed with:          |
  |  npm install <pkg>        |    |  npm install -D <pkg>     |
  +---------------------------+    +---------------------------+
```

---

## 4. Installing Packages

### Installation Types

```bash
# Production dependency (saved to "dependencies")
npm install express
npm i express              # shorthand

# Development dependency (saved to "devDependencies")
npm install --save-dev nodemon
npm i -D nodemon           # shorthand

# Global installation (available system-wide, not project-specific)
npm install -g nodemon

# Install a specific version
npm install express@4.18.2

# Install all dependencies listed in package.json
npm install
npm i                      # shorthand
```

### Comparison Table

| Command                        | Where It Installs        | Saved In              | Use Case                     |
|--------------------------------|--------------------------|-----------------------|------------------------------|
| `npm install express`          | `./node_modules`         | `dependencies`        | Packages your app needs      |
| `npm install -D nodemon`       | `./node_modules`         | `devDependencies`     | Development tools            |
| `npm install -g nodemon`       | Global system directory  | Not saved in project  | CLI tools used across projects|

### Uninstalling Packages

```bash
# Remove a package
npm uninstall express
npm un express             # shorthand

# Remove a dev dependency
npm uninstall -D nodemon

# Remove a global package
npm uninstall -g nodemon
```

### Useful npm Commands

```bash
# List installed packages
npm list                   # project dependencies
npm list -g --depth=0      # globally installed packages

# Check for outdated packages
npm outdated

# Update packages to latest compatible version
npm update

# View info about a package
npm info express
```

---

## 5. node_modules and .gitignore

### What is `node_modules`?

When you run `npm install`, npm downloads all packages and their sub-dependencies into a folder called `node_modules`. This folder can grow very large.

```
  my-project/
  +-- package.json
  +-- package-lock.json
  +-- index.js
  +-- node_modules/           <-- Can be 100MB+ with thousands of files
      +-- express/
      +-- mongoose/
      +-- body-parser/
      +-- ... (hundreds more)
```

### Why You MUST `.gitignore` node_modules

```
  node_modules Problems:
  +-----------------------------------------+
  |  - Can contain 50,000+ files            |
  |  - Can be 200MB+ in size               |
  |  - Slows down git operations            |
  |  - Different on each operating system   |
  |  - Can be regenerated with npm install  |
  +-----------------------------------------+

  Solution: Add "node_modules" to .gitignore
```

### Creating a `.gitignore` File

Create a file called `.gitignore` in your project root:

```
# Dependencies
node_modules/

# Environment variables
.env

# OS files
.DS_Store
Thumbs.db

# IDE settings
.vscode/
.idea/

# Logs
*.log
npm-debug.log*
```

### The Rule

> **Never commit `node_modules` to Git.** Anyone who clones your project simply runs `npm install`, and npm reads `package.json` to download all the exact packages your project needs.

```
  Developer A                          Developer B
  +-----------------+                  +-----------------+
  |  Writes code    |                  |  Clones repo    |
  |  npm install    |                  |  npm install    |
  |  Commits code   | --- git push --> |  Gets same      |
  |  (.gitignore    |                  |  node_modules   |
  |   excludes      |                  |  automatically  |
  |   node_modules) |                  |                 |
  +-----------------+                  +-----------------+
```

---

## 6. package-lock.json

### What is It?

`package-lock.json` is an **auto-generated** file that records the **exact version** of every installed package (and their sub-dependencies). It ensures that every developer and every deployment gets identical dependency versions.

### Why It Matters

```
  WITHOUT package-lock.json:

  Developer A runs "npm install"   -->  Gets express 4.18.2
  Developer B runs "npm install"   -->  Gets express 4.18.3 (newer)
  Production server runs "npm install" --> Gets express 4.19.0

  Result: "It works on my machine!" bugs

  -------------------------------------------------------

  WITH package-lock.json:

  Developer A runs "npm install"   -->  Gets express 4.18.2
  Developer B runs "npm install"   -->  Gets express 4.18.2 (same!)
  Production server runs "npm install" --> Gets express 4.18.2 (same!)

  Result: Consistent behavior everywhere
```

### Rules for `package-lock.json`

| Rule                                  | Reason                                         |
|---------------------------------------|------------------------------------------------|
| **DO** commit it to Git               | Ensures consistent installations across teams. |
| **DO NOT** edit it manually           | It is auto-generated by npm.                   |
| **DO NOT** add it to `.gitignore`     | It must be shared with all developers.         |

---

## 7. Semantic Versioning

Every npm package follows **Semantic Versioning** (SemVer), a versioning standard that communicates what changed.

### Version Format: MAJOR.MINOR.PATCH

```
         4  .  18  .  2
         |      |     |
         |      |     +-- PATCH: Bug fixes (safe to update)
         |      +-------- MINOR: New features, backward compatible
         +--------------- MAJOR: Breaking changes (may break your code)
```

### Version Ranges in `package.json`

```json
{
  "dependencies": {
    "express": "4.18.2",     // Exact version only
    "mongoose": "^7.6.3",   // Caret: allows MINOR + PATCH updates
    "lodash": "~4.17.21"    // Tilde: allows PATCH updates only
  }
}
```

| Symbol   | Meaning                     | Example: `^1.2.3`       | Example: `~1.2.3`       |
|----------|-----------------------------|--------------------------|--------------------------|
| None     | Exact version only          | `1.2.3` only             | `1.2.3` only             |
| `^`      | Compatible with version     | `>=1.2.3` and `<2.0.0`  | -                         |
| `~`      | Approximately equivalent    | -                         | `>=1.2.3` and `<1.3.0`  |
| `*`      | Any version                 | Latest available          | Latest available          |

### Visual Comparison

```
  Given version 1.2.3:

  Exact (1.2.3):    [1.2.3]
                     Only this version

  Tilde (~1.2.3):   [1.2.3] [1.2.4] [1.2.5] ... [1.2.99]
                     Patch updates only (safe bug fixes)

  Caret (^1.2.3):   [1.2.3] [1.2.4] ... [1.3.0] [1.4.0] ... [1.99.0]
                     Minor + Patch updates (new features, bug fixes)

  Star (*):          [1.0.0] [2.0.0] [3.0.0] ... [latest]
                     Any version (DANGEROUS - may include breaking changes)
```

> **Best Practice:** Use `^` (caret) for most packages. It is the default when you run `npm install <package>`. It allows minor and patch updates (safe) but blocks major updates (potentially breaking).

---

## 8. npm Scripts

npm scripts are custom commands defined in your `package.json` that automate common tasks.

### Defining Scripts

```json
{
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js",
    "test": "jest",
    "build": "webpack --mode production",
    "lint": "eslint .",
    "seed": "node seeds/seed.js",
    "clean": "rm -rf dist"
  }
}
```

### Running Scripts

```bash
# Special scripts (do not need "run" keyword)
npm start          # runs "start" script
npm test           # runs "test" script

# Custom scripts (need "run" keyword)
npm run dev        # runs "dev" script
npm run build      # runs "build" script
npm run lint       # runs "lint" script
npm run seed       # runs "seed" script
```

### Why Use npm Scripts?

| Benefit                    | Explanation                                                |
|----------------------------|------------------------------------------------------------|
| **Standardized commands**  | Every developer runs the same command to start the app.    |
| **Documentation**          | Looking at `scripts` tells you how to run the project.     |
| **No global installs**     | Scripts can use locally installed packages.                |
| **Chaining**               | You can run multiple commands in sequence.                 |

### Pre and Post Hooks

npm automatically runs scripts prefixed with `pre` and `post`:

```json
{
  "scripts": {
    "prestart": "echo 'About to start the server...'",
    "start": "node index.js",
    "poststart": "echo 'Server has started!'"
  }
}
```

When you run `npm start`, npm automatically runs: `prestart` then `start` then `poststart`.

---

## 9. Creating Custom Modules

As your project grows, you should organize your code into separate files (modules). Each module handles one responsibility.

### Example: Building a Utility Library

**Project structure:**

```
  my-project/
  +-- index.js            (main entry point)
  +-- utils/
  |   +-- math.js         (math utilities)
  |   +-- string.js       (string utilities)
  |   +-- validate.js     (validation helpers)
  +-- package.json
```

**`utils/math.js`** — Math utility module:

```javascript
// utils/math.js

const add = (a, b) => a + b;
const subtract = (a, b) => a - b;
const multiply = (a, b) => a * b;
const divide = (a, b) => {
  if (b === 0) throw new Error("Cannot divide by zero");
  return a / b;
};

const calculateAverage = (numbers) => {
  if (numbers.length === 0) return 0;
  const sum = numbers.reduce((acc, num) => acc + num, 0);
  return sum / numbers.length;
};

module.exports = { add, subtract, multiply, divide, calculateAverage };
```

**`utils/string.js`** — String utility module:

```javascript
// utils/string.js

const capitalize = (str) => str.charAt(0).toUpperCase() + str.slice(1);

const slugify = (str) =>
  str.toLowerCase().trim().replace(/\s+/g, "-").replace(/[^\w-]/g, "");

const truncate = (str, maxLength) =>
  str.length > maxLength ? str.slice(0, maxLength) + "..." : str;

module.exports = { capitalize, slugify, truncate };
```

**`utils/validate.js`** — Validation module:

```javascript
// utils/validate.js

const isEmail = (email) => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);

const isStrongPassword = (password) =>
  password.length >= 8 &&
  /[A-Z]/.test(password) &&
  /[a-z]/.test(password) &&
  /[0-9]/.test(password);

const isNotEmpty = (value) =>
  value !== null && value !== undefined && value.toString().trim() !== "";

module.exports = { isEmail, isStrongPassword, isNotEmpty };
```

**`index.js`** — Main file using all modules:

```javascript
// index.js
const { add, calculateAverage } = require("./utils/math");
const { capitalize, slugify } = require("./utils/string");
const { isEmail, isStrongPassword } = require("./utils/validate");

// Math utilities
console.log("5 + 3 =", add(5, 3));
console.log("Average:", calculateAverage([85, 92, 78, 95, 88]));

// String utilities
console.log(capitalize("hello world"));                 // Hello world
console.log(slugify("My Blog Post Title!"));            // my-blog-post-title

// Validation
console.log(isEmail("student@example.com"));            // true
console.log(isEmail("not-an-email"));                   // false
console.log(isStrongPassword("Abc12345"));              // true
console.log(isStrongPassword("weak"));                  // false
```

---

## 10. Environment Variables and dotenv

### What are Environment Variables?

Environment variables are values that exist **outside your code** — in your operating system's environment. They are used to store sensitive information that should never be hardcoded in your source files.

> Think of environment variables as a **secret notebook** that only you and the server can read. You would never write your bank PIN on a public whiteboard. Similarly, you should never write database passwords or API keys directly in your code.

### Common Use Cases

| Variable              | Purpose                                              |
|-----------------------|------------------------------------------------------|
| `PORT`                | Which port the server runs on (3000, 8080, etc.)     |
| `DATABASE_URL`        | Connection string for the database                   |
| `JWT_SECRET`          | Secret key for signing authentication tokens         |
| `API_KEY`             | Third-party API credentials                          |
| `NODE_ENV`            | Environment mode (`development`, `production`, `test`)|

### Using the `dotenv` Package

**Step 1:** Install dotenv:

```bash
npm install dotenv
```

**Step 2:** Create a `.env` file in your project root:

```
# .env
PORT=3000
DATABASE_URL=mongodb://localhost:27017/myapp
JWT_SECRET=my-super-secret-key-123
API_KEY=sk-abc123def456
NODE_ENV=development
```

**Step 3:** Load the variables in your code:

```javascript
// index.js
require("dotenv").config();

// Now all variables from .env are available in process.env
const port = process.env.PORT || 3000;
const dbUrl = process.env.DATABASE_URL;
const jwtSecret = process.env.JWT_SECRET;
const environment = process.env.NODE_ENV;

console.log(`Server will run on port: ${port}`);
console.log(`Environment: ${environment}`);
console.log(`Database: ${dbUrl}`);

// NEVER log secrets in production!
if (environment === "development") {
  console.log(`JWT Secret: ${jwtSecret}`);
}
```

### Security Rules

```
  +------------------------------------------+
  |        .env Security Checklist           |
  +------------------------------------------+
  |                                          |
  |  [x] Add .env to .gitignore             |
  |  [x] Never commit .env to Git           |
  |  [x] Create .env.example with           |
  |      placeholder values for teammates   |
  |  [x] Never log secrets in production    |
  |  [x] Use different .env files for       |
  |      development and production         |
  |                                          |
  +------------------------------------------+
```

**`.env.example`** — Share this with your team (safe because it has no real values):

```
# .env.example — Copy this to .env and fill in real values
PORT=3000
DATABASE_URL=mongodb://localhost:27017/your-database
JWT_SECRET=your-secret-key-here
API_KEY=your-api-key-here
NODE_ENV=development
```

---

## 11. Nodemon — Auto-Restart on Changes

### The Problem

Every time you change your code, you must stop the server (Ctrl+C) and restart it (`node index.js`). This is tedious during development.

### The Solution: Nodemon

**Nodemon** watches your files and automatically restarts the server whenever you save a change.

```bash
# Install as a dev dependency
npm install -D nodemon
```

### Using Nodemon

```bash
# Run directly (if installed globally)
nodemon index.js

# Run via npm script (recommended)
# In package.json:
# "scripts": { "dev": "nodemon index.js" }
npm run dev
```

### How It Works

```
  WITHOUT Nodemon:                    WITH Nodemon:
  +-------------------------+        +-------------------------+
  |  1. Edit code           |        |  1. Edit code           |
  |  2. Save file           |        |  2. Save file           |
  |  3. Switch to terminal  |        |  3. Nodemon detects     |
  |  4. Press Ctrl+C        |        |     the change and      |
  |  5. Type: node index.js |        |     restarts server     |
  |  6. Press Enter          |        |     automatically!     |
  |  7. Switch to browser   |        |  4. Switch to browser   |
  |  8. Refresh page        |        |  5. Refresh page        |
  +-------------------------+        +-------------------------+
       6 manual steps                     2 manual steps
```

### Nodemon Configuration

You can configure Nodemon by adding a `nodemonConfig` section to your `package.json`:

```json
{
  "nodemonConfig": {
    "watch": ["src"],
    "ext": "js,json",
    "ignore": ["node_modules", "logs"],
    "delay": "1000"
  }
}
```

| Option    | Purpose                                          |
|-----------|--------------------------------------------------|
| `watch`   | Directories to watch for changes.                |
| `ext`     | File extensions to watch.                        |
| `ignore`  | Directories/files to ignore.                     |
| `delay`   | Milliseconds to wait before restarting.          |

---

## 12. Summary

| Concept                | Key Takeaway                                                       |
|------------------------|--------------------------------------------------------------------|
| **npm**                | Node Package Manager — installs and manages third-party packages.  |
| **package.json**       | The identity card of your project; lists dependencies and scripts.  |
| **npm init -y**        | Quick way to create a `package.json` with default values.          |
| **dependencies**       | Packages needed to run the app in production.                      |
| **devDependencies**    | Packages needed only during development.                           |
| **node_modules**       | Folder where packages are downloaded. Never commit to Git.         |
| **package-lock.json**  | Locks exact versions for consistent installations. Commit to Git.  |
| **Semantic Versioning**| MAJOR.MINOR.PATCH — `^` allows minor updates, `~` allows patches.  |
| **npm scripts**        | Custom commands in `package.json` to automate tasks.               |
| **Custom modules**     | Organize code into separate files with `module.exports`/`require`. |
| **dotenv**             | Loads environment variables from a `.env` file into `process.env`. |
| **.env security**      | Never commit `.env` to Git. Use `.env.example` for templates.      |
| **Nodemon**            | Automatically restarts server on file changes during development.  |

### What is Coming Next

In **Week 24**, you will learn **Express.js** — a fast and minimal web framework that makes building servers, routes, and APIs dramatically easier than using the raw `http` module.

---

> **Pro Tip:** Run `npm audit` regularly to check your installed packages for known security vulnerabilities. If vulnerabilities are found, run `npm audit fix` to automatically update packages to secure versions.
