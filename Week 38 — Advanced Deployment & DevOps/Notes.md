# Week 38: Advanced Deployment & DevOps Basics

---

## Table of Contents

1. [CI/CD Concept](#1-cicd-concept)
2. [GitHub Actions Basics](#2-github-actions-basics)
3. [Docker Introduction](#3-docker-introduction)
4. [Performance Monitoring Basics](#4-performance-monitoring-basics)
5. [SEO Basics for Web Apps](#5-seo-basics-for-web-apps)
6. [Web Performance Optimization](#6-web-performance-optimization)
7. [Security Checklist for Production](#7-security-checklist-for-production)
8. [Summary](#8-summary)

---

## 1. CI/CD Concept

### What is CI/CD?

**CI/CD** stands for **Continuous Integration / Continuous Deployment**. It is the practice of automating the process of testing, building, and deploying your code every time a change is made.

### Real-Life Analogy: The Assembly Line

Think of a car manufacturing plant:

- **Without CI/CD:** A worker builds the entire car by hand, then manually inspects every part, then drives it to the dealership. If something is wrong, the whole process restarts. This is slow, error-prone, and unreliable.
- **With CI/CD:** The factory has an assembly line. Each station does one job automatically -- one installs the engine, another paints the body, another runs quality checks. If any station detects a defect, the line stops immediately and the team is alerted. Cars roll off the line consistently and reliably.

```
WITHOUT CI/CD (Manual Process):
+--------+     +-------+     +--------+     +--------+
| Write  |---->| Build |---->| Test   |---->| Deploy |
| Code   |     | (you) |     | (you)  |     | (you)  |
+--------+     +-------+     +--------+     +--------+
   "I hope I remembered to test everything..."


WITH CI/CD (Automated Pipeline):
+--------+     +-----------+     +----------+     +----------+
| Write  |---->| Build     |---->| Test     |---->| Deploy   |
| Code   |     | (auto)    |     | (auto)   |     | (auto)   |
| & Push |     |           |     |          |     |          |
+--------+     +-----------+     +----------+     +----------+
                    |                  |                |
                    v                  v                v
              "Build failed!"   "2 tests failed"  "Deployed to
               (stops here)     (stops here)       production!"
```

### Breaking It Down

#### Continuous Integration (CI)

Every time a developer pushes code, the system automatically:

1. Pulls the latest code
2. Installs dependencies
3. Runs the test suite
4. Reports success or failure

The goal is to **catch bugs early**, before they reach production.

#### Continuous Deployment (CD)

If all tests pass, the system automatically:

1. Builds the production version of the app
2. Deploys it to the live server
3. Notifies the team

The goal is to **release quickly and safely**, without manual intervention.

### CI/CD Pipeline Diagram

```
Developer pushes code to GitHub
          |
          v
+-------------------+
|   TRIGGER         |  "New code detected on main branch"
+-------------------+
          |
          v
+-------------------+
|   INSTALL         |  npm install
+-------------------+
          |
          v
+-------------------+
|   LINT            |  npm run lint (check code style)
+-------------------+
          |
          v
+-------------------+
|   TEST            |  npm test (run unit tests)
+-------------------+
          |
     Pass?|
    +-----+-----+
    |           |
   YES          NO
    |           |
    v           v
+--------+  +--------+
| BUILD  |  | STOP   |
| & DEPLOY|  | & ALERT|
+--------+  +--------+
    |
    v
"Live on production!"
```

### Why CI/CD Matters

| Without CI/CD | With CI/CD |
|---|---|
| "It works on my machine" | Works everywhere, every time |
| Manual testing -- easy to forget steps | Automated testing -- nothing is missed |
| Deploy once a week (scary) | Deploy multiple times a day (confident) |
| Bugs found by users | Bugs caught before deployment |
| One person knows how to deploy | Anyone can push code safely |

---

## 2. GitHub Actions Basics

**GitHub Actions** is GitHub's built-in CI/CD platform. It lets you automate workflows directly in your repository -- no external tools needed.

### Key Concepts

| Term | Meaning |
|---|---|
| **Workflow** | An automated process defined in a YAML file |
| **Trigger** | The event that starts a workflow (e.g., `push`, `pull_request`) |
| **Job** | A set of steps that run on the same machine |
| **Step** | A single task within a job (e.g., run a command) |
| **Runner** | The virtual machine that executes your jobs |
| **Action** | A reusable unit of code (from GitHub Marketplace or custom) |

### Workflow File Structure

Workflows live in the `.github/workflows/` directory of your repository. Each workflow is a `.yml` file.

```
my-project/
  .github/
    workflows/
      ci.yml          <-- Your CI/CD workflow
      deploy.yml      <-- Another workflow
  src/
  package.json
  ...
```

### Your First GitHub Actions Workflow

Create `.github/workflows/ci.yml`:

```yaml
# Name of the workflow (shown in the Actions tab)
name: CI Pipeline

# TRIGGERS: When should this workflow run?
on:
  push:
    branches: [main]        # Run on pushes to main
  pull_request:
    branches: [main]        # Run on PRs targeting main

# JOBS: What should happen?
jobs:
  build-and-test:
    # What machine to run on
    runs-on: ubuntu-latest

    # STEPS: Individual tasks
    steps:
      # Step 1: Check out the code
      - name: Checkout code
        uses: actions/checkout@v4

      # Step 2: Set up Node.js
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      # Step 3: Install dependencies
      - name: Install dependencies
        run: npm install

      # Step 4: Run linting
      - name: Run linter
        run: npm run lint

      # Step 5: Run tests
      - name: Run tests
        run: npm test

      # Step 6: Build the project
      - name: Build project
        run: npm run build
```

### Understanding Each Part

#### Triggers (`on:`)

```yaml
# Run on every push to main
on:
  push:
    branches: [main]

# Run on pull requests
on:
  pull_request:
    branches: [main]

# Run on a schedule (every day at midnight)
on:
  schedule:
    - cron: '0 0 * * *'

# Run manually from GitHub UI
on:
  workflow_dispatch:
```

#### Steps with `uses` vs `run`

```yaml
steps:
  # 'uses' runs a pre-built Action from the marketplace
  - name: Checkout code
    uses: actions/checkout@v4

  # 'run' executes a shell command
  - name: Install dependencies
    run: npm install
```

### A Real-World Workflow: Auto-Deploy to Vercel

```yaml
name: Deploy to Vercel

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Install
        run: npm install

      - name: Build
        run: npm run build

      - name: Deploy to Vercel
        uses: amondnet/vercel-action@v25
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          vercel-org-id: ${{ secrets.ORG_ID }}
          vercel-project-id: ${{ secrets.PROJECT_ID }}
          vercel-args: '--prod'
```

### Using GitHub Secrets

Sensitive values (API keys, tokens) are stored in **GitHub Secrets**, not in the workflow file.

1. Go to your repo on GitHub
2. **Settings** > **Secrets and variables** > **Actions**
3. Click **"New repository secret"**
4. Add name (e.g., `VERCEL_TOKEN`) and value

Access them in workflows with `${{ secrets.SECRET_NAME }}`.

### Viewing Workflow Results

1. Go to your repository on GitHub
2. Click the **"Actions"** tab
3. See all workflow runs with green (pass) or red (fail) indicators
4. Click a run to see detailed logs for each step

```
Actions Tab View:
+----------------------------------------------------------+
| CI Pipeline                                               |
+----------------------------------------------------------+
| Run #15  main  abc1234  "Add user auth"    [PASS]   2m   |
| Run #14  main  def5678  "Fix login bug"    [PASS]   1m   |
| Run #13  PR #7  ghi9012  "Add dashboard"   [FAIL]   45s  |
| Run #12  main  jkl3456  "Update README"    [PASS]   1m   |
+----------------------------------------------------------+
```

---

## 3. Docker Introduction

### What is Docker?

**Docker** is a platform that packages your application and all its dependencies into a standardized unit called a **container**. This container can run on any machine that has Docker installed, regardless of operating system or configuration.

### Real-Life Analogy: The Shipping Container

Before shipping containers were invented, loading and unloading cargo ships was chaotic. Every item -- boxes, barrels, crates -- had different sizes and shapes. Workers had to figure out how to pack and unpack everything individually. It was slow, expensive, and things often broke.

Then came the **standardized shipping container**. Now, everything goes inside the same-sized metal box. Cranes know exactly how to lift it. Trucks and trains are built to carry it. The contents do not matter -- it just works.

Docker containers do the same for software:

```
WITHOUT DOCKER:
+-----------------+     +-----------------+
| Developer's     |     | Production      |
| Machine         |     | Server          |
|                 |     |                 |
| Node 20         |     | Node 18  <-- DIFFERENT!
| MongoDB 7       |     | MongoDB 6 <-- DIFFERENT!
| macOS           |     | Ubuntu         |
| npm 10          |     | npm 9   <-- DIFFERENT!
+-----------------+     +-----------------+
"It works on my machine!" ... "It doesn't work on the server."


WITH DOCKER:
+-----------------+     +-----------------+
| Developer's     |     | Production      |
| Machine         |     | Server          |
|                 |     |                 |
| +-------------+ |     | +-------------+ |
| | Container   | |     | | Container   | |
| | Node 20     | |     | | Node 20     | |
| | MongoDB 7   | |     | | MongoDB 7   | |
| | npm 10      | |     | | npm 10      | |
| | Your Code   | |     | | Your Code   | |
| +-------------+ |     | +-------------+ |
+-----------------+     +-----------------+
"Same container, same behavior, everywhere."
```

### Key Docker Concepts

| Concept | Description | Analogy |
|---|---|---|
| **Image** | A blueprint/template for a container | A recipe for a dish |
| **Container** | A running instance of an image | The actual dish, cooked and served |
| **Dockerfile** | Instructions to build an image | The recipe card |
| **Docker Hub** | A registry of public images | A cookbook library |
| **Volume** | Persistent storage for containers | A pantry that survives kitchen cleanup |

### A Simple Dockerfile for a Node.js/Express App

```dockerfile
# Start from the official Node.js image
FROM node:20-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy package files first (for better caching)
COPY package*.json ./

# Install dependencies
RUN npm install --production

# Copy the rest of the application code
COPY . .

# Expose the port the app runs on
EXPOSE 5000

# Command to start the application
CMD ["node", "server.js"]
```

### Understanding Each Dockerfile Instruction

```
FROM node:20-alpine
  ^    ^     ^
  |    |     +-- Lightweight Linux variant (smaller image)
  |    +-------- Node.js version 20
  +------------- Start from this base image

WORKDIR /app
  +------------- All following commands run inside /app

COPY package*.json ./
  +------------- Copy package.json and package-lock.json first

RUN npm install --production
  +------------- Install only production dependencies

COPY . .
  +------------- Copy all remaining source code

EXPOSE 5000
  +------------- Document which port the app uses

CMD ["node", "server.js"]
  +------------- The command to start the app
```

### Basic Docker Commands

```bash
# Build an image from a Dockerfile
docker build -t my-express-app .

# Run a container from the image
docker run -p 5000:5000 my-express-app

# List running containers
docker ps

# Stop a container
docker stop <container_id>

# List all images
docker images
```

### The `.dockerignore` File

Just like `.gitignore`, create a `.dockerignore` file to exclude files from the image:

```
node_modules
.env
.git
.gitignore
README.md
```

### When to Use Docker

Docker is powerful, but for beginners deploying to platforms like Vercel and Render, **you do not need Docker**. These platforms handle the environment for you.

Docker becomes essential when:

- You need identical environments across development, testing, and production
- You are deploying to AWS, Google Cloud, or DigitalOcean
- Your app has complex dependencies (databases, Redis, message queues)
- You work on a team and need everyone to have the same setup

---

## 4. Performance Monitoring Basics

Once your application is deployed, you need to know if it is working correctly and performing well. This is where **monitoring** comes in.

### What to Monitor

```
+----------------------------------------------------------+
|                    MONITORING DASHBOARD                    |
+----------------------------------------------------------+
|                                                          |
|  Uptime:          99.9%  [=============================] |
|  Response Time:   245ms  [==========                   ] |
|  Error Rate:      0.3%   [=                            ] |
|  CPU Usage:       23%    [======                       ] |
|  Memory Usage:    512MB  [============                 ] |
|  Active Users:    47     [===========                  ] |
|                                                          |
+----------------------------------------------------------+
```

### Key Metrics

| Metric | What It Measures | Healthy Range |
|---|---|---|
| **Uptime** | Percentage of time your app is accessible | 99.9% or higher |
| **Response time** | How long a request takes to complete | Under 500ms |
| **Error rate** | Percentage of requests that fail | Under 1% |
| **CPU usage** | Server processor load | Under 70% |
| **Memory usage** | How much RAM your app consumes | Below allocated limit |
| **Throughput** | Number of requests handled per second | Depends on your app |

### Free Monitoring Tools

1. **UptimeRobot** (uptimerobot.com)
   - Pings your website every 5 minutes
   - Alerts you by email if your site goes down
   - Free tier: 50 monitors

2. **Render Dashboard**
   - Built-in logs and metrics for your deployed services
   - Shows deploy history, CPU/memory usage

3. **Vercel Analytics**
   - Page load times, Web Vitals scores
   - Geographic distribution of users

4. **Google Search Console**
   - Reports how Google sees your site
   - Shows indexing issues and search performance

### Application-Level Logging

Replace `console.log` with proper logging in production:

```javascript
// Simple logging middleware for Express
app.use((req, res, next) => {
  const start = Date.now();

  res.on('finish', () => {
    const duration = Date.now() - start;
    console.log(
      `${req.method} ${req.originalUrl} ${res.statusCode} - ${duration}ms`
    );
  });

  next();
});

// Output:
// GET /api/posts 200 - 45ms
// POST /api/posts 201 - 123ms
// GET /api/posts/999 404 - 12ms
```

---

## 5. SEO Basics for Web Apps

**SEO (Search Engine Optimization)** is the practice of making your website discoverable by search engines like Google.

### Why SEO Matters

If your portfolio website does not appear in search results, potential employers and clients will never find it. Good SEO can be the difference between your site being on page 1 or page 50 of Google.

### Essential Meta Tags

Every page should have these tags in the `<head>`:

```html
<head>
  <!-- Page title (shown in search results and browser tab) -->
  <title>John Doe | Full-Stack Web Developer</title>

  <!-- Description (shown below title in search results) -->
  <meta name="description" content="Full-stack web developer specializing
    in React, Node.js, and MongoDB. View my portfolio and blog." />

  <!-- Viewport for responsive design -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <!-- Open Graph tags (for social media sharing) -->
  <meta property="og:title" content="John Doe | Web Developer" />
  <meta property="og:description" content="View my portfolio and blog." />
  <meta property="og:image" content="https://mysite.com/preview.jpg" />
  <meta property="og:url" content="https://mysite.com" />
  <meta property="og:type" content="website" />

  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:title" content="John Doe | Web Developer" />
  <meta name="twitter:description" content="View my portfolio and blog." />
  <meta name="twitter:image" content="https://mysite.com/preview.jpg" />

  <!-- Canonical URL (prevents duplicate content issues) -->
  <link rel="canonical" href="https://mysite.com/" />
</head>
```

### Setting Meta Tags in React (with react-helmet-async)

```bash
npm install react-helmet-async
```

```jsx
import { Helmet } from 'react-helmet-async';

function HomePage() {
  return (
    <>
      <Helmet>
        <title>John Doe | Full-Stack Web Developer</title>
        <meta name="description" content="Full-stack web developer
          specializing in React, Node.js, and MongoDB." />
      </Helmet>

      <h1>Welcome to My Portfolio</h1>
      {/* ... */}
    </>
  );
}
```

### SEO Checklist

```
+----------------------------------------------------------+
|                    SEO CHECKLIST                          |
+----------------------------------------------------------+
|                                                          |
|  [ ] Unique <title> on every page                        |
|  [ ] Meta description on every page (150-160 chars)      |
|  [ ] Open Graph tags for social sharing                  |
|  [ ] Semantic HTML (h1, h2, nav, main, article)          |
|  [ ] Alt text on all images                              |
|  [ ] Fast loading speed (under 3 seconds)                |
|  [ ] Mobile responsive design                            |
|  [ ] HTTPS enabled                                       |
|  [ ] sitemap.xml file                                    |
|  [ ] robots.txt file                                     |
|  [ ] Submit site to Google Search Console                |
|  [ ] No broken links (404 errors)                        |
|                                                          |
+----------------------------------------------------------+
```

### The robots.txt File

Place at the root of your site (`public/robots.txt`):

```
User-agent: *
Allow: /
Sitemap: https://mysite.com/sitemap.xml
```

### The sitemap.xml File

A sitemap tells search engines about all the pages on your site:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://mysite.com/</loc>
    <lastmod>2025-01-15</lastmod>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://mysite.com/projects</loc>
    <lastmod>2025-01-10</lastmod>
    <priority>0.8</priority>
  </url>
  <url>
    <loc>https://mysite.com/blog</loc>
    <lastmod>2025-01-14</lastmod>
    <priority>0.7</priority>
  </url>
</urlset>
```

### SPA SEO Limitation

Single Page Applications (like React) have an SEO challenge: search engine crawlers may not execute JavaScript, so they see an empty page. Solutions include:

1. **Pre-rendering** -- Generate static HTML at build time
2. **Server-Side Rendering (SSR)** -- Use Next.js to render pages on the server
3. **Meta tag management** -- Use `react-helmet-async` for dynamic meta tags

For a portfolio site, pre-rendering or using Next.js is recommended if SEO is critical.

---

## 6. Web Performance Optimization

A fast website provides a better user experience, ranks higher on Google, and keeps users engaged. Studies show that **53% of mobile users abandon a site that takes more than 3 seconds to load**.

### Core Web Vitals

Google measures website performance using three key metrics:

```
+------------------+-------------------+--------------------+
|       LCP        |       FID         |       CLS          |
| Largest Content  | First Input       | Cumulative Layout  |
| ful Paint        | Delay             | Shift              |
+------------------+-------------------+--------------------+
| How long until   | How long until    | How much the page  |
| the main content | the page responds | layout shifts       |
| is visible       | to user input     | while loading      |
+------------------+-------------------+--------------------+
| GOOD: < 2.5s     | GOOD: < 100ms    | GOOD: < 0.1        |
| POOR: > 4.0s     | POOR: > 300ms    | POOR: > 0.25       |
+------------------+-------------------+--------------------+
```

### Optimization Technique 1: Lazy Loading

Load images and components only when they are needed (when they enter the viewport).

#### Lazy Loading Images

```html
<!-- Native lazy loading (no JavaScript needed) -->
<img src="project-screenshot.jpg" alt="Project" loading="lazy" />
```

#### Lazy Loading React Components

```jsx
import { lazy, Suspense } from 'react';

// Instead of: import Dashboard from './pages/Dashboard';
const Dashboard = lazy(() => import('./pages/Dashboard'));

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <Routes>
        <Route path="/dashboard" element={<Dashboard />} />
      </Routes>
    </Suspense>
  );
}
```

### Optimization Technique 2: Code Splitting

Vite automatically splits your code into smaller bundles. You can optimize further:

```jsx
// Before: Everything loads at once
import { Chart } from 'chart.js';            // 200KB
import { Editor } from '@tiptap/react';       // 150KB
import { Calendar } from 'react-big-calendar'; // 100KB
// Total initial load: 450KB+ of JavaScript

// After: Components load only when needed
const Chart = lazy(() => import('./components/Chart'));
const Editor = lazy(() => import('./components/Editor'));
const Calendar = lazy(() => import('./components/Calendar'));
// Initial load: only what the user needs right now
```

### Optimization Technique 3: Image Optimization

Images are often the largest files on a webpage. Optimize them:

```
+-----------------------------------------------------------+
|              IMAGE OPTIMIZATION GUIDE                      |
+-----------------------------------------------------------+
|                                                           |
|  FORMAT CHOICE:                                           |
|  +--------+----------+-----------------------------------+
|  | Format | Best For | Notes                             |
|  +--------+----------+-----------------------------------+
|  | WebP   | Photos   | 30% smaller than JPEG             |
|  | AVIF   | Photos   | 50% smaller than JPEG (newer)     |
|  | SVG    | Icons    | Scalable, tiny file size           |
|  | PNG    | Graphics | When transparency is needed        |
|  +--------+----------+-----------------------------------+
|                                                           |
|  SIZE GUIDELINES:                                         |
|  - Hero images: max 1920px wide, < 200KB                 |
|  - Thumbnails: max 400px wide, < 50KB                    |
|  - Icons: use SVG or icon fonts                          |
|                                                           |
|  TOOLS:                                                   |
|  - squoosh.app (browser-based compression)                |
|  - tinypng.com (batch compression)                        |
|  - sharp (Node.js library for server-side)                |
|                                                           |
+-----------------------------------------------------------+
```

#### Responsive Images in HTML

```html
<picture>
  <!-- Modern browsers get WebP -->
  <source srcset="hero.webp" type="image/webp" />
  <!-- Fallback for older browsers -->
  <img src="hero.jpg" alt="Hero image" loading="lazy" />
</picture>

<!-- Different sizes for different screens -->
<img
  srcset="project-400.jpg 400w,
          project-800.jpg 800w,
          project-1200.jpg 1200w"
  sizes="(max-width: 600px) 400px,
         (max-width: 1024px) 800px,
         1200px"
  src="project-800.jpg"
  alt="Project screenshot"
/>
```

### Optimization Technique 4: Caching

```javascript
// Express: Set cache headers for static files
app.use(express.static('public', {
  maxAge: '1y',           // Cache for 1 year
  etag: true,             // Enable ETag for validation
  immutable: true         // File won't change (use with hashed filenames)
}));
```

### Measuring Performance with Lighthouse

**Google Lighthouse** is a built-in Chrome tool that audits your website:

1. Open Chrome DevTools (F12)
2. Click the **"Lighthouse"** tab
3. Select categories: Performance, Accessibility, Best Practices, SEO
4. Click **"Analyze page load"**

Lighthouse scores each category from 0 to 100:

```
+-----------------------------------------------------------+
|              LIGHTHOUSE REPORT                             |
+-----------------------------------------------------------+
|                                                           |
|  Performance:    92  [============================  ]     |
|  Accessibility:  98  [==============================]     |
|  Best Practices: 95  [=============================  ]    |
|  SEO:            100 [===============================]    |
|                                                           |
|  Opportunities:                                           |
|  - Serve images in WebP format        (-350KB, -1.2s)    |
|  - Remove unused JavaScript           (-120KB, -0.5s)    |
|  - Add explicit width/height to imgs  (CLS improvement)  |
|                                                           |
+-----------------------------------------------------------+
```

---

## 7. Security Checklist for Production

Security is not optional. A single vulnerability can compromise your users' data, destroy your reputation, and even expose you to legal liability.

### Production Security Checklist

```
+--------------------------------------------------------------+
|              SECURITY CHECKLIST FOR PRODUCTION                |
+--------------------------------------------------------------+
|                                                              |
|  AUTHENTICATION & AUTHORIZATION                              |
|  [ ] Passwords hashed with bcrypt (cost factor >= 10)        |
|  [ ] JWT tokens have short expiration (e.g., 1 hour)         |
|  [ ] Refresh tokens stored in HttpOnly cookies               |
|  [ ] Protected routes check auth on EVERY request            |
|  [ ] Admin routes verify admin role, not just auth           |
|                                                              |
|  DATA VALIDATION                                             |
|  [ ] All user input validated on the server (not just UI)    |
|  [ ] MongoDB queries use parameterized inputs (no injection) |
|  [ ] File uploads validated (type, size, content)            |
|  [ ] API rate limiting implemented                           |
|                                                              |
|  HEADERS & TRANSPORT                                         |
|  [ ] HTTPS enforced (redirect HTTP to HTTPS)                 |
|  [ ] Security headers set (Helmet.js)                        |
|  [ ] CORS restricted to known origins                        |
|  [ ] Cookies set with Secure, HttpOnly, SameSite flags       |
|                                                              |
|  SECRETS & CONFIGURATION                                     |
|  [ ] .env file in .gitignore                                 |
|  [ ] No secrets in client-side code                          |
|  [ ] Strong, unique JWT_SECRET in production                 |
|  [ ] Database credentials not in source code                 |
|                                                              |
|  DEPENDENCIES                                                |
|  [ ] npm audit shows no critical vulnerabilities             |
|  [ ] Dependencies kept up to date                            |
|  [ ] No unnecessary packages installed                       |
|                                                              |
+--------------------------------------------------------------+
```

### Using Helmet.js for Security Headers

```bash
npm install helmet
```

```javascript
const helmet = require('helmet');

// Add security headers to all responses
app.use(helmet());
```

Helmet sets these headers automatically:

| Header | Purpose |
|---|---|
| `X-Content-Type-Options: nosniff` | Prevents MIME type sniffing |
| `X-Frame-Options: DENY` | Prevents clickjacking |
| `X-XSS-Protection: 1; mode=block` | Enables XSS filter |
| `Strict-Transport-Security` | Forces HTTPS |
| `Content-Security-Policy` | Controls resource loading |

### Rate Limiting

Prevent abuse by limiting how many requests a user can make:

```bash
npm install express-rate-limit
```

```javascript
const rateLimit = require('express-rate-limit');

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000,   // 15 minutes
  max: 100,                     // Limit each IP to 100 requests per window
  message: { error: 'Too many requests, please try again later.' }
});

// Apply to all routes
app.use(limiter);

// Or apply to specific routes (e.g., login)
const loginLimiter = rateLimit({
  windowMs: 15 * 60 * 1000,
  max: 5,   // Only 5 login attempts per 15 minutes
  message: { error: 'Too many login attempts. Try again in 15 minutes.' }
});

app.post('/api/auth/login', loginLimiter, authController.login);
```

### Running a Security Audit

```bash
# Check for known vulnerabilities in your dependencies
npm audit

# Fix automatically where possible
npm audit fix

# See detailed report
npm audit --json
```

---

## 8. Summary

### What We Covered

| Topic | Key Takeaway |
|---|---|
| **CI/CD** | Automate testing and deployment to catch bugs early and deploy safely |
| **GitHub Actions** | Define workflows in YAML files to run on push, PR, or schedule |
| **Docker** | Package your app with its environment so it runs the same everywhere |
| **Monitoring** | Track uptime, response time, and errors to know when things go wrong |
| **SEO** | Meta tags, sitemaps, and semantic HTML help search engines find your site |
| **Performance** | Lazy loading, code splitting, and image optimization make your site fast |
| **Security** | Helmet, rate limiting, input validation, and proper auth protect your users |

### DevOps Workflow Overview

```
+------------------------------------------------------------------+
|                     MODERN WEB DEVELOPMENT WORKFLOW               |
+------------------------------------------------------------------+
|                                                                  |
|  1. WRITE CODE                                                   |
|     |                                                            |
|  2. PUSH TO GITHUB                                               |
|     |                                                            |
|  3. CI/CD PIPELINE (GitHub Actions)                              |
|     |-- Lint code                                                |
|     |-- Run tests                                                |
|     |-- Build project                                            |
|     |                                                            |
|  4. DEPLOY (Automated)                                           |
|     |-- Frontend --> Vercel/Netlify                               |
|     |-- Backend  --> Render/Railway                               |
|     |                                                            |
|  5. MONITOR                                                      |
|     |-- Uptime checks                                            |
|     |-- Error tracking                                           |
|     |-- Performance metrics                                      |
|     |                                                            |
|  6. ITERATE                                                      |
|     +-- Back to step 1                                           |
|                                                                  |
+------------------------------------------------------------------+
```

### Key Takeaways

1. **CI/CD automates the boring, error-prone parts** of deployment so you can focus on writing code.
2. **GitHub Actions** is free for public repositories and integrates seamlessly with your GitHub workflow.
3. **Docker is not required for beginners** but becomes essential as your applications grow in complexity.
4. **Monitor your deployed applications** -- you cannot fix problems you do not know about.
5. **SEO is not just for marketing** -- it is how people discover your portfolio and projects.
6. **Performance matters** -- fast sites rank higher, convert better, and provide superior user experiences.
7. **Security is not optional** -- one breach can undo months of work and trust.

---

*Next week, we begin building our final project -- a full-stack portfolio website with a blog.*
