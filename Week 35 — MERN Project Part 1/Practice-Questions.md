# Week 35 — MERN Project Part 1: Project Checklist

This week is project-based, so instead of traditional multiple-choice questions, you will work through a guided checklist. Each item represents a concrete task you need to complete to build a full-stack MERN application. Check off each item as you finish it, and make sure you understand why each step matters before moving on.

---

## Part 1: Backend Checklist

### Project Setup

- [ ] Initialize a `server/` directory with `npm init` — this creates your `package.json` and establishes the backend as its own Node.js project.
- [ ] Install dependencies: `express`, `mongoose`, `cors`, `dotenv`, `bcryptjs`, `jsonwebtoken` — each serves a specific role (server framework, database ODM, cross-origin requests, environment variables, password hashing, and token-based auth).
- [ ] Create a `.env` file with `MONGO_URI`, `JWT_SECRET`, and `PORT` — keeping sensitive configuration out of your source code is a fundamental security practice.
- [ ] Set up `server.js` with Express and MongoDB connection — this is your application entry point that wires everything together.

### Models

- [ ] Create a **User** model with fields: `name`, `email`, `password`, `role`, and `timestamps` — this defines how user data is stored and validated in your database.
- [ ] Create a **Task** model with fields: `title`, `description`, `status`, `priority`, `dueDate`, and a `user` reference — the user reference establishes ownership, linking each task to the user who created it.
- [ ] Create a **Category** model with fields: `name` and a `user` reference — categories let users organize their tasks in a personalized way.
- [ ] Add validation to all models — validation at the schema level prevents bad data from ever reaching the database.

### Routes & Controllers

- [ ] Auth routes: `POST /register`, `POST /login`, `GET /me`, `POST /logout` — these handle the full authentication lifecycle from account creation to session management.
- [ ] Task routes: `GET /`, `GET /:id`, `POST /`, `PUT /:id`, `DELETE /:id` — standard RESTful CRUD endpoints that follow conventional API design patterns.
- [ ] Category routes: `GET /`, `POST /`, `DELETE /:id` — a simpler resource that reinforces REST principles without the complexity of full CRUD.

### Middleware

- [ ] JWT authentication middleware — this intercepts requests and verifies the user's token before allowing access to protected routes.
- [ ] Error handling middleware — centralized error handling keeps your controllers clean and ensures consistent error responses across the API.
- [ ] Input validation — validating incoming request data prevents malformed or malicious input from causing unexpected behavior.

### Testing

- [ ] Test all auth routes with Postman or Thunder Client — verifying each endpoint manually helps you catch issues early before building the frontend.
- [ ] Test all task CRUD routes — confirm that creating, reading, updating, and deleting tasks all work as expected with valid data.
- [ ] Verify protected routes reject unauthorized requests — ensuring that unauthenticated or invalid tokens are properly rejected is critical for security.

---

## Part 2: Frontend Checklist

### Project Setup

- [ ] Initialize `client/` with Vite + React — Vite provides a fast development server and optimized build process for modern React applications.
- [ ] Install dependencies: `react-router-dom`, `axios`, `tailwindcss` — these handle client-side routing, HTTP requests, and utility-first styling respectively.
- [ ] Configure Tailwind CSS — proper configuration ensures your utility classes work and unused styles are purged in production.
- [ ] Set up project folder structure: `pages/`, `components/`, `context/`, `services/` — a clear folder structure makes your codebase maintainable and easier to navigate as it grows.

### Pages

- [ ] **Home** page (landing) — the first page visitors see; it should communicate the app's purpose and guide users to sign up or log in.
- [ ] **Login** page — a form that collects credentials and authenticates the user against your backend.
- [ ] **Register** page — a form for new user sign-up with proper validation feedback.
- [ ] **Dashboard** page (list tasks) — the main authenticated view where users see and manage all their tasks.
- [ ] **Create Task** page — a form for adding new tasks with all required fields.
- [ ] **Edit Task** page — a pre-populated form that lets users update existing task details.

### Components

- [ ] **Navbar** with navigation links — persistent navigation gives users a consistent way to move between pages.
- [ ] **TaskCard** component — a reusable card that displays task information in a clean, scannable format.
- [ ] **LoadingSpinner** component — visual feedback during API calls prevents users from thinking the app is broken.
- [ ] **ErrorMessage** component — a consistent way to display errors keeps the user informed when something goes wrong.
- [ ] **PrivateRoute** component — a wrapper that redirects unauthenticated users away from protected pages.

### Routing

- [ ] Set up React Router with all routes — defines the URL structure of your application and maps paths to pages.
- [ ] Protected routes for authenticated pages — ensures that only logged-in users can access the dashboard, task creation, and editing pages.
- [ ] Redirect logic for login/register — logged-in users should be redirected away from auth pages, and unauthenticated users should be sent to login.

### API Integration

- [ ] Create an axios instance with base URL — a configured instance avoids repeating the API base URL and lets you attach headers globally.
- [ ] Auth service (register, login, logout) — encapsulating auth API calls in a service module keeps your components clean and focused on UI.
- [ ] Task service (CRUD operations) — a dedicated service for task-related API calls makes data fetching reusable across components.
- [ ] **AuthContext** for state management — React Context provides a way to share authentication state (user info, token) across the entire component tree without prop drilling.

---

## Part 3: Integration Checklist

- [ ] Connect registration form to backend — the form should send user data to `POST /register` and handle both success and error responses.
- [ ] Connect login form to backend — on successful login, store the JWT token and redirect the user to the dashboard.
- [ ] Display tasks from API on dashboard — fetch tasks on mount and render them using your TaskCard component.
- [ ] Create new task from form — the create form should POST to the API, then redirect to the dashboard with the new task visible.
- [ ] Edit existing task — pre-fill the form with current data, send a PUT request on submit, and reflect the changes immediately.
- [ ] Delete task with confirmation — always confirm before deleting; this prevents accidental data loss and is a standard UX practice.
- [ ] Protected routes working correctly — verify that unauthenticated users cannot access any protected page and are redirected to login.
- [ ] Loading states on all API calls — every network request should show a loading indicator so users know the app is working.
- [ ] Error handling on all API calls — network failures, validation errors, and server errors should all be caught and displayed to the user gracefully.

---

## Milestone Check

At this point, you should have a fully functional MERN application with user registration, login, and complete task management (create, read, update, delete). The backend should have a clean REST API with JWT-based authentication, and the frontend should be a React app that communicates with your API, protects routes, and provides clear feedback through loading states and error messages. If every item above is checked off, you have built a production-style full-stack application and are ready for Part 2, where you will add advanced features and polish.
