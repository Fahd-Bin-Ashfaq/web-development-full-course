# Tools & Setup Guide — Complete Installation Reference

This guide lists **every tool, platform, and extension** you will need throughout the 10-month MERN stack course. Install them **only when needed** — each tool is listed with the week it is first required.

---

## Week 1 — HTML Phase

### 1. Google Chrome (Browser)

- **What:** The recommended browser for web development
- **Why:** Best developer tools (DevTools) for inspecting and debugging
- **Download:** https://www.google.com/chrome/
- **Setup:** Install and set as default browser

### 2. Visual Studio Code (Code Editor)

- **What:** Free, lightweight code editor by Microsoft
- **Why:** Most popular editor for web development with thousands of extensions
- **Download:** https://code.visualstudio.com/
- **Setup:**
  1. Download for your operating system (Windows/Mac/Linux)
  2. Run the installer
  3. Check "Add to PATH" during installation (Windows)
  4. Launch VS Code

### 3. VS Code Extensions (Install from VS Code)

Open VS Code → Click Extensions icon (left sidebar) → Search and install:

| Extension | Purpose | Install in Week |
|-----------|---------|-----------------|
| **Live Server** | Auto-reload HTML pages in browser | Week 1 |
| **Prettier** | Auto-format your code | Week 1 |
| **Auto Rename Tag** | Renames matching HTML tags automatically | Week 1 |
| **HTML CSS Support** | CSS class name autocomplete in HTML | Week 1 |
| **ESLint** | JavaScript error detection | Week 9 |
| **Tailwind CSS IntelliSense** | Tailwind class autocomplete | Week 14 |
| **ES7+ React Snippets** | React component shortcuts | Week 16 |
| **Thunder Client** | API testing inside VS Code (Postman alternative) | Week 24 |
| **MongoDB for VS Code** | Browse MongoDB databases inside VS Code | Week 28 |
| **GitLens** | Enhanced Git features | Week 13 |

**How to install extensions:**
1. Open VS Code
2. Press `Ctrl + Shift + X` (Windows) or `Cmd + Shift + X` (Mac)
3. Search for the extension name
4. Click **Install**

---

## Week 9 — JavaScript Phase

### 4. Node.js (JavaScript Runtime)

- **What:** Allows JavaScript to run outside the browser (on your computer/server)
- **Why:** Required for npm, React, Express, and everything from Week 9 onwards
- **Download:** https://nodejs.org/ (choose **LTS** version — Long Term Support)
- **Setup:**
  1. Download the LTS version for your OS
  2. Run the installer (keep all defaults checked)
  3. Restart your terminal after installation
  4. Verify installation:

```bash
node -v       # Should show something like v20.x.x
npm -v        # Should show something like 10.x.x
```

> **Important:** npm (Node Package Manager) is installed automatically with Node.js. You do NOT need to install npm separately.

---

## Week 13 — Git & GitHub

### 5. Git (Version Control)

- **What:** Version control system to track code changes
- **Why:** Essential for collaboration, backup, and deployment
- **Download:** https://git-scm.com/downloads
- **Setup:**
  1. Download for your OS
  2. Run installer (keep defaults, select VS Code as default editor)
  3. Verify installation:

```bash
git --version    # Should show something like git version 2.x.x
```

  4. Configure your identity:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### 6. GitHub Account

- **What:** Online platform to store and share your Git repositories
- **Why:** Portfolio showcase, collaboration, deployment
- **Sign up:** https://github.com/ (free account)
- **Setup:**
  1. Create an account
  2. Verify your email
  3. Create your first repository
  4. (Optional) Set up SSH key for passwordless access

---

## Week 14 — Tailwind CSS

### 7. Tailwind CSS

- **What:** Utility-first CSS framework
- **Why:** Rapid UI development with pre-built classes
- **Install:** Via npm (no separate download needed)

```bash
# CDN for learning (add to HTML <head>)
# <script src="https://cdn.tailwindcss.com"></script>

# Production setup with Vite (covered in Week 14 Notes)
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

---

## Week 16 — React Phase

### 8. Vite (React Project Tool)

- **What:** Fast build tool for modern web projects
- **Why:** Creates React projects quickly, fast hot reload
- **Install:** Via npm (no separate download)

```bash
npm create vite@latest my-app -- --template react
cd my-app
npm install
npm run dev
```

> **Note:** You do NOT need to install Create React App (CRA). Vite is the modern recommended approach.

---

## Week 22 — Backend Phase

### 9. Nodemon (Auto-Restart Server)

- **What:** Automatically restarts Node.js server when files change
- **Why:** No need to manually stop and restart the server during development
- **Install:**

```bash
npm install -D nodemon
```

Add to `package.json` scripts:

```json
{
  "scripts": {
    "dev": "nodemon server.js",
    "start": "node server.js"
  }
}
```

---

## Week 24 — Express & API Testing

### 10. Postman (API Testing Tool)

- **What:** Application to test API endpoints (send requests, view responses)
- **Why:** Test your backend without building a frontend first
- **Download:** https://www.postman.com/downloads/
- **Setup:**
  1. Download and install
  2. Create a free account (or use without account)
  3. Create a new collection for your project
  4. Add requests (GET, POST, PUT, DELETE) to test your API

**Alternative:** Use **Thunder Client** extension inside VS Code (no separate app needed)
- Install from VS Code Extensions → Search "Thunder Client" → Install

---

## Week 28 — MongoDB Phase

### 11. MongoDB Community Server (Local Database)

- **What:** The database engine that runs on your computer
- **Why:** Store data locally during development
- **Download:** https://www.mongodb.com/try/download/community
- **Setup:**
  1. Download the MSI installer (Windows) or DMG (Mac)
  2. Run installer → Choose "Complete" installation
  3. Check "Install MongoDB as a Service" (Windows)
  4. Verify installation:

```bash
mongod --version    # Should show the version number
```

> **Note on Windows:** If `mongod` is not recognized, add MongoDB's `bin` folder to your system PATH:
> `C:\Program Files\MongoDB\Server\7.0\bin`

### 12. MongoDB Compass (GUI for MongoDB)

- **What:** Visual interface to browse and manage MongoDB databases
- **Why:** See your data, run queries, and manage collections without command line
- **Download:** https://www.mongodb.com/try/download/compass
- **Setup:**
  1. Download and install
  2. Open Compass
  3. Connect to `mongodb://localhost:27017` (local)
  4. Browse databases, collections, and documents visually

### 13. MongoDB Atlas (Cloud Database)

- **What:** MongoDB hosted in the cloud (free tier available)
- **Why:** Required for production deployment — your deployed app needs an online database
- **Sign up:** https://www.mongodb.com/cloud/atlas/register (free)
- **Setup:**
  1. Create a free account
  2. Create a new cluster (choose FREE tier — M0 Sandbox)
  3. Choose a cloud provider and region (any is fine for learning)
  4. Create a database user (username + password)
  5. Add your IP address to the whitelist (or allow access from anywhere: `0.0.0.0/0`)
  6. Click "Connect" → "Connect your application"
  7. Copy the connection string:

```
mongodb+srv://username:password@cluster0.abc123.mongodb.net/myDatabase?retryWrites=true&w=majority
```

  8. Replace `username`, `password`, and `myDatabase` with your values
  9. Store this in your `.env` file as `MONGO_URI`

---

## Week 37 — Deployment Phase

### 14. Vercel (Frontend Hosting)

- **What:** Free hosting platform for frontend/React applications
- **Why:** Automatic deployments from GitHub, free SSL, fast CDN
- **Sign up:** https://vercel.com/ (sign in with GitHub)
- **Deploy:**
  1. Push your React project to GitHub
  2. Go to vercel.com → "New Project"
  3. Import your GitHub repository
  4. Vercel auto-detects Vite/React and configures build settings
  5. Click "Deploy"
  6. Your site is live at `your-project.vercel.app`

### 15. Render (Backend Hosting)

- **What:** Free hosting platform for backend/Node.js applications
- **Why:** Easy Express.js deployment, free tier available
- **Sign up:** https://render.com/ (sign in with GitHub)
- **Deploy:**
  1. Push your Express project to GitHub
  2. Go to render.com → "New" → "Web Service"
  3. Connect your GitHub repository
  4. Set build command: `npm install`
  5. Set start command: `node server.js`
  6. Add environment variables (MONGO_URI, JWT_SECRET, etc.)
  7. Click "Create Web Service"
  8. Your API is live at `your-app.onrender.com`

### 16. Netlify (Alternative Frontend Hosting)

- **What:** Another free frontend hosting platform
- **Why:** Drag-and-drop deploy option, form handling, serverless functions
- **Sign up:** https://www.netlify.com/ (sign in with GitHub)

---

## Quick Reference: When to Install What

| Week | Tool | Type | Required |
|------|------|------|----------|
| **Week 1** | Google Chrome | Browser | Yes |
| **Week 1** | VS Code | Code Editor | Yes |
| **Week 1** | Live Server (extension) | VS Code Extension | Yes |
| **Week 1** | Prettier (extension) | VS Code Extension | Recommended |
| **Week 9** | Node.js + npm | Runtime | Yes |
| **Week 9** | ESLint (extension) | VS Code Extension | Recommended |
| **Week 13** | Git | Version Control | Yes |
| **Week 13** | GitHub account | Platform | Yes |
| **Week 14** | Tailwind IntelliSense (extension) | VS Code Extension | Recommended |
| **Week 16** | ES7+ React Snippets (extension) | VS Code Extension | Recommended |
| **Week 22** | Nodemon | npm package | Recommended |
| **Week 24** | Postman or Thunder Client | API Testing | Yes |
| **Week 28** | MongoDB Community Server | Database | Yes |
| **Week 28** | MongoDB Compass | GUI Tool | Recommended |
| **Week 28** | MongoDB Atlas account | Cloud Database | Yes (for deployment) |
| **Week 37** | Vercel account | Hosting | Yes |
| **Week 37** | Render account | Hosting | Yes |

---

## Troubleshooting Common Installation Issues

| Problem | Solution |
|---------|----------|
| `node` not recognized | Restart terminal, or add Node.js to PATH |
| `git` not recognized | Restart terminal, or add Git to PATH |
| `mongod` not recognized | Add MongoDB `bin` folder to system PATH |
| npm permission errors (Mac/Linux) | Use `sudo npm install -g` or fix npm permissions |
| VS Code extension not working | Reload VS Code window (`Ctrl+Shift+P` → "Reload Window") |
| MongoDB Compass can't connect | Make sure MongoDB service is running |
| Port already in use | Kill the process using that port, or change the port number |
| CORS errors in browser | Install and configure `cors` package in Express |

---

**Install tools only when you reach the relevant week. Do not install everything at once.**
