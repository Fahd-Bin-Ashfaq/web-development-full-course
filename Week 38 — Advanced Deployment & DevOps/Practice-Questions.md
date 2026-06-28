# Week 38 — Advanced Deployment & DevOps: Practice Questions

**Total Questions: 20** (10 MCQs + 5 Short Answer + 5 Practical Exercises)

---

## Part 1: Multiple Choice Questions (MCQs)

**1. What does "CI" stand for in CI/CD, and what is its primary purpose?**

- A) Continuous Integration -- automatically merging and testing code changes from multiple developers
- B) Code Inspection -- manually reviewing code before deployment
- C) Continuous Installation -- automatically installing dependencies on servers
- D) Code Integration -- copying files from one server to another

<details>
<summary>Answer</summary>

**A) Continuous Integration -- automatically merging and testing code changes from multiple developers**

Continuous Integration (CI) is a development practice where developers frequently merge their code changes into a shared repository, often multiple times a day. Each merge triggers an automated build and test process, ensuring that new changes do not break existing functionality. This catches bugs early and reduces the risk of integration conflicts that grow larger over time.

</details>

---

**2. Where do GitHub Actions workflow files live in a repository?**

- A) In the root directory as `actions.yml`
- B) In the `.github/workflows/` directory as YAML files
- C) In the `config/` directory as JSON files
- D) In the `package.json` under the `"actions"` key

<details>
<summary>Answer</summary>

**B) In the `.github/workflows/` directory as YAML files**

GitHub Actions workflow files must be placed in the `.github/workflows/` directory at the root of your repository. Each workflow is defined in a separate YAML file (e.g., `ci.yml`, `deploy.yml`). GitHub automatically detects and runs these workflows based on the triggers defined in each file. The directory structure looks like this:

```
my-project/
  .github/
    workflows/
      ci.yml
      deploy.yml
  src/
  package.json
```

</details>

---

**3. What is the difference between a Docker image and a Docker container?**

- A) They are the same thing with different names
- B) An image is a running process; a container is the blueprint
- C) An image is a read-only template (blueprint); a container is a running instance of that image
- D) A container is stored on Docker Hub; an image runs on your machine

<details>
<summary>Answer</summary>

**C) An image is a read-only template (blueprint); a container is a running instance of that image**

A Docker image is a lightweight, standalone, and immutable package that contains everything needed to run an application: code, runtime, libraries, and system tools. A container is a running instance created from an image. You can think of an image as a class and a container as an object instantiated from that class. One image can spawn many containers, each running independently.

```
+------------------+       docker run       +------------------+
|   Docker Image   |  ===================>  | Docker Container |
|   (Blueprint)    |                        |   (Running App)  |
|   - Read-only    |                        |   - Read-write   |
|   - Shareable    |                        |   - Isolated     |
+------------------+                        +------------------+
```

</details>

---

**4. What does Google Lighthouse measure when you run an audit on a web page?**

- A) Only the page load speed in seconds
- B) Performance, Accessibility, Best Practices, SEO, and Progressive Web App scores
- C) The number of HTTP requests and total file size only
- D) Server response time and database query speed only

<details>
<summary>Answer</summary>

**B) Performance, Accessibility, Best Practices, SEO, and Progressive Web App scores**

Google Lighthouse is an open-source auditing tool that evaluates web pages across five categories. Performance measures loading speed and responsiveness using metrics like FCP, LCP, TBT, and CLS. Accessibility checks that the page is usable by people with disabilities. Best Practices verifies modern web standards (HTTPS, no console errors, correct image aspect ratios). SEO checks search engine discoverability. PWA evaluates Progressive Web App readiness. Each category receives a score from 0 to 100.

</details>

---

**5. What is the purpose of a meta description tag in HTML?**

- A) It sets the font size of the page
- B) It provides a brief summary of the page content that search engines display in search results
- C) It prevents the page from being cached by browsers
- D) It links the page to an external CSS stylesheet

<details>
<summary>Answer</summary>

**B) It provides a brief summary of the page content that search engines display in search results**

The meta description tag gives search engines a concise summary of a page's content, typically 150-160 characters. This description often appears below the page title in search engine results pages (SERPs), influencing whether users click on the link. While it does not directly affect search rankings, a well-written meta description improves click-through rates (CTR), which indirectly benefits SEO.

```html
<meta name="description" content="Learn how to deploy a MERN stack application to production with CI/CD, Docker, and performance optimization.">
```

</details>

---

**6. What is LCP (Largest Contentful Paint), and why is it important?**

- A) The time it takes for the browser to parse all JavaScript files
- B) The time it takes for the largest visible content element (image, heading, or block) to render on the screen
- C) The total time the browser spends downloading CSS files
- D) The number of pixels painted on the first frame of the page

<details>
<summary>Answer</summary>

**B) The time it takes for the largest visible content element (image, heading, or block) to render on the screen**

Largest Contentful Paint (LCP) measures how long it takes for the main content of a page to become visible to the user. It typically tracks the largest image, video, or text block in the viewport. Google considers LCP one of the three Core Web Vitals, and a good score is 2.5 seconds or less. A poor LCP (over 4 seconds) signals to both users and search engines that the page is slow to load, which hurts rankings and user experience.

```
LCP Thresholds:
+--------+------------+--------+
|  Good  |  Needs     |  Poor  |
| <=2.5s | Improvement| >4.0s  |
+--------+------------+--------+
```

</details>

---

**7. What does the `helmet` middleware do in an Express.js application?**

- A) It compresses HTTP responses to reduce file size
- B) It sets various HTTP security headers to protect the app from common web vulnerabilities
- C) It encrypts the database connection string
- D) It serves static files from the public directory

<details>
<summary>Answer</summary>

**B) It sets various HTTP security headers to protect the app from common web vulnerabilities**

Helmet is a collection of middleware functions that set HTTP response headers to help secure Express applications. It protects against well-known vulnerabilities by setting headers like `Content-Security-Policy` (prevents XSS and injection attacks), `X-Frame-Options` (prevents clickjacking), `Strict-Transport-Security` (enforces HTTPS), `X-Content-Type-Options` (prevents MIME sniffing), and several others. Using `app.use(helmet())` applies sensible defaults for all these headers at once.

```javascript
const helmet = require('helmet');
app.use(helmet()); // Sets 11+ security headers automatically
```

</details>

---

**8. What does `React.lazy()` do in a React application?**

- A) It delays the rendering of all components until the page is fully loaded
- B) It dynamically imports a component so it is only loaded when it is actually rendered
- C) It reduces the re-render count of a component
- D) It caches the component's props to prevent unnecessary updates

<details>
<summary>Answer</summary>

**B) It dynamically imports a component so it is only loaded when it is actually rendered**

`React.lazy()` enables code splitting at the component level. Instead of bundling the entire application into one large JavaScript file, `React.lazy()` tells the bundler (Webpack or Vite) to split the specified component into a separate chunk. That chunk is only downloaded from the server when the component is about to be rendered. This reduces the initial bundle size and speeds up the first page load. It must be used with `<Suspense>` to show a fallback while the component loads.

```javascript
import { lazy, Suspense } from 'react';

const Dashboard = lazy(() => import('./Dashboard'));

function App() {
  return (
    <Suspense fallback={<p>Loading...</p>}>
      <Dashboard />
    </Suspense>
  );
}
```

</details>

---

**9. What is the primary benefit of using dynamic `import()` for code splitting?**

- A) It makes the code run faster at runtime by compiling it ahead of time
- B) It reduces the initial bundle size by loading modules on demand only when they are needed
- C) It automatically minifies the imported module
- D) It allows importing CSS files directly into JavaScript

<details>
<summary>Answer</summary>

**B) It reduces the initial bundle size by loading modules on demand only when they are needed**

Dynamic `import()` returns a Promise that resolves to the module, allowing you to load JavaScript modules asynchronously at runtime rather than including them in the initial bundle. This is particularly useful for large libraries or features that are not needed immediately (e.g., a charting library that is only used on an analytics page). The bundler creates separate chunks for dynamically imported modules, which are fetched over the network only when the `import()` call executes.

```javascript
// Without code splitting -- heavy-chart-lib is in the main bundle
import { renderChart } from 'heavy-chart-lib';

// With code splitting -- heavy-chart-lib is loaded only when needed
button.addEventListener('click', async () => {
  const { renderChart } = await import('heavy-chart-lib');
  renderChart(data);
});
```

</details>

---

**10. What does the `CMD` instruction do in a Dockerfile?**

- A) It installs system packages inside the container
- B) It specifies the default command that runs when a container is started from the image
- C) It copies files from the host machine into the container
- D) It sets environment variables for the build process

<details>
<summary>Answer</summary>

**B) It specifies the default command that runs when a container is started from the image**

The `CMD` instruction in a Dockerfile defines the default command and arguments that execute when a container starts. Unlike `RUN`, which executes during the image build phase, `CMD` runs at container startup. There should only be one `CMD` instruction per Dockerfile; if multiple are specified, only the last one takes effect. The command can be overridden at runtime by passing a different command to `docker run`.

```dockerfile
# CMD with exec form (preferred)
CMD ["node", "server.js"]

# This means: when you run `docker run my-app`,
# it automatically executes `node server.js`
```

</details>

---

## Part 2: Short Answer Questions

**11. Explain the benefits of CI/CD for a development team. Give at least four advantages and a real-world scenario.**

<details>
<summary>Answer</summary>

CI/CD (Continuous Integration / Continuous Deployment) provides numerous advantages for development teams:

**1. Early Bug Detection**
Automated tests run on every commit, catching bugs within minutes rather than days or weeks. Developers receive immediate feedback and can fix issues while the code is still fresh in their minds.

**2. Faster Release Cycles**
By automating the build, test, and deployment pipeline, teams can release new features and fixes multiple times per day instead of once a month. This accelerates the feedback loop with users.

**3. Consistent and Reliable Deployments**
Automated pipelines eliminate human error in the deployment process. Every deployment follows the exact same steps, reducing the risk of configuration mistakes, missed steps, or "works on my machine" issues.

**4. Improved Team Collaboration**
When every developer's code is integrated and tested continuously, merge conflicts are smaller and easier to resolve. The shared pipeline serves as a single source of truth for the project's health.

**5. Reduced Manual Work**
Developers no longer need to manually run tests, build artifacts, or deploy to servers. This frees up time for writing features and improving code quality.

**6. Audit Trail and Rollback**
Every build and deployment is logged, providing a complete history. If a deployment causes issues, the team can quickly identify which commit introduced the problem and roll back.

**Real-World Scenario:**

A five-person team is building a MERN stack job board. Without CI/CD, a developer pushes code on Friday, it breaks the main branch, and nobody notices until Monday. With CI/CD:

```
Developer pushes code
        |
        v
GitHub Actions triggers automatically
        |
        v
+-------------------+
| 1. Install deps   |
| 2. Run linter     | -- Catches a missing import
| 3. Run tests      | -- Catches a broken API route
| 4. Build project  | -- Verifies production build works
+-------------------+
        |
        v
Pipeline FAILS -- developer is notified in 3 minutes
        |
        v
Developer fixes the issues before merging
```

The broken code never reaches the main branch, and the rest of the team is unaffected.

</details>

---

**12. Describe the structure of a GitHub Actions workflow file. Explain each key section (name, on, jobs, steps) with a brief example.**

<details>
<summary>Answer</summary>

A GitHub Actions workflow file is written in YAML and placed in `.github/workflows/`. It has four main sections:

**1. `name` -- Workflow Name**
A human-readable name displayed in the GitHub Actions tab. It helps identify the workflow when you have multiple workflows.

**2. `on` -- Trigger Events**
Defines when the workflow should run. Common triggers include `push`, `pull_request`, and `schedule` (cron). You can also specify branches and paths to filter triggers.

**3. `jobs` -- Job Definitions**
A workflow contains one or more jobs that run in parallel by default. Each job runs on a specified virtual machine (runner) and contains a sequence of steps. Jobs can be made sequential using the `needs` keyword.

**4. `steps` -- Individual Tasks**
Each job contains an ordered list of steps. A step can either run a shell command (`run`) or use a pre-built action (`uses`). Steps execute sequentially within a job.

Here is a complete example with annotations:

```yaml
# 1. WORKFLOW NAME
name: CI Pipeline

# 2. TRIGGER EVENTS
on:
  push:
    branches: [main]        # Run on pushes to main
  pull_request:
    branches: [main]        # Run on PRs targeting main

# 3. JOB DEFINITIONS
jobs:
  test:                      # Job ID (can be any name)
    runs-on: ubuntu-latest   # Virtual machine to use

    # 4. STEPS
    steps:
      - name: Checkout code              # Step 1: Get the code
        uses: actions/checkout@v4

      - name: Setup Node.js              # Step 2: Install Node
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Install dependencies       # Step 3: npm install
        run: npm ci

      - name: Run tests                  # Step 4: Execute tests
        run: npm test
```

**Workflow Structure Diagram:**

```
Workflow (ci.yml)
  |
  +-- name: "CI Pipeline"
  |
  +-- on: push, pull_request
  |
  +-- jobs:
       |
       +-- test:
       |    +-- runs-on: ubuntu-latest
       |    +-- steps:
       |         +-- Checkout code
       |         +-- Setup Node.js
       |         +-- Install dependencies
       |         +-- Run tests
       |
       +-- deploy: (optional second job)
            +-- needs: test
            +-- runs-on: ubuntu-latest
            +-- steps: ...
```

</details>

---

**13. Compare Docker containers to traditional virtual machines. Use a comparison table covering: startup time, resource usage, isolation level, image size, and use case.**

<details>
<summary>Answer</summary>

Docker containers and virtual machines (VMs) both provide isolation for running applications, but they work at fundamentally different levels. Containers share the host operating system's kernel, while VMs include a full guest operating system.

**Comparison Table:**

| Feature | Docker Containers | Virtual Machines |
|---|---|---|
| **Startup Time** | Seconds (typically 1-5s) | Minutes (typically 1-5 min) |
| **Resource Usage** | Lightweight -- shares host OS kernel, uses only MBs of RAM | Heavy -- runs full OS, uses GBs of RAM |
| **Isolation Level** | Process-level isolation (shared kernel) | Full hardware-level isolation (separate OS) |
| **Image Size** | Small (50MB - 500MB typically) | Large (1GB - 20GB+ with full OS) |
| **Use Case** | Microservices, CI/CD, app packaging | Running different OS types, legacy apps, strict security |
| **Portability** | Highly portable across any Docker host | Portable but heavier to move |
| **Density** | Can run hundreds on one host | Typically tens on one host |

**Architecture Diagram:**

```
Virtual Machines:                    Docker Containers:

+-------+ +-------+ +-------+       +-------+ +-------+ +-------+
| App A | | App B | | App C |       | App A | | App B | | App C |
+-------+ +-------+ +-------+       +-------+ +-------+ +-------+
| Bins/ | | Bins/ | | Bins/ |       | Bins/ | | Bins/ | | Bins/ |
| Libs  | | Libs  | | Libs  |       | Libs  | | Libs  | | Libs  |
+-------+ +-------+ +-------+       +-------+-+-------+-+-------+
|Guest  | |Guest  | |Guest  |       |      Docker Engine         |
|  OS   | |  OS   | |  OS   |       +----------------------------+
+-------+-+-------+-+-------+       |        Host OS             |
|       Hypervisor          |       +----------------------------+
+---------------------------+       |       Hardware             |
|        Host OS            |       +----------------------------+
+---------------------------+
|       Hardware            |
+---------------------------+
```

**Key Takeaway:** For a MERN stack application, Docker containers are the preferred choice because they are lightweight, start quickly, and make it easy to package your Node.js app with its exact dependencies. VMs are better suited for scenarios requiring complete OS-level isolation or running multiple different operating systems on the same hardware.

</details>

---

**14. Explain the four core Lighthouse metrics (FCP, LCP, TBT, CLS) and give one practical fix for each to improve the score.**

<details>
<summary>Answer</summary>

The four core Lighthouse performance metrics measure different aspects of the user experience:

**1. FCP -- First Contentful Paint**
Measures the time from navigation to when the browser renders the first piece of DOM content (text, image, canvas, or SVG). It answers: "How quickly does the user see something?"

- **Good:** <= 1.8 seconds
- **Fix:** Eliminate render-blocking resources by deferring non-critical CSS and JavaScript.

```html
<!-- Before: Render-blocking CSS -->
<link rel="stylesheet" href="/styles/animations.css">

<!-- After: Non-critical CSS loaded asynchronously -->
<link rel="preload" href="/styles/animations.css" as="style"
      onload="this.onload=null;this.rel='stylesheet'">
```

**2. LCP -- Largest Contentful Paint**
Measures the time it takes for the largest visible content element (hero image, heading, or video) to fully render. It answers: "When does the main content appear?"

- **Good:** <= 2.5 seconds
- **Fix:** Optimize and preload the largest image on the page.

```html
<!-- Before: Large unoptimized image -->
<img src="/hero-banner.png" alt="Hero">

<!-- After: Optimized with modern format, preloaded, and sized -->
<link rel="preload" as="image" href="/hero-banner.webp">
<img src="/hero-banner.webp" alt="Hero"
     width="1200" height="600"
     fetchpriority="high">
```

**3. TBT -- Total Blocking Time**
Measures the total time between FCP and TTI (Time to Interactive) during which the main thread is blocked by long tasks (tasks taking more than 50ms). It answers: "Can the user interact with the page?"

- **Good:** <= 200 milliseconds
- **Fix:** Break up long JavaScript tasks and defer non-essential scripts.

```javascript
// Before: One long blocking task
function processAllItems(items) {
  items.forEach(item => heavyComputation(item)); // Blocks for 500ms
}

// After: Break into smaller chunks using requestIdleCallback
function processItemsInChunks(items) {
  const chunk = items.splice(0, 10);
  chunk.forEach(item => heavyComputation(item));

  if (items.length > 0) {
    requestIdleCallback(() => processItemsInChunks(items));
  }
}
```

**4. CLS -- Cumulative Layout Shift**
Measures the total of all unexpected layout shifts that occur during the page's entire lifespan. It answers: "Does the content jump around while loading?"

- **Good:** <= 0.1
- **Fix:** Always set explicit width and height on images and embedded content.

```html
<!-- Before: No dimensions -- causes layout shift when image loads -->
<img src="/profile.jpg" alt="Profile">

<!-- After: Explicit dimensions prevent layout shift -->
<img src="/profile.jpg" alt="Profile" width="200" height="200">
```

**Metrics Summary:**

```
+----------+----------------------------+----------+
| Metric   | Measures                   | Good     |
+----------+----------------------------+----------+
| FCP      | First content visible      | <= 1.8s  |
| LCP      | Main content visible       | <= 2.5s  |
| TBT      | Main thread blocked time   | <= 200ms |
| CLS      | Visual stability (shifts)  | <= 0.1   |
+----------+----------------------------+----------+
```

</details>

---

**15. Create a production security checklist for a MERN stack application. Cover at least 8 security measures across frontend, backend, and database layers.**

<details>
<summary>Answer</summary>

A comprehensive production security checklist for a MERN stack application covers three layers:

**Frontend (React) Security:**

1. **Sanitize user input** -- Never render raw user input with `dangerouslySetInnerHTML`. Use libraries like `DOMPurify` to sanitize any HTML content before rendering.

2. **Use environment variables for API URLs** -- Never hardcode API keys or backend URLs in client-side code. Use `VITE_` prefixed environment variables and never expose secrets to the frontend.

3. **Implement Content Security Policy (CSP)** -- Restrict which sources can load scripts, styles, and images to prevent XSS attacks.

```html
<meta http-equiv="Content-Security-Policy"
      content="default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline';">
```

**Backend (Express/Node.js) Security:**

4. **Use Helmet middleware** -- Sets security headers automatically (X-Frame-Options, Strict-Transport-Security, X-Content-Type-Options, etc.).

```javascript
const helmet = require('helmet');
app.use(helmet());
```

5. **Configure CORS properly** -- Restrict allowed origins to your specific frontend domain instead of allowing all origins.

```javascript
app.use(cors({
  origin: 'https://myapp.vercel.app',
  credentials: true
}));
```

6. **Implement rate limiting** -- Prevent brute-force attacks and API abuse by limiting the number of requests per IP address.

```javascript
const rateLimit = require('express-rate-limit');
app.use(rateLimit({
  windowMs: 15 * 60 * 1000,  // 15 minutes
  max: 100                    // 100 requests per window
}));
```

7. **Validate and sanitize all input** -- Use libraries like `express-validator` or `joi` to validate request bodies, params, and query strings on the server side.

8. **Hash passwords with bcrypt** -- Never store plain-text passwords. Use bcrypt with a salt factor of at least 10.

```javascript
const bcrypt = require('bcrypt');
const hashedPassword = await bcrypt.hash(password, 12);
```

9. **Use HTTP-only cookies for JWTs** -- Store authentication tokens in HTTP-only cookies instead of localStorage to prevent XSS attacks from stealing tokens.

```javascript
res.cookie('token', token, {
  httpOnly: true,
  secure: true,
  sameSite: 'strict',
  maxAge: 24 * 60 * 60 * 1000  // 1 day
});
```

**Database (MongoDB) Security:**

10. **Use MongoDB Atlas with IP whitelisting** -- Restrict database access to only your application server's IP address instead of allowing all IPs (`0.0.0.0/0`) in production.

11. **Create least-privilege database users** -- Use separate database users with only the permissions they need (read-only for reporting, read-write for the app).

12. **Prevent NoSQL injection** -- Sanitize query inputs using `express-mongo-sanitize` to strip `$` and `.` characters from user input.

```javascript
const mongoSanitize = require('express-mongo-sanitize');
app.use(mongoSanitize());
```

**Security Checklist Summary:**

```
+-------------------+----------------------------------+----------+
| Layer             | Security Measure                 | Priority |
+-------------------+----------------------------------+----------+
| Frontend          | Sanitize user input (DOMPurify)  | High     |
| Frontend          | Environment variables for keys   | High     |
| Frontend          | Content Security Policy          | Medium   |
| Backend           | Helmet security headers          | High     |
| Backend           | CORS with specific origins       | High     |
| Backend           | Rate limiting                    | High     |
| Backend           | Input validation                 | High     |
| Backend           | Bcrypt password hashing          | High     |
| Backend           | HTTP-only cookies for JWTs       | High     |
| Database          | IP whitelisting on Atlas         | Medium   |
| Database          | Least-privilege DB users         | Medium   |
| Database          | NoSQL injection prevention       | High     |
+-------------------+----------------------------------+----------+
```

</details>

---

## Part 3: Practical Exercises

**16. Create a complete GitHub Actions workflow file (`.github/workflows/ci.yml`) for a Node.js Express application.**

The workflow should: trigger on push to main and pull requests, set up Node.js 20, install dependencies, run the linter, run tests, and build the project. Include environment variables for a MongoDB test URI.

<details>
<summary>Answer</summary>

Create the file `.github/workflows/ci.yml` with the following content:

```yaml
# Workflow name displayed in the GitHub Actions tab
name: Node.js CI Pipeline

# Trigger events -- when should this workflow run?
on:
  push:
    branches: [main]          # Run on every push to main branch
  pull_request:
    branches: [main]          # Run on every PR targeting main branch

# Job definitions
jobs:
  build-and-test:
    # Use the latest Ubuntu runner provided by GitHub
    runs-on: ubuntu-latest

    # Environment variables available to all steps in this job
    env:
      MONGODB_URI: mongodb://localhost:27017/testdb
      JWT_SECRET: test-secret-for-ci
      NODE_ENV: test

    # Strategy matrix -- test against multiple Node.js versions (optional)
    strategy:
      matrix:
        node-version: [18, 20]

    steps:
      # Step 1: Check out the repository code
      - name: Checkout repository
        uses: actions/checkout@v4

      # Step 2: Set up Node.js with the version from the matrix
      - name: Setup Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}
          cache: 'npm'          # Cache npm dependencies for faster builds

      # Step 3: Install project dependencies
      # Using `npm ci` instead of `npm install` for clean, reproducible installs
      - name: Install dependencies
        run: npm ci

      # Step 4: Run the linter to check code quality
      - name: Run linter
        run: npm run lint

      # Step 5: Run the test suite
      - name: Run tests
        run: npm test
        env:
          MONGODB_URI: mongodb://localhost:27017/testdb

      # Step 6: Build the project to verify it compiles successfully
      - name: Build project
        run: npm run build

      # Step 7: Upload build artifacts (optional but useful)
      - name: Upload build artifacts
        if: matrix.node-version == 20
        uses: actions/upload-artifact@v4
        with:
          name: build-output
          path: dist/
          retention-days: 7
```

**How it works step by step:**

```
Developer pushes to main (or opens a PR)
        |
        v
GitHub detects the push/PR event
        |
        v
Workflow triggers on ubuntu-latest
        |
        v
+-----------------------------------+
| 1. Checkout code from repository  |
| 2. Install Node.js 20             |
| 3. Cache and install npm packages |
| 4. Run linter (npm run lint)      |
| 5. Run tests (npm test)           |
| 6. Build project (npm run build)  |
| 7. Upload build artifacts         |
+-----------------------------------+
        |
   Pass or Fail
        |
   +----+----+
   |         |
  PASS      FAIL
   |         |
 Green      Red badge on PR
 check      + email notification
 mark       to developer
```

**Required `package.json` scripts for this workflow:**

```json
{
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js",
    "lint": "eslint .",
    "test": "jest --coverage",
    "build": "npm run lint && echo 'Build complete'"
  }
}
```

</details>

---

**17. Write a basic Dockerfile for a Node.js Express application and a `.dockerignore` file.**

The Dockerfile should: use `node:20-alpine` as the base image, set the working directory, copy package files first (for layer caching), install production dependencies only, copy the application source, expose port 5000, and run the application.

<details>
<summary>Answer</summary>

**Dockerfile:**

```dockerfile
# Stage 1: Use the official Node.js 20 Alpine image as the base
# Alpine is a minimal Linux distribution (~5MB) that keeps the image small
FROM node:20-alpine

# Set the working directory inside the container
# All subsequent commands will run from this directory
WORKDIR /app

# Copy only package.json and package-lock.json first
# This takes advantage of Docker's layer caching:
# If these files haven't changed, Docker reuses the cached layer
# and skips the npm install step (which is the slowest step)
COPY package.json package-lock.json ./

# Install ONLY production dependencies (no devDependencies)
# --omit=dev excludes packages like nodemon, jest, eslint
# Using npm ci for clean, reproducible installs from the lockfile
RUN npm ci --omit=dev

# Now copy the rest of the application source code
# This step changes frequently, but the npm install layer above is cached
COPY . .

# Document which port the application listens on
# This does not actually publish the port -- it serves as documentation
EXPOSE 5000

# Define the command that runs when the container starts
# Using exec form (JSON array) for proper signal handling
CMD ["node", "server.js"]
```

**`.dockerignore` file:**

```dockerfile
# Dependencies -- these are installed inside the container
node_modules

# Environment files -- secrets should be passed via docker run -e
.env
.env.local
.env.production

# Git files -- not needed in the container
.git
.gitignore

# IDE and editor files
.vscode
.idea
*.swp
*.swo

# Documentation -- not needed at runtime
README.md
LICENSE
docs/

# Test files -- not needed in production
__tests__
*.test.js
*.spec.js
coverage/
jest.config.js

# CI/CD configuration
.github
.gitlab-ci.yml

# Docker files -- prevent recursive copying
Dockerfile
docker-compose.yml
.dockerignore

# Build artifacts and logs
npm-debug.log*
yarn-debug.log*
```

**Why layer caching matters:**

```
Without layer caching:          With layer caching:

COPY . .                        COPY package*.json ./
RUN npm install                 RUN npm ci --omit=dev
                                COPY . .

Every code change =             Code change only =
  reinstall ALL packages          reuse cached npm install
  (2-3 minutes)                   copy new source files
                                  (5-10 seconds)
```

**Building and running the Docker image:**

```dockerfile
# Build the image (run from the project root)
# -t gives the image a name and tag
docker build -t my-express-app:latest .

# Run the container
# -p maps host port 5000 to container port 5000
# -e passes environment variables
# -d runs in detached mode (background)
docker run -d \
  -p 5000:5000 \
  -e MONGODB_URI="mongodb+srv://user:pass@cluster.mongodb.net/mydb" \
  -e JWT_SECRET="my-production-secret" \
  --name my-app \
  my-express-app:latest

# Verify the container is running
docker ps

# View container logs
docker logs my-app

# Stop and remove the container
docker stop my-app && docker rm my-app
```

</details>

---

**18. Describe how to run a Lighthouse audit on a deployed web application and provide specific code fixes for common performance issues.**

Show the steps to run an audit, then provide before/after code for: (a) improving LCP by optimizing images, (b) reducing CLS by setting image dimensions, and (c) improving FCP by deferring non-critical CSS.

<details>
<summary>Answer</summary>

**How to Run a Lighthouse Audit:**

There are three ways to run Lighthouse on a deployed application:

**Method 1: Chrome DevTools (Easiest)**
1. Open your deployed site in Google Chrome
2. Press `F12` to open DevTools
3. Click the **Lighthouse** tab
4. Select categories: Performance, Accessibility, Best Practices, SEO
5. Choose **Mobile** or **Desktop** mode
6. Click **Analyze page load**

**Method 2: Command Line (For CI/CD integration)**
```
# Install Lighthouse globally
npm install -g lighthouse

# Run an audit and generate an HTML report
lighthouse https://myapp.vercel.app --output html --output-path ./report.html

# Run with specific categories
lighthouse https://myapp.vercel.app --only-categories=performance,seo
```

**Method 3: PageSpeed Insights (Online)**
Visit [pagespeed.web.dev](https://pagespeed.web.dev) and enter your URL.

---

**(a) Improving LCP by Optimizing Images**

The hero image is often the largest contentful element. Optimizing it dramatically improves LCP.

**Before -- Unoptimized:**

```html
<!-- Large PNG image, no preloading, no size hints -->
<div class="hero">
  <img src="/images/hero-banner.png" alt="Welcome to our platform">
  <h1>Welcome to Our Platform</h1>
</div>
```

```css
.hero img {
  width: 100%;
}
```

**After -- Optimized:**

```html
<!-- Preload the hero image so the browser fetches it early -->
<link rel="preload" as="image" href="/images/hero-banner.webp"
      imagesrcset="/images/hero-banner-400.webp 400w,
                   /images/hero-banner-800.webp 800w,
                   /images/hero-banner-1200.webp 1200w"
      imagesizes="100vw">

<div class="hero">
  <!-- Use modern WebP format with PNG fallback -->
  <!-- fetchpriority="high" tells the browser this image is critical -->
  <picture>
    <source srcset="/images/hero-banner-400.webp 400w,
                    /images/hero-banner-800.webp 800w,
                    /images/hero-banner-1200.webp 1200w"
            sizes="100vw"
            type="image/webp">
    <img src="/images/hero-banner-800.png"
         alt="Welcome to our platform"
         width="1200"
         height="600"
         fetchpriority="high"
         decoding="async">
  </picture>
  <h1>Welcome to Our Platform</h1>
</div>
```

**Key improvements:**
- WebP format (30-50% smaller than PNG)
- Responsive `srcset` serves appropriate size per screen width
- `fetchpriority="high"` prioritizes the hero image
- `rel="preload"` starts the download before the browser parses the `<img>` tag

---

**(b) Reducing CLS by Setting Image Dimensions**

Layout shifts occur when the browser does not know an element's size before it loads.

**Before -- Causes Layout Shift:**

```html
<!-- No width/height -- browser doesn't know the size until the image loads -->
<div class="blog-card">
  <img src="/images/post-thumbnail.jpg" alt="Blog post">
  <h2>How to Deploy a MERN App</h2>
  <p>Learn the step-by-step process...</p>
</div>
```

```css
.blog-card img {
  width: 100%;
}
```

**After -- No Layout Shift:**

```html
<!-- Explicit width and height tell the browser the aspect ratio -->
<div class="blog-card">
  <img src="/images/post-thumbnail.jpg"
       alt="Blog post"
       width="800"
       height="450"
       loading="lazy">
  <h2>How to Deploy a MERN App</h2>
  <p>Learn the step-by-step process...</p>
</div>
```

```css
.blog-card img {
  width: 100%;
  height: auto;          /* Maintains aspect ratio from width/height attributes */
  aspect-ratio: 16 / 9;  /* Modern CSS fallback for aspect ratio */
}

/* Reserve space for ads or dynamic content */
.ad-container {
  min-height: 250px;     /* Prevents shift when ad loads */
}
```

**Key improvements:**
- `width` and `height` attributes allow the browser to calculate the aspect ratio before the image loads
- `aspect-ratio` CSS property provides additional protection
- `loading="lazy"` defers off-screen images (also helps performance)
- Fixed height on dynamic containers prevents content from jumping

---

**(c) Improving FCP by Deferring Non-Critical CSS**

Stylesheets in the `<head>` block rendering until they are downloaded and parsed.

**Before -- All CSS is Render-Blocking:**

```html
<head>
  <!-- All stylesheets block the first paint -->
  <link rel="stylesheet" href="/css/main.css">
  <link rel="stylesheet" href="/css/animations.css">
  <link rel="stylesheet" href="/css/print.css">
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap">
</head>
```

**After -- Only Critical CSS Blocks Rendering:**

```html
<head>
  <!-- Critical CSS inlined for instant first paint -->
  <style>
    /* Only above-the-fold styles are inlined */
    body { margin: 0; font-family: 'Roboto', sans-serif; }
    .header { background: #1a1a2e; color: white; padding: 1rem; }
    .hero { text-align: center; padding: 4rem 2rem; }
    .hero h1 { font-size: 2.5rem; margin-bottom: 1rem; }
  </style>

  <!-- Main CSS loaded normally (it contains above-the-fold styles too) -->
  <link rel="stylesheet" href="/css/main.css">

  <!-- Non-critical CSS loaded asynchronously -->
  <link rel="preload" href="/css/animations.css" as="style"
        onload="this.onload=null;this.rel='stylesheet'">
  <noscript><link rel="stylesheet" href="/css/animations.css"></noscript>

  <!-- Print CSS only loads when printing -->
  <link rel="stylesheet" href="/css/print.css" media="print">

  <!-- Google Fonts with display=swap prevents font-blocking -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link rel="stylesheet"
        href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap">
</head>
```

**Key improvements:**
- Critical CSS is inlined so the browser can render above-the-fold content immediately
- Non-critical CSS (animations) is loaded asynchronously using `rel="preload"` with `onload` swap
- Print CSS uses `media="print"` so it never blocks screen rendering
- `font-display: swap` (via `&display=swap`) shows fallback text immediately while fonts load
- `rel="preconnect"` establishes early connections to Google Fonts servers

</details>

---

**19. Add comprehensive SEO meta tags to a React application's `index.html`.**

Include: title, description, keywords, Open Graph tags, Twitter Card tags, canonical URL, viewport, robots, and structured data (JSON-LD). Show the complete `<head>` section.

<details>
<summary>Answer</summary>

Here is the complete `index.html` file with comprehensive SEO meta tags for a MERN stack portfolio application:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <!-- Basic Meta Tags -->
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- Page Title (50-60 characters for best SEO results) -->
  <title>John Doe | Full-Stack MERN Developer Portfolio</title>

  <!-- Meta Description (150-160 characters -- shown in search results) -->
  <meta name="description"
        content="Full-stack web developer specializing in MongoDB, Express.js, React, and Node.js. View my projects, blog posts, and contact me for freelance work.">

  <!-- Keywords (less impactful for SEO today, but still used by some engines) -->
  <meta name="keywords"
        content="MERN stack, full-stack developer, React developer, Node.js, MongoDB, Express.js, web developer portfolio, JavaScript">

  <!-- Author -->
  <meta name="author" content="John Doe">

  <!-- Robots (tell search engines how to index this page) -->
  <meta name="robots" content="index, follow, max-snippet:-1, max-image-preview:large">

  <!-- Canonical URL (prevents duplicate content issues) -->
  <link rel="canonical" href="https://johndoe.dev/">

  <!-- ==================== Open Graph Tags (Facebook, LinkedIn) ==================== -->
  <meta property="og:type" content="website">
  <meta property="og:title" content="John Doe | Full-Stack MERN Developer Portfolio">
  <meta property="og:description"
        content="Full-stack web developer specializing in MongoDB, Express.js, React, and Node.js. View my projects and blog posts.">
  <meta property="og:image" content="https://johndoe.dev/images/og-preview.png">
  <meta property="og:image:width" content="1200">
  <meta property="og:image:height" content="630">
  <meta property="og:image:alt" content="John Doe - MERN Stack Developer Portfolio">
  <meta property="og:url" content="https://johndoe.dev/">
  <meta property="og:site_name" content="John Doe Portfolio">
  <meta property="og:locale" content="en_US">

  <!-- ==================== Twitter Card Tags ==================== -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="John Doe | Full-Stack MERN Developer Portfolio">
  <meta name="twitter:description"
        content="Full-stack web developer specializing in MongoDB, Express.js, React, and Node.js.">
  <meta name="twitter:image" content="https://johndoe.dev/images/og-preview.png">
  <meta name="twitter:image:alt" content="John Doe - MERN Stack Developer Portfolio">
  <meta name="twitter:site" content="@johndoe_dev">
  <meta name="twitter:creator" content="@johndoe_dev">

  <!-- ==================== Additional SEO Tags ==================== -->

  <!-- Favicon -->
  <link rel="icon" type="image/svg+xml" href="/favicon.svg">
  <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png">

  <!-- Theme Color (browser address bar color on mobile) -->
  <meta name="theme-color" content="#1a1a2e">

  <!-- Preconnect to external domains for faster loading -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

  <!-- ==================== Structured Data (JSON-LD) ==================== -->
  <!-- Helps search engines understand the content and display rich results -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "WebSite",
    "name": "John Doe Portfolio",
    "url": "https://johndoe.dev",
    "description": "Full-stack web developer specializing in MERN stack development.",
    "author": {
      "@type": "Person",
      "name": "John Doe",
      "url": "https://johndoe.dev",
      "jobTitle": "Full-Stack Web Developer",
      "sameAs": [
        "https://github.com/johndoe",
        "https://linkedin.com/in/johndoe",
        "https://twitter.com/johndoe_dev"
      ],
      "knowsAbout": [
        "JavaScript",
        "React",
        "Node.js",
        "MongoDB",
        "Express.js",
        "HTML",
        "CSS"
      ]
    },
    "potentialAction": {
      "@type": "SearchAction",
      "target": "https://johndoe.dev/search?q={search_term_string}",
      "query-input": "required name=search_term_string"
    }
  }
  </script>

  <!-- Person Schema for rich contact card in search results -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "Person",
    "name": "John Doe",
    "url": "https://johndoe.dev",
    "image": "https://johndoe.dev/images/profile.jpg",
    "jobTitle": "Full-Stack MERN Developer",
    "worksFor": {
      "@type": "Organization",
      "name": "Freelance"
    },
    "email": "john@johndoe.dev",
    "address": {
      "@type": "PostalAddress",
      "addressLocality": "San Francisco",
      "addressRegion": "CA",
      "addressCountry": "US"
    },
    "sameAs": [
      "https://github.com/johndoe",
      "https://linkedin.com/in/johndoe",
      "https://twitter.com/johndoe_dev"
    ]
  }
  </script>
</head>
<body>
  <!-- React root element -->
  <div id="root"></div>
  <script type="module" src="/src/main.jsx"></script>
</body>
</html>
```

**What each section does:**

```
+---------------------------+----------------------------------------------+
| Tag / Section             | Purpose                                      |
+---------------------------+----------------------------------------------+
| <title>                   | Displayed in browser tab and search results  |
| meta description          | Summary shown below title in search results  |
| meta keywords             | Hints for search engines (minor impact)      |
| meta robots               | Controls indexing and crawling behavior       |
| link canonical            | Prevents duplicate content penalties         |
| og:* tags                 | Controls appearance when shared on Facebook  |
| twitter:* tags            | Controls appearance when shared on Twitter   |
| JSON-LD WebSite           | Enables rich search results and site search  |
| JSON-LD Person            | Enables knowledge panel in Google results    |
+---------------------------+----------------------------------------------+
```

**Open Graph preview when shared on social media:**

```
+--------------------------------------------------+
|                                                  |
|        [og:image -- 1200x630 preview image]      |
|                                                  |
+--------------------------------------------------+
| johndoe.dev                                      |
| John Doe | Full-Stack MERN Developer Portfolio   |
| Full-stack web developer specializing in         |
| MongoDB, Express.js, React, and Node.js...       |
+--------------------------------------------------+
```

</details>

---

**20. Create a production security configuration for an Express application.**

Write middleware that includes: helmet setup with custom CSP, CORS configuration for specific origins, rate limiting with `express-rate-limit`, request size limiting, MongoDB injection prevention, and XSS protection. Show the complete security middleware file.

<details>
<summary>Answer</summary>

Create a file called `middleware/security.js` that centralizes all security configuration:

```javascript
// middleware/security.js
// Production security middleware for Express.js MERN application

const helmet = require('helmet');
const cors = require('cors');
const rateLimit = require('express-rate-limit');
const mongoSanitize = require('express-mongo-sanitize');

// ============================================================
// 1. HELMET -- Sets secure HTTP headers
// ============================================================
const helmetConfig = helmet({
  // Content Security Policy -- controls which resources can be loaded
  contentSecurityPolicy: {
    directives: {
      defaultSrc: ["'self'"],                          // Only allow resources from same origin
      scriptSrc: ["'self'"],                           // Only allow scripts from same origin
      styleSrc: ["'self'", "'unsafe-inline'",          // Allow inline styles (needed for some React libs)
                 "https://fonts.googleapis.com"],
      fontSrc: ["'self'",
                "https://fonts.gstatic.com"],          // Allow Google Fonts
      imgSrc: ["'self'", "data:", "https:"],           // Allow images from HTTPS sources
      connectSrc: ["'self'",
                   process.env.FRONTEND_URL || "http://localhost:5173"],  // API connections
      frameSrc: ["'none'"],                            // Prevent embedding in iframes
      objectSrc: ["'none'"],                           // Block Flash/Java plugins
      upgradeInsecureRequests: [],                     // Auto-upgrade HTTP to HTTPS
    },
  },

  // Prevent clickjacking by disallowing iframe embedding
  frameguard: { action: 'deny' },

  // Force HTTPS for 1 year (includeSubDomains for full coverage)
  hsts: {
    maxAge: 31536000,          // 1 year in seconds
    includeSubDomains: true,
    preload: true,
  },

  // Prevent MIME-type sniffing
  noSniff: true,

  // Remove X-Powered-By header (hides that the server runs Express)
  hidePoweredBy: true,

  // Control referrer information sent with requests
  referrerPolicy: { policy: 'strict-origin-when-cross-origin' },
});

// ============================================================
// 2. CORS -- Cross-Origin Resource Sharing
// ============================================================
const allowedOrigins = [
  process.env.FRONTEND_URL || 'http://localhost:5173',
  'https://myapp.vercel.app',
];

const corsConfig = cors({
  origin: function (origin, callback) {
    // Allow requests with no origin (mobile apps, Postman, server-to-server)
    if (!origin) return callback(null, true);

    if (allowedOrigins.includes(origin)) {
      callback(null, true);
    } else {
      callback(new Error('Not allowed by CORS'));
    }
  },
  credentials: true,             // Allow cookies to be sent cross-origin
  methods: ['GET', 'POST', 'PUT', 'DELETE', 'PATCH'],
  allowedHeaders: ['Content-Type', 'Authorization'],
  exposedHeaders: ['X-Total-Count'],   // Headers the frontend can read
  maxAge: 86400,                 // Cache preflight requests for 24 hours
});

// ============================================================
// 3. RATE LIMITING -- Prevent brute-force and DDoS attacks
// ============================================================

// General API rate limiter
const generalLimiter = rateLimit({
  windowMs: 15 * 60 * 1000,     // 15-minute window
  max: 100,                      // Limit each IP to 100 requests per window
  message: {
    status: 429,
    error: 'Too many requests. Please try again after 15 minutes.',
  },
  standardHeaders: true,         // Return rate limit info in RateLimit-* headers
  legacyHeaders: false,          // Disable X-RateLimit-* headers
});

// Strict limiter for authentication routes (login, register, password reset)
const authLimiter = rateLimit({
  windowMs: 15 * 60 * 1000,     // 15-minute window
  max: 10,                       // Only 10 auth attempts per window
  message: {
    status: 429,
    error: 'Too many authentication attempts. Please try again after 15 minutes.',
  },
  standardHeaders: true,
  legacyHeaders: false,
});

// ============================================================
// 4. MONGODB INJECTION PREVENTION
// ============================================================
// Strips $ and . from req.body, req.query, and req.params
// Prevents attacks like: { "email": { "$gt": "" } }
const mongoSanitizeConfig = mongoSanitize({
  replaceWith: '_',              // Replace prohibited characters with underscore
  onSanitize: ({ req, key }) => {
    console.warn(`Sanitized key: ${key} in request from IP: ${req.ip}`);
  },
});

// ============================================================
// 5. REQUEST SIZE LIMITING -- Prevent payload-based DoS attacks
// ============================================================
const express = require('express');

const jsonParser = express.json({
  limit: '10kb',                 // Limit JSON body to 10KB
});

const urlencodedParser = express.urlencoded({
  extended: true,
  limit: '10kb',                 // Limit URL-encoded body to 10KB
});

// ============================================================
// 6. XSS PROTECTION -- Custom middleware to sanitize output
// ============================================================
const xssProtection = (req, res, next) => {
  // Set additional XSS protection header
  res.setHeader('X-XSS-Protection', '1; mode=block');

  // Override res.json to sanitize outgoing data
  const originalJson = res.json.bind(res);
  res.json = (data) => {
    if (typeof data === 'string') {
      data = data
        .replace(/</g, '&lt;')
        .replace(/>/g, '&gt;')
        .replace(/"/g, '&quot;');
    }
    return originalJson(data);
  };

  next();
};

// ============================================================
// 7. APPLY ALL SECURITY MIDDLEWARE
// ============================================================
function applySecurityMiddleware(app) {
  // Order matters -- apply in this sequence

  // 1. Set secure HTTP headers first
  app.use(helmetConfig);

  // 2. Configure CORS before any route handling
  app.use(corsConfig);

  // 3. Parse request bodies with size limits
  app.use(jsonParser);
  app.use(urlencodedParser);

  // 4. Sanitize MongoDB queries
  app.use(mongoSanitizeConfig);

  // 5. Apply general rate limiting to all routes
  app.use('/api/', generalLimiter);

  // 6. Apply strict rate limiting to auth routes
  app.use('/api/auth/', authLimiter);

  // 7. Apply XSS protection
  app.use(xssProtection);

  // 8. Disable X-Powered-By (also handled by helmet, but as a safeguard)
  app.disable('x-powered-by');

  console.log('Security middleware applied successfully');
}

// Export individual middleware and the combined setup function
module.exports = {
  applySecurityMiddleware,
  helmetConfig,
  corsConfig,
  generalLimiter,
  authLimiter,
  mongoSanitizeConfig,
  xssProtection,
};
```

**Using the security middleware in `server.js`:**

```javascript
// server.js
const express = require('express');
const mongoose = require('mongoose');
const { applySecurityMiddleware } = require('./middleware/security');

const app = express();

// Apply all security middleware in one call
applySecurityMiddleware(app);

// Your routes come AFTER the security middleware
const authRoutes = require('./routes/auth');
const postRoutes = require('./routes/posts');

app.use('/api/auth', authRoutes);
app.use('/api/posts', postRoutes);

// Global error handler (catches CORS errors and other security rejections)
app.use((err, req, res, next) => {
  if (err.message === 'Not allowed by CORS') {
    return res.status(403).json({ error: 'CORS policy: Origin not allowed' });
  }
  console.error(err.stack);
  res.status(500).json({ error: 'Internal server error' });
});

const PORT = process.env.PORT || 5000;

mongoose.connect(process.env.MONGODB_URI)
  .then(() => {
    app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
  })
  .catch(err => console.error('Database connection failed:', err));
```

**Required npm packages:**

```javascript
// Install all security dependencies
// npm install helmet cors express-rate-limit express-mongo-sanitize
```

**Security middleware flow:**

```
Incoming Request
      |
      v
+------------------+
|  Helmet          |  Sets 11+ security headers
+------------------+
      |
      v
+------------------+
|  CORS            |  Blocks unauthorized origins
+------------------+
      |
      v
+------------------+
|  Body Parser     |  Rejects payloads > 10KB
|  (size limit)    |
+------------------+
      |
      v
+------------------+
|  Mongo Sanitize  |  Strips $ and . from input
+------------------+
      |
      v
+------------------+
|  Rate Limiter    |  Blocks IPs exceeding limits
+------------------+
      |
      v
+------------------+
|  XSS Protection  |  Sanitizes response output
+------------------+
      |
      v
   Route Handler
```

</details>

---

## Summary

| Category | Count |
|---|---|
| Multiple Choice Questions | 10 |
| Short Answer Questions | 5 |
| Practical Exercises | 5 |
| **Total** | **20** |
