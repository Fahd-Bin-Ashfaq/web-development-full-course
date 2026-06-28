# Week 35 — MERN Project Part 1

> **Prerequisites:** Week 28-34 (MongoDB, Mongoose, Express.js, React, MERN Stack Integration, Authentication in MERN, Advanced Features)
> **Goal:** Plan, design, and build the foundation of a full-stack MERN application from scratch — covering project planning, database schema design, backend API development, frontend scaffolding, and connecting the two layers together.

---

## Table of Contents

1. [Project Planning](#1-project-planning)
2. [Wireframing and Feature List](#2-wireframing-and-feature-list)
3. [Database Schema Design](#3-database-schema-design)
4. [Setting Up Project Structure](#4-setting-up-project-structure)
5. [Building the Backend: Models, Routes, Controllers, Middleware](#5-building-the-backend-models-routes-controllers-middleware)
6. [Building the Frontend: Pages, Components, Routing](#6-building-the-frontend-pages-components-routing)
7. [Connecting Frontend to Backend](#7-connecting-frontend-to-backend)
8. [Summary of Part 1 Progress](#8-summary-of-part-1-progress)

---

## 1. Project Planning

Before writing a single line of code, every professional project begins with **planning**. This phase determines what you are building, why you are building it, and how the pieces will fit together.

> Think of building a software project like **building a house**. No construction crew shows up with bricks and cement on day one. First, an architect draws a **blueprint** — a detailed plan that shows every room, door, window, and pipe. The blueprint answers critical questions before construction begins: How many rooms? Where does the plumbing go? What materials are needed? Without a blueprint, you end up tearing down walls and redoing work. A software project without planning suffers the same fate — wasted time, broken features, and frustrating rewrites.

### Choosing a Project

For a MERN stack capstone project, three common choices stand out. Each teaches different concepts and presents different levels of complexity.

### Project Comparison Table

| Feature / Aspect         | Blog Platform              | Task Manager               | E-Commerce Store            |
|--------------------------|----------------------------|----------------------------|-----------------------------|
| **User Authentication**  | Yes (author accounts)      | Yes (personal tasks)       | Yes (buyer + seller)        |
| **CRUD Operations**      | Posts, Comments             | Tasks, Categories          | Products, Orders, Cart      |
| **Relationships**        | User -> Posts -> Comments   | User -> Tasks, Categories  | User -> Orders -> Products  |
| **File Uploads**         | Cover images               | Optional attachments       | Product images (multiple)   |
| **Real-Time Features**   | Optional (live comments)   | Optional (notifications)   | Cart updates, stock alerts  |
| **Payment Integration**  | No                         | No                         | Yes (Stripe, PayPal)        |
| **Complexity Level**     | Medium                     | Medium                     | High                        |
| **Time to Build**        | 2-3 weeks                  | 2-3 weeks                  | 4-6 weeks                   |
| **Learning Value**       | High                       | High                       | Very High                   |
| **Best For**             | Content-focused apps       | Productivity apps          | Transaction-based apps      |

### Why Task Manager?

We will use a **Task Manager** application as our primary project throughout this week and the next. Here is why:

1. **Balanced complexity** — complex enough to teach real patterns, simple enough to complete in two weeks
2. **Core CRUD** — every feature maps to create, read, update, or delete operations
3. **Authentication** — users must sign up, log in, and manage their own tasks
4. **Relationships** — tasks belong to users and can be organized into categories
5. **Filtering and sorting** — tasks have status, priority, and due dates to query against
6. **Extensible** — easy to add features like notifications, drag-and-drop, or collaboration later

### Planning Features Before Coding

Before opening your code editor, answer these questions:

```
  PLANNING CHECKLIST
  +----------------------------------------------------------+
  |                                                            |
  |  1. WHO are the users?                                     |
  |     --> Individuals managing personal tasks                |
  |                                                            |
  |  2. WHAT can users do?                                     |
  |     --> Register, login, create/edit/delete tasks,         |
  |         organize by category, filter by status             |
  |                                                            |
  |  3. WHAT data do we store?                                 |
  |     --> Users, Tasks, Categories                           |
  |                                                            |
  |  4. HOW do users interact?                                 |
  |     --> Web browser (React frontend)                       |
  |                                                            |
  |  5. WHAT is the tech stack?                                |
  |     --> MongoDB + Express + React + Node.js (MERN)         |
  |                                                            |
  +----------------------------------------------------------+
```

### The Planning Workflow

```
  IDEA
    |
    v
  +------------------+     +------------------+     +------------------+
  | Define Features  | --> | Design Database  | --> | Plan API Routes  |
  | (what it does)   |     | (how data is     |     | (how frontend    |
  |                  |     |  structured)     |     |  talks to backend)|
  +------------------+     +------------------+     +------------------+
    |                                                        |
    v                                                        v
  +------------------+     +------------------+     +------------------+
  | Wireframe UI     | --> | Build Backend    | --> | Build Frontend   |
  | (how it looks)   |     | (server + API)   |     | (React app)      |
  +------------------+     +------------------+     +------------------+
                                                             |
                                                             v
                                                    +------------------+
                                                    | Connect & Test   |
                                                    | (integration)    |
                                                    +------------------+
```

---

## 2. Wireframing and Feature List

**Wireframing** is the process of creating simple visual sketches of your application's pages. These are not polished designs — they are rough layouts that show where elements will go.

> Think of wireframes like the **floor plan** of your house. The floor plan does not show paint colors or furniture styles — it simply shows where each room is, how big it is, and where the doors and windows go. Similarly, a wireframe shows the layout of buttons, forms, and content areas without worrying about colors, fonts, or final styling.

### Wireframe: Home Page

```
  +----------------------------------------------------------+
  |  LOGO          Home   Login   Register                    |
  +----------------------------------------------------------+
  |                                                            |
  |              Welcome to TaskFlow                           |
  |      Organize your life, one task at a time.              |
  |                                                            |
  |              [ Get Started ]   [ Learn More ]              |
  |                                                            |
  +----------------------------------------------------------+
  |                                                            |
  |   +----------------+  +----------------+  +-------------+ |
  |   |  Create Tasks  |  |  Organize      |  | Track       | |
  |   |  Quickly add   |  |  Use categories|  | Monitor     | |
  |   |  tasks with    |  |  to group your |  | progress    | |
  |   |  priorities    |  |  work          |  | with status | |
  |   +----------------+  +----------------+  +-------------+ |
  |                                                            |
  +----------------------------------------------------------+
  |  Footer: (c) 2025 TaskFlow. All rights reserved.          |
  +----------------------------------------------------------+
```

### Wireframe: Login Page

```
  +----------------------------------------------------------+
  |  LOGO          Home   Login   Register                    |
  +----------------------------------------------------------+
  |                                                            |
  |                  +------------------------+                |
  |                  |     Login to TaskFlow  |                |
  |                  |                        |                |
  |                  |  Email:                |                |
  |                  |  [ ________________ ] |                |
  |                  |                        |                |
  |                  |  Password:             |                |
  |                  |  [ ________________ ] |                |
  |                  |                        |                |
  |                  |  [ Login Button     ]  |                |
  |                  |                        |                |
  |                  |  Don't have an account?|                |
  |                  |  Register here         |                |
  |                  +------------------------+                |
  |                                                            |
  +----------------------------------------------------------+
```

### Wireframe: Dashboard Page

```
  +----------------------------------------------------------+
  |  LOGO     Dashboard   Create Task   Profile   Logout      |
  +----------------------------------------------------------+
  |                                                            |
  |  Welcome, Ali!              Total: 12  Done: 5  Pending: 7|
  |                                                            |
  |  Filter: [All v]  Status: [All v]  Priority: [All v]     |
  |                                                            |
  |  +------------------------------------------------------+ |
  |  | [ ] Build login page       | High   | In Progress     | |
  |  |     Due: Jan 20, 2025      | Web Dev |                 | |
  |  +------------------------------------------------------+ |
  |  | [x] Design database schema | Medium | Completed       | |
  |  |     Due: Jan 18, 2025      | Web Dev |                 | |
  |  +------------------------------------------------------+ |
  |  | [ ] Write API tests        | Low    | Pending         | |
  |  |     Due: Jan 25, 2025      | Testing |                 | |
  |  +------------------------------------------------------+ |
  |  | [ ] Deploy to production   | High   | Pending         | |
  |  |     Due: Feb 01, 2025      | DevOps  |                 | |
  |  +------------------------------------------------------+ |
  |                                                            |
  |  [  < Previous  ]                [  Next >  ]             |
  |                                                            |
  +----------------------------------------------------------+
```

### Wireframe: Create Task Page

```
  +----------------------------------------------------------+
  |  LOGO     Dashboard   Create Task   Profile   Logout      |
  +----------------------------------------------------------+
  |                                                            |
  |           +----------------------------------+             |
  |           |       Create New Task            |             |
  |           |                                  |             |
  |           |  Title:                          |             |
  |           |  [ __________________________ ] |             |
  |           |                                  |             |
  |           |  Description:                    |             |
  |           |  [ __________________________ ] |             |
  |           |  [ __________________________ ] |             |
  |           |  [ __________________________ ] |             |
  |           |                                  |             |
  |           |  Priority:     Status:           |             |
  |           |  [ High v ]    [ Pending v ]     |             |
  |           |                                  |             |
  |           |  Category:     Due Date:         |             |
  |           |  [ Web Dev v ] [ 2025-01-20  ]   |             |
  |           |                                  |             |
  |           |  [ Create Task ]   [ Cancel ]    |             |
  |           +----------------------------------+             |
  |                                                            |
  +----------------------------------------------------------+
```

### Feature List by Priority

Features should be organized by priority to ensure the most important functionality is built first.

| Priority         | Feature                          | Description                                      |
|------------------|----------------------------------|--------------------------------------------------|
| **Must-Have**    | User Registration                | Sign up with name, email, and password           |
| **Must-Have**    | User Login / Logout              | Authenticate with JWT tokens                     |
| **Must-Have**    | Create Task                      | Add a new task with title, description, priority  |
| **Must-Have**    | View All Tasks                   | Display a list of user's tasks on the dashboard  |
| **Must-Have**    | Edit Task                        | Update task details (title, status, priority)    |
| **Must-Have**    | Delete Task                      | Remove a task permanently                        |
| **Must-Have**    | Task Status                      | Mark tasks as Pending, In Progress, or Completed |
| **Must-Have**    | Protected Routes                 | Only logged-in users can access the dashboard    |
| **Nice-to-Have** | Categories                       | Organize tasks into custom categories            |
| **Nice-to-Have** | Filter by Status                 | Show only Pending, In Progress, or Completed     |
| **Nice-to-Have** | Filter by Priority               | Show only High, Medium, or Low priority tasks    |
| **Nice-to-Have** | Search Tasks                     | Search tasks by title or description             |
| **Nice-to-Have** | Due Date with Reminders          | Set deadlines and highlight overdue tasks        |
| **Future**       | Drag-and-Drop Kanban Board       | Reorder tasks visually across status columns     |
| **Future**       | Team Collaboration               | Share tasks with other users                     |
| **Future**       | File Attachments                 | Attach files or images to tasks                  |
| **Future**       | Email Notifications              | Send email when a task is due                    |
| **Future**       | Dark Mode                        | Toggle between light and dark themes             |

### User Stories

User stories describe features from the perspective of the end user. They follow a standard format:

**As a [type of user], I want to [action], so that [benefit].**

| #  | User Story                                                                                 |
|----|--------------------------------------------------------------------------------------------|
| 1  | As a new user, I want to register an account so that I can start managing my tasks.        |
| 2  | As a registered user, I want to log in so that I can access my personal dashboard.         |
| 3  | As a logged-in user, I want to create a task so that I can track what needs to be done.    |
| 4  | As a logged-in user, I want to view all my tasks so that I can see my workload at a glance.|
| 5  | As a logged-in user, I want to edit a task so that I can update its status or details.     |
| 6  | As a logged-in user, I want to delete a task so that I can remove completed or irrelevant items.|
| 7  | As a logged-in user, I want to filter tasks by status so that I can focus on what matters. |
| 8  | As a logged-in user, I want to categorize tasks so that I can organize my work logically.  |
| 9  | As a logged-in user, I want to log out so that my account stays secure on shared devices.  |

---

## 3. Database Schema Design

The database schema defines **what data** your application stores and **how different data entities relate** to each other. Getting this right early prevents painful migrations later.

> Think of a database schema like the **organizational chart** of a company. It defines the departments (collections), the roles within each department (fields), and how departments communicate with each other (relationships). A poorly designed org chart leads to confusion and bottlenecks — a poorly designed schema leads to slow queries and data inconsistencies.

### Entity-Relationship Diagram

```
  +---------------------+          +-------------------------+
  |       USER          |          |        CATEGORY         |
  +---------------------+          +-------------------------+
  | _id     : ObjectId  |          | _id      : ObjectId     |
  | name    : String    |<---+     | name     : String       |
  | email   : String    |    |     | color    : String       |
  | password: String    |    +-----| user     : ObjectId ref |
  | role    : String    |    |     | createdAt: Date         |
  | createdAt: Date     |    |     +-------------------------+
  | updatedAt: Date     |    |
  +---------------------+    |
         |                   |
         | One User has      |
         | many Tasks        |
         |                   |
         v                   |
  +-------------------------+|
  |         TASK             ||
  +-------------------------+|
  | _id        : ObjectId   ||
  | title      : String     ||
  | description: String     ||
  | status     : String     ||
  | priority   : String     ||
  | dueDate    : Date       ||
  | user       : ObjectId --+  (references USER)
  | category   : ObjectId ---> (references CATEGORY)
  | createdAt  : Date       |
  | updatedAt  : Date       |
  +-------------------------+
```

### Relationship Summary

| Relationship          | Type         | Description                                    |
|-----------------------|--------------|------------------------------------------------|
| User -> Task          | One-to-Many  | One user can have many tasks                   |
| User -> Category      | One-to-Many  | One user can create many categories            |
| Task -> Category      | Many-to-One  | Many tasks can belong to one category          |
| Task -> User          | Many-to-One  | Many tasks belong to one user                  |

### User Model

The User model stores account information and authentication credentials.

```javascript
// server/models/User.js

const mongoose = require("mongoose");
const bcrypt = require("bcryptjs");

const userSchema = new mongoose.Schema(
  {
    name: {
      type: String,
      required: [true, "Name is required"],
      trim: true,
      minlength: [2, "Name must be at least 2 characters"],
      maxlength: [50, "Name cannot exceed 50 characters"],
    },
    email: {
      type: String,
      required: [true, "Email is required"],
      unique: true,
      trim: true,
      lowercase: true,
      match: [
        /^\w([.-]?\w+)*@\w([.-]?\w+)*(\.\w{2,3})+$/,
        "Please provide a valid email address",
      ],
    },
    password: {
      type: String,
      required: [true, "Password is required"],
      minlength: [6, "Password must be at least 6 characters"],
      select: false, // Do not return password in queries by default
    },
    role: {
      type: String,
      enum: ["user", "admin"],
      default: "user",
    },
  },
  {
    timestamps: true, // Adds createdAt and updatedAt automatically
  }
);

// Hash password before saving
userSchema.pre("save", async function (next) {
  if (!this.isModified("password")) return next();
  const salt = await bcrypt.genSalt(10);
  this.password = await bcrypt.hash(this.password, salt);
  next();
});

// Compare entered password with hashed password
userSchema.methods.comparePassword = async function (enteredPassword) {
  return await bcrypt.compare(enteredPassword, this.password);
};

module.exports = mongoose.model("User", userSchema);
```

### Task Model

The Task model is the core of our application — it stores everything about a task.

```javascript
// server/models/Task.js

const mongoose = require("mongoose");

const taskSchema = new mongoose.Schema(
  {
    title: {
      type: String,
      required: [true, "Task title is required"],
      trim: true,
      maxlength: [100, "Title cannot exceed 100 characters"],
    },
    description: {
      type: String,
      trim: true,
      maxlength: [500, "Description cannot exceed 500 characters"],
      default: "",
    },
    status: {
      type: String,
      enum: ["pending", "in-progress", "completed"],
      default: "pending",
    },
    priority: {
      type: String,
      enum: ["low", "medium", "high"],
      default: "medium",
    },
    dueDate: {
      type: Date,
      default: null,
    },
    user: {
      type: mongoose.Schema.Types.ObjectId,
      ref: "User",
      required: [true, "Task must belong to a user"],
    },
    category: {
      type: mongoose.Schema.Types.ObjectId,
      ref: "Category",
      default: null,
    },
  },
  {
    timestamps: true,
  }
);

// Index for faster queries — users frequently query their own tasks
taskSchema.index({ user: 1, status: 1 });
taskSchema.index({ user: 1, priority: 1 });
taskSchema.index({ user: 1, dueDate: 1 });

module.exports = mongoose.model("Task", taskSchema);
```

### Category Model

Categories let users organize tasks into logical groups.

```javascript
// server/models/Category.js

const mongoose = require("mongoose");

const categorySchema = new mongoose.Schema(
  {
    name: {
      type: String,
      required: [true, "Category name is required"],
      trim: true,
      maxlength: [30, "Category name cannot exceed 30 characters"],
    },
    color: {
      type: String,
      default: "#6366f1", // Default indigo color
      match: [/^#([A-Fa-f0-9]{6})$/, "Please provide a valid hex color"],
    },
    user: {
      type: mongoose.Schema.Types.ObjectId,
      ref: "User",
      required: [true, "Category must belong to a user"],
    },
  },
  {
    timestamps: true,
  }
);

// Ensure a user cannot create two categories with the same name
categorySchema.index({ user: 1, name: 1 }, { unique: true });

module.exports = mongoose.model("Category", categorySchema);
```

### How Relationships Work

```
  USER: Ali (ObjectId: "abc123")
    |
    |-- creates --> CATEGORY: "Web Dev" (user: "abc123")
    |-- creates --> CATEGORY: "Personal" (user: "abc123")
    |
    |-- creates --> TASK: "Build login page"
    |                 user: "abc123"
    |                 category: (ObjectId of "Web Dev")
    |
    |-- creates --> TASK: "Buy groceries"
    |                 user: "abc123"
    |                 category: (ObjectId of "Personal")
    |
    v
  When Ali logs in, we query:
    Task.find({ user: "abc123" })
  This returns ONLY Ali's tasks, not anyone else's.
```

---

## 4. Setting Up Project Structure

A well-organized folder structure keeps your code maintainable as the project grows. We will set up a **monorepo-style** structure with separate `client/` and `server/` directories under one root folder.

> Think of your project structure like the **departments in a building**. The building (root folder) has a clear floor plan: the marketing team (frontend) works on one floor, the operations team (backend) works on another, and shared resources (configuration files) sit at the reception desk (root). Everyone knows where to find things because the building is logically organized.

### Complete Folder Structure

```
  taskflow/
  |
  |-- client/                        # React frontend
  |   |-- public/
  |   |   |-- index.html
  |   |   |-- favicon.ico
  |   |
  |   |-- src/
  |   |   |-- components/            # Reusable UI components
  |   |   |   |-- Navbar.jsx
  |   |   |   |-- Footer.jsx
  |   |   |   |-- TaskCard.jsx
  |   |   |   |-- LoadingSpinner.jsx
  |   |   |   |-- PrivateRoute.jsx
  |   |   |
  |   |   |-- pages/                 # Full page components
  |   |   |   |-- Home.jsx
  |   |   |   |-- Login.jsx
  |   |   |   |-- Register.jsx
  |   |   |   |-- Dashboard.jsx
  |   |   |   |-- CreateTask.jsx
  |   |   |   |-- EditTask.jsx
  |   |   |
  |   |   |-- services/              # API call functions
  |   |   |   |-- api.js
  |   |   |   |-- authService.js
  |   |   |   |-- taskService.js
  |   |   |
  |   |   |-- context/               # React Context for state
  |   |   |   |-- AuthContext.jsx
  |   |   |
  |   |   |-- App.jsx
  |   |   |-- main.jsx
  |   |   |-- index.css
  |   |
  |   |-- package.json
  |   |-- vite.config.js
  |
  |-- server/                        # Express backend
  |   |-- config/
  |   |   |-- db.js                  # MongoDB connection
  |   |
  |   |-- controllers/
  |   |   |-- authController.js
  |   |   |-- taskController.js
  |   |   |-- categoryController.js
  |   |
  |   |-- middleware/
  |   |   |-- authMiddleware.js
  |   |   |-- errorMiddleware.js
  |   |
  |   |-- models/
  |   |   |-- User.js
  |   |   |-- Task.js
  |   |   |-- Category.js
  |   |
  |   |-- routes/
  |   |   |-- authRoutes.js
  |   |   |-- taskRoutes.js
  |   |   |-- categoryRoutes.js
  |   |
  |   |-- server.js                  # Entry point
  |   |-- package.json
  |
  |-- .gitignore
  |-- .env
  |-- package.json                   # Root package.json (scripts)
  |-- README.md
```

### Step 1: Initialize the Root Project

```bash
# Create the project folder
mkdir taskflow
cd taskflow

# Initialize root package.json
npm init -y
```

### Step 2: Set Up the Backend

```bash
# Create the server directory and navigate into it
mkdir server
cd server

# Initialize package.json for the server
npm init -y

# Install backend dependencies
npm install express mongoose dotenv bcryptjs jsonwebtoken cors

# Install dev dependencies
npm install --save-dev nodemon
```

### Step 3: Set Up the Frontend

```bash
# Go back to root
cd ..

# Create React app with Vite
npm create vite@latest client -- --template react

# Navigate into client and install dependencies
cd client
npm install

# Install additional frontend packages
npm install axios react-router-dom react-icons react-toastify
```

### Step 4: Root package.json with Concurrent Scripts

Install `concurrently` so you can start both the frontend and backend with a single command.

```bash
# In the root directory
cd ..
npm install --save-dev concurrently
```

Edit the root `package.json`:

```json
{
  "name": "taskflow",
  "version": "1.0.0",
  "description": "A full-stack MERN task manager application",
  "scripts": {
    "server": "cd server && npm run dev",
    "client": "cd client && npm run dev",
    "dev": "concurrently \"npm run server\" \"npm run client\"",
    "install-all": "npm install && cd server && npm install && cd ../client && npm install",
    "build": "cd client && npm run build"
  },
  "devDependencies": {
    "concurrently": "^8.2.0"
  }
}
```

Add a dev script to the server's `package.json`:

```json
{
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  }
}
```

### Step 5: Environment Variables

Create a `.env` file in the root directory:

```env
# Server Configuration
PORT=5000
NODE_ENV=development

# MongoDB Connection
MONGO_URI=mongodb+srv://yourUsername:yourPassword@cluster0.xxxxx.mongodb.net/taskflow?retryWrites=true&w=majority

# JWT Secret (use a long, random string in production)
JWT_SECRET=your_super_secret_jwt_key_change_this_in_production
JWT_EXPIRE=30d
```

### Step 6: Git Ignore Configuration

Create a `.gitignore` file in the root directory:

```gitignore
# Dependencies
node_modules/
client/node_modules/
server/node_modules/

# Environment variables (NEVER commit these)
.env
.env.local
.env.production

# Build output
client/dist/
client/build/

# OS files
.DS_Store
Thumbs.db

# IDE files
.vscode/
.idea/

# Logs
*.log
npm-debug.log*
```

### Starting the Application

```
  Terminal Command: npm run dev
  +----------------------------------------------------------+
  |                                                            |
  |  concurrently runs TWO processes simultaneously:           |
  |                                                            |
  |  +------------------------+  +-------------------------+  |
  |  |  SERVER (Express)      |  |  CLIENT (React + Vite)  |  |
  |  |  Port: 5000            |  |  Port: 5173             |  |
  |  |  nodemon server.js     |  |  vite dev server        |  |
  |  |  Watches for changes   |  |  Hot Module Replacement |  |
  |  +------------------------+  +-------------------------+  |
  |                                                            |
  +----------------------------------------------------------+
```

---

## 5. Building the Backend: Models, Routes, Controllers, Middleware

The backend is the **engine** of our application. It handles data storage, business logic, authentication, and exposes an API for the frontend to consume.

### The MVC Pattern

We organize our backend code using the **MVC (Model-View-Controller)** pattern. In a REST API context, the "View" is replaced by JSON responses sent to the frontend.

> Think of MVC like a **restaurant**. The **Model** is the kitchen — it knows how to prepare and store food (data). The **Controller** is the waiter — it takes orders from customers (requests), asks the kitchen to prepare the food, and delivers it to the table (response). The **Routes** are the menu — they list what the restaurant offers and direct orders to the right waiter.

```
  THE MVC PATTERN IN A REST API
  +----------------------------------------------------------+
  |                                                            |
  |  CLIENT (React)                                            |
  |     |                                                      |
  |     | HTTP Request (GET /api/tasks)                        |
  |     v                                                      |
  |  ROUTES  ------>  Which endpoint was requested?            |
  |     |              (authRoutes, taskRoutes, etc.)           |
  |     v                                                      |
  |  MIDDLEWARE ----> Is the user authenticated?               |
  |     |              (authMiddleware, errorMiddleware)        |
  |     v                                                      |
  |  CONTROLLER --->  What logic should run?                   |
  |     |              (getTasks, createTask, etc.)             |
  |     v                                                      |
  |  MODEL --------> What data should be read/written?         |
  |     |              (Task.find(), Task.create(), etc.)       |
  |     v                                                      |
  |  DATABASE -----> MongoDB stores/retrieves the data         |
  |     |                                                      |
  |     v                                                      |
  |  JSON RESPONSE -> Sent back to the client                  |
  |                                                            |
  +----------------------------------------------------------+
```

### Database Connection

```javascript
// server/config/db.js

const mongoose = require("mongoose");

const connectDB = async () => {
  try {
    const conn = await mongoose.connect(process.env.MONGO_URI);
    console.log(`MongoDB Connected: ${conn.connection.host}`);
  } catch (error) {
    console.error(`Error: ${error.message}`);
    process.exit(1); // Exit process with failure
  }
};

module.exports = connectDB;
```

### Server Entry Point

```javascript
// server/server.js

const express = require("express");
const dotenv = require("dotenv");
const cors = require("cors");
const connectDB = require("./config/db");
const { errorHandler } = require("./middleware/errorMiddleware");

// Load environment variables
dotenv.config({ path: "../.env" });

// Connect to MongoDB
connectDB();

const app = express();

// Middleware
app.use(cors());
app.use(express.json()); // Parse JSON request bodies
app.use(express.urlencoded({ extended: false })); // Parse URL-encoded bodies

// Routes
app.use("/api/auth", require("./routes/authRoutes"));
app.use("/api/tasks", require("./routes/taskRoutes"));
app.use("/api/categories", require("./routes/categoryRoutes"));

// Health check route
app.get("/api/health", (req, res) => {
  res.json({ status: "OK", message: "TaskFlow API is running" });
});

// Error handling middleware (must be after routes)
app.use(errorHandler);

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => {
  console.log(`Server running in ${process.env.NODE_ENV} mode on port ${PORT}`);
});
```

### Auth Controller

```javascript
// server/controllers/authController.js

const User = require("../models/User");
const jwt = require("jsonwebtoken");

// Generate JWT Token
const generateToken = (id) => {
  return jwt.sign({ id }, process.env.JWT_SECRET, {
    expiresIn: process.env.JWT_EXPIRE,
  });
};

// @desc    Register a new user
// @route   POST /api/auth/register
// @access  Public
const register = async (req, res, next) => {
  try {
    const { name, email, password } = req.body;

    // Check if user already exists
    const userExists = await User.findOne({ email });
    if (userExists) {
      res.status(400);
      throw new Error("User already exists with this email");
    }

    // Create the user
    const user = await User.create({ name, email, password });

    // Respond with user data and token
    res.status(201).json({
      success: true,
      data: {
        _id: user._id,
        name: user.name,
        email: user.email,
        role: user.role,
        token: generateToken(user._id),
      },
    });
  } catch (error) {
    next(error);
  }
};

// @desc    Login user
// @route   POST /api/auth/login
// @access  Public
const login = async (req, res, next) => {
  try {
    const { email, password } = req.body;

    // Check if email and password are provided
    if (!email || !password) {
      res.status(400);
      throw new Error("Please provide email and password");
    }

    // Find user and include password field
    const user = await User.findOne({ email }).select("+password");

    if (!user) {
      res.status(401);
      throw new Error("Invalid email or password");
    }

    // Check if password matches
    const isMatch = await user.comparePassword(password);

    if (!isMatch) {
      res.status(401);
      throw new Error("Invalid email or password");
    }

    // Respond with user data and token
    res.json({
      success: true,
      data: {
        _id: user._id,
        name: user.name,
        email: user.email,
        role: user.role,
        token: generateToken(user._id),
      },
    });
  } catch (error) {
    next(error);
  }
};

// @desc    Get current logged-in user
// @route   GET /api/auth/me
// @access  Private
const getMe = async (req, res, next) => {
  try {
    const user = await User.findById(req.user.id);

    res.json({
      success: true,
      data: user,
    });
  } catch (error) {
    next(error);
  }
};

module.exports = { register, login, getMe };
```

### Task Controller

```javascript
// server/controllers/taskController.js

const Task = require("../models/Task");

// @desc    Get all tasks for logged-in user
// @route   GET /api/tasks
// @access  Private
const getTasks = async (req, res, next) => {
  try {
    // Build query object
    const query = { user: req.user.id };

    // Optional filters from query parameters
    if (req.query.status) query.status = req.query.status;
    if (req.query.priority) query.priority = req.query.priority;
    if (req.query.category) query.category = req.query.category;

    // Find tasks with optional sorting
    const sortBy = req.query.sortBy || "-createdAt"; // Default: newest first

    const tasks = await Task.find(query)
      .populate("category", "name color")
      .sort(sortBy);

    res.json({
      success: true,
      count: tasks.length,
      data: tasks,
    });
  } catch (error) {
    next(error);
  }
};

// @desc    Get a single task by ID
// @route   GET /api/tasks/:id
// @access  Private
const getTask = async (req, res, next) => {
  try {
    const task = await Task.findById(req.params.id).populate(
      "category",
      "name color"
    );

    if (!task) {
      res.status(404);
      throw new Error("Task not found");
    }

    // Ensure the task belongs to the logged-in user
    if (task.user.toString() !== req.user.id) {
      res.status(403);
      throw new Error("Not authorized to access this task");
    }

    res.json({
      success: true,
      data: task,
    });
  } catch (error) {
    next(error);
  }
};

// @desc    Create a new task
// @route   POST /api/tasks
// @access  Private
const createTask = async (req, res, next) => {
  try {
    // Add the logged-in user's ID to the request body
    req.body.user = req.user.id;

    const task = await Task.create(req.body);

    res.status(201).json({
      success: true,
      data: task,
    });
  } catch (error) {
    next(error);
  }
};

// @desc    Update a task
// @route   PUT /api/tasks/:id
// @access  Private
const updateTask = async (req, res, next) => {
  try {
    let task = await Task.findById(req.params.id);

    if (!task) {
      res.status(404);
      throw new Error("Task not found");
    }

    // Ensure the task belongs to the logged-in user
    if (task.user.toString() !== req.user.id) {
      res.status(403);
      throw new Error("Not authorized to update this task");
    }

    task = await Task.findByIdAndUpdate(req.params.id, req.body, {
      new: true, // Return the updated document
      runValidators: true, // Run schema validators on update
    });

    res.json({
      success: true,
      data: task,
    });
  } catch (error) {
    next(error);
  }
};

// @desc    Delete a task
// @route   DELETE /api/tasks/:id
// @access  Private
const deleteTask = async (req, res, next) => {
  try {
    const task = await Task.findById(req.params.id);

    if (!task) {
      res.status(404);
      throw new Error("Task not found");
    }

    // Ensure the task belongs to the logged-in user
    if (task.user.toString() !== req.user.id) {
      res.status(403);
      throw new Error("Not authorized to delete this task");
    }

    await task.deleteOne();

    res.json({
      success: true,
      data: {},
      message: "Task removed successfully",
    });
  } catch (error) {
    next(error);
  }
};

module.exports = { getTasks, getTask, createTask, updateTask, deleteTask };
```

### Category Controller

```javascript
// server/controllers/categoryController.js

const Category = require("../models/Category");

// @desc    Get all categories for logged-in user
// @route   GET /api/categories
// @access  Private
const getCategories = async (req, res, next) => {
  try {
    const categories = await Category.find({ user: req.user.id }).sort("name");

    res.json({
      success: true,
      count: categories.length,
      data: categories,
    });
  } catch (error) {
    next(error);
  }
};

// @desc    Create a new category
// @route   POST /api/categories
// @access  Private
const createCategory = async (req, res, next) => {
  try {
    req.body.user = req.user.id;

    const category = await Category.create(req.body);

    res.status(201).json({
      success: true,
      data: category,
    });
  } catch (error) {
    next(error);
  }
};

// @desc    Delete a category
// @route   DELETE /api/categories/:id
// @access  Private
const deleteCategory = async (req, res, next) => {
  try {
    const category = await Category.findById(req.params.id);

    if (!category) {
      res.status(404);
      throw new Error("Category not found");
    }

    if (category.user.toString() !== req.user.id) {
      res.status(403);
      throw new Error("Not authorized to delete this category");
    }

    await category.deleteOne();

    res.json({
      success: true,
      data: {},
      message: "Category removed successfully",
    });
  } catch (error) {
    next(error);
  }
};

module.exports = { getCategories, createCategory, deleteCategory };
```

### Auth Routes

```javascript
// server/routes/authRoutes.js

const express = require("express");
const router = express.Router();
const { register, login, getMe } = require("../controllers/authController");
const { protect } = require("../middleware/authMiddleware");

router.post("/register", register);
router.post("/login", login);
router.get("/me", protect, getMe);

module.exports = router;
```

### Task Routes

```javascript
// server/routes/taskRoutes.js

const express = require("express");
const router = express.Router();
const {
  getTasks,
  getTask,
  createTask,
  updateTask,
  deleteTask,
} = require("../controllers/taskController");
const { protect } = require("../middleware/authMiddleware");

// All task routes require authentication
router.use(protect);

router.route("/").get(getTasks).post(createTask);
router.route("/:id").get(getTask).put(updateTask).delete(deleteTask);

module.exports = router;
```

### Category Routes

```javascript
// server/routes/categoryRoutes.js

const express = require("express");
const router = express.Router();
const {
  getCategories,
  createCategory,
  deleteCategory,
} = require("../controllers/categoryController");
const { protect } = require("../middleware/authMiddleware");

router.use(protect);

router.route("/").get(getCategories).post(createCategory);
router.route("/:id").delete(deleteCategory);

module.exports = router;
```

### Auth Middleware

```javascript
// server/middleware/authMiddleware.js

const jwt = require("jsonwebtoken");
const User = require("../models/User");

const protect = async (req, res, next) => {
  let token;

  // Check for token in the Authorization header
  if (
    req.headers.authorization &&
    req.headers.authorization.startsWith("Bearer")
  ) {
    try {
      // Extract token from "Bearer <token>"
      token = req.headers.authorization.split(" ")[1];

      // Verify token
      const decoded = jwt.verify(token, process.env.JWT_SECRET);

      // Attach user to request (excluding password)
      req.user = await User.findById(decoded.id).select("-password");

      next();
    } catch (error) {
      res.status(401);
      throw new Error("Not authorized — token is invalid or expired");
    }
  }

  if (!token) {
    res.status(401);
    throw new Error("Not authorized — no token provided");
  }
};

module.exports = { protect };
```

### Error Handling Middleware

```javascript
// server/middleware/errorMiddleware.js

const errorHandler = (err, req, res, next) => {
  // If status code is 200 (default), change it to 500
  let statusCode = res.statusCode === 200 ? 500 : res.statusCode;
  let message = err.message;

  // Handle Mongoose bad ObjectId errors
  if (err.name === "CastError" && err.kind === "ObjectId") {
    statusCode = 404;
    message = "Resource not found";
  }

  // Handle Mongoose duplicate key errors
  if (err.code === 11000) {
    statusCode = 400;
    const field = Object.keys(err.keyValue)[0];
    message = `Duplicate value for field: ${field}`;
  }

  // Handle Mongoose validation errors
  if (err.name === "ValidationError") {
    statusCode = 400;
    message = Object.values(err.errors)
      .map((val) => val.message)
      .join(", ");
  }

  res.status(statusCode).json({
    success: false,
    message: message,
    stack: process.env.NODE_ENV === "production" ? null : err.stack,
  });
};

module.exports = { errorHandler };
```

### API Routes Summary

| Method   | Endpoint              | Description               | Access  |
|----------|-----------------------|---------------------------|---------|
| `POST`   | `/api/auth/register`  | Register a new user       | Public  |
| `POST`   | `/api/auth/login`     | Login and get token       | Public  |
| `GET`    | `/api/auth/me`        | Get current user profile  | Private |
| `GET`    | `/api/tasks`          | Get all user's tasks      | Private |
| `GET`    | `/api/tasks/:id`      | Get a single task         | Private |
| `POST`   | `/api/tasks`          | Create a new task         | Private |
| `PUT`    | `/api/tasks/:id`      | Update a task             | Private |
| `DELETE` | `/api/tasks/:id`      | Delete a task             | Private |
| `GET`    | `/api/categories`     | Get all user's categories | Private |
| `POST`   | `/api/categories`     | Create a new category     | Private |
| `DELETE` | `/api/categories/:id` | Delete a category         | Private |

---

## 6. Building the Frontend: Pages, Components, Routing

The frontend is what users see and interact with. We will use **React** with **Vite** as the build tool, **React Router** for navigation, and a clean component-based architecture.

### Component Tree

```
  App.jsx
  |
  |-- <Navbar />                     (shown on every page)
  |
  |-- <Routes>
  |     |
  |     |-- "/" ---------> <Home />
  |     |-- "/login" ----> <Login />
  |     |-- "/register" -> <Register />
  |     |
  |     |-- (Protected Routes)
  |     |     |-- "/dashboard" -----> <Dashboard />
  |     |     |     |-- <TaskCard />  (repeated for each task)
  |     |     |
  |     |     |-- "/create-task" ---> <CreateTask />
  |     |     |-- "/edit-task/:id" -> <EditTask />
  |     |
  |-- <Footer />                     (shown on every page)
  |
  |-- <LoadingSpinner />             (shown during API calls)
```

### React Router Setup

```jsx
// client/src/App.jsx

import { BrowserRouter as Router, Routes, Route } from "react-router-dom";
import Navbar from "./components/Navbar";
import Footer from "./components/Footer";
import PrivateRoute from "./components/PrivateRoute";
import Home from "./pages/Home";
import Login from "./pages/Login";
import Register from "./pages/Register";
import Dashboard from "./pages/Dashboard";
import CreateTask from "./pages/CreateTask";
import EditTask from "./pages/EditTask";
import { AuthProvider } from "./context/AuthContext";
import { ToastContainer } from "react-toastify";
import "react-toastify/dist/ReactToastify.css";

function App() {
  return (
    <AuthProvider>
      <Router>
        <div className="app">
          <Navbar />
          <main className="container">
            <Routes>
              {/* Public Routes */}
              <Route path="/" element={<Home />} />
              <Route path="/login" element={<Login />} />
              <Route path="/register" element={<Register />} />

              {/* Protected Routes */}
              <Route
                path="/dashboard"
                element={
                  <PrivateRoute>
                    <Dashboard />
                  </PrivateRoute>
                }
              />
              <Route
                path="/create-task"
                element={
                  <PrivateRoute>
                    <CreateTask />
                  </PrivateRoute>
                }
              />
              <Route
                path="/edit-task/:id"
                element={
                  <PrivateRoute>
                    <EditTask />
                  </PrivateRoute>
                }
              />
            </Routes>
          </main>
          <Footer />
        </div>
        <ToastContainer position="top-right" autoClose={3000} />
      </Router>
    </AuthProvider>
  );
}

export default App;
```

### Navbar Component

```jsx
// client/src/components/Navbar.jsx

import { Link, useNavigate } from "react-router-dom";
import { useAuth } from "../context/AuthContext";

function Navbar() {
  const { user, logout } = useAuth();
  const navigate = useNavigate();

  const handleLogout = () => {
    logout();
    navigate("/login");
  };

  return (
    <nav className="navbar">
      <div className="navbar-brand">
        <Link to="/">TaskFlow</Link>
      </div>
      <ul className="navbar-links">
        {user ? (
          <>
            <li>
              <Link to="/dashboard">Dashboard</Link>
            </li>
            <li>
              <Link to="/create-task">Create Task</Link>
            </li>
            <li>
              <span>Hello, {user.name}</span>
            </li>
            <li>
              <button onClick={handleLogout} className="btn btn-logout">
                Logout
              </button>
            </li>
          </>
        ) : (
          <>
            <li>
              <Link to="/login">Login</Link>
            </li>
            <li>
              <Link to="/register">Register</Link>
            </li>
          </>
        )}
      </ul>
    </nav>
  );
}

export default Navbar;
```

### TaskCard Component

```jsx
// client/src/components/TaskCard.jsx

import { Link } from "react-router-dom";

function TaskCard({ task, onDelete }) {
  // Determine badge color based on priority
  const priorityColors = {
    high: "#ef4444",
    medium: "#f59e0b",
    low: "#22c55e",
  };

  // Determine badge color based on status
  const statusColors = {
    pending: "#6b7280",
    "in-progress": "#3b82f6",
    completed: "#22c55e",
  };

  // Format the due date for display
  const formatDate = (dateString) => {
    if (!dateString) return "No due date";
    return new Date(dateString).toLocaleDateString("en-US", {
      year: "numeric",
      month: "short",
      day: "numeric",
    });
  };

  return (
    <div className="task-card">
      <div className="task-card-header">
        <h3>{task.title}</h3>
        <span
          className="badge"
          style={{ backgroundColor: priorityColors[task.priority] }}
        >
          {task.priority}
        </span>
      </div>

      {task.description && (
        <p className="task-description">{task.description}</p>
      )}

      <div className="task-card-meta">
        <span
          className="badge"
          style={{ backgroundColor: statusColors[task.status] }}
        >
          {task.status}
        </span>
        <span className="due-date">Due: {formatDate(task.dueDate)}</span>
      </div>

      {task.category && (
        <span
          className="category-badge"
          style={{ borderColor: task.category.color }}
        >
          {task.category.name}
        </span>
      )}

      <div className="task-card-actions">
        <Link to={`/edit-task/${task._id}`} className="btn btn-edit">
          Edit
        </Link>
        <button
          onClick={() => onDelete(task._id)}
          className="btn btn-delete"
        >
          Delete
        </button>
      </div>
    </div>
  );
}

export default TaskCard;
```

### PrivateRoute Component

```jsx
// client/src/components/PrivateRoute.jsx

import { Navigate } from "react-router-dom";
import { useAuth } from "../context/AuthContext";
import LoadingSpinner from "./LoadingSpinner";

function PrivateRoute({ children }) {
  const { user, loading } = useAuth();

  if (loading) {
    return <LoadingSpinner />;
  }

  if (!user) {
    return <Navigate to="/login" />;
  }

  return children;
}

export default PrivateRoute;
```

### LoadingSpinner Component

```jsx
// client/src/components/LoadingSpinner.jsx

function LoadingSpinner() {
  return (
    <div className="spinner-container">
      <div className="spinner"></div>
      <p>Loading...</p>
    </div>
  );
}

export default LoadingSpinner;
```

### Auth Context

```jsx
// client/src/context/AuthContext.jsx

import { createContext, useContext, useState, useEffect } from "react";

const AuthContext = createContext();

export const AuthProvider = ({ children }) => {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  // Check localStorage for existing user on mount
  useEffect(() => {
    const storedUser = localStorage.getItem("user");
    if (storedUser) {
      setUser(JSON.parse(storedUser));
    }
    setLoading(false);
  }, []);

  // Login: save user to state and localStorage
  const login = (userData) => {
    setUser(userData);
    localStorage.setItem("user", JSON.stringify(userData));
  };

  // Logout: clear user from state and localStorage
  const logout = () => {
    setUser(null);
    localStorage.removeItem("user");
  };

  return (
    <AuthContext.Provider value={{ user, loading, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
};

// Custom hook for using the auth context
export const useAuth = () => {
  const context = useContext(AuthContext);
  if (!context) {
    throw new Error("useAuth must be used within an AuthProvider");
  }
  return context;
};
```

### Dashboard Page

```jsx
// client/src/pages/Dashboard.jsx

import { useState, useEffect } from "react";
import TaskCard from "../components/TaskCard";
import LoadingSpinner from "../components/LoadingSpinner";
import { getTasks, deleteTask } from "../services/taskService";
import { toast } from "react-toastify";

function Dashboard() {
  const [tasks, setTasks] = useState([]);
  const [loading, setLoading] = useState(true);
  const [filter, setFilter] = useState({
    status: "",
    priority: "",
  });

  // Fetch tasks on component mount and when filters change
  useEffect(() => {
    fetchTasks();
  }, [filter]);

  const fetchTasks = async () => {
    try {
      setLoading(true);
      const data = await getTasks(filter);
      setTasks(data);
    } catch (error) {
      toast.error("Failed to fetch tasks");
    } finally {
      setLoading(false);
    }
  };

  const handleDelete = async (taskId) => {
    if (window.confirm("Are you sure you want to delete this task?")) {
      try {
        await deleteTask(taskId);
        setTasks(tasks.filter((task) => task._id !== taskId));
        toast.success("Task deleted successfully");
      } catch (error) {
        toast.error("Failed to delete task");
      }
    }
  };

  if (loading) return <LoadingSpinner />;

  return (
    <div className="dashboard">
      <h1>My Tasks</h1>

      {/* Filter Controls */}
      <div className="filters">
        <select
          value={filter.status}
          onChange={(e) => setFilter({ ...filter, status: e.target.value })}
        >
          <option value="">All Statuses</option>
          <option value="pending">Pending</option>
          <option value="in-progress">In Progress</option>
          <option value="completed">Completed</option>
        </select>

        <select
          value={filter.priority}
          onChange={(e) => setFilter({ ...filter, priority: e.target.value })}
        >
          <option value="">All Priorities</option>
          <option value="high">High</option>
          <option value="medium">Medium</option>
          <option value="low">Low</option>
        </select>
      </div>

      {/* Task Stats */}
      <div className="task-stats">
        <span>Total: {tasks.length}</span>
        <span>
          Completed: {tasks.filter((t) => t.status === "completed").length}
        </span>
        <span>
          Pending: {tasks.filter((t) => t.status === "pending").length}
        </span>
      </div>

      {/* Task List */}
      {tasks.length === 0 ? (
        <p className="no-tasks">No tasks found. Create your first task!</p>
      ) : (
        <div className="task-list">
          {tasks.map((task) => (
            <TaskCard key={task._id} task={task} onDelete={handleDelete} />
          ))}
        </div>
      )}
    </div>
  );
}

export default Dashboard;
```

---

## 7. Connecting Frontend to Backend

The frontend and backend are separate applications that communicate over HTTP using a REST API. The frontend sends requests (using **axios**), and the backend responds with JSON data.

> Think of the frontend and backend like a **customer and a bank teller**. The customer (frontend) fills out a form and slides it through the window. The teller (backend) reads the form, checks the vault (database), and slides back the information. The window between them is the **API** — a standardized way to communicate. The customer does not need to know how the vault works, and the teller does not need to know what the customer will do with the information.

### API Service File (Axios Instance)

Creating a centralized axios instance ensures consistent configuration across all API calls — base URL, headers, and error handling in one place.

```javascript
// client/src/services/api.js

import axios from "axios";

// Create an axios instance with default configuration
const api = axios.create({
  baseURL: "http://localhost:5000/api",
  headers: {
    "Content-Type": "application/json",
  },
});

// Request Interceptor: attach token to every request
api.interceptors.request.use(
  (config) => {
    const user = JSON.parse(localStorage.getItem("user"));
    if (user && user.token) {
      config.headers.Authorization = `Bearer ${user.token}`;
    }
    return config;
  },
  (error) => {
    return Promise.reject(error);
  }
);

// Response Interceptor: handle common errors globally
api.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response) {
      // Server responded with an error status
      const message = error.response.data.message || "Something went wrong";

      // If token is expired or invalid, redirect to login
      if (error.response.status === 401) {
        localStorage.removeItem("user");
        window.location.href = "/login";
      }

      return Promise.reject(new Error(message));
    }

    // Network error (server is down)
    return Promise.reject(new Error("Network error — server may be offline"));
  }
);

export default api;
```

### How Interceptors Work

```
  OUTGOING REQUEST (Request Interceptor)
  +----------------------------------------------------------+
  |                                                            |
  |  Component calls: api.get("/tasks")                        |
  |       |                                                    |
  |       v                                                    |
  |  Request Interceptor runs BEFORE the request is sent       |
  |       |                                                    |
  |       +--> Reads token from localStorage                   |
  |       +--> Attaches: Authorization: "Bearer <token>"       |
  |       |                                                    |
  |       v                                                    |
  |  Actual HTTP request sent to http://localhost:5000/api      |
  |                                                            |
  +----------------------------------------------------------+

  INCOMING RESPONSE (Response Interceptor)
  +----------------------------------------------------------+
  |                                                            |
  |  Server responds with data or error                        |
  |       |                                                    |
  |       v                                                    |
  |  Response Interceptor runs BEFORE the component gets data  |
  |       |                                                    |
  |       +--> 200 OK? Pass the response through               |
  |       +--> 401 Unauthorized? Redirect to /login            |
  |       +--> 500 Error? Format error message                 |
  |       |                                                    |
  |       v                                                    |
  |  Component receives the processed response                 |
  |                                                            |
  +----------------------------------------------------------+
```

### Auth Service

```javascript
// client/src/services/authService.js

import api from "./api";

// Register a new user
export const registerUser = async (userData) => {
  const response = await api.post("/auth/register", userData);
  return response.data.data;
};

// Login an existing user
export const loginUser = async (credentials) => {
  const response = await api.post("/auth/login", credentials);
  return response.data.data;
};

// Get current user profile
export const getCurrentUser = async () => {
  const response = await api.get("/auth/me");
  return response.data.data;
};
```

### Task Service

```javascript
// client/src/services/taskService.js

import api from "./api";

// Get all tasks (with optional filters)
export const getTasks = async (filters = {}) => {
  // Build query string from filter object
  const params = new URLSearchParams();
  if (filters.status) params.append("status", filters.status);
  if (filters.priority) params.append("priority", filters.priority);
  if (filters.category) params.append("category", filters.category);
  if (filters.sortBy) params.append("sortBy", filters.sortBy);

  const response = await api.get(`/tasks?${params.toString()}`);
  return response.data.data;
};

// Get a single task by ID
export const getTask = async (taskId) => {
  const response = await api.get(`/tasks/${taskId}`);
  return response.data.data;
};

// Create a new task
export const createTask = async (taskData) => {
  const response = await api.post("/tasks", taskData);
  return response.data.data;
};

// Update an existing task
export const updateTask = async (taskId, taskData) => {
  const response = await api.put(`/tasks/${taskId}`, taskData);
  return response.data.data;
};

// Delete a task
export const deleteTask = async (taskId) => {
  const response = await api.delete(`/tasks/${taskId}`);
  return response.data;
};
```

### Example: Making API Calls from a Component

Here is a complete example of the Login page, showing how a component uses the service layer to interact with the backend.

```jsx
// client/src/pages/Login.jsx

import { useState } from "react";
import { useNavigate, Link } from "react-router-dom";
import { useAuth } from "../context/AuthContext";
import { loginUser } from "../services/authService";
import { toast } from "react-toastify";

function Login() {
  const [formData, setFormData] = useState({
    email: "",
    password: "",
  });
  const [loading, setLoading] = useState(false);

  const { login } = useAuth();
  const navigate = useNavigate();

  const handleChange = (e) => {
    setFormData({ ...formData, [e.target.name]: e.target.value });
  };

  const handleSubmit = async (e) => {
    e.preventDefault();

    // Basic validation
    if (!formData.email || !formData.password) {
      toast.error("Please fill in all fields");
      return;
    }

    try {
      setLoading(true);
      const userData = await loginUser(formData);
      login(userData); // Save to context and localStorage
      toast.success("Login successful!");
      navigate("/dashboard");
    } catch (error) {
      toast.error(error.message);
    } finally {
      setLoading(false);
    }
  };

  return (
    <div className="auth-page">
      <form onSubmit={handleSubmit} className="auth-form">
        <h2>Login to TaskFlow</h2>

        <div className="form-group">
          <label htmlFor="email">Email</label>
          <input
            type="email"
            id="email"
            name="email"
            value={formData.email}
            onChange={handleChange}
            placeholder="Enter your email"
          />
        </div>

        <div className="form-group">
          <label htmlFor="password">Password</label>
          <input
            type="password"
            id="password"
            name="password"
            value={formData.password}
            onChange={handleChange}
            placeholder="Enter your password"
          />
        </div>

        <button type="submit" className="btn btn-primary" disabled={loading}>
          {loading ? "Logging in..." : "Login"}
        </button>

        <p className="auth-redirect">
          Do not have an account? <Link to="/register">Register here</Link>
        </p>
      </form>
    </div>
  );
}

export default Login;
```

### The Full Data Flow

```
  USER ACTION: Clicks "Login" button
  +----------------------------------------------------------+
  |                                                            |
  |  1. Login.jsx calls loginUser({ email, password })         |
  |       |                                                    |
  |       v                                                    |
  |  2. authService.js sends: api.post("/auth/login", data)   |
  |       |                                                    |
  |       v                                                    |
  |  3. api.js (axios instance) adds headers, sends request    |
  |       |                                                    |
  |       v                                                    |
  |  4. Express receives POST /api/auth/login                  |
  |       |                                                    |
  |       v                                                    |
  |  5. authRoutes.js directs to authController.login          |
  |       |                                                    |
  |       v                                                    |
  |  6. authController.js queries User.findOne({ email })      |
  |       |                                                    |
  |       v                                                    |
  |  7. MongoDB returns the user document                      |
  |       |                                                    |
  |       v                                                    |
  |  8. Controller compares passwords, generates JWT            |
  |       |                                                    |
  |       v                                                    |
  |  9. JSON response sent back: { token, user data }          |
  |       |                                                    |
  |       v                                                    |
  | 10. api.js response interceptor processes the response     |
  |       |                                                    |
  |       v                                                    |
  | 11. authService.js returns the data to Login.jsx           |
  |       |                                                    |
  |       v                                                    |
  | 12. Login.jsx calls login(userData) from AuthContext        |
  |       |                                                    |
  |       v                                                    |
  | 13. User state updated, token saved to localStorage        |
  |       |                                                    |
  |       v                                                    |
  | 14. navigate("/dashboard") redirects to the dashboard      |
  |                                                            |
  +----------------------------------------------------------+
```

### Handling Loading and Error States

Every API call should account for three states: **loading**, **success**, and **error**. Here is the pattern used consistently across the application:

```
  API CALL LIFECYCLE
  +----------------------------------------------------------+
  |                                                            |
  |  IDLE STATE                                                |
  |  loading: false, error: null, data: null                   |
  |       |                                                    |
  |       | User triggers action (click, form submit)          |
  |       v                                                    |
  |  LOADING STATE                                             |
  |  loading: true, error: null, data: null                    |
  |  --> Show spinner or disable button                        |
  |       |                                                    |
  |       +-------+-------+                                    |
  |       |               |                                    |
  |       v               v                                    |
  |  SUCCESS STATE    ERROR STATE                               |
  |  loading: false   loading: false                            |
  |  error: null      error: "message"                          |
  |  data: [...]      data: null                                |
  |  --> Show data    --> Show error toast                       |
  |                                                            |
  +----------------------------------------------------------+
```

---

## 8. Summary of Part 1 Progress

At this point, you have completed the foundational work for a full-stack MERN application. Here is a checklist of everything that should be in place.

### Part 1 Completion Checklist

| #  | Task                                      | Status       |
|----|-------------------------------------------|--------------|
| 1  | Project idea selected (Task Manager)      | Completed    |
| 2  | Features listed and prioritized           | Completed    |
| 3  | User stories written                      | Completed    |
| 4  | Wireframes sketched for all key pages     | Completed    |
| 5  | Database schema designed (User, Task, Category) | Completed |
| 6  | Mongoose models created with validation   | Completed    |
| 7  | Project folder structure set up           | Completed    |
| 8  | Backend dependencies installed            | Completed    |
| 9  | Frontend scaffolded with Vite             | Completed    |
| 10 | Root `package.json` with concurrent scripts | Completed  |
| 11 | `.env` file configured                    | Completed    |
| 12 | `.gitignore` file created                 | Completed    |
| 13 | MongoDB connection established            | Completed    |
| 14 | Express server entry point written        | Completed    |
| 15 | Auth controller (register, login, getMe)  | Completed    |
| 16 | Task controller (full CRUD)               | Completed    |
| 17 | Category controller (get, create, delete) | Completed    |
| 18 | Auth, Task, and Category routes defined   | Completed    |
| 19 | Auth middleware (JWT protection)          | Completed    |
| 20 | Error handling middleware                 | Completed    |
| 21 | React Router setup with public/private routes | Completed |
| 22 | AuthContext for global state management   | Completed    |
| 23 | Navbar, Footer, TaskCard, LoadingSpinner  | Completed    |
| 24 | API service layer (axios with interceptors) | Completed  |
| 25 | Auth and Task service files               | Completed    |
| 26 | Login page with full data flow            | Completed    |
| 27 | Dashboard page with filters and task list | Completed    |

### Architecture Overview

```
  +----------------------------------------------------------+
  |                  TASKFLOW APPLICATION                      |
  +----------------------------------------------------------+
  |                                                            |
  |  FRONTEND (React + Vite)         BACKEND (Express + Node) |
  |  Port: 5173                      Port: 5000               |
  |                                                            |
  |  +------------------------+     +------------------------+|
  |  | Pages                  |     | Routes                 ||
  |  |  Home, Login, Register |     |  /api/auth/*           ||
  |  |  Dashboard, CreateTask |     |  /api/tasks/*          ||
  |  |  EditTask              |     |  /api/categories/*     ||
  |  +------------------------+     +------------------------+|
  |           |                              |                 |
  |  +------------------------+     +------------------------+|
  |  | Components             |     | Controllers            ||
  |  |  Navbar, Footer        |     |  authController        ||
  |  |  TaskCard, Spinner     |     |  taskController        ||
  |  |  PrivateRoute          |     |  categoryController    ||
  |  +------------------------+     +------------------------+|
  |           |                              |                 |
  |  +------------------------+     +------------------------+|
  |  | Services               |     | Models (Mongoose)      ||
  |  |  api.js (axios)        |     |  User, Task, Category  ||
  |  |  authService.js        |     +------------------------+|
  |  |  taskService.js        |              |                 |
  |  +------------------------+     +------------------------+|
  |           |                     | Middleware              ||
  |  +------------------------+     |  authMiddleware        ||
  |  | Context                |     |  errorMiddleware       ||
  |  |  AuthContext           |     +------------------------+|
  |  +------------------------+              |                 |
  |                                 +------------------------+|
  |                                 | Database (MongoDB)     ||
  |                                 |  Collections:          ||
  |                                 |  users, tasks,         ||
  |                                 |  categories            ||
  |                                 +------------------------+|
  |                                                            |
  +----------------------------------------------------------+
```

### What Comes Next in Part 2

In **Week 36 — MERN Project Part 2**, you will complete the application by covering:

| Topic                                | Description                                            |
|--------------------------------------|--------------------------------------------------------|
| **Register Page**                    | Complete the user registration flow                    |
| **CreateTask and EditTask Pages**    | Build full forms with validation and API integration   |
| **Styling with CSS / Tailwind**      | Apply responsive, polished styling to all pages        |
| **Search and Advanced Filtering**    | Add search by title and multi-filter combinations      |
| **Task Statistics Dashboard**        | Display charts or counters for task completion rates    |
| **Profile Page**                     | Let users view and update their profile information    |
| **Testing the Full Application**     | End-to-end testing of all features with Postman        |
| **Bug Fixes and Polish**            | Handle edge cases, improve UX, and prepare for deploy  |

By the end of Part 2, you will have a **fully functional, production-ready MERN stack application** that you can deploy and add to your portfolio.
