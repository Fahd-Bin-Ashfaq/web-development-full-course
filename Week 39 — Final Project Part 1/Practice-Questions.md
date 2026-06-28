# Week 39 — Final Project Part 1: Project Checklist

**This is a hands-on project checklist, not a multiple-choice quiz.** Work through each section systematically. Check off each item as you complete it. By the end of Week 39, every box should be checked.

---

## Backend Checklist

### Project Setup (5 Items)

- [ ] Created `server/` directory and initialized with `npm init -y`
- [ ] Installed all required dependencies: `express`, `mongoose`, `dotenv`, `cors`, `bcryptjs`, `jsonwebtoken`
- [ ] Installed dev dependency: `nodemon`
- [ ] Created `.env` file with `PORT`, `MONGO_URI`, and `JWT_SECRET` values
- [ ] Created `server.js` entry point with Express app, middleware (CORS, JSON parser), and MongoDB connection

**Verification:** Run `npm run dev` (or `npx nodemon server.js`). You should see:
```
Connected to MongoDB
Server running on port 5000
```

---

### Models Created (4 Items)

- [ ] **User Model** (`server/models/User.js`) -- Fields: name, email (unique), password (select: false), role (enum: admin/user). Includes pre-save hook for password hashing and `comparePassword` instance method.
- [ ] **Post Model** (`server/models/Post.js`) -- Fields: title, content, image, author (ObjectId ref to User), tags (array of strings), published (boolean, default false). Includes timestamps.
- [ ] **Project Model** (`server/models/Project.js`) -- Fields: title, description, techStack (array), liveUrl, githubUrl, image, featured (boolean), order (number). Includes timestamps.
- [ ] **Contact Model** (`server/models/Contact.js`) -- Fields: name, email, subject, message, read (boolean, default false). Includes timestamps.

**Verification:** Open MongoDB Atlas or Compass. After the server connects, you should see the database created (collections appear after the first document is inserted).

---

### Routes & Controllers (5 Items)

- [ ] **Auth Routes** (`/api/auth`) -- POST `/register` creates a new user, POST `/login` returns JWT token, GET `/me` returns current user (protected). Controller handles input validation, duplicate email check, password comparison, and token generation.
- [ ] **Post Routes** (`/api/posts`) -- GET `/` returns published posts with pagination, GET `/:id` returns single post, GET `/admin/all` returns all posts including drafts (protected), POST `/` creates a post (protected), PUT `/:id` updates a post (protected), DELETE `/:id` deletes a post (protected).
- [ ] **Project Routes** (`/api/projects`) -- GET `/` returns all projects (public), GET `/:id` returns single project (public), POST `/` creates a project (protected), PUT `/:id` updates (protected), DELETE `/:id` deletes (protected).
- [ ] **Contact Routes** (`/api/contacts`) -- POST `/` submits a message (public), GET `/` lists all messages (protected), PUT `/:id` marks as read (protected), DELETE `/:id` deletes message (protected).
- [ ] All routes are imported and mounted in `server.js` using `app.use('/api/auth', authRoutes)`, etc.

**Verification:** Visit `http://localhost:5000/api/posts` in your browser. You should see:
```json
{ "success": true, "data": [], "pagination": { "page": 1, "pages": 0, "total": 0 } }
```

---

### Auth Middleware (3 Items)

- [ ] **protect middleware** (`server/middleware/auth.js`) -- Extracts token from `Authorization: Bearer <token>` header, verifies with `jwt.verify()`, finds user by decoded ID, attaches user to `req.user`, calls `next()`. Returns 401 if no token or invalid token.
- [ ] **adminOnly middleware** -- Checks `req.user.role === 'admin'`, returns 403 if not admin. Used on routes that only the admin should access.
- [ ] **Error handler middleware** (`server/middleware/errorHandler.js`) -- Catches Mongoose CastError (bad ID), duplicate key errors (code 11000), validation errors, and returns formatted JSON responses.

**Verification:** Try calling `GET /api/posts/admin/all` without a token. You should get:
```json
{ "success": false, "message": "Not authorized -- no token provided" }
```

---

### Testing with Postman (4 Items)

Test each of the following flows in Postman (or Thunder Client in VS Code):

- [ ] **Registration flow:** POST `http://localhost:5000/api/auth/register` with body `{ "name": "Admin", "email": "admin@test.com", "password": "123456" }`. Expect 201 with token returned.
- [ ] **Login flow:** POST `http://localhost:5000/api/auth/login` with body `{ "email": "admin@test.com", "password": "123456" }`. Expect 200 with token returned. Copy this token.
- [ ] **Protected route test:** GET `http://localhost:5000/api/auth/me` with header `Authorization: Bearer <your_token>`. Expect 200 with user data.
- [ ] **CRUD test:** Create a post (POST `/api/posts` with token), read it (GET `/api/posts/:id`), update it (PUT `/api/posts/:id` with token), delete it (DELETE `/api/posts/:id` with token). All four operations should succeed.

**Verification:** All four Postman tests return expected status codes and response bodies.

---

## Frontend Checklist

### React Setup with Vite (4 Items)

- [ ] Created React project with `npm create vite@latest client -- --template react`
- [ ] Installed dependencies: `react-router-dom`, `axios`
- [ ] Installed and configured Tailwind CSS (installed `tailwindcss` and `@tailwindcss/vite`, added `@import "tailwindcss"` to `index.css`, added the Tailwind Vite plugin to `vite.config.js`)
- [ ] Created `.env` file with `VITE_API_URL=http://localhost:5000/api`

**Verification:** Run `npm run dev`. The app opens at `http://localhost:3000` with Tailwind styles working. Add a `className="text-blue-500 text-3xl"` to any element to confirm.

---

### Pages Created (6 Items)

Each page should be a functional React component with at least a heading and basic layout. Full content will be completed in Week 40.

- [ ] **Home.jsx** -- Hero section with name and title, About section placeholder, Skills section placeholder, Featured Projects placeholder
- [ ] **Projects.jsx** -- Page heading, project grid layout (empty or with placeholder cards)
- [ ] **Blog.jsx** -- Page heading, post list layout (empty or with placeholder cards), pagination placeholder
- [ ] **SinglePost.jsx** -- Fetches post by ID from URL params, displays title, content, author, date, tags
- [ ] **Contact.jsx** -- Contact form with name, email, subject, message fields and submit button
- [ ] **Login.jsx** -- Login form with email and password fields, submit button, error message display

**Verification:** Navigate to each route in the browser (`/`, `/projects`, `/blog`, `/contact`, `/login`). Each page renders without errors.

---

### Components (5 Items)

- [ ] **Navbar.jsx** -- Logo/brand name, navigation links (Home, Projects, Blog, Contact), dark mode toggle button, login/logout button (conditional), responsive hamburger menu for mobile
- [ ] **Footer.jsx** -- Copyright text, social media links (GitHub, LinkedIn, Twitter), consistent styling across pages
- [ ] **ProjectCard.jsx** -- Displays project image, title, description (truncated), tech stack badges, live URL and GitHub URL buttons. Accepts props: `project`
- [ ] **PostCard.jsx** -- Displays post thumbnail, title, excerpt (first 100 characters of content), tags, date, "Read More" link. Accepts props: `post`
- [ ] **ProtectedRoute.jsx** -- Checks AuthContext for logged-in user. If authenticated, renders child routes via `<Outlet />`. If not, redirects to `/login` with `<Navigate>`.

**Verification:** The Navbar appears on every page with working links. The Footer appears at the bottom. Cards render correctly with sample/placeholder data.

---

### Routing Setup (4 Items)

- [ ] **React Router installed** and `<BrowserRouter>` wrapping the entire app in `App.jsx`
- [ ] **Public routes configured:** `/` (Home), `/projects` (Projects), `/projects/:id` (ProjectDetail), `/blog` (Blog), `/blog/:id` (SinglePost), `/contact` (Contact), `/login` (Login)
- [ ] **Protected admin routes configured:** `/admin/dashboard` (Dashboard), `/admin/posts` (ManagePosts), `/admin/projects` (ManageProjects), `/admin/messages` (Messages) -- all wrapped in `<ProtectedRoute>`
- [ ] **Navigation works:** Clicking links in the Navbar navigates to the correct page without a full page reload (client-side routing confirmed)

**Verification:** Click every link in the Navbar. Each page loads instantly without a browser refresh. Try navigating to `/admin/dashboard` while logged out -- you should be redirected to `/login`.

---

### API Integration (4 Items)

- [ ] **Axios instance created** (`services/api.js`) with base URL from environment variable, request interceptor that attaches JWT token from localStorage, and response interceptor that handles 401 errors
- [ ] **Auth service functions** work: `login(email, password)` calls POST `/auth/login` and stores token in localStorage, `logout()` clears token and user from localStorage
- [ ] **Post service functions** created: `getPosts()`, `getPost(id)`, `createPost(data)`, `updatePost(id, data)`, `deletePost(id)`
- [ ] **Project and Contact service functions** created: `getProjects()`, `getProject(id)`, `createProject(data)`, `submitContact(data)`, `getContacts()`

**Verification:** Open the browser console. Call a service function (e.g., from a useEffect in Home.jsx that calls `getProjects()`). Check the Network tab -- the request should go to `http://localhost:5000/api/projects` and return data.

---

## Integration Checklist

### End-to-End Connectivity (5 Items)

- [ ] **CORS configured** on the backend (`app.use(cors())`) -- frontend can make API calls without CORS errors in the browser console
- [ ] **Environment variables** set correctly: backend `.env` has MONGO_URI, JWT_SECRET, PORT; frontend `.env` has VITE_API_URL
- [ ] **Login flow works end-to-end:** Type email/password in the Login page form, submit, JWT token is stored in localStorage, user is redirected to admin dashboard, Navbar shows "Logout" instead of "Login"
- [ ] **Data flows from database to UI:** Create a test post via Postman, then visit the Blog page -- the post appears on screen
- [ ] **Git repository initialized** with a proper `.gitignore` that excludes `node_modules/`, `.env`, `dist/`, and `*.log` files

**Verification:** Open the app in the browser, log in, navigate to the admin dashboard. You should see the dashboard page without any console errors. Open the Network tab and confirm all API calls return 200 status.

---

## Milestone Check: What Should Be Working by End of Week 39

```
END OF WEEK 39 STATUS
======================

BACKEND (Should be 100% complete):
  [x] Server starts and connects to MongoDB
  [x] All 4 models defined and validated
  [x] All API endpoints respond correctly
  [x] JWT auth protects admin routes
  [x] Error handling returns clean JSON

FRONTEND (Should be ~60% complete):
  [x] App runs with React + Tailwind
  [x] All pages exist (some may be basic)
  [x] Routing works for all paths
  [x] Auth context manages login state
  [x] Dark mode toggle works
  [ ] Full UI for all pages (Week 40)
  [ ] All CRUD forms complete (Week 40)

INTEGRATION (Should be ~30% complete):
  [x] Frontend talks to backend
  [x] Login works end-to-end
  [x] CORS and env vars configured
  [ ] All features connected (Week 40)
  [ ] Testing complete (Week 40)
  [ ] Deployed to production (Week 40)
```

If you have completed all checked items above, you are on track. In Week 40, you will finish the remaining UI, connect all features, test everything, and deploy your portfolio to the internet.

---

**Total Checklist Items: 55** (Backend: 21, Frontend: 23, Integration: 5, Milestone: 6)
