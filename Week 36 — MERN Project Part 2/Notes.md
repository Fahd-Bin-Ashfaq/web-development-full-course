# Week 36 — MERN Project Part 2

> **Prerequisites:** Week 35 (MERN Project Part 1) completed with a working Express API, MongoDB connection, and a basic React frontend with routing.
>
> **Goal:** Complete the full-stack MERN project by adding authentication, all CRUD operations, search/filter/pagination, Tailwind CSS styling, responsive design, and thorough testing.

---

## Table of Contents

1. [Adding Authentication (Register/Login/Logout)](#1-adding-authentication-registerloginlogout)
2. [Implementing All CRUD Features](#2-implementing-all-crud-features)
3. [Adding Search, Filter, and Pagination](#3-adding-search-filter-and-pagination)
4. [Styling with Tailwind CSS](#4-styling-with-tailwind-css)
5. [Responsive Design](#5-responsive-design)
6. [Testing and Bug Fixing](#6-testing-and-bug-fixing)
7. [Code Review Checklist](#7-code-review-checklist)
8. [Project Completion Criteria](#8-project-completion-criteria)
9. [Summary](#9-summary)

---

## 1. Adding Authentication (Register/Login/Logout)

### Why Authentication Matters

Every real application needs to know who is using it. Authentication is the process of verifying a user's identity. Without it, anyone could access anyone else's data, modify records they should not touch, or delete information that belongs to someone else.

> **Real-life analogy: A Hotel Key Card**
>
> When you check into a hotel, the front desk verifies your identity (registration/login) and gives you a key card (token). That key card opens only your room. You cannot open other guests' rooms. When you check out, the key card is deactivated (logout). The hotel does not leave every room unlocked for everyone to walk in.

```
  AUTHENTICATION FLOW
  =====================

  1. REGISTER
     User fills form --> POST /api/auth/register --> Server hashes password
                                                      --> Saves to MongoDB
                                                      --> Returns JWT token

  2. LOGIN
     User enters credentials --> POST /api/auth/login --> Server checks password
                                                          --> If valid, returns JWT
                                                          --> If invalid, returns error

  3. PROTECTED REQUEST
     User sends request + JWT in header --> Server verifies JWT
                                            --> If valid, processes request
                                            --> If invalid, returns 401

  4. LOGOUT
     User clicks logout --> Client removes JWT from localStorage
                            --> Redirects to login page
```

### Registration Form with Validation

The registration form collects the user's name, email, and password. Before sending any data to the server, the form should validate that all fields are filled, the email format is correct, and the password meets minimum requirements.

```jsx
// src/pages/Register.jsx
import { useState } from "react";
import { useNavigate, Link } from "react-router-dom";
import axios from "axios";

function Register() {
  const [formData, setFormData] = useState({
    name: "",
    email: "",
    password: "",
    confirmPassword: "",
  });
  const [errors, setErrors] = useState({});
  const [serverError, setServerError] = useState("");
  const [loading, setLoading] = useState(false);
  const navigate = useNavigate();

  // Validate all fields before submission
  function validate() {
    const newErrors = {};

    if (!formData.name.trim()) {
      newErrors.name = "Name is required";
    }

    if (!formData.email.trim()) {
      newErrors.email = "Email is required";
    } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(formData.email)) {
      newErrors.email = "Please enter a valid email address";
    }

    if (!formData.password) {
      newErrors.password = "Password is required";
    } else if (formData.password.length < 6) {
      newErrors.password = "Password must be at least 6 characters";
    }

    if (formData.password !== formData.confirmPassword) {
      newErrors.confirmPassword = "Passwords do not match";
    }

    setErrors(newErrors);
    return Object.keys(newErrors).length === 0;
  }

  function handleChange(e) {
    setFormData({ ...formData, [e.target.name]: e.target.value });
    // Clear the error for this field as user types
    if (errors[e.target.name]) {
      setErrors({ ...errors, [e.target.name]: "" });
    }
  }

  async function handleSubmit(e) {
    e.preventDefault();
    setServerError("");

    if (!validate()) return;

    setLoading(true);
    try {
      const response = await axios.post("/api/auth/register", {
        name: formData.name,
        email: formData.email,
        password: formData.password,
      });

      // Save the token and redirect
      localStorage.setItem("token", response.data.token);
      navigate("/dashboard");
    } catch (error) {
      if (error.response && error.response.data.message) {
        setServerError(error.response.data.message);
      } else {
        setServerError("Registration failed. Please try again.");
      }
    } finally {
      setLoading(false);
    }
  }

  return (
    <div>
      <h2>Create an Account</h2>

      {serverError && <p style={{ color: "red" }}>{serverError}</p>}

      <form onSubmit={handleSubmit}>
        <div>
          <label>Name</label>
          <input
            type="text"
            name="name"
            value={formData.name}
            onChange={handleChange}
          />
          {errors.name && <span style={{ color: "red" }}>{errors.name}</span>}
        </div>

        <div>
          <label>Email</label>
          <input
            type="email"
            name="email"
            value={formData.email}
            onChange={handleChange}
          />
          {errors.email && <span style={{ color: "red" }}>{errors.email}</span>}
        </div>

        <div>
          <label>Password</label>
          <input
            type="password"
            name="password"
            value={formData.password}
            onChange={handleChange}
          />
          {errors.password && (
            <span style={{ color: "red" }}>{errors.password}</span>
          )}
        </div>

        <div>
          <label>Confirm Password</label>
          <input
            type="password"
            name="confirmPassword"
            value={formData.confirmPassword}
            onChange={handleChange}
          />
          {errors.confirmPassword && (
            <span style={{ color: "red" }}>{errors.confirmPassword}</span>
          )}
        </div>

        <button type="submit" disabled={loading}>
          {loading ? "Registering..." : "Register"}
        </button>
      </form>

      <p>
        Already have an account? <Link to="/login">Login here</Link>
      </p>
    </div>
  );
}

export default Register;
```

### Login Form with Error Handling

The login form is simpler than registration. It collects email and password, sends them to the server, and either receives a token (success) or an error message (failure).

```jsx
// src/pages/Login.jsx
import { useState } from "react";
import { useNavigate, Link } from "react-router-dom";
import { useAuth } from "../context/AuthContext";
import axios from "axios";

function Login() {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const [error, setError] = useState("");
  const [loading, setLoading] = useState(false);
  const navigate = useNavigate();
  const { login } = useAuth();

  async function handleSubmit(e) {
    e.preventDefault();
    setError("");

    if (!email || !password) {
      setError("Please fill in all fields");
      return;
    }

    setLoading(true);
    try {
      const response = await axios.post("/api/auth/login", { email, password });
      login(response.data.token, response.data.user);
      navigate("/dashboard");
    } catch (error) {
      if (error.response && error.response.status === 401) {
        setError("Invalid email or password");
      } else if (error.response && error.response.data.message) {
        setError(error.response.data.message);
      } else {
        setError("Login failed. Please try again.");
      }
    } finally {
      setLoading(false);
    }
  }

  return (
    <div>
      <h2>Login</h2>

      {error && <p style={{ color: "red" }}>{error}</p>}

      <form onSubmit={handleSubmit}>
        <div>
          <label>Email</label>
          <input
            type="email"
            value={email}
            onChange={(e) => setEmail(e.target.value)}
          />
        </div>

        <div>
          <label>Password</label>
          <input
            type="password"
            value={password}
            onChange={(e) => setPassword(e.target.value)}
          />
        </div>

        <button type="submit" disabled={loading}>
          {loading ? "Logging in..." : "Login"}
        </button>
      </form>

      <p>
        Don't have an account? <Link to="/register">Register here</Link>
      </p>
    </div>
  );
}

export default Login;
```

### AuthContext for Persisting Login State

The AuthContext is the central piece that holds the user's authentication state and makes it available to every component in the application. When the app loads, the context checks localStorage for an existing token and validates it. This way, users do not need to log in again every time they refresh the page.

```jsx
// src/context/AuthContext.jsx
import { createContext, useContext, useState, useEffect } from "react";
import axios from "axios";

const AuthContext = createContext();

export function AuthProvider({ children }) {
  const [user, setUser] = useState(null);
  const [token, setToken] = useState(localStorage.getItem("token"));
  const [loading, setLoading] = useState(true);

  // On app load, verify the stored token
  useEffect(() => {
    async function verifyToken() {
      if (!token) {
        setLoading(false);
        return;
      }

      try {
        // Set the token in axios default headers
        axios.defaults.headers.common["Authorization"] = `Bearer ${token}`;
        const response = await axios.get("/api/auth/me");
        setUser(response.data.user);
      } catch (error) {
        // Token is invalid or expired
        localStorage.removeItem("token");
        setToken(null);
        delete axios.defaults.headers.common["Authorization"];
      } finally {
        setLoading(false);
      }
    }

    verifyToken();
  }, [token]);

  function login(newToken, userData) {
    localStorage.setItem("token", newToken);
    setToken(newToken);
    setUser(userData);
    axios.defaults.headers.common["Authorization"] = `Bearer ${newToken}`;
  }

  function logout() {
    localStorage.removeItem("token");
    setToken(null);
    setUser(null);
    delete axios.defaults.headers.common["Authorization"];
  }

  return (
    <AuthContext.Provider value={{ user, token, login, logout, loading }}>
      {children}
    </AuthContext.Provider>
  );
}

export function useAuth() {
  return useContext(AuthContext);
}
```

### Protecting Routes

Once authentication is in place, certain pages should only be accessible to logged-in users. A `ProtectedRoute` component wraps those pages and redirects unauthenticated users to the login page.

```jsx
// src/components/ProtectedRoute.jsx
import { Navigate } from "react-router-dom";
import { useAuth } from "../context/AuthContext";

function ProtectedRoute({ children }) {
  const { user, loading } = useAuth();

  if (loading) {
    return <p>Loading...</p>;
  }

  if (!user) {
    return <Navigate to="/login" />;
  }

  return children;
}

export default ProtectedRoute;
```

```
  AUTH STATE FLOW
  ================

  App Loads
     |
     v
  Check localStorage for token
     |
     +-- No token --> Show Login page
     |
     +-- Token found --> Verify with server (GET /api/auth/me)
                            |
                            +-- Valid --> Set user in context --> Show Dashboard
                            |
                            +-- Invalid --> Clear token --> Show Login page
```

---

## 2. Implementing All CRUD Features

### Understanding CRUD

CRUD stands for Create, Read, Update, and Delete. These are the four fundamental operations you can perform on any data. Every application that manages data -- whether it is a to-do list, a blog, an e-commerce store, or a social media platform -- relies on these four operations.

> **Real-life analogy: A Notebook**
>
> Think of a physical notebook where you keep a list of tasks. **Create** is writing a new task on the page. **Read** is looking at the page to see what tasks are there. **Update** is crossing out a word and writing the corrected version above it. **Delete** is erasing a task entirely when it is no longer needed. Your MERN application does the same thing, but with a database instead of paper.

```
  THE CRUD CYCLE
  ================

  +----------+     +-----------+     +----------+     +----------+
  |          |     |           |     |          |     |          |
  | CREATE   |---->|   READ    |---->|  UPDATE  |---->|  DELETE  |
  |          |     |           |     |          |     |          |
  | POST     |     | GET       |     | PUT/PATCH|     | DELETE   |
  | /api/    |     | /api/     |     | /api/:id |     | /api/:id |
  | tasks    |     | tasks     |     |          |     |          |
  +----------+     +-----------+     +----------+     +----------+
       |                                                    |
       |                                                    |
       +----------------------------------------------------+
                     Cycle repeats as user
                     interacts with the app
```

### Create: Adding New Items

The create operation involves a form where the user enters data, validation to ensure the data is correct, an API call to save the data, and a redirect to the list view after success.

```jsx
// src/pages/CreateTask.jsx
import { useState } from "react";
import { useNavigate } from "react-router-dom";
import axios from "axios";

function CreateTask() {
  const [formData, setFormData] = useState({
    title: "",
    description: "",
    priority: "medium",
    status: "pending",
    dueDate: "",
  });
  const [errors, setErrors] = useState({});
  const [loading, setLoading] = useState(false);
  const navigate = useNavigate();

  function validate() {
    const newErrors = {};
    if (!formData.title.trim()) {
      newErrors.title = "Title is required";
    } else if (formData.title.length > 100) {
      newErrors.title = "Title must be under 100 characters";
    }
    if (formData.description.length > 500) {
      newErrors.description = "Description must be under 500 characters";
    }
    setErrors(newErrors);
    return Object.keys(newErrors).length === 0;
  }

  function handleChange(e) {
    setFormData({ ...formData, [e.target.name]: e.target.value });
  }

  async function handleSubmit(e) {
    e.preventDefault();
    if (!validate()) return;

    setLoading(true);
    try {
      await axios.post("/api/tasks", formData);
      navigate("/dashboard");
    } catch (error) {
      console.error("Failed to create task:", error);
    } finally {
      setLoading(false);
    }
  }

  return (
    <div>
      <h2>Create New Task</h2>
      <form onSubmit={handleSubmit}>
        <div>
          <label>Title</label>
          <input
            type="text"
            name="title"
            value={formData.title}
            onChange={handleChange}
          />
          {errors.title && <span>{errors.title}</span>}
        </div>

        <div>
          <label>Description</label>
          <textarea
            name="description"
            value={formData.description}
            onChange={handleChange}
            rows="4"
          />
          {errors.description && <span>{errors.description}</span>}
        </div>

        <div>
          <label>Priority</label>
          <select
            name="priority"
            value={formData.priority}
            onChange={handleChange}
          >
            <option value="low">Low</option>
            <option value="medium">Medium</option>
            <option value="high">High</option>
          </select>
        </div>

        <div>
          <label>Due Date</label>
          <input
            type="date"
            name="dueDate"
            value={formData.dueDate}
            onChange={handleChange}
          />
        </div>

        <button type="submit" disabled={loading}>
          {loading ? "Creating..." : "Create Task"}
        </button>
      </form>
    </div>
  );
}

export default CreateTask;
```

### Read: Displaying Items

Reading data involves two views: a **list view** that shows all items and a **detail view** that shows a single item with full information.

```jsx
// src/pages/Dashboard.jsx (List View)
import { useState, useEffect } from "react";
import { Link } from "react-router-dom";
import axios from "axios";

function Dashboard() {
  const [tasks, setTasks] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    async function fetchTasks() {
      try {
        const response = await axios.get("/api/tasks");
        setTasks(response.data.tasks);
      } catch (error) {
        console.error("Failed to fetch tasks:", error);
      } finally {
        setLoading(false);
      }
    }
    fetchTasks();
  }, []);

  if (loading) return <p>Loading tasks...</p>;

  return (
    <div>
      <h2>Your Tasks</h2>
      <Link to="/tasks/new">+ Create New Task</Link>

      {tasks.length === 0 ? (
        <p>No tasks yet. Create your first task!</p>
      ) : (
        <div>
          {tasks.map((task) => (
            <div key={task._id} style={{ border: "1px solid #ccc", padding: "16px", marginBottom: "12px" }}>
              <h3>
                <Link to={`/tasks/${task._id}`}>{task.title}</Link>
              </h3>
              <p>{task.description}</p>
              <span>Priority: {task.priority}</span>
              <span> | Status: {task.status}</span>
            </div>
          ))}
        </div>
      )}
    </div>
  );
}

export default Dashboard;
```

```jsx
// src/pages/TaskDetail.jsx (Single Item View)
import { useState, useEffect } from "react";
import { useParams, useNavigate, Link } from "react-router-dom";
import axios from "axios";

function TaskDetail() {
  const { id } = useParams();
  const navigate = useNavigate();
  const [task, setTask] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    async function fetchTask() {
      try {
        const response = await axios.get(`/api/tasks/${id}`);
        setTask(response.data.task);
      } catch (error) {
        console.error("Failed to fetch task:", error);
        navigate("/dashboard");
      } finally {
        setLoading(false);
      }
    }
    fetchTask();
  }, [id, navigate]);

  if (loading) return <p>Loading...</p>;
  if (!task) return <p>Task not found.</p>;

  return (
    <div>
      <h2>{task.title}</h2>
      <p>{task.description}</p>
      <p>Priority: {task.priority}</p>
      <p>Status: {task.status}</p>
      <p>Due Date: {task.dueDate ? new Date(task.dueDate).toLocaleDateString() : "No due date"}</p>
      <p>Created: {new Date(task.createdAt).toLocaleDateString()}</p>

      <Link to={`/tasks/${task._id}/edit`}>Edit Task</Link>
    </div>
  );
}

export default TaskDetail;
```

### Update: Editing Existing Items

The update form looks similar to the create form but is pre-filled with existing data. When the user submits, a PATCH request is sent instead of POST.

```jsx
// src/pages/EditTask.jsx
import { useState, useEffect } from "react";
import { useParams, useNavigate } from "react-router-dom";
import axios from "axios";

function EditTask() {
  const { id } = useParams();
  const navigate = useNavigate();
  const [formData, setFormData] = useState({
    title: "",
    description: "",
    priority: "medium",
    status: "pending",
    dueDate: "",
  });
  const [loading, setLoading] = useState(true);
  const [saving, setSaving] = useState(false);

  // Fetch existing task data to pre-fill the form
  useEffect(() => {
    async function fetchTask() {
      try {
        const response = await axios.get(`/api/tasks/${id}`);
        const task = response.data.task;
        setFormData({
          title: task.title,
          description: task.description || "",
          priority: task.priority,
          status: task.status,
          dueDate: task.dueDate ? task.dueDate.split("T")[0] : "",
        });
      } catch (error) {
        console.error("Failed to fetch task:", error);
        navigate("/dashboard");
      } finally {
        setLoading(false);
      }
    }
    fetchTask();
  }, [id, navigate]);

  function handleChange(e) {
    setFormData({ ...formData, [e.target.name]: e.target.value });
  }

  async function handleSubmit(e) {
    e.preventDefault();
    if (!formData.title.trim()) return;

    setSaving(true);
    try {
      await axios.patch(`/api/tasks/${id}`, formData);
      navigate(`/tasks/${id}`);
    } catch (error) {
      console.error("Failed to update task:", error);
    } finally {
      setSaving(false);
    }
  }

  if (loading) return <p>Loading task...</p>;

  return (
    <div>
      <h2>Edit Task</h2>
      <form onSubmit={handleSubmit}>
        <div>
          <label>Title</label>
          <input
            type="text"
            name="title"
            value={formData.title}
            onChange={handleChange}
          />
        </div>

        <div>
          <label>Description</label>
          <textarea
            name="description"
            value={formData.description}
            onChange={handleChange}
            rows="4"
          />
        </div>

        <div>
          <label>Priority</label>
          <select name="priority" value={formData.priority} onChange={handleChange}>
            <option value="low">Low</option>
            <option value="medium">Medium</option>
            <option value="high">High</option>
          </select>
        </div>

        <div>
          <label>Status</label>
          <select name="status" value={formData.status} onChange={handleChange}>
            <option value="pending">Pending</option>
            <option value="in-progress">In Progress</option>
            <option value="completed">Completed</option>
          </select>
        </div>

        <div>
          <label>Due Date</label>
          <input
            type="date"
            name="dueDate"
            value={formData.dueDate}
            onChange={handleChange}
          />
        </div>

        <button type="submit" disabled={saving}>
          {saving ? "Saving..." : "Save Changes"}
        </button>
      </form>
    </div>
  );
}

export default EditTask;
```

### Delete: Removing Items with Confirmation

Deleting should never happen without confirmation. The user should be asked "Are you sure?" before the item is permanently removed. Optimistic UI means we remove the item from the screen immediately and only show an error if the server request fails.

```jsx
// src/components/DeleteButton.jsx
import { useState } from "react";
import axios from "axios";

function DeleteButton({ taskId, onDelete }) {
  const [showConfirm, setShowConfirm] = useState(false);
  const [deleting, setDeleting] = useState(false);

  async function handleDelete() {
    setDeleting(true);

    // Optimistic UI: call onDelete immediately to remove from list
    onDelete(taskId);

    try {
      await axios.delete(`/api/tasks/${taskId}`);
    } catch (error) {
      console.error("Failed to delete task:", error);
      // In a real app, you would restore the item here
      alert("Failed to delete task. Please refresh the page.");
    } finally {
      setDeleting(false);
      setShowConfirm(false);
    }
  }

  if (showConfirm) {
    return (
      <div>
        <p>Are you sure you want to delete this task?</p>
        <button onClick={handleDelete} disabled={deleting}>
          {deleting ? "Deleting..." : "Yes, Delete"}
        </button>
        <button onClick={() => setShowConfirm(false)}>Cancel</button>
      </div>
    );
  }

  return <button onClick={() => setShowConfirm(true)}>Delete</button>;
}

export default DeleteButton;
```

| Operation | HTTP Method | Endpoint        | Request Body           | Response               |
|-----------|-------------|-----------------|------------------------|------------------------|
| Create    | POST        | `/api/tasks`    | `{ title, ... }`       | `{ task: newTask }`    |
| Read All  | GET         | `/api/tasks`    | None                   | `{ tasks: [...] }`     |
| Read One  | GET         | `/api/tasks/:id`| None                   | `{ task: {...} }`      |
| Update    | PATCH       | `/api/tasks/:id`| `{ fields to update }` | `{ task: updatedTask }`|
| Delete    | DELETE      | `/api/tasks/:id`| None                   | `{ message: "..." }`  |

---

## 3. Adding Search, Filter, and Pagination

### Why Search, Filter, and Pagination Matter

When your application has a handful of tasks, showing them all on one page works fine. But as data grows -- ten tasks, fifty tasks, hundreds of tasks -- users need ways to find what they are looking for without scrolling through everything.

> **Real-life analogy: A Library**
>
> A library does not dump all its books into one pile. It organizes them on shelves by category (filtering), provides a search catalog (search), and spreads books across multiple aisles (pagination). Without these systems, finding a single book among thousands would be nearly impossible.

```
  SEARCH, FILTER, PAGINATION FLOW
  ==================================

  User Interface
  +-------------------------------------------------------+
  |  [Search: ________]  [Status: All v]  [Priority: v]   |
  |  [Sort by: Date v]                                     |
  +-------------------------------------------------------+
        |              |              |             |
        v              v              v             v
  Build Query String:
  /api/tasks?search=deploy&status=pending&priority=high&sort=-createdAt&page=1&limit=10
        |
        v
  Backend receives query --> Builds MongoDB filter --> Returns paginated results
        |
        v
  +-------------------------------------------------------+
  |  Task 1: Deploy to staging         Priority: High      |
  |  Task 2: Deploy documentation      Priority: High      |
  +-------------------------------------------------------+
  |  [< Prev]  Page 1 of 3  [Next >]                      |
  +-------------------------------------------------------+
```

### Backend: Query Handling

The backend controller needs to parse query parameters and build a MongoDB query dynamically.

```javascript
// controllers/taskController.js
async function getTasks(req, res) {
  try {
    const { search, status, priority, sort, page = 1, limit = 10 } = req.query;

    // Build the filter object
    const filter = { user: req.user._id };

    // Search by title or description
    if (search) {
      filter.$or = [
        { title: { $regex: search, $options: "i" } },
        { description: { $regex: search, $options: "i" } },
      ];
    }

    // Filter by status
    if (status && status !== "all") {
      filter.status = status;
    }

    // Filter by priority
    if (priority && priority !== "all") {
      filter.priority = priority;
    }

    // Build sort object
    let sortObj = { createdAt: -1 }; // Default: newest first
    if (sort === "oldest") sortObj = { createdAt: 1 };
    if (sort === "priority") sortObj = { priority: -1 };
    if (sort === "title") sortObj = { title: 1 };
    if (sort === "dueDate") sortObj = { dueDate: 1 };

    // Calculate pagination
    const pageNum = parseInt(page);
    const limitNum = parseInt(limit);
    const skip = (pageNum - 1) * limitNum;

    // Execute query with pagination
    const tasks = await Task.find(filter)
      .sort(sortObj)
      .skip(skip)
      .limit(limitNum);

    // Get total count for pagination info
    const total = await Task.countDocuments(filter);

    res.json({
      tasks,
      currentPage: pageNum,
      totalPages: Math.ceil(total / limitNum),
      totalTasks: total,
    });
  } catch (error) {
    res.status(500).json({ message: "Server error" });
  }
}
```

### Frontend: Search Bar with Debounce

Debounce means waiting until the user stops typing before sending the API request. Without debounce, every single keystroke would trigger a network request, which wastes bandwidth and overloads the server.

```jsx
// src/hooks/useDebounce.js
import { useState, useEffect } from "react";

function useDebounce(value, delay = 500) {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const timer = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);

    // Cleanup: if the value changes before the delay, cancel the previous timer
    return () => clearTimeout(timer);
  }, [value, delay]);

  return debouncedValue;
}

export default useDebounce;
```

### Frontend: Complete Search, Filter, and Pagination Component

```jsx
// src/pages/Dashboard.jsx (with search, filter, and pagination)
import { useState, useEffect } from "react";
import { Link } from "react-router-dom";
import axios from "axios";
import useDebounce from "../hooks/useDebounce";
import DeleteButton from "../components/DeleteButton";

function Dashboard() {
  const [tasks, setTasks] = useState([]);
  const [loading, setLoading] = useState(true);

  // Search, filter, and sort state
  const [search, setSearch] = useState("");
  const [statusFilter, setStatusFilter] = useState("all");
  const [priorityFilter, setPriorityFilter] = useState("all");
  const [sortBy, setSortBy] = useState("newest");

  // Pagination state
  const [currentPage, setCurrentPage] = useState(1);
  const [totalPages, setTotalPages] = useState(1);
  const [totalTasks, setTotalTasks] = useState(0);

  // Debounce the search input
  const debouncedSearch = useDebounce(search, 500);

  useEffect(() => {
    async function fetchTasks() {
      setLoading(true);
      try {
        const params = new URLSearchParams();
        if (debouncedSearch) params.append("search", debouncedSearch);
        if (statusFilter !== "all") params.append("status", statusFilter);
        if (priorityFilter !== "all") params.append("priority", priorityFilter);
        params.append("sort", sortBy);
        params.append("page", currentPage);
        params.append("limit", 10);

        const response = await axios.get(`/api/tasks?${params.toString()}`);
        setTasks(response.data.tasks);
        setTotalPages(response.data.totalPages);
        setTotalTasks(response.data.totalTasks);
      } catch (error) {
        console.error("Failed to fetch tasks:", error);
      } finally {
        setLoading(false);
      }
    }
    fetchTasks();
  }, [debouncedSearch, statusFilter, priorityFilter, sortBy, currentPage]);

  // Reset to page 1 when filters change
  useEffect(() => {
    setCurrentPage(1);
  }, [debouncedSearch, statusFilter, priorityFilter, sortBy]);

  function handleDelete(taskId) {
    setTasks(tasks.filter((task) => task._id !== taskId));
    setTotalTasks((prev) => prev - 1);
  }

  return (
    <div>
      <h2>Your Tasks ({totalTasks})</h2>
      <Link to="/tasks/new">+ Create New Task</Link>

      {/* Search Bar */}
      <div>
        <input
          type="text"
          placeholder="Search tasks..."
          value={search}
          onChange={(e) => setSearch(e.target.value)}
        />
      </div>

      {/* Filters */}
      <div>
        <select value={statusFilter} onChange={(e) => setStatusFilter(e.target.value)}>
          <option value="all">All Statuses</option>
          <option value="pending">Pending</option>
          <option value="in-progress">In Progress</option>
          <option value="completed">Completed</option>
        </select>

        <select value={priorityFilter} onChange={(e) => setPriorityFilter(e.target.value)}>
          <option value="all">All Priorities</option>
          <option value="low">Low</option>
          <option value="medium">Medium</option>
          <option value="high">High</option>
        </select>

        <select value={sortBy} onChange={(e) => setSortBy(e.target.value)}>
          <option value="newest">Newest First</option>
          <option value="oldest">Oldest First</option>
          <option value="priority">Priority</option>
          <option value="title">Title (A-Z)</option>
          <option value="dueDate">Due Date</option>
        </select>
      </div>

      {/* Task List */}
      {loading ? (
        <p>Loading...</p>
      ) : tasks.length === 0 ? (
        <p>No tasks found.</p>
      ) : (
        <div>
          {tasks.map((task) => (
            <div key={task._id}>
              <h3><Link to={`/tasks/${task._id}`}>{task.title}</Link></h3>
              <p>{task.description}</p>
              <span>Priority: {task.priority}</span>
              <span> | Status: {task.status}</span>
              <div>
                <Link to={`/tasks/${task._id}/edit`}>Edit</Link>
                <DeleteButton taskId={task._id} onDelete={handleDelete} />
              </div>
            </div>
          ))}
        </div>
      )}

      {/* Pagination */}
      {totalPages > 1 && (
        <div>
          <button
            onClick={() => setCurrentPage((prev) => Math.max(prev - 1, 1))}
            disabled={currentPage === 1}
          >
            Previous
          </button>

          {Array.from({ length: totalPages }, (_, i) => i + 1).map((page) => (
            <button
              key={page}
              onClick={() => setCurrentPage(page)}
              style={{ fontWeight: currentPage === page ? "bold" : "normal" }}
            >
              {page}
            </button>
          ))}

          <button
            onClick={() => setCurrentPage((prev) => Math.min(prev + 1, totalPages))}
            disabled={currentPage === totalPages}
          >
            Next
          </button>
        </div>
      )}
    </div>
  );
}

export default Dashboard;
```

| Feature    | What It Does                           | User Benefit                      |
|------------|----------------------------------------|-----------------------------------|
| Search     | Finds tasks by title or description    | Locate specific tasks instantly   |
| Status     | Filters by pending/in-progress/done    | Focus on what needs attention     |
| Priority   | Filters by low/medium/high             | Tackle important tasks first      |
| Sort       | Orders by date, priority, or title     | View tasks in meaningful order    |
| Pagination | Shows 10 tasks per page                | Keeps the page fast and readable  |

---

## 4. Styling with Tailwind CSS

### Why Tailwind CSS for This Project

Up to this point, the components have minimal styling. Tailwind CSS allows you to style components directly in the JSX using utility classes, which means no separate CSS files and no coming up with class names. The result is faster development and consistent design.

> **Real-life analogy: Building with LEGO vs Sculpting from Clay**
>
> Traditional CSS is like sculpting from clay. You have total creative freedom, but you have to build everything from scratch. Tailwind CSS is like building with LEGO bricks. Each brick (utility class) does one specific thing: `bg-blue-500` makes the background blue, `p-4` adds padding, `rounded-lg` rounds the corners. You snap bricks together to build exactly what you need, quickly and consistently.

### Applying Tailwind to the Login Page

Here is the Login page before and after applying Tailwind classes.

**Before Tailwind (plain HTML):**

```jsx
<div>
  <h2>Login</h2>
  {error && <p style={{ color: "red" }}>{error}</p>}
  <form onSubmit={handleSubmit}>
    <div>
      <label>Email</label>
      <input type="email" value={email} onChange={(e) => setEmail(e.target.value)} />
    </div>
    <div>
      <label>Password</label>
      <input type="password" value={password} onChange={(e) => setPassword(e.target.value)} />
    </div>
    <button type="submit">Login</button>
  </form>
</div>
```

**After Tailwind:**

```jsx
<div className="min-h-screen flex items-center justify-center bg-gray-50">
  <div className="max-w-md w-full bg-white rounded-xl shadow-lg p-8">
    <h2 className="text-2xl font-bold text-gray-900 text-center mb-6">
      Login
    </h2>

    {error && (
      <div className="bg-red-50 border border-red-200 text-red-700 px-4 py-3 rounded-lg mb-4">
        {error}
      </div>
    )}

    <form onSubmit={handleSubmit} className="space-y-4">
      <div>
        <label className="block text-sm font-medium text-gray-700 mb-1">
          Email
        </label>
        <input
          type="email"
          value={email}
          onChange={(e) => setEmail(e.target.value)}
          className="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none transition"
        />
      </div>

      <div>
        <label className="block text-sm font-medium text-gray-700 mb-1">
          Password
        </label>
        <input
          type="password"
          value={password}
          onChange={(e) => setPassword(e.target.value)}
          className="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none transition"
        />
      </div>

      <button
        type="submit"
        disabled={loading}
        className="w-full bg-blue-600 text-white py-2 px-4 rounded-lg hover:bg-blue-700 disabled:bg-blue-300 transition font-medium"
      >
        {loading ? "Logging in..." : "Login"}
      </button>
    </form>

    <p className="text-center text-sm text-gray-600 mt-6">
      Don't have an account?{" "}
      <Link to="/register" className="text-blue-600 hover:text-blue-800 font-medium">
        Register here
      </Link>
    </p>
  </div>
</div>
```

### Design System: Color Scheme and Component Styles

A consistent design system ensures every page looks like it belongs to the same application.

```
  DESIGN SYSTEM
  ===============

  Colors:
  +------------------+-------------------+--------------------+
  | Primary          | Secondary         | Accent             |
  | blue-600         | gray-100 to 900   | green-500 / red-500|
  | (buttons, links) | (text, borders)   | (success, error)   |
  +------------------+-------------------+--------------------+

  Spacing Scale:
  p-1 (4px)  p-2 (8px)  p-4 (16px)  p-6 (24px)  p-8 (32px)

  Border Radius:
  rounded (4px)  rounded-lg (8px)  rounded-xl (12px)  rounded-full (50%)

  Shadows:
  shadow-sm (subtle)  shadow (default)  shadow-lg (prominent)
```

### Styling Task Cards

```jsx
// Task card with Tailwind
<div className="bg-white rounded-xl shadow-sm border border-gray-200 p-6 hover:shadow-md transition">
  <div className="flex items-start justify-between">
    <div>
      <h3 className="text-lg font-semibold text-gray-900">{task.title}</h3>
      <p className="text-gray-600 mt-1 text-sm">{task.description}</p>
    </div>
    <span
      className={`px-3 py-1 rounded-full text-xs font-medium ${
        task.priority === "high"
          ? "bg-red-100 text-red-700"
          : task.priority === "medium"
          ? "bg-yellow-100 text-yellow-700"
          : "bg-green-100 text-green-700"
      }`}
    >
      {task.priority}
    </span>
  </div>

  <div className="flex items-center justify-between mt-4 pt-4 border-t border-gray-100">
    <span
      className={`text-sm font-medium ${
        task.status === "completed"
          ? "text-green-600"
          : task.status === "in-progress"
          ? "text-blue-600"
          : "text-gray-500"
      }`}
    >
      {task.status}
    </span>
    <div className="flex gap-2">
      <Link
        to={`/tasks/${task._id}/edit`}
        className="text-sm text-blue-600 hover:text-blue-800"
      >
        Edit
      </Link>
      <button className="text-sm text-red-600 hover:text-red-800">
        Delete
      </button>
    </div>
  </div>
</div>
```

### Styling Buttons

```jsx
{/* Primary Button */}
<button className="bg-blue-600 text-white px-6 py-2 rounded-lg hover:bg-blue-700 transition font-medium">
  Create Task
</button>

{/* Secondary Button */}
<button className="bg-gray-200 text-gray-800 px-6 py-2 rounded-lg hover:bg-gray-300 transition font-medium">
  Cancel
</button>

{/* Danger Button */}
<button className="bg-red-600 text-white px-6 py-2 rounded-lg hover:bg-red-700 transition font-medium">
  Delete
</button>

{/* Outline Button */}
<button className="border-2 border-blue-600 text-blue-600 px-6 py-2 rounded-lg hover:bg-blue-600 hover:text-white transition font-medium">
  Learn More
</button>
```

| Component     | Key Tailwind Classes                                     | Purpose                     |
|---------------|----------------------------------------------------------|-----------------------------|
| Page wrapper  | `min-h-screen bg-gray-50 p-6`                           | Full-height gray background |
| Card          | `bg-white rounded-xl shadow-sm border p-6`              | Content container           |
| Input         | `w-full px-4 py-2 border rounded-lg focus:ring-2`       | Form inputs                 |
| Primary btn   | `bg-blue-600 text-white rounded-lg hover:bg-blue-700`   | Main actions                |
| Danger btn    | `bg-red-600 text-white rounded-lg hover:bg-red-700`     | Destructive actions         |
| Badge         | `px-3 py-1 rounded-full text-xs font-medium`            | Status/priority labels      |

---

## 5. Responsive Design

### Mobile-First Approach

Responsive design ensures your application works well on phones, tablets, and desktops. The mobile-first approach means you design for the smallest screen first, then add styles for larger screens using Tailwind's responsive prefixes.

> **Real-life analogy: Packing a Suitcase**
>
> If you start by packing for a large suitcase and then try to fit everything into a carry-on, you will have to remove items. But if you start by packing for a carry-on (the essentials), you can easily add more items when you get a bigger suitcase. Mobile-first design works the same way: start with the essential layout for small screens, then enhance it for larger ones.

```
  RESPONSIVE BREAKPOINTS IN TAILWIND
  =====================================

  Phone          Tablet          Desktop         Large Desktop
  < 640px        640px+          1024px+         1280px+
  (default)      (sm:)           (lg:)           (xl:)
  
  +-------+    +----------+    +----------------+    +--------------------+
  | Stack |    | 2 cols   |    | 3 cols         |    | 4 cols             |
  | every |    |          |    |                |    |                    |
  | thing |    | +--+ +--+|    | +--+ +--+ +--+|    | +--+ +--+ +--+ +--|
  |       |    | |  | |  ||    | |  | |  | |  ||    | |  | |  | |  | |  |
  +-------+    +----------+    +----------------+    +--------------------+

  Tailwind class: grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4
```

### Responsive Navbar with Hamburger Menu

On desktop, the navbar shows all links horizontally. On mobile, it collapses into a hamburger menu that toggles open and closed.

```jsx
// src/components/Navbar.jsx
import { useState } from "react";
import { Link } from "react-router-dom";
import { useAuth } from "../context/AuthContext";

function Navbar() {
  const { user, logout } = useAuth();
  const [menuOpen, setMenuOpen] = useState(false);

  return (
    <nav className="bg-white shadow-sm border-b border-gray-200">
      <div className="max-w-6xl mx-auto px-4">
        <div className="flex items-center justify-between h-16">
          {/* Logo */}
          <Link to="/" className="text-xl font-bold text-blue-600">
            TaskManager
          </Link>

          {/* Desktop Navigation */}
          <div className="hidden md:flex items-center gap-6">
            {user ? (
              <>
                <Link to="/dashboard" className="text-gray-700 hover:text-blue-600">
                  Dashboard
                </Link>
                <Link to="/tasks/new" className="text-gray-700 hover:text-blue-600">
                  New Task
                </Link>
                <span className="text-gray-500">Hello, {user.name}</span>
                <button
                  onClick={logout}
                  className="bg-red-500 text-white px-4 py-2 rounded-lg hover:bg-red-600 text-sm"
                >
                  Logout
                </button>
              </>
            ) : (
              <>
                <Link to="/login" className="text-gray-700 hover:text-blue-600">
                  Login
                </Link>
                <Link
                  to="/register"
                  className="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 text-sm"
                >
                  Register
                </Link>
              </>
            )}
          </div>

          {/* Hamburger Button (visible on mobile only) */}
          <button
            className="md:hidden text-gray-700"
            onClick={() => setMenuOpen(!menuOpen)}
          >
            {menuOpen ? (
              // X icon
              <svg className="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M6 18L18 6M6 6l12 12" />
              </svg>
            ) : (
              // Hamburger icon
              <svg className="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M4 6h16M4 12h16M4 18h16" />
              </svg>
            )}
          </button>
        </div>

        {/* Mobile Menu (shown when menuOpen is true) */}
        {menuOpen && (
          <div className="md:hidden pb-4 space-y-2">
            {user ? (
              <>
                <Link to="/dashboard" className="block py-2 text-gray-700" onClick={() => setMenuOpen(false)}>
                  Dashboard
                </Link>
                <Link to="/tasks/new" className="block py-2 text-gray-700" onClick={() => setMenuOpen(false)}>
                  New Task
                </Link>
                <button onClick={logout} className="block w-full text-left py-2 text-red-600">
                  Logout
                </button>
              </>
            ) : (
              <>
                <Link to="/login" className="block py-2 text-gray-700" onClick={() => setMenuOpen(false)}>
                  Login
                </Link>
                <Link to="/register" className="block py-2 text-gray-700" onClick={() => setMenuOpen(false)}>
                  Register
                </Link>
              </>
            )}
          </div>
        )}
      </div>
    </nav>
  );
}

export default Navbar;
```

### Responsive Grid Layouts

The task list should display differently on different screen sizes.

```jsx
{/* Responsive task grid */}
<div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
  {tasks.map((task) => (
    <div key={task._id} className="bg-white rounded-xl shadow-sm border p-6">
      {/* Task card content */}
    </div>
  ))}
</div>
```

### Responsive Form Layout

```jsx
{/* Form that adjusts width based on screen size */}
<div className="max-w-lg mx-auto px-4 sm:px-0">
  <form className="bg-white rounded-xl shadow-lg p-6 sm:p-8">
    <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
      <div className="sm:col-span-2">
        <label className="block text-sm font-medium text-gray-700 mb-1">Title</label>
        <input type="text" className="w-full px-4 py-2 border rounded-lg" />
      </div>

      <div>
        <label className="block text-sm font-medium text-gray-700 mb-1">Priority</label>
        <select className="w-full px-4 py-2 border rounded-lg">
          <option>Low</option>
          <option>Medium</option>
          <option>High</option>
        </select>
      </div>

      <div>
        <label className="block text-sm font-medium text-gray-700 mb-1">Due Date</label>
        <input type="date" className="w-full px-4 py-2 border rounded-lg" />
      </div>

      <div className="sm:col-span-2">
        <label className="block text-sm font-medium text-gray-700 mb-1">Description</label>
        <textarea className="w-full px-4 py-2 border rounded-lg" rows="4"></textarea>
      </div>
    </div>

    <button className="w-full sm:w-auto mt-6 bg-blue-600 text-white px-8 py-2 rounded-lg">
      Create Task
    </button>
  </form>
</div>
```

| Tailwind Prefix | Breakpoint | Common Use Case                        |
|-----------------|------------|----------------------------------------|
| (default)       | 0px+       | Mobile styles (base layout)            |
| `sm:`           | 640px+     | Large phones, small tablets            |
| `md:`           | 768px+     | Tablets, show/hide navigation          |
| `lg:`           | 1024px+    | Laptops, multi-column layouts          |
| `xl:`           | 1280px+    | Desktops, wider content areas          |
| `2xl:`          | 1536px+    | Large monitors, maximum width content  |

---

## 6. Testing and Bug Fixing

### Common Bugs in MERN Projects

Every developer encounters bugs. The key is knowing what to look for and how to fix them. Here are the most common issues you will face in a MERN project and their solutions.

> **Real-life analogy: A Car Mechanic's Checklist**
>
> When a car will not start, a mechanic does not randomly replace parts. They follow a systematic checklist: Is there fuel? Is the battery charged? Is the starter motor working? Debugging software follows the same principle. You start with the most common causes and work your way through systematically.

### Common Errors and Solutions

| Error | Cause | Solution |
|-------|-------|----------|
| `CORS error` | Backend does not allow requests from frontend origin | Add `cors()` middleware in Express: `app.use(cors({ origin: "http://localhost:5173" }))` |
| `401 Unauthorized` | Missing or expired JWT token | Check that the token is being sent in the Authorization header. Verify it has not expired. |
| `404 Not Found` | Wrong API endpoint URL | Compare the URL in your axios call with the route defined in Express. Check for typos. |
| `500 Internal Server Error` | Backend crash (unhandled error) | Check the server terminal for the error message. Add try/catch to your controller. |
| `Network Error` | Backend is not running | Make sure the Express server is running on the correct port. Check the terminal. |
| `Cannot read properties of undefined` | Accessing data before it loads | Add loading state and conditional rendering. Check if data exists before accessing properties. |
| `Objects are not valid as a React child` | Rendering an object instead of a string | Check what you are putting inside `{}`. Render `obj.property` not `obj`. |
| `Each child in a list should have a unique key` | Missing key prop in `.map()` | Add `key={item._id}` to the outermost element in the map callback. |
| `Proxy error` | Vite proxy not configured | Add proxy config in `vite.config.js` pointing to your backend URL. |
| `MongoServerError: E11000 duplicate key` | Trying to insert a duplicate unique field | Check for existing document before inserting. Show proper error message to user. |

### Debugging with Browser DevTools

The browser's Developer Tools are your most powerful debugging weapon. Here is what to check and where.

```
  BROWSER DEVTOOLS DEBUGGING GUIDE
  ==================================

  1. CONSOLE TAB
     +----------------------------------------------+
     | Look for:                                     |
     | - Red error messages                          |
     | - Warning messages (yellow)                   |
     | - console.log() output from your code         |
     |                                               |
     | Tip: Click the file:line link to jump         |
     |      directly to the source code              |
     +----------------------------------------------+

  2. NETWORK TAB
     +----------------------------------------------+
     | Look for:                                     |
     | - Red entries (failed requests)               |
     | - Status codes (200, 401, 404, 500)           |
     | - Request headers (is Authorization present?) |
     | - Request payload (is the body correct?)      |
     | - Response body (what did the server return?) |
     |                                               |
     | Tip: Filter by "Fetch/XHR" to see only        |
     |      API calls                                |
     +----------------------------------------------+

  3. APPLICATION TAB
     +----------------------------------------------+
     | Look for:                                     |
     | - localStorage: Is the token stored?          |
     | - Is the token value correct?                 |
     |                                               |
     | Tip: You can manually edit or delete           |
     |      localStorage values here                 |
     +----------------------------------------------+

  4. REACT DEVTOOLS (browser extension)
     +----------------------------------------------+
     | Look for:                                     |
     | - Component tree and their current state      |
     | - Props being passed to each component        |
     | - Context values                              |
     |                                               |
     | Tip: Click a component to see its state       |
     |      and props in real time                   |
     +----------------------------------------------+
```

### Testing Checklist

Use this checklist to manually test every feature of your application before considering it complete.

**Authentication Testing:**

- [ ] Register with valid data -- should succeed and redirect to dashboard
- [ ] Register with duplicate email -- should show error message
- [ ] Register with weak password -- should show validation error
- [ ] Login with correct credentials -- should succeed and redirect
- [ ] Login with wrong password -- should show error
- [ ] Login with non-existent email -- should show error
- [ ] Refresh the page after login -- should stay logged in
- [ ] Logout -- should redirect to login and clear token
- [ ] Access protected route without login -- should redirect to login

**CRUD Testing:**

- [ ] Create a new task with all fields -- should appear in list
- [ ] Create a task without required fields -- should show validation error
- [ ] View task list -- should show all tasks
- [ ] View single task detail -- should show full information
- [ ] Edit a task -- changes should persist after refresh
- [ ] Delete a task -- should disappear from list with confirmation

**Search, Filter, and Pagination Testing:**

- [ ] Search by task title -- should show matching results
- [ ] Filter by status -- should show only tasks with that status
- [ ] Filter by priority -- should show only tasks with that priority
- [ ] Sort by different criteria -- order should change
- [ ] Navigate between pages -- should show different tasks
- [ ] Combine search with filter -- should work together

**Responsive Design Testing:**

- [ ] Resize browser to mobile width -- layout should stack vertically
- [ ] Hamburger menu should appear on mobile
- [ ] Forms should be usable on mobile
- [ ] Cards should display as single column on mobile
- [ ] No horizontal scrolling on any screen size

---

## 7. Code Review Checklist

### Why Code Review Matters

Before submitting your project, reviewing your own code catches issues that testing alone might miss. A code review examines not just whether the code works, but whether it is secure, performant, and maintainable.

> **Real-life analogy: Proofreading an Essay**
>
> After writing an essay, you read it again to check for grammar mistakes, unclear sentences, and missing arguments. You might even read it out loud to catch things your eyes skipped. A code review is the same process applied to code. You look for security holes, performance problems, and readability issues that you missed while writing.

### Security Checklist

| Check | Question | How to Verify |
|-------|----------|---------------|
| Password Hashing | Are passwords hashed before storing in the database? | Look for `bcrypt.hash()` in the register controller. Passwords should never be stored as plain text. |
| JWT Verification | Is every protected route checking the JWT token? | Verify that the `auth` middleware is applied to all routes that need protection. |
| Input Validation | Is user input validated on the server side? | Check controllers for validation logic. Never trust client-side validation alone. |
| SQL/NoSQL Injection | Are database queries safe from injection? | Use Mongoose methods (`find`, `findById`) instead of raw queries. Sanitize user input. |
| Sensitive Data Exposure | Are passwords excluded from API responses? | Check that user queries use `.select("-password")` or manually remove the password field. |
| Environment Variables | Are secrets stored in `.env` and not committed to Git? | Check `.gitignore` includes `.env`. Verify no hardcoded secrets in source code. |
| CORS Configuration | Is CORS restricted to known origins? | Do not use `cors()` with no options in production. Specify the allowed origin. |
| Rate Limiting | Is there protection against brute force attacks? | Consider adding `express-rate-limit` to login and register routes. |

### Performance Checklist

| Check | Question | How to Verify |
|-------|----------|---------------|
| Unnecessary Re-renders | Are components re-rendering when they should not? | Use React DevTools Profiler to check. Memoize with `React.memo` where needed. |
| Database Indexing | Do frequently queried fields have indexes? | Add indexes to fields used in `find()` queries: `title`, `status`, `priority`, `user`. |
| Pagination | Are you loading all records at once? | Verify that list endpoints use `skip()` and `limit()`, not `find()` with no limit. |
| Image/Asset Optimization | Are images optimized and appropriately sized? | Use WebP format, compress images, and use lazy loading. |
| Bundle Size | Is the JavaScript bundle unnecessarily large? | Run `npm run build` and check the output size. Remove unused dependencies. |
| API Call Efficiency | Are you making redundant API calls? | Check for duplicate `useEffect` fetches. Use state to cache data when appropriate. |

### Code Quality Checklist

| Check | Question | How to Verify |
|-------|----------|---------------|
| Consistent Naming | Do variables and functions follow a consistent naming convention? | Use camelCase for variables/functions, PascalCase for components. |
| Error Handling | Does every async operation have error handling? | Every `async/await` should be wrapped in `try/catch`. Every `.then()` should have `.catch()`. |
| Code Duplication | Is there repeated code that could be extracted into a function? | Look for repeated patterns. Extract into custom hooks or utility functions. |
| Comments | Are complex sections explained with comments? | Add comments for non-obvious logic. Do not comment obvious code like `// set name`. |
| File Organization | Are files organized logically? | Components in `/components`, pages in `/pages`, hooks in `/hooks`, context in `/context`. |
| Unused Code | Is there dead code (unused imports, variables, functions)? | Remove commented-out code, unused imports, and console.log statements before submission. |
| Environment Configuration | Is the app configurable without code changes? | API URLs, ports, and secrets should come from environment variables, not hardcoded strings. |

---

## 8. Project Completion Criteria

### Minimum Viable Product (MVP) Definition

An MVP is the smallest version of your project that still provides value and demonstrates your skills. It must have all core features working end to end, but it does not need to be perfect.

> **Real-life analogy: A Food Stall**
>
> You do not need a full restaurant with chandeliers and a 50-item menu to prove you can cook. A food stall with three well-made dishes, a clean setup, and friendly service proves the same point. Your MERN project does not need every conceivable feature. It needs the core features working reliably, clean code, and a polished presentation.

```
  MVP vs NICE-TO-HAVE
  =====================

  MVP (Must Have)                         Nice-to-Have (Future)
  +---------------------------+           +---------------------------+
  | User registration/login   |           | Social login (Google)     |
  | Create, read, update,     |           | File uploads              |
  |   delete tasks            |           | Real-time notifications   |
  | Search and filter         |           | Email reminders           |
  | Responsive design         |           | Dark mode                 |
  | Basic error handling      |           | Drag-and-drop reordering  |
  | Clean, consistent UI      |           | Analytics dashboard       |
  +---------------------------+           +---------------------------+
       Complete these FIRST                   Add these LATER
```

### Feature Completeness Table

| Feature | Status | Notes |
|---------|--------|-------|
| User Registration | Required | Form with validation, password hashing, JWT returned |
| User Login | Required | Email/password authentication, error messages |
| User Logout | Required | Clear token, redirect to login |
| Auth Persistence | Required | Stay logged in on page refresh |
| Protected Routes | Required | Redirect unauthenticated users |
| Create Task | Required | Form with validation, all fields |
| View Task List | Required | Display all user's tasks |
| View Task Detail | Required | Full information for a single task |
| Edit Task | Required | Pre-filled form, save changes |
| Delete Task | Required | Confirmation dialog |
| Search | Required | By title or description |
| Filter by Status | Required | All, pending, in-progress, completed |
| Filter by Priority | Required | All, low, medium, high |
| Sort | Recommended | By date, priority, or title |
| Pagination | Recommended | Page numbers, next/previous |
| Tailwind Styling | Required | Consistent, professional appearance |
| Responsive Design | Required | Works on mobile, tablet, desktop |
| Error Handling | Required | User-friendly error messages |
| Loading States | Recommended | Show loading indicators during API calls |

### What Makes a Portfolio-Worthy Project

A project on your portfolio represents your skills to potential employers. Here is what separates a basic project from an impressive one.

| Aspect | Basic | Portfolio-Worthy |
|--------|-------|------------------|
| **Code** | Works but messy | Clean, organized, well-commented |
| **UI** | Functional but plain | Polished, consistent, professional |
| **UX** | Requires guessing | Intuitive with clear feedback |
| **Errors** | App crashes or shows blank screen | Graceful error messages guide the user |
| **README** | No README or one sentence | Screenshots, features list, setup instructions |
| **Demo** | Have to run locally | Live link or video demo |
| **Git** | One giant commit | Multiple meaningful commits with clear messages |
| **Responsive** | Broken on mobile | Works perfectly on all screen sizes |

### Preparing a Demo

Before presenting your project, prepare it for demonstration.

```
  DEMO PREPARATION CHECKLIST
  ============================

  1. SEED DATA
     - Add 15-20 realistic tasks to your database
     - Mix of statuses (pending, in-progress, completed)
     - Mix of priorities (low, medium, high)
     - Realistic titles and descriptions

  2. SCREENSHOTS
     - Login page
     - Dashboard with tasks
     - Create/Edit form
     - Task detail view
     - Mobile view

  3. README.md
     - Project title and description
     - Technologies used (with icons/badges)
     - Screenshots
     - Setup instructions (git clone, npm install, environment variables)
     - Features list
     - Folder structure

  4. VIDEO DEMO (optional but recommended)
     - 2-3 minute walkthrough
     - Show: register, login, create task, edit, delete, search, filter
     - Show responsive design
```

---

## 9. Summary

### What You Built in This Project

Over Weeks 35 and 36, you built a complete full-stack MERN application from scratch. This is not a tutorial copy-paste project. You made architectural decisions, handled real-world problems like authentication and pagination, and styled the application for production use.

```
  YOUR COMPLETE MERN PROJECT
  ============================

  Frontend (React + Tailwind)         Backend (Express + MongoDB)
  +-----------------------------+     +-----------------------------+
  |                             |     |                             |
  |  Login / Register Pages     |     |  Auth Routes                |
  |  Dashboard (Task List)      |     |    POST /api/auth/register  |
  |  Task Detail Page           |     |    POST /api/auth/login     |
  |  Create Task Form           |     |    GET  /api/auth/me        |
  |  Edit Task Form             |     |                             |
  |  Responsive Navbar          |     |  Task Routes                |
  |  Search & Filter Bar        |     |    GET    /api/tasks        |
  |  Pagination Controls        |     |    GET    /api/tasks/:id    |
  |                             |     |    POST   /api/tasks        |
  |  AuthContext (global state) |     |    PATCH  /api/tasks/:id    |
  |  Protected Routes           |     |    DELETE /api/tasks/:id    |
  |  Custom Hooks (useDebounce) |     |                             |
  |                             |     |  Auth Middleware (JWT)      |
  +-----------------------------+     |  Error Handling             |
              |                       +-----------------------------+
              |                                    |
              +-------- HTTP Requests ------------>+
              +<------- JSON Responses -----------+
                                                   |
                                          +--------+--------+
                                          |    MongoDB      |
                                          |                 |
                                          |  Users          |
                                          |  Tasks          |
                                          +-----------------+
```

### Skills Acquired

| Skill | What You Learned |
|-------|------------------|
| Authentication | Implementing JWT-based register, login, and logout with secure password hashing |
| Context API | Managing global state (auth state) accessible to all components |
| CRUD Operations | Building create, read, update, and delete features with forms and API calls |
| Search & Filter | Implementing debounced search, multi-criteria filtering, and sorting |
| Pagination | Splitting large datasets across pages with backend query handling |
| Tailwind CSS | Applying utility-first styling for a consistent, professional UI |
| Responsive Design | Building mobile-first layouts with responsive breakpoints |
| Debugging | Using DevTools to identify and fix common MERN bugs |
| Code Quality | Following security, performance, and maintainability best practices |
| Project Management | Defining MVP scope and preparing a portfolio-ready project |

### Key Takeaways

1. **Authentication is not optional.** Any application that stores user data must verify identity. JWT tokens provide a stateless, scalable solution.

2. **CRUD is the foundation.** Every application you will ever build relies on these four operations. Mastering them in one project makes every future project easier.

3. **User experience matters.** Search, filter, pagination, loading states, and error messages are not luxury features. They are what separate a student project from a professional application.

4. **Styling is not an afterthought.** A well-styled application demonstrates attention to detail. Tailwind CSS makes it practical to achieve a polished look without spending weeks on CSS.

5. **Test everything.** Manually walk through every feature. Click every button. Try every edge case. Submit empty forms. Refresh the page. Use a different browser. The bugs you find and fix before submission are bugs that do not embarrass you later.

### What is Next?

In the upcoming weeks, you will learn how to **deploy your MERN project** to the internet so that anyone with a link can use it. You will deploy the backend to a cloud platform, host the frontend, connect to a production database, and configure environment variables for production. Your project will go from running on `localhost` to being live on the web.
