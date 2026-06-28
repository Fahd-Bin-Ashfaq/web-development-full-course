# Week 37: Deployment Fundamentals

---

## Table of Contents

1. [What is Deployment?](#1-what-is-deployment)
2. [Development vs Production](#2-development-vs-production)
3. [Domain Names and DNS Basics](#3-domain-names-and-dns-basics)
4. [Frontend Deployment on Vercel](#4-frontend-deployment-on-vercel)
5. [Frontend Deployment on Netlify](#5-frontend-deployment-on-netlify)
6. [Backend Deployment on Render](#6-backend-deployment-on-render)
7. [Backend Deployment on Railway](#7-backend-deployment-on-railway)
8. [MongoDB Atlas for Production Database](#8-mongodb-atlas-for-production-database)
9. [Environment Variables in Production](#9-environment-variables-in-production)
10. [HTTPS and SSL Basics](#10-https-and-ssl-basics)
11. [Summary](#11-summary)

---

## 1. What is Deployment?

**Deployment** is the process of taking your application from your local computer and making it available on the internet for anyone in the world to access.

### Real-Life Analogy: Building a House

Think of it this way:

- **Development** is like building a house. You lay the foundation, put up the walls, install plumbing and electricity, paint the rooms, and furnish everything. But right now, only the construction workers (you, the developer) can walk through it.
- **Deployment** is like opening the front door and putting the address on a map so that visitors (users) can find it and walk in.

Until you deploy, your beautiful application only exists on `localhost:3000` -- visible to no one but you.

```
+--------------------------------------------------+
|              YOUR LOCAL MACHINE                   |
|                                                   |
|   localhost:3000  -->  Only YOU can see it         |
|                                                   |
+--------------------------------------------------+
                      |
                      | DEPLOYMENT
                      v
+--------------------------------------------------+
|              THE INTERNET                         |
|                                                   |
|   www.yourapp.com  -->  EVERYONE can see it       |
|                                                   |
+--------------------------------------------------+
```

### What Actually Happens During Deployment?

1. Your code is uploaded to a remote **server** (a computer that is always on and connected to the internet).
2. The server installs your dependencies (`npm install`).
3. The server builds your project (`npm run build`).
4. The server starts serving your application to incoming requests.

---

## 2. Development vs Production

Development and production are two entirely different **environments**. Understanding the differences is critical before you deploy.

### Comparison Table

| Aspect | Development | Production |
|---|---|---|
| **URL** | `http://localhost:3000` | `https://www.yourapp.com` |
| **Who can access** | Only you | Everyone on the internet |
| **Error messages** | Detailed stack traces | Generic "Something went wrong" |
| **Performance** | Not optimized | Minified, compressed, cached |
| **Database** | Local MongoDB or test data | MongoDB Atlas (cloud) |
| **Environment variables** | `.env` file on your machine | Set in hosting platform dashboard |
| **HTTPS** | Usually HTTP | Must be HTTPS |
| **Debugging** | Console logs everywhere | Logging service (no console.log) |
| **Hot reload** | Yes (Vite/React dev server) | No -- serves static build |

### How Builds Differ

In **development**, React runs a dev server with hot module replacement:

```bash
npm run dev
# Serves unoptimized code with source maps
```

In **production**, React code is compiled into static files:

```bash
npm run build
# Creates optimized /dist folder with minified JS, CSS, HTML
```

```
DEVELOPMENT                          PRODUCTION
+-----------+                        +-----------+
| App.jsx   |   npm run build        | app.3f2a.js|  (minified)
| Home.jsx  |  ================>     | style.8b1c.css|
| About.jsx |                        | index.html |
| style.css |                        +-----------+
+-----------+                          (dist/ folder)
```

For the **backend**, production means:

- `NODE_ENV=production`
- No `nodemon` -- use `node server.js` directly
- Real database connection strings
- Real API keys (Stripe, SendGrid, etc.)
- Proper error handling (no stack traces to users)

---

## 3. Domain Names and DNS Basics

### What is a Domain Name?

A domain name is the human-readable address of a website. Instead of remembering `185.199.108.153`, you type `github.com`.

### What is DNS?

**DNS (Domain Name System)** is like the phone book of the internet. It translates domain names into IP addresses that computers use to find each other.

### How DNS Works -- Step by Step

```
User types: www.myportfolio.com
          |
          v
+-------------------+
|  Browser Cache    |  "Do I already know this address?"
+-------------------+
          |  No
          v
+-------------------+
|  DNS Resolver     |  (Usually your ISP)
|  "Let me look     |
|   this up..."     |
+-------------------+
          |
          v
+-------------------+
|  Root Name Server |  "I know who handles .com domains"
+-------------------+
          |
          v
+-------------------+
|  .com TLD Server  |  "myportfolio.com is managed by
|                   |   Cloudflare DNS"
+-------------------+
          |
          v
+-------------------+
|  Authoritative    |  "myportfolio.com points to
|  Name Server      |   76.76.21.21 (Vercel)"
+-------------------+
          |
          v
+-------------------+
|  Browser connects |  Browser loads the website
|  to 76.76.21.21   |  from the server
+-------------------+
```

### DNS Record Types

| Record Type | Purpose | Example |
|---|---|---|
| **A** | Points domain to an IPv4 address | `mysite.com -> 76.76.21.21` |
| **AAAA** | Points domain to an IPv6 address | `mysite.com -> 2606:4700::1` |
| **CNAME** | Points domain to another domain | `www.mysite.com -> mysite.vercel.app` |
| **MX** | Mail server records | `mysite.com -> mail.google.com` |
| **TXT** | Verification and other text | Used for domain verification |

### Where to Buy Domains

- **Namecheap** -- affordable, good UI
- **Google Domains** (now Squarespace Domains)
- **Cloudflare Registrar** -- at-cost pricing
- **GoDaddy** -- popular but often more expensive

---

## 4. Frontend Deployment on Vercel

**Vercel** is the company behind Next.js, but it works perfectly for any Vite/React application. It is the most popular platform for frontend deployment.

### Why Vercel?

- Free tier is generous (100 deployments/day)
- Automatic HTTPS
- Automatic deployments on every `git push`
- Global CDN (Content Delivery Network)
- Preview deployments for pull requests

### Step-by-Step: Deploy a Vite + React App to Vercel

#### Step 1: Prepare Your Project

Make sure your project is pushed to GitHub:

```bash
# Initialize git if not already done
git init
git add .
git commit -m "Initial commit"

# Create a repo on GitHub, then:
git remote add origin https://github.com/yourusername/my-portfolio.git
git branch -M main
git push -u origin main
```

#### Step 2: Sign Up on Vercel

1. Go to [vercel.com](https://vercel.com)
2. Click **"Sign Up"**
3. Choose **"Continue with GitHub"**
4. Authorize Vercel to access your GitHub account

#### Step 3: Import Your Repository

1. Click **"Add New Project"**
2. Select **"Import Git Repository"**
3. Find your repository in the list and click **"Import"**

#### Step 4: Configure Build Settings

Vercel auto-detects Vite projects, but verify these settings:

```
Framework Preset:   Vite
Build Command:      npm run build
Output Directory:   dist
Install Command:    npm install
```

#### Step 5: Add Environment Variables (if needed)

If your app uses environment variables (like API URLs):

```
VITE_API_URL = https://my-backend.onrender.com/api
```

> **Important:** In Vite, frontend environment variables must start with `VITE_` to be included in the build.

#### Step 6: Click "Deploy"

Vercel will:
1. Clone your repository
2. Run `npm install`
3. Run `npm run build`
4. Deploy the `/dist` folder to its global CDN

#### Step 7: Your App is Live

You will get a URL like:

```
https://my-portfolio-abc123.vercel.app
```

### Deployment Flow Diagram

```
+----------+      git push      +----------+      build       +--------+
|  Your    | =================> |  GitHub  | ===============> | Vercel |
|  Code    |                    |  Repo    |   (automatic)    | CDN    |
+----------+                    +----------+                  +--------+
                                                                  |
                                                                  v
                                                          +---------------+
                                                          | Your app is   |
                                                          | live at       |
                                                          | myapp.vercel  |
                                                          | .app          |
                                                          +---------------+
```

### Connecting a Custom Domain

1. Go to your project on Vercel dashboard
2. Click **Settings** > **Domains**
3. Type your domain: `myportfolio.com`
4. Vercel gives you DNS records to add at your domain registrar
5. Add the records (usually an A record or CNAME)
6. Wait for DNS propagation (can take up to 48 hours, usually minutes)

---

## 5. Frontend Deployment on Netlify

**Netlify** is another excellent platform for deploying frontend applications, very similar to Vercel.

### Step-by-Step: Deploy to Netlify

#### Step 1: Sign Up

1. Go to [netlify.com](https://www.netlify.com)
2. Click **"Sign up"** > **"GitHub"**

#### Step 2: Add New Site

1. Click **"Add new site"** > **"Import an existing project"**
2. Choose **GitHub** as the Git provider
3. Select your repository

#### Step 3: Configure Build Settings

```
Branch to deploy:    main
Build command:       npm run build
Publish directory:   dist
```

#### Step 4: Set Environment Variables

Go to **Site settings** > **Environment variables** > **Add a variable**:

```
VITE_API_URL = https://my-backend.onrender.com/api
```

#### Step 5: Deploy

Click **"Deploy site"**. Your app will be live at:

```
https://random-name-abc123.netlify.app
```

#### Handling Client-Side Routing (React Router)

If you use React Router, you need to tell Netlify to redirect all routes to `index.html`. Create a `_redirects` file in your `public/` folder:

```
/*    /index.html   200
```

Or create a `netlify.toml` in your project root:

```toml
[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

### Vercel vs Netlify Comparison

| Feature | Vercel | Netlify |
|---|---|---|
| Free tier | 100 deployments/day | 300 build minutes/month |
| Auto HTTPS | Yes | Yes |
| Custom domains | Yes | Yes |
| Preview deploys | Yes | Yes |
| Serverless functions | Yes (API routes) | Yes (Netlify Functions) |
| Best for | Next.js, Vite, React | Any static site, Gatsby |

---

## 6. Backend Deployment on Render

**Render** is the best free platform for deploying Node.js/Express backends. It replaced Heroku as the go-to free backend hosting.

### Why Render?

- Free tier available for web services
- Automatic deployments from GitHub
- Easy environment variable management
- Built-in HTTPS
- Supports Node.js, Python, Go, and more

### Step-by-Step: Deploy an Express App to Render

#### Step 1: Prepare Your Express App

Make sure your `server.js` (or `index.js`) listens on the correct port:

```javascript
// server.js
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');
require('dotenv').config();

const app = express();

// Middleware
app.use(cors());
app.use(express.json());

// Routes
app.use('/api/posts', require('./routes/posts'));
app.use('/api/auth', require('./routes/auth'));

// Health check route
app.get('/', (req, res) => {
  res.json({ message: 'API is running' });
});

// IMPORTANT: Use process.env.PORT for production
const PORT = process.env.PORT || 5000;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

> **Critical:** Always use `process.env.PORT`. Render assigns its own port -- you cannot hardcode it.

#### Step 2: Add a `start` Script

In your `package.json`, make sure you have:

```json
{
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  }
}
```

> **Note:** Do NOT use `nodemon` in the start script. Nodemon is a development tool only.

#### Step 3: Push to GitHub

```bash
git add .
git commit -m "Prepare for deployment"
git push origin main
```

#### Step 4: Create a Render Account

1. Go to [render.com](https://render.com)
2. Sign up with GitHub

#### Step 5: Create a New Web Service

1. Click **"New"** > **"Web Service"**
2. Connect your GitHub repository
3. Configure:

```
Name:             my-portfolio-api
Runtime:          Node
Branch:           main
Build Command:    npm install
Start Command:    node server.js
Plan:             Free
```

#### Step 6: Add Environment Variables

Click **"Environment"** and add:

```
MONGODB_URI = mongodb+srv://user:pass@cluster.mongodb.net/mydb
JWT_SECRET = your_super_secret_key_here
NODE_ENV = production
```

#### Step 7: Deploy

Click **"Create Web Service"**. Render will build and deploy your app.

Your backend will be live at:

```
https://my-portfolio-api.onrender.com
```

### Important Note About Render Free Tier

Render's free tier **spins down** your service after 15 minutes of inactivity. The first request after inactivity takes 30-50 seconds (cold start). This is normal for the free tier.

### Full MERN Deployment Architecture

```
+------------------+         +-------------------+         +-----------------+
|    FRONTEND      |  API    |     BACKEND       |  Query  |    DATABASE     |
|                  | Calls   |                   |         |                 |
|  React + Vite    |-------->|  Express + Node   |-------->|  MongoDB Atlas  |
|  Deployed on     |         |  Deployed on      |         |  (Cloud)        |
|  Vercel          |<--------|  Render           |<--------|                 |
|                  |  JSON   |                   |  Data   |                 |
+------------------+         +-------------------+         +-----------------+
  myapp.vercel.app          myapi.onrender.com         cluster0.mongodb.net
```

---

## 7. Backend Deployment on Railway

**Railway** is a modern alternative to Render with a developer-friendly experience. It offers a usage-based pricing model with a free trial.

### Quick Deployment Steps

1. Go to [railway.app](https://railway.app) and sign up with GitHub
2. Click **"New Project"** > **"Deploy from GitHub repo"**
3. Select your Express repository
4. Railway auto-detects Node.js and configures the build
5. Add environment variables in the **Variables** tab
6. Railway generates a public URL for your service

### Railway vs Render

| Feature | Render | Railway |
|---|---|---|
| Free tier | Yes (with cold starts) | Trial credits ($5) |
| Cold starts | Yes (free tier) | No |
| Auto deploy | Yes | Yes |
| Custom domains | Yes | Yes |
| Databases | External (Atlas) | Built-in Postgres, Redis, MongoDB |

Railway is excellent if you want a database and backend hosted in the same place, but for beginners, Render + MongoDB Atlas is the standard free approach.

---

## 8. MongoDB Atlas for Production Database

In development, you may have used a local MongoDB installation (`mongodb://localhost:27017`). In production, you need a cloud-hosted database. **MongoDB Atlas** is the official cloud service.

### Step-by-Step: Set Up MongoDB Atlas

#### Step 1: Create an Atlas Account

1. Go to [mongodb.com/atlas](https://www.mongodb.com/atlas)
2. Sign up for free

#### Step 2: Create a Cluster

1. Click **"Build a Cluster"**
2. Choose the **Free Tier (M0)**
3. Select a cloud provider (AWS is recommended)
4. Choose the region closest to your users
5. Click **"Create Cluster"**

#### Step 3: Create a Database User

1. Go to **Database Access** in the sidebar
2. Click **"Add New Database User"**
3. Choose **Password** authentication
4. Enter a username and a strong password
5. Set permissions to **"Read and write to any database"**

> **Important:** Do NOT use special characters (`@`, `#`, `%`) in your password. They cause connection string issues.

#### Step 4: Whitelist IP Addresses

1. Go to **Network Access**
2. Click **"Add IP Address"**
3. For production, click **"Allow Access from Anywhere"** (`0.0.0.0/0`)

> **Note:** Allowing all IPs is acceptable because your database is still protected by the username/password. For higher security, whitelist only your server's IP.

#### Step 5: Get the Connection String

1. Go to **Database** > **Connect**
2. Choose **"Connect your application"**
3. Copy the connection string:

```
mongodb+srv://myuser:mypassword@cluster0.abc123.mongodb.net/myPortfolioDB?retryWrites=true&w=majority
```

4. Replace `<password>` with your actual password
5. Add your database name after the `/`

#### Step 6: Use in Your Express App

```javascript
// server.js
const mongoose = require('mongoose');

mongoose.connect(process.env.MONGODB_URI)
  .then(() => console.log('Connected to MongoDB Atlas'))
  .catch(err => console.error('MongoDB connection error:', err));
```

### Local vs Atlas Connection

```
DEVELOPMENT                          PRODUCTION
+-------------------+                +-------------------+
| mongodb://         |                | mongodb+srv://    |
| localhost:27017/   |                | user:pass@        |
| mydb               |                | cluster0.abc123   |
|                    |                | .mongodb.net/mydb |
+-------------------+                +-------------------+
   Your computer                       MongoDB Cloud
   (only you)                          (accessible globally)
```

---

## 9. Environment Variables in Production

Environment variables store sensitive information (API keys, database passwords, secrets) outside your code. **Never hardcode secrets in your source code.**

### The Golden Rule

```
+------------------------------------------------------+
|                                                      |
|   NEVER commit your .env file to GitHub.             |
|   NEVER hardcode passwords, API keys, or secrets.    |
|                                                      |
+------------------------------------------------------+
```

### .env File (Development Only)

```env
# .env -- THIS FILE IS IN .gitignore
MONGODB_URI=mongodb://localhost:27017/mydb
JWT_SECRET=my_dev_secret_123
PORT=5000
VITE_API_URL=http://localhost:5000/api
```

### .gitignore Must Include:

```
# .gitignore
node_modules/
.env
.env.local
.env.production
```

### Setting Environment Variables on Each Platform

#### Vercel (Frontend)

1. Go to **Project Settings** > **Environment Variables**
2. Add variables with the `VITE_` prefix:

```
Name:   VITE_API_URL
Value:  https://my-api.onrender.com/api
```

#### Render (Backend)

1. Go to your service **Dashboard** > **Environment**
2. Add each variable:

```
MONGODB_URI  =  mongodb+srv://user:pass@cluster.mongodb.net/mydb
JWT_SECRET   =  a_very_long_random_string_here
NODE_ENV     =  production
```

### How Environment Variables Flow

```
+-----------+       +------------------+       +------------------+
|  .env     |       | Vercel Dashboard |       | Render Dashboard |
|  (local)  |       | (frontend vars)  |       | (backend vars)   |
+-----------+       +------------------+       +------------------+
     |                      |                         |
     v                      v                         v
 Your laptop          Vercel's servers          Render's servers
 (development)         (production)             (production)

THE SAME CODE reads process.env.VARIABLE_NAME in all environments.
The VALUE changes based on WHERE the code is running.
```

---

## 10. HTTPS and SSL Basics

### What is HTTPS?

**HTTPS** (HyperText Transfer Protocol Secure) is the secure version of HTTP. It encrypts all data sent between the browser and the server.

### Real-Life Analogy

- **HTTP** is like sending a postcard. Anyone who handles it (mail carriers, sorting facilities) can read what is written on it.
- **HTTPS** is like sending a sealed, locked envelope. Only the intended recipient has the key to open it.

### What is SSL/TLS?

**SSL** (Secure Sockets Layer) and its successor **TLS** (Transport Layer Security) are the encryption protocols that make HTTPS work. When people say "SSL certificate," they usually mean a TLS certificate.

### How HTTPS Works (Simplified)

```
+--------+                              +--------+
| Browser|                              | Server |
+--------+                              +--------+
    |                                        |
    |  1. "Hello, I want a secure           |
    |      connection"                       |
    |--------------------------------------->|
    |                                        |
    |  2. "Here is my SSL certificate        |
    |      and my public key"                |
    |<---------------------------------------|
    |                                        |
    |  3. Browser verifies the certificate   |
    |     is valid and trusted               |
    |                                        |
    |  4. Browser creates a session key,     |
    |     encrypts it with the public key,   |
    |     and sends it                       |
    |--------------------------------------->|
    |                                        |
    |  5. Both sides now have the session    |
    |     key. ALL further communication     |
    |     is encrypted.                      |
    |<======================================>|
    |         (Encrypted channel)            |
```

### Do You Need to Set Up SSL Manually?

**No.** All modern hosting platforms (Vercel, Netlify, Render, Railway) provide **free automatic HTTPS** via Let's Encrypt certificates. Your app will be served over HTTPS by default.

### Why HTTPS Matters

1. **Security** -- Protects user data (passwords, credit cards)
2. **SEO** -- Google ranks HTTPS sites higher
3. **Trust** -- Browsers show a padlock icon; without HTTPS, they show "Not Secure"
4. **Required** -- Many browser APIs (geolocation, camera, notifications) only work over HTTPS

---

## 11. Summary

Deployment is the final step that brings your application from your local machine to the world. Here is a quick reference of everything covered:

### Deployment Checklist

```
+-------------------------------------------------------+
|              DEPLOYMENT CHECKLIST                      |
+-------------------------------------------------------+
|                                                       |
|  [ ] Code pushed to GitHub                            |
|  [ ] .env file is in .gitignore                       |
|  [ ] No hardcoded secrets in code                     |
|  [ ] Frontend builds successfully (npm run build)     |
|  [ ] Backend uses process.env.PORT                    |
|  [ ] MongoDB Atlas cluster created                    |
|  [ ] Database user created with password              |
|  [ ] Network access configured (IP whitelist)         |
|  [ ] Connection string saved as env variable          |
|  [ ] Frontend deployed to Vercel or Netlify           |
|  [ ] Backend deployed to Render or Railway            |
|  [ ] Environment variables set on all platforms       |
|  [ ] CORS configured for production frontend URL      |
|  [ ] App tested on live URLs                          |
|  [ ] Custom domain connected (optional)               |
|                                                       |
+-------------------------------------------------------+
```

### Quick Reference

| What | Where | URL Pattern |
|---|---|---|
| Frontend | Vercel | `myapp.vercel.app` |
| Frontend | Netlify | `myapp.netlify.app` |
| Backend | Render | `myapi.onrender.com` |
| Backend | Railway | `myapi.up.railway.app` |
| Database | MongoDB Atlas | `cluster0.abc123.mongodb.net` |

### Key Takeaways

1. **Deployment makes your app accessible to the world** -- it is not optional if you want users.
2. **Frontend and backend are deployed separately** in a MERN stack.
3. **Environment variables** keep your secrets safe -- never commit `.env` files.
4. **HTTPS is automatic** on modern platforms -- you do not need to configure it manually.
5. **MongoDB Atlas** replaces your local database for production.
6. **DNS** translates human-readable domain names into server IP addresses.
7. **Every git push triggers a new deployment** when properly configured.

---

*Next week, we will explore advanced deployment topics including CI/CD, Docker, and performance optimization.*
