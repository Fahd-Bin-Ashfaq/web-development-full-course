# Week 39: Final Project Part 1 — Portfolio Website with Blog

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Feature List](#2-feature-list)
3. [Tech Stack](#3-tech-stack)
4. [Wireframes](#4-wireframes)
5. [Database Schema Design](#5-database-schema-design)
6. [API Endpoints List](#6-api-endpoints-list)
7. [Project Folder Structure](#7-project-folder-structure)
8. [Building the Backend](#8-building-the-backend)
9. [Building the Frontend](#9-building-the-frontend)
10. [Part 1 Progress Checklist](#10-part-1-progress-checklist)

---

## 1. Project Overview

### What Are We Building?

We are building a **full-stack portfolio website with an integrated blog** -- the kind of website that professional developers use to showcase their work, share their knowledge, and attract employers or clients.

### Real-Life Analogy: Your Digital Storefront

Think of your portfolio website as your **professional storefront**:

- A physical shop has a window display (your **hero section**), product shelves (your **projects showcase**), a notice board (your **blog**), a suggestion box (your **contact form**), and a back office where the owner manages everything (your **admin panel**).
- Without a storefront, customers walk past without noticing you. Without a portfolio, employers skip your application without a second look.

```
THE DEVELOPER'S DIGITAL STOREFRONT
====================================

+--------------------------------------------------+
|                   YOUR PORTFOLIO                  |
|                                                   |
|   +----------+  +-----------+  +---------------+ |
|   |  WINDOW  |  |  PRODUCT  |  |    NOTICE     | |
|   | DISPLAY  |  |  SHELVES  |  |    BOARD      | |
|   | (Hero +  |  | (Projects |  |   (Blog       | |
|   |  About)  |  |  Gallery) |  |    Posts)     | |
|   +----------+  +-----------+  +---------------+ |
|                                                   |
|   +----------+  +------------------------------+ |
|   |SUGGESTION|  |        BACK OFFICE            | |
|   |   BOX    |  |     (Admin Panel --           | |
|   | (Contact |  |      manage posts,            | |
|   |   Form)  |  |      projects, messages)      | |
|   +----------+  +------------------------------+ |
+--------------------------------------------------+
```

### Why a Portfolio with a Blog?

When a hiring manager reviews candidates, they look at three things:

1. **Can you build things?** -- Your projects section answers this.
2. **Do you understand concepts?** -- Your blog posts answer this.
3. **Can I reach you?** -- Your contact form answers this.

A portfolio website that you built yourself proves all three at once. It is simultaneously the **resume**, the **proof of work**, and the **communication channel**.

### What Makes This Project Special?

This is not a tutorial project that you follow step by step and forget. This project combines **every skill** you have learned across 39 weeks:

- **HTML/CSS** (Weeks 1-8): Structure and styling
- **JavaScript** (Weeks 9-12): Logic and interactivity
- **Git/GitHub** (Week 13): Version control
- **Tailwind CSS** (Weeks 14-15): Utility-first styling
- **React** (Weeks 16-26): Component-based frontend
- **Node.js/Express** (Weeks 27-29): Backend server
- **MongoDB** (Weeks 30-31): Database
- **MERN Integration** (Weeks 32-36): Full-stack connection
- **Deployment** (Weeks 37-38): Launching to the world

```
YOUR 39-WEEK JOURNEY COMES TOGETHER HERE
==========================================

Week 1-4        Week 5-8       Week 9-12      Week 13
  HTML    -----> CSS    -----> JavaScript ---> Git
   |              |              |              |
   v              v              v              v
 Structure     Styling        Logic         Version Control
   |              |              |              |
   +------+-------+------+------+------+-------+
          |              |             |
          v              v             v
       Week 14-15    Week 16-26   Week 27-31
       Tailwind      React       Node+MongoDB
          |              |             |
          +------+-------+------+------+
                 |              |
                 v              v
             Week 32-36    Week 37-38
             MERN Stack    Deployment
                 |              |
                 +------+-------+
                        |
                        v
                   WEEK 39-40
              YOUR PORTFOLIO WEBSITE
               (Everything Combined)
```

---

## 2. Feature List

### Home Page

| Feature | Description | Why It Matters |
|---------|-------------|----------------|
| Hero Section | Large banner with your name, title, and a call-to-action button | First impression -- visitors decide in 3 seconds whether to stay |
| About Section | Short bio explaining who you are and what you do | Humanizes you beyond just code |
| Skills Section | Visual display of your technical skills | Lets employers quickly assess your fit |
| Featured Projects | Top 2-3 projects highlighted with images and links | Saves visitors time by showing your best work first |

### Projects Page

| Feature | Description | Why It Matters |
|---------|-------------|----------------|
| Project Grid | Cards showing all projects with thumbnails | Visual browsing is faster than reading lists |
| Project Details | Each project has description, tech stack, live URL, GitHub link | Employers want to see both the product and the code |
| Filter by Tech | Filter projects by technology used | Helps employers find relevant work quickly |

### Blog Page (CRUD)

| Feature | Description | Why It Matters |
|---------|-------------|----------------|
| **C**reate | Admin can write and publish new blog posts | Demonstrates your ability to explain concepts |
| **R**ead | Visitors can browse and read all published posts | Showcases your knowledge and communication skills |
| **U**pdate | Admin can edit existing posts | Shows real-world content management |
| **D**elete | Admin can remove outdated posts | Keeps the portfolio clean and current |
| Tags | Posts are categorized by topic (React, CSS, etc.) | Helps readers find relevant content |

### Contact Page

| Feature | Description | Why It Matters |
|---------|-------------|----------------|
| Contact Form | Name, email, and message fields with validation | Makes it easy for employers to reach you |
| Email Notification | Form submission triggers notification to your email | You never miss an opportunity |
| Success Feedback | User sees confirmation after sending | Professional user experience |

### Admin Panel

| Feature | Description | Why It Matters |
|---------|-------------|----------------|
| Login/Logout | Secure JWT-based authentication | Only you can manage content |
| Manage Posts | Create, edit, delete blog posts | Full content management |
| Manage Projects | Add, update, remove projects | Keep your portfolio current |
| View Messages | Read contact form submissions | Respond to inquiries |

### Responsive Design & Dark Mode

| Feature | Description | Why It Matters |
|---------|-------------|----------------|
| Mobile Layout | Adapts to screens 320px and up | Over 50% of web traffic is mobile |
| Tablet Layout | Optimized for medium screens | Tablets are common for browsing portfolios |
| Desktop Layout | Full-width layout with multi-column grids | The primary device for hiring managers |
| Dark Mode Toggle | Switch between light and dark themes | Shows attention to user preference and modern design |

```
FEATURE MAP OVERVIEW
=====================

+------------------+     +------------------+     +------------------+
|    HOME PAGE     |     |  PROJECTS PAGE   |     |   BLOG PAGE      |
|                  |     |                  |     |                  |
| - Hero Section   |     | - Project Grid   |     | - Post List      |
| - About Me       |     | - Project Detail |     | - Single Post    |
| - Skills         |     | - Tech Filter    |     | - Tags/Filter    |
| - Featured Work  |     | - Live + GitHub  |     | - CRUD (admin)   |
+------------------+     +------------------+     +------------------+
        |                        |                        |
        +------------------------+------------------------+
                                 |
                    +---------------------------+
                    |       SHARED FEATURES     |
                    |                           |
                    | - Responsive Design       |
                    | - Dark Mode Toggle        |
                    | - Navigation Bar          |
                    | - Footer                  |
                    +---------------------------+
                                 |
              +------------------+------------------+
              |                                     |
    +------------------+              +------------------+
    |  CONTACT PAGE    |              |   ADMIN PANEL    |
    |                  |              |                  |
    | - Contact Form   |              | - Login/Logout   |
    | - Validation     |              | - Manage Posts   |
    | - Email Alert    |              | - Manage Projects|
    | - Success Msg    |              | - View Messages  |
    +------------------+              +------------------+
```

---

## 3. Tech Stack

### The Full Stack at a Glance

```
TECH STACK ARCHITECTURE
========================

    FRONTEND                    BACKEND                    DATABASE
+---------------+         +---------------+         +---------------+
|               |         |               |         |               |
|  React 18     |  HTTP   |  Express.js   |  Query  |  MongoDB      |
|  + React      | ------> |  + Node.js    | ------> |  (Atlas)      |
|    Router     | <------ |               | <------ |               |
|               |  JSON   |               |  BSON   |               |
|  Tailwind CSS |         |  JWT Auth     |         |  Mongoose     |
|               |         |               |         |  (ODM)        |
+---------------+         +---------------+         +---------------+

    Browser                    Server                    Cloud DB
  (User's Device)          (Render.com)             (MongoDB Atlas)
```

### Frontend Technologies

| Technology | Purpose | Real-Life Analogy |
|------------|---------|-------------------|
| **React 18** | Component-based UI library | Building with LEGO blocks -- each component is a reusable piece |
| **React Router** | Client-side page navigation | A building's elevator -- moves between floors without leaving the building |
| **Tailwind CSS** | Utility-first CSS framework | A well-organized toolbox -- every tool (class) has one specific job |
| **Axios** | HTTP client for API calls | A postal service -- sends requests and delivers responses |
| **React Context** | Global state management | A company-wide intercom -- shares information across all departments |

### Backend Technologies

| Technology | Purpose | Real-Life Analogy |
|------------|---------|-------------------|
| **Node.js** | JavaScript runtime for the server | The engine that powers the backend -- runs JS outside the browser |
| **Express.js** | Web framework for building APIs | A receptionist -- receives requests, routes them, sends back responses |
| **Mongoose** | MongoDB object modeling (ODM) | A translator -- converts between JavaScript objects and database documents |
| **JWT** | JSON Web Tokens for authentication | A security badge -- proves your identity without re-entering credentials |
| **bcrypt** | Password hashing | A one-way lock -- converts passwords into unreadable hashes that cannot be reversed |
| **dotenv** | Environment variable management | A secure vault -- keeps sensitive data (API keys, passwords) out of your code |

### Authentication Flow

```
JWT AUTHENTICATION FLOW
========================

1. LOGIN REQUEST
   +--------+                    +--------+
   | Client | --- POST /login -> | Server |
   | (React)|    {email, pass}   |(Express|
   +--------+                    +--------+
                                     |
                          Compare password with
                          hashed version in DB
                                     |
                              +------+------+
                              |             |
                           MATCH         NO MATCH
                              |             |
                              v             v
                        Generate JWT    Return 401
                        (contains       "Invalid
                         user ID)       credentials"
                              |
                              v
2. TOKEN RETURNED
   +--------+                    +--------+
   | Client | <-- {token, user} -| Server |
   | stores |                    |        |
   | token  |                    +--------+
   | in     |
   |localStorage|
   +--------+

3. AUTHENTICATED REQUESTS
   +--------+                    +--------+
   | Client | --- GET /posts --> | Server |
   | sends  |  Authorization:   | checks |
   | token  |  Bearer <token>   | token  |
   | in     |                   | valid? |
   | header |                   +--------+
   +--------+                       |
                              +-----+-----+
                              |           |
                           VALID       INVALID
                              |           |
                              v           v
                         Process      Return 401
                         request      "Not
                         normally     authorized"
```

---

## 4. Wireframes

### Home Page Wireframe

```
+================================================================+
|  [Logo] Portfolio    Home  Projects  Blog  Contact    [Dark/Light] |
+================================================================+
|                                                                |
|                    Hello, I'm [Your Name]                      |
|                    Full-Stack MERN Developer                   |
|                                                                |
|              [View My Work]     [Contact Me]                   |
|                                                                |
+----------------------------------------------------------------+
|                                                                |
|                       ABOUT ME                                 |
|  +------------------+  +------------------------------------+  |
|  |                  |  |                                    |  |
|  |   [Your Photo]   |  |  I am a passionate web developer  |  |
|  |                  |  |  with expertise in the MERN stack. |  |
|  |   200 x 200     |  |  I love building clean, efficient  |  |
|  |                  |  |  applications that solve real      |  |
|  +------------------+  |  problems...                       |  |
|                        +------------------------------------+  |
+----------------------------------------------------------------+
|                                                                |
|                       MY SKILLS                                |
|  +--------+  +--------+  +--------+  +--------+  +--------+   |
|  |  HTML  |  |  CSS   |  |   JS   |  | React  |  | Node   |   |
|  |  90%   |  |  85%   |  |  80%   |  |  85%   |  |  75%   |   |
|  | ====== |  | =====  |  | ====   |  | =====  |  | ====   |   |
|  +--------+  +--------+  +--------+  +--------+  +--------+   |
|                                                                |
|  +--------+  +--------+  +--------+  +--------+               |
|  |Express |  |MongoDB |  |Tailwind|  |  Git   |               |
|  |  75%   |  |  70%   |  |  80%   |  |  85%   |               |
|  | ====   |  | ===    |  | ====   |  | =====  |               |
|  +--------+  +--------+  +--------+  +--------+               |
+----------------------------------------------------------------+
|                                                                |
|                   FEATURED PROJECTS                            |
|  +--------------------+  +--------------------+                |
|  | [Project Image]    |  | [Project Image]    |                |
|  | Task Manager App   |  | E-Commerce Store   |                |
|  | React + Express    |  | MERN Stack         |                |
|  | [Live] [GitHub]    |  | [Live] [GitHub]    |                |
|  +--------------------+  +--------------------+                |
|                                                                |
|                    [See All Projects ->]                       |
+----------------------------------------------------------------+
|                                                                |
|  (c) 2026 Your Name  |  GitHub  LinkedIn  Twitter              |
|                                                                |
+================================================================+
```

### Blog Page Wireframe

```
+================================================================+
|  [Logo] Portfolio    Home  Projects  Blog  Contact    [Dark/Light] |
+================================================================+
|                                                                |
|                        MY BLOG                                 |
|           Thoughts on web development and tech                 |
|                                                                |
|  [Search posts...]                    [Filter by tag: All  v]  |
|                                                                |
+----------------------------------------------------------------+
|                                                                |
|  +----------------------------------------------------------+ |
|  | [Thumbnail]  Understanding React Hooks                    | |
|  |              A deep dive into useState, useEffect...      | |
|  |              Tags: [React] [Hooks]   Jan 15, 2026         | |
|  |              [Read More ->]                               | |
|  +----------------------------------------------------------+ |
|                                                                |
|  +----------------------------------------------------------+ |
|  | [Thumbnail]  CSS Grid vs Flexbox: When to Use What        | |
|  |              A practical comparison with real examples...  | |
|  |              Tags: [CSS] [Layout]    Jan 10, 2026         | |
|  |              [Read More ->]                               | |
|  +----------------------------------------------------------+ |
|                                                                |
|  +----------------------------------------------------------+ |
|  | [Thumbnail]  Building REST APIs with Express              | |
|  |              Step-by-step guide to creating APIs...        | |
|  |              Tags: [Node] [Express]  Jan 5, 2026          | |
|  |              [Read More ->]                               | |
|  +----------------------------------------------------------+ |
|                                                                |
|              [<- Previous]  Page 1 of 3  [Next ->]             |
|                                                                |
+================================================================+
```

### Single Blog Post Wireframe

```
+================================================================+
|  [Logo] Portfolio    Home  Projects  Blog  Contact    [Dark/Light] |
+================================================================+
|                                                                |
|  <- Back to Blog                                               |
|                                                                |
|  Understanding React Hooks                                     |
|  ============================================================  |
|                                                                |
|  By [Your Name]  |  January 15, 2026  |  5 min read            |
|  Tags: [React] [Hooks] [JavaScript]                            |
|                                                                |
|  +----------------------------------------------------------+  |
|  |                                                          |  |
|  |               [Featured Image]                           |  |
|  |               800 x 400                                  |  |
|  |                                                          |  |
|  +----------------------------------------------------------+  |
|                                                                |
|  React Hooks were introduced in React 16.8 and have           |
|  fundamentally changed how we write React components.          |
|  In this post, we will explore the most commonly used          |
|  hooks and understand when and why to use them...              |
|                                                                |
|  ## What are Hooks?                                            |
|                                                                |
|  Hooks are functions that let you "hook into" React state      |
|  and lifecycle features from function components...            |
|                                                                |
|  ```javascript                                                 |
|  const [count, setCount] = useState(0);                        |
|  ```                                                           |
|                                                                |
|  ...                                                           |
|                                                                |
|  ---                                                           |
|  Share: [Twitter] [LinkedIn] [Copy Link]                       |
|                                                                |
+================================================================+
```

### Admin Dashboard Wireframe

```
+================================================================+
|  [Logo] Admin Panel                         Welcome, Admin [Logout] |
+================================================================+
|          |                                                     |
| SIDEBAR  |  DASHBOARD OVERVIEW                                 |
|          |                                                     |
| Dashboard|  +------------+  +------------+  +------------+     |
| Posts    |  |   POSTS    |  |  PROJECTS  |  |  MESSAGES  |     |
| Projects |  |     12     |  |      8     |  |      5     |     |
| Messages |  | [Manage ->]|  | [Manage ->]|  | [View ->]  |     |
| Settings |  +------------+  +------------+  +------------+     |
|          |                                                     |
|          |  RECENT POSTS                                       |
|          |  +-------------------------------------------------+|
|          |  | Title          | Date       | Status  | Actions ||
|          |  |----------------|------------|---------|---------|+
|          |  | React Hooks    | Jan 15     | Published| [E] [D]||
|          |  | CSS Grid       | Jan 10     | Draft   | [E] [D]||
|          |  | REST APIs      | Jan 5      | Published| [E] [D]||
|          |  +-------------------------------------------------+|
|          |                                                     |
|          |  [+ Create New Post]                                |
|          |                                                     |
|          |  RECENT MESSAGES                                    |
|          |  +-------------------------------------------------+|
|          |  | From           | Subject    | Date    | Status  ||
|          |  |----------------|------------|---------|---------|+
|          |  | john@mail.com  | Job Offer  | Jan 14  | Unread  ||
|          |  | jane@mail.com  | Freelance  | Jan 12  | Read    ||
|          |  +-------------------------------------------------+|
|          |                                                     |
+================================================================+
   [E] = Edit    [D] = Delete
```

### Contact Page Wireframe

```
+================================================================+
|  [Logo] Portfolio    Home  Projects  Blog  Contact    [Dark/Light] |
+================================================================+
|                                                                |
|                      GET IN TOUCH                              |
|        Have a question or want to work together?               |
|               I would love to hear from you.                   |
|                                                                |
+----------------------------------------------------------------+
|                                                                |
|  +---------------------------+  +---------------------------+  |
|  |                           |  |                           |  |
|  |  CONTACT FORM             |  |  CONTACT INFO             |  |
|  |                           |  |                           |  |
|  |  Name:                    |  |  Email:                   |  |
|  |  [___________________]    |  |  your@email.com           |  |
|  |                           |  |                           |  |
|  |  Email:                   |  |  Location:                |  |
|  |  [___________________]    |  |  Your City, Country       |  |
|  |                           |  |                           |  |
|  |  Subject:                 |  |  Social Links:            |  |
|  |  [___________________]    |  |  - GitHub                 |  |
|  |                           |  |  - LinkedIn               |  |
|  |  Message:                 |  |  - Twitter                |  |
|  |  [___________________]    |  |                           |  |
|  |  [___________________]    |  |  Availability:            |  |
|  |  [___________________]    |  |  Open for freelance       |  |
|  |  [___________________]    |  |  and full-time roles      |  |
|  |                           |  |                           |  |
|  |  [Send Message]           |  |                           |  |
|  |                           |  |                           |  |
|  +---------------------------+  +---------------------------+  |
|                                                                |
+================================================================+
```

---

## 5. Database Schema Design

### Entity Relationship Diagram

```
DATABASE SCHEMA -- ENTITY RELATIONSHIP DIAGRAM
================================================

+------------------+         +------------------+
|      USER        |         |      POST        |
|------------------|         |------------------|
| _id    (ObjectId)|<-----+  | _id    (ObjectId)|
| name   (String)  |      |  | title  (String)  |
| email  (String)  |      +--| author (ObjectId)|  (references User)
| password (String)|         | content (String) |
| role   (String)  |         | image  (String)  |
| createdAt (Date) |         | tags   ([String])|
+------------------+         | published (Bool) |
                              | createdAt (Date) |
                              | updatedAt (Date) |
                              +------------------+

+------------------+         +------------------+
|    PROJECT       |         |    CONTACT       |
|------------------|         |------------------|
| _id    (ObjectId)|         | _id    (ObjectId)|
| title  (String)  |         | name   (String)  |
| description (Str)|         | email  (String)  |
| techStack ([Str])|         | subject (String) |
| liveUrl (String) |         | message (String) |
| githubUrl (Str)  |         | read   (Boolean) |
| image  (String)  |         | createdAt (Date) |
| featured (Bool)  |         +------------------+
| order  (Number)  |
| createdAt (Date) |
+------------------+

RELATIONSHIPS:
==============
User  ---< Post      (One user has many posts)
                      (Each post belongs to one user via "author" field)

Project               (Standalone -- managed by admin)
Contact               (Standalone -- submitted by visitors)
```

### User Model

```javascript
// server/models/User.js
const mongoose = require('mongoose');
const bcrypt = require('bcryptjs');

const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: [true, 'Name is required'],
    trim: true,
    maxlength: [50, 'Name cannot exceed 50 characters']
  },
  email: {
    type: String,
    required: [true, 'Email is required'],
    unique: true,
    lowercase: true,
    match: [/^\S+@\S+\.\S+$/, 'Please provide a valid email']
  },
  password: {
    type: String,
    required: [true, 'Password is required'],
    minlength: [6, 'Password must be at least 6 characters'],
    select: false  // Do not return password in queries by default
  },
  role: {
    type: String,
    enum: ['admin', 'user'],
    default: 'user'
  }
}, {
  timestamps: true  // Automatically adds createdAt and updatedAt
});

// Hash password before saving
userSchema.pre('save', async function(next) {
  if (!this.isModified('password')) return next();
  const salt = await bcrypt.genSalt(10);
  this.password = await bcrypt.hash(this.password, salt);
  next();
});

// Compare entered password with hashed password
userSchema.methods.comparePassword = async function(enteredPassword) {
  return await bcrypt.compare(enteredPassword, this.password);
};

module.exports = mongoose.model('User', userSchema);
```

### Post Model

```javascript
// server/models/Post.js
const mongoose = require('mongoose');

const postSchema = new mongoose.Schema({
  title: {
    type: String,
    required: [true, 'Post title is required'],
    trim: true,
    maxlength: [200, 'Title cannot exceed 200 characters']
  },
  content: {
    type: String,
    required: [true, 'Post content is required']
  },
  image: {
    type: String,
    default: ''  // URL to the post's featured image
  },
  author: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User',
    required: true
  },
  tags: [{
    type: String,
    trim: true,
    lowercase: true
  }],
  published: {
    type: Boolean,
    default: false  // Posts start as drafts
  }
}, {
  timestamps: true
});

// Index for efficient queries
postSchema.index({ tags: 1 });
postSchema.index({ published: 1, createdAt: -1 });

module.exports = mongoose.model('Post', postSchema);
```

### Project Model

```javascript
// server/models/Project.js
const mongoose = require('mongoose');

const projectSchema = new mongoose.Schema({
  title: {
    type: String,
    required: [true, 'Project title is required'],
    trim: true
  },
  description: {
    type: String,
    required: [true, 'Project description is required']
  },
  techStack: [{
    type: String,
    trim: true
  }],
  liveUrl: {
    type: String,
    default: ''
  },
  githubUrl: {
    type: String,
    default: ''
  },
  image: {
    type: String,
    default: ''  // URL to project screenshot
  },
  featured: {
    type: Boolean,
    default: false  // Show on home page?
  },
  order: {
    type: Number,
    default: 0  // Display order on the page
  }
}, {
  timestamps: true
});

module.exports = mongoose.model('Project', projectSchema);
```

### Contact Model

```javascript
// server/models/Contact.js
const mongoose = require('mongoose');

const contactSchema = new mongoose.Schema({
  name: {
    type: String,
    required: [true, 'Name is required'],
    trim: true
  },
  email: {
    type: String,
    required: [true, 'Email is required'],
    match: [/^\S+@\S+\.\S+$/, 'Please provide a valid email']
  },
  subject: {
    type: String,
    trim: true,
    default: 'No Subject'
  },
  message: {
    type: String,
    required: [true, 'Message is required'],
    maxlength: [2000, 'Message cannot exceed 2000 characters']
  },
  read: {
    type: Boolean,
    default: false
  }
}, {
  timestamps: true
});

module.exports = mongoose.model('Contact', contactSchema);
```

### How the Models Connect

```
DATA FLOW THROUGH MODELS
==========================

VISITOR submits contact form
   |
   v
Contact.create({ name, email, message })
   |
   v
Saved in MongoDB "contacts" collection
   |
   v
Admin views in Admin Panel (GET /api/contacts)


ADMIN creates a blog post
   |
   v
Post.create({ title, content, tags, author: admin._id })
   |
   v
Saved in MongoDB "posts" collection
   |
   v
Visitors read on Blog page (GET /api/posts?published=true)


ADMIN adds a project
   |
   v
Project.create({ title, description, techStack, liveUrl, githubUrl })
   |
   v
Saved in MongoDB "projects" collection
   |
   v
Visitors browse on Projects page (GET /api/projects)
```

---

## 6. API Endpoints List

### Authentication Endpoints

| Method | Route | Description | Auth Required |
|--------|-------|-------------|---------------|
| POST | `/api/auth/register` | Register a new admin user | No |
| POST | `/api/auth/login` | Login and receive JWT token | No |
| GET | `/api/auth/me` | Get current logged-in user profile | Yes |

### Blog Post Endpoints

| Method | Route | Description | Auth Required |
|--------|-------|-------------|---------------|
| GET | `/api/posts` | Get all published posts (public) | No |
| GET | `/api/posts/:id` | Get a single post by ID | No |
| GET | `/api/posts/admin/all` | Get all posts including drafts | Yes |
| POST | `/api/posts` | Create a new blog post | Yes |
| PUT | `/api/posts/:id` | Update an existing post | Yes |
| DELETE | `/api/posts/:id` | Delete a post | Yes |

### Project Endpoints

| Method | Route | Description | Auth Required |
|--------|-------|-------------|---------------|
| GET | `/api/projects` | Get all projects (public) | No |
| GET | `/api/projects/:id` | Get a single project by ID | No |
| POST | `/api/projects` | Create a new project | Yes |
| PUT | `/api/projects/:id` | Update an existing project | Yes |
| DELETE | `/api/projects/:id` | Delete a project | Yes |

### Contact Endpoints

| Method | Route | Description | Auth Required |
|--------|-------|-------------|---------------|
| POST | `/api/contacts` | Submit a contact form message | No |
| GET | `/api/contacts` | Get all contact messages | Yes |
| PUT | `/api/contacts/:id` | Mark a message as read | Yes |
| DELETE | `/api/contacts/:id` | Delete a contact message | Yes |

### API Design Diagram

```
API ENDPOINT MAP
=================

                        /api
                         |
          +--------------+--------------+---------------+
          |              |              |               |
        /auth          /posts       /projects       /contacts
          |              |              |               |
     +----+----+    +----+----+    +----+----+     +----+----+
     |    |    |    |    |    |    |    |    |     |    |    |
   POST  POST GET  GET POST PUT  GET POST PUT   POST  GET  PUT
   /reg  /login /me  /   /   /:id  /   /  /:id   /    /   /:id
                    /:id      DEL  /:id    DEL         DEL
                    /admin    /:id        /:id         /:id
                    /all

  [Public]  [Public]  [Auth]     [Public] [Auth]   [Public][Auth]
```

---

## 7. Project Folder Structure

```
portfolio-website/
|
+-- client/                          # React Frontend (Vite)
|   +-- public/
|   |   +-- favicon.ico
|   +-- src/
|   |   +-- assets/                  # Images, icons, static files
|   |   |   +-- images/
|   |   |   +-- icons/
|   |   +-- components/              # Reusable UI components
|   |   |   +-- layout/
|   |   |   |   +-- Navbar.jsx
|   |   |   |   +-- Footer.jsx
|   |   |   |   +-- Sidebar.jsx
|   |   |   +-- common/
|   |   |   |   +-- Button.jsx
|   |   |   |   +-- Card.jsx
|   |   |   |   +-- Loading.jsx
|   |   |   |   +-- Modal.jsx
|   |   |   +-- home/
|   |   |   |   +-- Hero.jsx
|   |   |   |   +-- About.jsx
|   |   |   |   +-- Skills.jsx
|   |   |   |   +-- FeaturedProjects.jsx
|   |   |   +-- blog/
|   |   |   |   +-- PostCard.jsx
|   |   |   |   +-- PostList.jsx
|   |   |   +-- project/
|   |   |   |   +-- ProjectCard.jsx
|   |   |   |   +-- ProjectGrid.jsx
|   |   |   +-- contact/
|   |   |   |   +-- ContactForm.jsx
|   |   |   +-- admin/
|   |   |       +-- PostForm.jsx
|   |   |       +-- ProjectForm.jsx
|   |   |       +-- MessageList.jsx
|   |   +-- pages/                   # Page-level components
|   |   |   +-- Home.jsx
|   |   |   +-- Projects.jsx
|   |   |   +-- ProjectDetail.jsx
|   |   |   +-- Blog.jsx
|   |   |   +-- SinglePost.jsx
|   |   |   +-- Contact.jsx
|   |   |   +-- Login.jsx
|   |   |   +-- admin/
|   |   |       +-- Dashboard.jsx
|   |   |       +-- ManagePosts.jsx
|   |   |       +-- ManageProjects.jsx
|   |   |       +-- Messages.jsx
|   |   +-- context/                 # React Context providers
|   |   |   +-- AuthContext.jsx
|   |   |   +-- ThemeContext.jsx
|   |   +-- hooks/                   # Custom React hooks
|   |   |   +-- useAuth.js
|   |   |   +-- useFetch.js
|   |   |   +-- useTheme.js
|   |   +-- services/                # API call functions
|   |   |   +-- api.js               # Axios instance with base URL
|   |   |   +-- authService.js
|   |   |   +-- postService.js
|   |   |   +-- projectService.js
|   |   |   +-- contactService.js
|   |   +-- utils/                   # Helper functions
|   |   |   +-- formatDate.js
|   |   |   +-- validators.js
|   |   +-- App.jsx
|   |   +-- main.jsx
|   |   +-- index.css                # Tailwind directives
|   +-- tailwind.config.js
|   +-- postcss.config.js
|   +-- vite.config.js
|   +-- package.json
|   +-- .env                         # VITE_API_URL=http://localhost:5000
|
+-- server/                          # Express Backend
|   +-- config/
|   |   +-- db.js                    # MongoDB connection
|   +-- controllers/
|   |   +-- authController.js
|   |   +-- postController.js
|   |   +-- projectController.js
|   |   +-- contactController.js
|   +-- middleware/
|   |   +-- auth.js                  # JWT verification middleware
|   |   +-- errorHandler.js          # Global error handler
|   +-- models/
|   |   +-- User.js
|   |   +-- Post.js
|   |   +-- Project.js
|   |   +-- Contact.js
|   +-- routes/
|   |   +-- authRoutes.js
|   |   +-- postRoutes.js
|   |   +-- projectRoutes.js
|   |   +-- contactRoutes.js
|   +-- utils/
|   |   +-- generateToken.js         # JWT token creation helper
|   +-- server.js                    # Entry point
|   +-- package.json
|   +-- .env                         # PORT, MONGO_URI, JWT_SECRET
|
+-- .gitignore
+-- README.md
```

### Understanding the Structure

```
WHY THIS STRUCTURE?
====================

Think of it like a company with two departments:

CLIENT (Marketing Department)          SERVER (Operations Department)
================================       ================================
pages/      = Different offices        routes/      = Reception desks
components/ = Shared tools/supplies    controllers/ = Department managers
context/    = Company-wide memos       middleware/  = Security guards
hooks/      = Reusable procedures      models/      = Filing cabinets
services/   = Mail room (sends/        config/      = Company settings
              receives from server)    utils/       = Shared utilities

The CLIENT department handles everything the customer (user) sees.
The SERVER department handles everything behind the scenes.
They communicate through the MAIL ROOM (API calls via services/).
```

---

## 8. Building the Backend

### Step 1: Initialize the Server Project

```bash
# Create the server directory and initialize
mkdir server
cd server
npm init -y
npm install express mongoose dotenv cors bcryptjs jsonwebtoken
npm install -D nodemon
```

### Step 2: Server Entry Point

```javascript
// server/server.js
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');
const dotenv = require('dotenv');

// Load environment variables
dotenv.config();

const app = express();

// Middleware
app.use(cors());
app.use(express.json());  // Parse JSON request bodies

// Import routes
const authRoutes = require('./routes/authRoutes');
const postRoutes = require('./routes/postRoutes');
const projectRoutes = require('./routes/projectRoutes');
const contactRoutes = require('./routes/contactRoutes');

// Use routes
app.use('/api/auth', authRoutes);
app.use('/api/posts', postRoutes);
app.use('/api/projects', projectRoutes);
app.use('/api/contacts', contactRoutes);

// Root route
app.get('/', (req, res) => {
  res.json({ message: 'Portfolio API is running' });
});

// Error handling middleware
const errorHandler = require('./middleware/errorHandler');
app.use(errorHandler);

// Connect to MongoDB and start server
const PORT = process.env.PORT || 5000;

mongoose.connect(process.env.MONGO_URI)
  .then(() => {
    console.log('Connected to MongoDB');
    app.listen(PORT, () => {
      console.log(`Server running on port ${PORT}`);
    });
  })
  .catch((err) => {
    console.error('MongoDB connection error:', err.message);
    process.exit(1);
  });
```

### Step 3: Database Configuration

```javascript
// server/config/db.js
const mongoose = require('mongoose');

const connectDB = async () => {
  try {
    const conn = await mongoose.connect(process.env.MONGO_URI);
    console.log(`MongoDB Connected: ${conn.connection.host}`);
  } catch (error) {
    console.error(`Database Error: ${error.message}`);
    process.exit(1);
  }
};

module.exports = connectDB;
```

### Step 4: Environment Variables

```bash
# server/.env
PORT=5000
MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/portfolio?retryWrites=true&w=majority
JWT_SECRET=your_super_secret_jwt_key_change_this_in_production
JWT_EXPIRE=30d
```

**WARNING:** Never commit your `.env` file to Git. Always add it to `.gitignore`.

### Step 5: Auth Middleware

```javascript
// server/middleware/auth.js
const jwt = require('jsonwebtoken');
const User = require('../models/User');

const protect = async (req, res, next) => {
  let token;

  // Check for token in Authorization header
  if (
    req.headers.authorization &&
    req.headers.authorization.startsWith('Bearer')
  ) {
    token = req.headers.authorization.split(' ')[1];
  }

  // If no token found, deny access
  if (!token) {
    return res.status(401).json({
      success: false,
      message: 'Not authorized -- no token provided'
    });
  }

  try {
    // Verify the token
    const decoded = jwt.verify(token, process.env.JWT_SECRET);

    // Find the user and attach to request
    req.user = await User.findById(decoded.id);

    if (!req.user) {
      return res.status(401).json({
        success: false,
        message: 'User belonging to this token no longer exists'
      });
    }

    next();
  } catch (error) {
    return res.status(401).json({
      success: false,
      message: 'Not authorized -- invalid token'
    });
  }
};

// Restrict to admin only
const adminOnly = (req, res, next) => {
  if (req.user.role !== 'admin') {
    return res.status(403).json({
      success: false,
      message: 'Access denied -- admin only'
    });
  }
  next();
};

module.exports = { protect, adminOnly };
```

### Step 6: Error Handler Middleware

```javascript
// server/middleware/errorHandler.js
const errorHandler = (err, req, res, next) => {
  console.error(err.stack);

  // Mongoose bad ObjectId
  if (err.name === 'CastError') {
    return res.status(400).json({
      success: false,
      message: 'Resource not found -- invalid ID format'
    });
  }

  // Mongoose duplicate key
  if (err.code === 11000) {
    return res.status(400).json({
      success: false,
      message: 'Duplicate field value entered'
    });
  }

  // Mongoose validation error
  if (err.name === 'ValidationError') {
    const messages = Object.values(err.errors).map(val => val.message);
    return res.status(400).json({
      success: false,
      message: messages.join(', ')
    });
  }

  // Default server error
  res.status(err.statusCode || 500).json({
    success: false,
    message: err.message || 'Internal Server Error'
  });
};

module.exports = errorHandler;
```

### Step 7: Token Generation Utility

```javascript
// server/utils/generateToken.js
const jwt = require('jsonwebtoken');

const generateToken = (userId) => {
  return jwt.sign(
    { id: userId },
    process.env.JWT_SECRET,
    { expiresIn: process.env.JWT_EXPIRE || '30d' }
  );
};

module.exports = generateToken;
```

### Step 8: Auth Controller

```javascript
// server/controllers/authController.js
const User = require('../models/User');
const generateToken = require('../utils/generateToken');

// Register a new user
// POST /api/auth/register
const register = async (req, res, next) => {
  try {
    const { name, email, password } = req.body;

    // Check if user already exists
    const existingUser = await User.findOne({ email });
    if (existingUser) {
      return res.status(400).json({
        success: false,
        message: 'A user with this email already exists'
      });
    }

    // Create user (password is hashed by the pre-save hook)
    const user = await User.create({ name, email, password });

    // Generate token
    const token = generateToken(user._id);

    res.status(201).json({
      success: true,
      token,
      user: {
        id: user._id,
        name: user.name,
        email: user.email,
        role: user.role
      }
    });
  } catch (error) {
    next(error);
  }
};

// Login user
// POST /api/auth/login
const login = async (req, res, next) => {
  try {
    const { email, password } = req.body;

    // Validate input
    if (!email || !password) {
      return res.status(400).json({
        success: false,
        message: 'Please provide both email and password'
      });
    }

    // Find user and include password field
    const user = await User.findOne({ email }).select('+password');

    if (!user) {
      return res.status(401).json({
        success: false,
        message: 'Invalid credentials'
      });
    }

    // Check password
    const isMatch = await user.comparePassword(password);

    if (!isMatch) {
      return res.status(401).json({
        success: false,
        message: 'Invalid credentials'
      });
    }

    // Generate token
    const token = generateToken(user._id);

    res.json({
      success: true,
      token,
      user: {
        id: user._id,
        name: user.name,
        email: user.email,
        role: user.role
      }
    });
  } catch (error) {
    next(error);
  }
};

// Get current user
// GET /api/auth/me
const getMe = async (req, res) => {
  res.json({
    success: true,
    user: {
      id: req.user._id,
      name: req.user.name,
      email: req.user.email,
      role: req.user.role
    }
  });
};

module.exports = { register, login, getMe };
```

### Step 9: Auth Routes

```javascript
// server/routes/authRoutes.js
const express = require('express');
const router = express.Router();
const { register, login, getMe } = require('../controllers/authController');
const { protect } = require('../middleware/auth');

router.post('/register', register);
router.post('/login', login);
router.get('/me', protect, getMe);

module.exports = router;
```

### Step 10: Post Controller (CRUD)

```javascript
// server/controllers/postController.js
const Post = require('../models/Post');

// Get all published posts (public)
// GET /api/posts
const getPosts = async (req, res, next) => {
  try {
    const { tag, page = 1, limit = 6 } = req.query;

    const query = { published: true };
    if (tag) query.tags = tag;

    const posts = await Post.find(query)
      .populate('author', 'name')
      .sort({ createdAt: -1 })
      .skip((page - 1) * limit)
      .limit(Number(limit));

    const total = await Post.countDocuments(query);

    res.json({
      success: true,
      data: posts,
      pagination: {
        page: Number(page),
        pages: Math.ceil(total / limit),
        total
      }
    });
  } catch (error) {
    next(error);
  }
};

// Get single post
// GET /api/posts/:id
const getPost = async (req, res, next) => {
  try {
    const post = await Post.findById(req.params.id)
      .populate('author', 'name');

    if (!post) {
      return res.status(404).json({
        success: false,
        message: 'Post not found'
      });
    }

    res.json({ success: true, data: post });
  } catch (error) {
    next(error);
  }
};

// Get all posts including drafts (admin)
// GET /api/posts/admin/all
const getAllPosts = async (req, res, next) => {
  try {
    const posts = await Post.find()
      .populate('author', 'name')
      .sort({ createdAt: -1 });

    res.json({ success: true, data: posts });
  } catch (error) {
    next(error);
  }
};

// Create a post
// POST /api/posts
const createPost = async (req, res, next) => {
  try {
    req.body.author = req.user._id;
    const post = await Post.create(req.body);

    res.status(201).json({ success: true, data: post });
  } catch (error) {
    next(error);
  }
};

// Update a post
// PUT /api/posts/:id
const updatePost = async (req, res, next) => {
  try {
    const post = await Post.findByIdAndUpdate(
      req.params.id,
      req.body,
      { new: true, runValidators: true }
    );

    if (!post) {
      return res.status(404).json({
        success: false,
        message: 'Post not found'
      });
    }

    res.json({ success: true, data: post });
  } catch (error) {
    next(error);
  }
};

// Delete a post
// DELETE /api/posts/:id
const deletePost = async (req, res, next) => {
  try {
    const post = await Post.findByIdAndDelete(req.params.id);

    if (!post) {
      return res.status(404).json({
        success: false,
        message: 'Post not found'
      });
    }

    res.json({ success: true, message: 'Post deleted successfully' });
  } catch (error) {
    next(error);
  }
};

module.exports = { getPosts, getPost, getAllPosts, createPost, updatePost, deletePost };
```

### Step 11: Post Routes

```javascript
// server/routes/postRoutes.js
const express = require('express');
const router = express.Router();
const {
  getPosts, getPost, getAllPosts,
  createPost, updatePost, deletePost
} = require('../controllers/postController');
const { protect } = require('../middleware/auth');

// Public routes
router.get('/', getPosts);
router.get('/:id', getPost);

// Protected routes (admin only)
router.get('/admin/all', protect, getAllPosts);
router.post('/', protect, createPost);
router.put('/:id', protect, updatePost);
router.delete('/:id', protect, deletePost);

module.exports = router;
```

### Step 12: Project and Contact Routes (Similar Pattern)

```javascript
// server/routes/projectRoutes.js
const express = require('express');
const router = express.Router();
const {
  getProjects, getProject,
  createProject, updateProject, deleteProject
} = require('../controllers/projectController');
const { protect } = require('../middleware/auth');

router.get('/', getProjects);
router.get('/:id', getProject);
router.post('/', protect, createProject);
router.put('/:id', protect, updateProject);
router.delete('/:id', protect, deleteProject);

module.exports = router;
```

```javascript
// server/routes/contactRoutes.js
const express = require('express');
const router = express.Router();
const {
  submitContact, getContacts,
  markAsRead, deleteContact
} = require('../controllers/contactController');
const { protect } = require('../middleware/auth');

router.post('/', submitContact);            // Public -- visitors can submit
router.get('/', protect, getContacts);      // Admin only
router.put('/:id', protect, markAsRead);    // Admin only
router.delete('/:id', protect, deleteContact); // Admin only

module.exports = router;
```

### Backend Request Flow

```
HOW A REQUEST FLOWS THROUGH THE BACKEND
=========================================

Client sends: POST /api/posts  (with JWT token)
   |
   v
server.js receives request
   |
   v
app.use('/api/posts', postRoutes)  --> matches "/api/posts"
   |
   v
postRoutes.js: router.post('/', protect, createPost)
   |
   v
middleware/auth.js: protect()
   |-- Extracts token from Authorization header
   |-- Verifies token with jwt.verify()
   |-- Finds user in database
   |-- Attaches user to req.user
   |-- Calls next()
   |
   v
controllers/postController.js: createPost()
   |-- Reads req.body (title, content, tags, etc.)
   |-- Sets req.body.author = req.user._id
   |-- Calls Post.create(req.body)
   |-- Returns 201 with created post
   |
   v
Response sent back to client as JSON
```

---

## 9. Building the Frontend

### Step 1: Initialize the React Project

```bash
# Create the client directory with Vite
npm create vite@latest client -- --template react
cd client
npm install
npm install react-router-dom axios
npm install -D tailwindcss @tailwindcss/vite
```

### Step 2: Configure Tailwind CSS

```javascript
// client/vite.config.js
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import tailwindcss from '@tailwindcss/vite';

export default defineConfig({
  plugins: [react(), tailwindcss()],
  server: {
    port: 3000,
    proxy: {
      '/api': 'http://localhost:5000'
    }
  }
});
```

```css
/* client/src/index.css */
@import "tailwindcss";
```

### Step 3: API Service Setup

```javascript
// client/src/services/api.js
import axios from 'axios';

const API = axios.create({
  baseURL: import.meta.env.VITE_API_URL || 'http://localhost:5000/api'
});

// Automatically attach JWT token to every request
API.interceptors.request.use((config) => {
  const token = localStorage.getItem('token');
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});

// Handle expired tokens globally
API.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      localStorage.removeItem('token');
      localStorage.removeItem('user');
      window.location.href = '/login';
    }
    return Promise.reject(error);
  }
);

export default API;
```

### Step 4: Auth Context

```jsx
// client/src/context/AuthContext.jsx
import { createContext, useState, useEffect } from 'react';
import API from '../services/api';

export const AuthContext = createContext();

export const AuthProvider = ({ children }) => {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  // Check if user is logged in on app load
  useEffect(() => {
    const storedUser = localStorage.getItem('user');
    const token = localStorage.getItem('token');

    if (storedUser && token) {
      setUser(JSON.parse(storedUser));
    }
    setLoading(false);
  }, []);

  // Login function
  const login = async (email, password) => {
    const { data } = await API.post('/auth/login', { email, password });

    localStorage.setItem('token', data.token);
    localStorage.setItem('user', JSON.stringify(data.user));
    setUser(data.user);

    return data;
  };

  // Logout function
  const logout = () => {
    localStorage.removeItem('token');
    localStorage.removeItem('user');
    setUser(null);
  };

  return (
    <AuthContext.Provider value={{ user, loading, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
};
```

### Step 5: Theme Context (Dark Mode)

```jsx
// client/src/context/ThemeContext.jsx
import { createContext, useState, useEffect } from 'react';

export const ThemeContext = createContext();

export const ThemeProvider = ({ children }) => {
  const [darkMode, setDarkMode] = useState(() => {
    // Check localStorage or system preference
    const saved = localStorage.getItem('darkMode');
    if (saved !== null) return JSON.parse(saved);
    return window.matchMedia('(prefers-color-scheme: dark)').matches;
  });

  useEffect(() => {
    // Apply dark class to HTML element
    if (darkMode) {
      document.documentElement.classList.add('dark');
    } else {
      document.documentElement.classList.remove('dark');
    }
    localStorage.setItem('darkMode', JSON.stringify(darkMode));
  }, [darkMode]);

  const toggleDarkMode = () => setDarkMode(prev => !prev);

  return (
    <ThemeContext.Provider value={{ darkMode, toggleDarkMode }}>
      {children}
    </ThemeContext.Provider>
  );
};
```

### Step 6: React Router Setup

```jsx
// client/src/App.jsx
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import { AuthProvider } from './context/AuthContext';
import { ThemeProvider } from './context/ThemeContext';

// Layout
import Navbar from './components/layout/Navbar';
import Footer from './components/layout/Footer';

// Public Pages
import Home from './pages/Home';
import Projects from './pages/Projects';
import ProjectDetail from './pages/ProjectDetail';
import Blog from './pages/Blog';
import SinglePost from './pages/SinglePost';
import Contact from './pages/Contact';
import Login from './pages/Login';

// Admin Pages
import Dashboard from './pages/admin/Dashboard';
import ManagePosts from './pages/admin/ManagePosts';
import ManageProjects from './pages/admin/ManageProjects';
import Messages from './pages/admin/Messages';

// Protected Route Component
import ProtectedRoute from './components/common/ProtectedRoute';

function App() {
  return (
    <AuthProvider>
      <ThemeProvider>
        <Router>
          <div className="min-h-screen bg-white dark:bg-gray-900 text-gray-900 dark:text-gray-100">
            <Navbar />
            <main>
              <Routes>
                {/* Public Routes */}
                <Route path="/" element={<Home />} />
                <Route path="/projects" element={<Projects />} />
                <Route path="/projects/:id" element={<ProjectDetail />} />
                <Route path="/blog" element={<Blog />} />
                <Route path="/blog/:id" element={<SinglePost />} />
                <Route path="/contact" element={<Contact />} />
                <Route path="/login" element={<Login />} />

                {/* Protected Admin Routes */}
                <Route path="/admin" element={<ProtectedRoute />}>
                  <Route path="dashboard" element={<Dashboard />} />
                  <Route path="posts" element={<ManagePosts />} />
                  <Route path="projects" element={<ManageProjects />} />
                  <Route path="messages" element={<Messages />} />
                </Route>
              </Routes>
            </main>
            <Footer />
          </div>
        </Router>
      </ThemeProvider>
    </AuthProvider>
  );
}

export default App;
```

### Step 7: Protected Route Component

```jsx
// client/src/components/common/ProtectedRoute.jsx
import { useContext } from 'react';
import { Navigate, Outlet } from 'react-router-dom';
import { AuthContext } from '../../context/AuthContext';

const ProtectedRoute = () => {
  const { user, loading } = useContext(AuthContext);

  if (loading) {
    return (
      <div className="flex justify-center items-center h-screen">
        <div className="animate-spin rounded-full h-12 w-12 border-b-2 border-blue-600"></div>
      </div>
    );
  }

  // If no user is logged in, redirect to login page
  if (!user) {
    return <Navigate to="/login" replace />;
  }

  // If user is logged in, render the child routes
  return <Outlet />;
};

export default ProtectedRoute;
```

### Step 8: Navbar Component

```jsx
// client/src/components/layout/Navbar.jsx
import { useContext, useState } from 'react';
import { Link, NavLink } from 'react-router-dom';
import { AuthContext } from '../../context/AuthContext';
import { ThemeContext } from '../../context/ThemeContext';

const Navbar = () => {
  const { user, logout } = useContext(AuthContext);
  const { darkMode, toggleDarkMode } = useContext(ThemeContext);
  const [menuOpen, setMenuOpen] = useState(false);

  const navLinks = [
    { to: '/', label: 'Home' },
    { to: '/projects', label: 'Projects' },
    { to: '/blog', label: 'Blog' },
    { to: '/contact', label: 'Contact' },
  ];

  return (
    <nav className="bg-white dark:bg-gray-800 shadow-md sticky top-0 z-50">
      <div className="max-w-6xl mx-auto px-4 py-3 flex justify-between items-center">
        {/* Logo */}
        <Link to="/" className="text-xl font-bold text-blue-600 dark:text-blue-400">
          Portfolio
        </Link>

        {/* Desktop Navigation */}
        <div className="hidden md:flex items-center gap-6">
          {navLinks.map(link => (
            <NavLink
              key={link.to}
              to={link.to}
              className={({ isActive }) =>
                `hover:text-blue-600 transition ${isActive ? 'text-blue-600 font-semibold' : ''}`
              }
            >
              {link.label}
            </NavLink>
          ))}

          {user && (
            <NavLink to="/admin/dashboard" className="hover:text-blue-600 transition">
              Admin
            </NavLink>
          )}

          {/* Dark Mode Toggle */}
          <button
            onClick={toggleDarkMode}
            className="p-2 rounded-lg bg-gray-100 dark:bg-gray-700"
          >
            {darkMode ? 'Light' : 'Dark'}
          </button>

          {user ? (
            <button onClick={logout} className="text-red-500 hover:text-red-700">
              Logout
            </button>
          ) : (
            <NavLink to="/login" className="hover:text-blue-600">
              Login
            </NavLink>
          )}
        </div>

        {/* Mobile Menu Button */}
        <button
          className="md:hidden p-2"
          onClick={() => setMenuOpen(!menuOpen)}
        >
          {menuOpen ? 'Close' : 'Menu'}
        </button>
      </div>

      {/* Mobile Menu */}
      {menuOpen && (
        <div className="md:hidden bg-white dark:bg-gray-800 border-t px-4 py-2 space-y-2">
          {navLinks.map(link => (
            <NavLink
              key={link.to}
              to={link.to}
              className="block py-2 hover:text-blue-600"
              onClick={() => setMenuOpen(false)}
            >
              {link.label}
            </NavLink>
          ))}
        </div>
      )}
    </nav>
  );
};

export default Navbar;
```

### Step 9: Service Functions (API Calls)

```javascript
// client/src/services/postService.js
import API from './api';

export const getPosts = (page = 1, tag = '') => {
  const params = { page };
  if (tag) params.tag = tag;
  return API.get('/posts', { params });
};

export const getPost = (id) => API.get(`/posts/${id}`);

export const getAllPosts = () => API.get('/posts/admin/all');

export const createPost = (postData) => API.post('/posts', postData);

export const updatePost = (id, postData) => API.put(`/posts/${id}`, postData);

export const deletePost = (id) => API.delete(`/posts/${id}`);
```

```javascript
// client/src/services/projectService.js
import API from './api';

export const getProjects = () => API.get('/projects');

export const getProject = (id) => API.get(`/projects/${id}`);

export const createProject = (data) => API.post('/projects', data);

export const updateProject = (id, data) => API.put(`/projects/${id}`, data);

export const deleteProject = (id) => API.delete(`/projects/${id}`);
```

```javascript
// client/src/services/contactService.js
import API from './api';

export const submitContact = (data) => API.post('/contacts', data);

export const getContacts = () => API.get('/contacts');

export const markAsRead = (id) => API.put(`/contacts/${id}`);

export const deleteContact = (id) => API.delete(`/contacts/${id}`);
```

### Frontend Component Hierarchy

```
COMPONENT HIERARCHY
====================

App.jsx
 |
 +-- AuthProvider (context)
 |    +-- ThemeProvider (context)
 |         +-- Router
 |              +-- Navbar
 |              +-- Routes
 |              |    +-- Home
 |              |    |    +-- Hero
 |              |    |    +-- About
 |              |    |    +-- Skills
 |              |    |    +-- FeaturedProjects
 |              |    |         +-- ProjectCard (x2-3)
 |              |    |
 |              |    +-- Projects
 |              |    |    +-- ProjectGrid
 |              |    |         +-- ProjectCard (xN)
 |              |    |
 |              |    +-- Blog
 |              |    |    +-- PostList
 |              |    |         +-- PostCard (xN)
 |              |    |
 |              |    +-- SinglePost
 |              |    |
 |              |    +-- Contact
 |              |    |    +-- ContactForm
 |              |    |
 |              |    +-- Login
 |              |    |
 |              |    +-- ProtectedRoute
 |              |         +-- Dashboard
 |              |         +-- ManagePosts
 |              |         |    +-- PostForm (modal)
 |              |         +-- ManageProjects
 |              |         |    +-- ProjectForm (modal)
 |              |         +-- Messages
 |              |              +-- MessageList
 |              |
 |              +-- Footer
```

---

## 10. Part 1 Progress Checklist

Use this checklist to track your Week 39 progress. By the end of this week, all items should be checked off.

### Backend Completed

- [ ] Server project initialized with all dependencies installed
- [ ] MongoDB Atlas database created and connection string configured
- [ ] Environment variables file (`.env`) created with PORT, MONGO_URI, JWT_SECRET
- [ ] All four models created: User, Post, Project, Contact
- [ ] Auth middleware created with `protect` and `adminOnly` functions
- [ ] Error handler middleware created
- [ ] Token generation utility created
- [ ] Auth routes and controller working (register, login, getMe)
- [ ] Post routes and controller working (full CRUD)
- [ ] Project routes and controller working (full CRUD)
- [ ] Contact routes and controller working (submit, list, read, delete)
- [ ] All endpoints tested with Postman or Thunder Client
- [ ] Server starts without errors

### Frontend Completed

- [ ] React project created with Vite
- [ ] Tailwind CSS configured and working
- [ ] Folder structure created (pages, components, context, hooks, services)
- [ ] API service with Axios instance and interceptors set up
- [ ] AuthContext created with login, logout, and persistence
- [ ] ThemeContext created with dark mode toggle and localStorage
- [ ] React Router configured with all public and admin routes
- [ ] ProtectedRoute component created
- [ ] Navbar component with responsive mobile menu
- [ ] All page components created (even if basic placeholders)
- [ ] All service files created (postService, projectService, contactService)

### Integration Started

- [ ] Frontend can successfully call backend API endpoints
- [ ] Login flow works end-to-end (form to JWT stored in localStorage)
- [ ] CORS configured correctly on the backend
- [ ] Environment variables set for both client and server
- [ ] Git repository initialized with proper `.gitignore`

```
WEEK 39 MILESTONE
==================

By the end of Week 39, you should have:

+------------------+     +------------------+     +------------------+
|    BACKEND       |     |    FRONTEND      |     |   INTEGRATION    |
|    COMPLETE      |     |    SCAFFOLDED    |     |    STARTED       |
|                  |     |                  |     |                  |
| - All models     |     | - All pages      |     | - Login works    |
| - All routes     |     | - All components |     | - API calls work |
| - All controllers|     | - Context set up |     | - CORS working   |
| - Auth working   |     | - Router working |     | - Env vars set   |
| - Tested in      |     | - Tailwind ready |     | - Git repo ready |
|   Postman        |     |                  |     |                  |
+------------------+     +------------------+     +------------------+

Status: Backend 100% | Frontend 60% | Integration 30%
(Completion continues in Week 40)
```

---

**Next Week:** In Week 40, we will complete all frontend features, connect every page to the backend, test thoroughly, deploy to production, and launch your portfolio website to the world.
