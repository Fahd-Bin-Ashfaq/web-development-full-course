# Week 33 — Authentication in MERN

> **Prerequisites:** React (components, hooks, React Router), Node.js, Express.js (routes, middleware), MongoDB with Mongoose, and basic understanding of HTTP requests and REST APIs from previous weeks.
>
> **Goal:** Build a complete authentication system in a MERN stack application. You will learn how to register users, hash passwords, generate JSON Web Tokens, protect frontend and backend routes, implement role-based access control, and handle persistent login sessions.

---

## Table of Contents

1. [Understanding Authentication vs Authorization](#1-understanding-authentication-vs-authorization)
2. [Full Authentication Flow Diagram](#2-full-authentication-flow-diagram)
3. [User Registration Flow](#3-user-registration-flow)
4. [User Login Flow](#4-user-login-flow)
5. [JWT Storage Options](#5-jwt-storage-options)
6. [Protecting Frontend Routes in React](#6-protecting-frontend-routes-in-react)
7. [Protecting Backend Routes](#7-protecting-backend-routes)
8. [Role-Based Access Control](#8-role-based-access-control)
9. [Logout Flow](#9-logout-flow)
10. [Persistent Login](#10-persistent-login)
11. [Summary](#11-summary)

---

## 1. Understanding Authentication vs Authorization

These two words sound similar, but they mean very different things. Every secure application needs both, and confusing them is one of the most common mistakes beginners make.

**Authentication** answers the question: _"Who are you?"_
**Authorization** answers the question: _"What are you allowed to do?"_

Authentication always comes first. You cannot decide what someone is allowed to do until you know who they are.

### Real-Life Analogy: Hotel Key Card

> Imagine you arrive at a hotel. At the front desk, you show your ID and credit card. The receptionist verifies your identity and gives you a key card. This is **authentication** -- the hotel has confirmed who you are.
>
> Now you walk to the elevator. Your key card lets you access floors 3 through 5, but not the penthouse suite on floor 20. You can enter your room (304), but not room 305. This is **authorization** -- the hotel has decided what you are allowed to access based on your identity.

```
  AUTHENTICATION vs AUTHORIZATION

  +------------------+                    +------------------+
  |  AUTHENTICATION  |                    |  AUTHORIZATION   |
  +------------------+                    +------------------+
  |                  |                    |                  |
  |  "Who are you?"  |                    | "What can you    |
  |                  |                    |  access?"        |
  |  - Login form    |   Happens first    |  - Admin panel   |
  |  - Username +    |  --------------->  |  - User profile  |
  |    Password      |                    |  - API endpoints |
  |  - Token issued  |                    |  - File access   |
  |                  |                    |                  |
  +------------------+                    +------------------+

  Hotel analogy:
  +------------------+                    +------------------+
  |  Front desk      |                    |  Key card access |
  |  checks your ID  |  --------------->  |  Floor 3-5: YES  |
  |  Gives key card  |                    |  Penthouse: NO   |
  +------------------+                    +------------------+
```

| Aspect              | Authentication                          | Authorization                          |
|----------------------|-----------------------------------------|----------------------------------------|
| **Question**         | Who is this user?                       | What can this user do?                 |
| **When it happens**  | During login                            | On every protected request             |
| **Frontend role**    | Collects credentials, stores token      | Shows/hides UI based on role           |
| **Backend role**     | Verifies password, issues JWT           | Checks JWT and user role               |
| **Fails with**       | 401 Unauthorized                        | 403 Forbidden                          |

### The Authentication Toolbox

| Tool            | Purpose                                         | Install Command              |
|-----------------|--------------------------------------------------|------------------------------|
| **bcrypt**      | Hash passwords so they are never stored as text  | `npm install bcrypt`         |
| **jsonwebtoken**| Create and verify JWT tokens                     | `npm install jsonwebtoken`   |
| **cookie-parser** | Read cookies from incoming requests            | `npm install cookie-parser`  |
| **dotenv**      | Load environment variables from `.env` file      | `npm install dotenv`         |

---

## 2. Full Authentication Flow Diagram

Before writing any code, you need to understand the complete picture. This diagram shows every step that happens when a user registers, logs in, and accesses a protected resource.

```
+-----------------------------------------------------------------------+
|                  FULL AUTHENTICATION FLOW IN MERN                     |
+-----------------------------------------------------------------------+
|                                                                       |
|  FRONTEND (React)                  BACKEND (Express + MongoDB)        |
|                                                                       |
|  1. REGISTRATION                                                      |
|  +------------------+              +---------------------------+      |
|  | Registration     |   POST       | /api/auth/register        |      |
|  | Form             | -----------> | a. Validate input         |      |
|  | {name, email,    |              | b. Check if user exists   |      |
|  |  password}       |              | c. Hash password (bcrypt) |      |
|  +------------------+              | d. Save to MongoDB        |      |
|         |                          +---------------------------+      |
|         v                                                             |
|  2. LOGIN                                                             |
|  +------------------+              +---------------------------+      |
|  | Login Form       |   POST       | /api/auth/login           |      |
|  | {email,          | -----------> | a. Find user by email     |      |
|  |  password}       |              | b. bcrypt.compare()       |      |
|  |                  |   <--------- | c. Generate JWT           |      |
|  |                  |  {token,     | d. Send token + user data |      |
|  |                  |   user}      +---------------------------+      |
|  +------------------+                                                 |
|         |                                                             |
|         v                                                             |
|  3. STORE TOKEN (localStorage or httpOnly cookie)                     |
|         |                                                             |
|         v                                                             |
|  4. PROTECTED REQUEST                                                 |
|  +------------------+              +---------------------------+      |
|  | Dashboard Page   |   GET        | /api/user/profile         |      |
|  |                  | -----------> | Authorization: Bearer JWT |      |
|  |                  |   <--------- | Verify JWT -> Return data |      |
|  +------------------+              +---------------------------+      |
|                                                                       |
+-----------------------------------------------------------------------+
```

**Step 1 -- Registration.** React sends user details to the backend. Express validates input, hashes the password with bcrypt, and saves the user to MongoDB. The raw password is never stored.

**Step 2 -- Login.** Express finds the user by email, compares the password hash, and generates a JWT containing the user's ID.

**Step 3 -- Token Storage.** React stores the JWT. Where you store it has important security implications (covered in Section 5).

**Step 4 -- Protected Requests.** React includes the JWT in request headers. Express middleware verifies the token before returning data.

---

## 3. User Registration Flow

Registration involves three parts: the MongoDB model, the Express route, and the React form.

> **Real-Life Analogy: Library Card Application.** When you apply for a library card, the librarian checks your ID, ensures you do not already have a card, and records your information. The card itself does not display your home address -- sensitive data stays private. Similarly, we never store the raw password.

### MongoDB User Model

```javascript
// models/User.js
const mongoose = require("mongoose");

const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: [true, "Name is required"],
    trim: true,
    minlength: 2,
    maxlength: 50,
  },
  email: {
    type: String,
    required: [true, "Email is required"],
    unique: true,
    lowercase: true,
    match: [/^\S+@\S+\.\S+$/, "Please enter a valid email"],
  },
  password: {
    type: String,
    required: [true, "Password is required"],
    minlength: 6,
  },
  role: {
    type: String,
    enum: ["user", "admin"],
    default: "user",
  },
}, { timestamps: true });

module.exports = mongoose.model("User", userSchema);
```

### Express Registration Route

```javascript
// routes/auth.js
const express = require("express");
const router = express.Router();
const bcrypt = require("bcrypt");
const User = require("../models/User");

router.post("/register", async (req, res) => {
  try {
    const { name, email, password } = req.body;

    // Validate input
    if (!name || !email || !password) {
      return res.status(400).json({ success: false, message: "All fields are required" });
    }

    // Check for existing user
    const existingUser = await User.findOne({ email });
    if (existingUser) {
      return res.status(400).json({ success: false, message: "Email already registered" });
    }

    // Hash the password (10 salt rounds)
    const salt = await bcrypt.genSalt(10);
    const hashedPassword = await bcrypt.hash(password, salt);

    // Create user with hashed password
    const newUser = await User.create({ name, email, password: hashedPassword });

    res.status(201).json({
      success: true,
      message: "Account created successfully",
      user: { id: newUser._id, name: newUser.name, email: newUser.email },
    });
  } catch (error) {
    res.status(500).json({ success: false, message: "Server error during registration" });
  }
});

module.exports = router;
```

### Understanding Password Hashing

```
  WHY WE HASH PASSWORDS

  Plain text (DANGEROUS):           Hashed (SECURE):
  +-------------------------+       +-------------------------------+
  | password: mySecret123   |       | password: $2b$10$xK9Lz...    |
  | Anyone can read it!     |       | Cannot be reversed!           |
  +-------------------------+       +-------------------------------+

  "mySecret123"  --->  bcrypt.hash()  --->  "$2b$10$xK9Lz..."
                       (one-way function, cannot be reversed)

  Verification:
  "mySecret123"  + "$2b$10$xK9Lz..."  --> bcrypt.compare() --> true
  "wrongPass"    + "$2b$10$xK9Lz..."  --> bcrypt.compare() --> false
```

### React Registration Form

```jsx
// pages/Register.jsx
import { useState } from "react";
import { useNavigate, Link } from "react-router-dom";

function Register() {
  const navigate = useNavigate();
  const [formData, setFormData] = useState({ name: "", email: "", password: "", confirmPassword: "" });
  const [error, setError] = useState("");
  const [loading, setLoading] = useState(false);

  const handleChange = (e) => {
    setFormData({ ...formData, [e.target.name]: e.target.value });
  };

  const handleSubmit = async (e) => {
    e.preventDefault();
    setError("");

    if (formData.password !== formData.confirmPassword) {
      return setError("Passwords do not match");
    }

    setLoading(true);
    try {
      const response = await fetch("http://localhost:5000/api/auth/register", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ name: formData.name, email: formData.email, password: formData.password }),
      });
      const data = await response.json();

      if (!response.ok) return setError(data.message || "Registration failed");
      navigate("/login");
    } catch (err) {
      setError("Network error. Please try again.");
    } finally {
      setLoading(false);
    }
  };

  return (
    <div>
      <h2>Create Account</h2>
      {error && <p style={{ color: "red" }}>{error}</p>}
      <form onSubmit={handleSubmit}>
        <input type="text" name="name" value={formData.name} onChange={handleChange} placeholder="Full Name" required />
        <input type="email" name="email" value={formData.email} onChange={handleChange} placeholder="Email" required />
        <input type="password" name="password" value={formData.password} onChange={handleChange} placeholder="Password" required />
        <input type="password" name="confirmPassword" value={formData.confirmPassword} onChange={handleChange} placeholder="Confirm Password" required />
        <button type="submit" disabled={loading}>{loading ? "Creating Account..." : "Register"}</button>
      </form>
      <p>Already have an account? <Link to="/login">Login here</Link></p>
    </div>
  );
}

export default Register;
```

---

## 4. User Login Flow

Login verifies a user's identity and issues a JWT that proves who they are for future requests.

> **Real-Life Analogy: Airport Boarding Pass.** After you check in at the airport (authentication), you receive a boarding pass. This pass contains your name, seat number, and flight details. Every staff member can verify it without calling the airline's database -- they simply scan the barcode. A JWT works the same way.

### Express Login Route

```javascript
// routes/auth.js (add to the same file)
const jwt = require("jsonwebtoken");

router.post("/login", async (req, res) => {
  try {
    const { email, password } = req.body;

    if (!email || !password) {
      return res.status(400).json({ success: false, message: "Email and password are required" });
    }

    // Find user -- use generic error message to prevent user enumeration
    const user = await User.findOne({ email });
    if (!user) {
      return res.status(401).json({ success: false, message: "Invalid email or password" });
    }

    // Compare password with stored hash
    const isPasswordCorrect = await bcrypt.compare(password, user.password);
    if (!isPasswordCorrect) {
      return res.status(401).json({ success: false, message: "Invalid email or password" });
    }

    // Generate JWT with user ID and role, expires in 7 days
    const token = jwt.sign(
      { userId: user._id, role: user.role },
      process.env.JWT_SECRET,
      { expiresIn: "7d" }
    );

    res.status(200).json({
      success: true,
      token,
      user: { id: user._id, name: user.name, email: user.email, role: user.role },
    });
  } catch (error) {
    res.status(500).json({ success: false, message: "Server error during login" });
  }
});
```

### Understanding JSON Web Tokens (JWT)

```
  ANATOMY OF A JWT

  eyJhbGciOiJIUzI1NiJ9.eyJ1c2VySWQiOiI2NWFiYzEyMyJ9.SflKxwRJSMeKKF2QT4fw

  |__________________|  |____________________________|  |___________________|
       HEADER                    PAYLOAD                    SIGNATURE
    (algorithm)          (user data + expiry)          (verification seal)

  HEADER:   { "alg": "HS256", "typ": "JWT" }
  PAYLOAD:  { "userId": "65abc123", "role": "user", "exp": 1705839367 }
  SIGNATURE: Created by signing HEADER + PAYLOAD with the secret key.
             If anyone changes the payload, the signature becomes invalid.
```

### React Login Form

```jsx
// pages/Login.jsx
import { useState } from "react";
import { useNavigate, Link } from "react-router-dom";
import { useAuth } from "../context/AuthContext";

function Login() {
  const navigate = useNavigate();
  const { login } = useAuth();
  const [formData, setFormData] = useState({ email: "", password: "" });
  const [error, setError] = useState("");
  const [loading, setLoading] = useState(false);

  const handleChange = (e) => {
    setFormData({ ...formData, [e.target.name]: e.target.value });
  };

  const handleSubmit = async (e) => {
    e.preventDefault();
    setError("");
    setLoading(true);

    try {
      const response = await fetch("http://localhost:5000/api/auth/login", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(formData),
      });
      const data = await response.json();

      if (!response.ok) return setError(data.message || "Login failed");

      login(data.token, data.user);
      navigate("/dashboard");
    } catch (err) {
      setError("Network error. Please try again.");
    } finally {
      setLoading(false);
    }
  };

  return (
    <div>
      <h2>Login</h2>
      {error && <p style={{ color: "red" }}>{error}</p>}
      <form onSubmit={handleSubmit}>
        <input type="email" name="email" value={formData.email} onChange={handleChange} placeholder="Email" required />
        <input type="password" name="password" value={formData.password} onChange={handleChange} placeholder="Password" required />
        <button type="submit" disabled={loading}>{loading ? "Logging in..." : "Login"}</button>
      </form>
      <p>Don't have an account? <Link to="/register">Register here</Link></p>
    </div>
  );
}

export default Login;
```

---

## 5. JWT Storage Options

Once React receives a JWT, it must store it somewhere for future requests. There are two main options with important security trade-offs.

### Comparison Table

| Feature                    | localStorage                           | httpOnly Cookie                        |
|----------------------------|----------------------------------------|----------------------------------------|
| **Access from JavaScript** | Yes (`localStorage.getItem`)           | No (browser manages automatically)     |
| **Sent with requests**     | Manually (add to headers)              | Automatically (browser attaches it)    |
| **Vulnerable to XSS**      | Yes -- scripts can steal it            | No -- JavaScript cannot read it        |
| **Vulnerable to CSRF**     | No -- not sent automatically           | Yes -- browser sends with all requests |
| **Ease of implementation** | Simple                                 | Requires backend cookie configuration  |
| **Best for**               | Learning and prototypes                | Production applications                |

### Security Risks Explained

```
  XSS ATTACK (Cross-Site Scripting)
  Attacker injects script --> reads localStorage --> steals token
  httpOnly cookies are SAFE because JavaScript cannot access them.

  CSRF ATTACK (Cross-Site Request Forgery)
  Attacker tricks browser --> browser sends cookie automatically --> unwanted action
  localStorage is SAFE because tokens are not sent automatically.
```

### localStorage Approach

```javascript
// Store after login
localStorage.setItem("token", data.token);

// Send with requests
const response = await fetch("/api/user/profile", {
  headers: { Authorization: `Bearer ${localStorage.getItem("token")}` },
});

// Remove on logout
localStorage.removeItem("token");
```

### httpOnly Cookie Approach

**Backend -- set the cookie in the login route:**

```javascript
res.cookie("token", token, {
  httpOnly: true,           // JavaScript cannot access this
  secure: true,             // Only sent over HTTPS
  sameSite: "strict",       // CSRF protection
  maxAge: 7 * 24 * 60 * 60 * 1000,
});
```

**Frontend -- include credentials in every request:**

```javascript
const response = await fetch("http://localhost:5000/api/auth/login", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  credentials: "include",   // Required for cookies
  body: JSON.stringify(formData),
});
```

**Backend CORS configuration (required for cookies):**

```javascript
app.use(cors({ origin: "http://localhost:3000", credentials: true }));
app.use(require("cookie-parser")());
```

For the rest of this document, we use localStorage for simplicity. Production apps should prefer httpOnly cookies.

---

## 6. Protecting Frontend Routes in React

Not every page should be visible to everyone. React Router lets us enforce access rules using a combination of Context and wrapper components.

> **Real-Life Analogy: Security Badge System.** In an office, every employee wears a badge. The badge carries your identity to every door -- you do not re-enter credentials each time. AuthContext is that badge system for your React app.

### AuthContext -- Centralized Authentication State

```jsx
// context/AuthContext.jsx
import { createContext, useContext, useState, useEffect } from "react";

const AuthContext = createContext(null);

export function AuthProvider({ children }) {
  const [user, setUser] = useState(null);
  const [token, setToken] = useState(null);
  const [loading, setLoading] = useState(true);

  // Check for existing token on app load
  useEffect(() => {
    const storedToken = localStorage.getItem("token");
    const storedUser = localStorage.getItem("user");
    if (storedToken && storedUser) {
      setToken(storedToken);
      setUser(JSON.parse(storedUser));
    }
    setLoading(false);
  }, []);

  const login = (newToken, userData) => {
    setToken(newToken);
    setUser(userData);
    localStorage.setItem("token", newToken);
    localStorage.setItem("user", JSON.stringify(userData));
  };

  const logout = () => {
    setToken(null);
    setUser(null);
    localStorage.removeItem("token");
    localStorage.removeItem("user");
  };

  return (
    <AuthContext.Provider value={{ user, token, loading, isAuthenticated: !!token, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
}

export function useAuth() {
  const context = useContext(AuthContext);
  if (!context) throw new Error("useAuth must be used within an AuthProvider");
  return context;
}
```

### PrivateRoute Component

```jsx
// components/PrivateRoute.jsx
import { Navigate } from "react-router-dom";
import { useAuth } from "../context/AuthContext";

function PrivateRoute({ children }) {
  const { isAuthenticated, loading } = useAuth();

  if (loading) return <div>Loading...</div>;
  if (!isAuthenticated) return <Navigate to="/login" replace />;
  return children;
}

export default PrivateRoute;
```

### Setting Up Routes with Protection

```jsx
// App.jsx
import { BrowserRouter, Routes, Route, Navigate } from "react-router-dom";
import { AuthProvider, useAuth } from "./context/AuthContext";
import PrivateRoute from "./components/PrivateRoute";
import Login from "./pages/Login";
import Register from "./pages/Register";
import Dashboard from "./pages/Dashboard";

function PublicRoute({ children }) {
  const { isAuthenticated, loading } = useAuth();
  if (loading) return <div>Loading...</div>;
  if (isAuthenticated) return <Navigate to="/dashboard" replace />;
  return children;
}

function App() {
  return (
    <BrowserRouter>
      <AuthProvider>
        <Routes>
          <Route path="/login" element={<PublicRoute><Login /></PublicRoute>} />
          <Route path="/register" element={<PublicRoute><Register /></PublicRoute>} />
          <Route path="/dashboard" element={<PrivateRoute><Dashboard /></PrivateRoute>} />
          <Route path="/profile" element={<PrivateRoute><Profile /></PrivateRoute>} />
          <Route path="/" element={<Navigate to="/dashboard" />} />
        </Routes>
      </AuthProvider>
    </BrowserRouter>
  );
}

export default App;
```

```
  ROUTE PROTECTION FLOW

  User visits /dashboard
        |
        v
  PrivateRoute checks auth
        |
        +--- Authenticated? ---> YES ---> Render <Dashboard />
        |
        +--- Not authenticated? ---> <Navigate to="/login" />
```

---

## 7. Protecting Backend Routes

Frontend route protection prevents users from seeing pages, but does not protect the data. Users can hit your API with Postman or curl directly. Backend middleware is the real security gate.

### JWT Verification Middleware

```javascript
// middleware/auth.js
const jwt = require("jsonwebtoken");
const User = require("../models/User");

const protect = async (req, res, next) => {
  try {
    let token;

    // Extract token from "Bearer <token>" header
    if (req.headers.authorization && req.headers.authorization.startsWith("Bearer")) {
      token = req.headers.authorization.split(" ")[1];
    }
    // For cookies: else if (req.cookies.token) { token = req.cookies.token; }

    if (!token) {
      return res.status(401).json({ success: false, message: "No token provided" });
    }

    // Verify the token
    const decoded = jwt.verify(token, process.env.JWT_SECRET);

    // Find user and attach to request (exclude password)
    req.user = await User.findById(decoded.userId).select("-password");
    if (!req.user) {
      return res.status(401).json({ success: false, message: "User no longer exists" });
    }

    next();
  } catch (error) {
    const message = error.name === "TokenExpiredError"
      ? "Token expired. Please log in again."
      : "Invalid token.";
    return res.status(401).json({ success: false, message });
  }
};

module.exports = { protect };
```

### Using Middleware on Routes

```javascript
// routes/user.js
const express = require("express");
const router = express.Router();
const { protect } = require("../middleware/auth");

// Protected route -- only authenticated users
router.get("/profile", protect, async (req, res) => {
  res.status(200).json({ success: true, user: req.user });
});

router.put("/profile", protect, async (req, res) => {
  const updatedUser = await User.findByIdAndUpdate(
    req.user._id,
    { name: req.body.name, email: req.body.email },
    { new: true, runValidators: true }
  ).select("-password");

  res.status(200).json({ success: true, user: updatedUser });
});

module.exports = router;
```

```
  REQUEST THROUGH MIDDLEWARE

  GET /api/user/profile
  Authorization: Bearer eyJhbGci...
        |
        v
  +------------------+
  | protect          |  Extract token -> Verify -> Find user
  | middleware        |  Attach user to req.user
  +------------------+
        |
        +--- Valid? --- YES ---> Route handler runs (req.user available)
        |
        +--- Invalid? ---> 401 Unauthorized (request stops)
```

---

## 8. Role-Based Access Control

Each user has a role (like "user" or "admin"), and routes specify which roles are allowed. Authentication tells us who the user is; authorization tells us what they can do.

> **Real-Life Analogy: Hospital Staff Badges.** Doctors (blue badge) access operating rooms and patient records. Nurses (green badge) access patient rooms and medication. Visitors (red badge) can only reach the waiting area. Everyone is authenticated, but authorized for different areas.

### Role Middleware

```javascript
// middleware/auth.js (add to the same file)

// Returns a middleware that checks if the user's role is in the allowed list
const authorize = (...allowedRoles) => {
  return (req, res, next) => {
    if (!req.user) {
      return res.status(401).json({ success: false, message: "Not authorized" });
    }

    if (!allowedRoles.includes(req.user.role)) {
      return res.status(403).json({
        success: false,
        message: `Role '${req.user.role}' is not authorized for this resource`,
      });
    }

    next();
  };
};

module.exports = { protect, authorize };
```

### Using Role Middleware

```javascript
// routes/admin.js
const express = require("express");
const router = express.Router();
const { protect, authorize } = require("../middleware/auth");

// Only admins can see all users
router.get("/users", protect, authorize("admin"), async (req, res) => {
  const users = await User.find().select("-password");
  res.status(200).json({ success: true, users });
});

// Only admins can delete a user
router.delete("/users/:id", protect, authorize("admin"), async (req, res) => {
  await User.findByIdAndDelete(req.params.id);
  res.status(200).json({ success: true, message: "User deleted" });
});

// Both admins and moderators can view reports
router.get("/reports", protect, authorize("admin", "moderator"), async (req, res) => {
  res.status(200).json({ success: true, message: "Reports data" });
});
```

### Role-Based Routing Diagram

```
  ROLE-BASED ACCESS CONTROL

  Request ---> protect middleware ---> authorize middleware ---> Route handler
               "Who are you?"          "What role do you have?"

  +------------------+     +-----------------------+
  |  /api/admin/*    |<----| authorize("admin")    |  Admin badge only
  |  Manage users    |     +-----------------------+
  +------------------+

  +------------------+     +-----------------------+
  |  /api/user/*     |<----| protect (any role)    |  Any valid badge
  |  View profile    |     +-----------------------+
  +------------------+

  +------------------+     +-----------------------+
  |  /api/auth/*     |<----| No middleware          |  Public access
  |  Register/Login  |     +-----------------------+
  +------------------+
```

### Frontend Role-Based Rendering

```jsx
// components/AdminRoute.jsx
import { Navigate } from "react-router-dom";
import { useAuth } from "../context/AuthContext";

function AdminRoute({ children }) {
  const { user, isAuthenticated, loading } = useAuth();
  if (loading) return <div>Loading...</div>;
  if (!isAuthenticated) return <Navigate to="/login" replace />;
  if (user.role !== "admin") return <Navigate to="/dashboard" replace />;
  return children;
}

export default AdminRoute;
```

```jsx
// Navbar -- conditionally show admin link
function Navbar() {
  const { user, isAuthenticated, logout } = useAuth();

  return (
    <nav>
      <a href="/">Home</a>
      {isAuthenticated ? (
        <>
          <a href="/dashboard">Dashboard</a>
          {user.role === "admin" && <a href="/admin">Admin Panel</a>}
          <button onClick={logout}>Logout</button>
        </>
      ) : (
        <>
          <a href="/login">Login</a>
          <a href="/register">Register</a>
        </>
      )}
    </nav>
  );
}
```

---

## 9. Logout Flow

Logging out means destroying the user's session so they can no longer access protected resources.

### localStorage Logout

Already implemented in our AuthContext:

```javascript
const logout = () => {
  setToken(null);        // Clear React state
  setUser(null);
  localStorage.removeItem("token");   // Clear persistent storage
  localStorage.removeItem("user");
};
```

When called: React state clears, components re-render as "logged out", and PrivateRoute redirects to `/login`.

### Cookie Logout (Backend)

When using httpOnly cookies, the backend must clear the cookie since JavaScript cannot access it.

```javascript
// routes/auth.js
router.post("/logout", (req, res) => {
  res.cookie("token", "", {
    httpOnly: true,
    secure: true,
    sameSite: "strict",
    expires: new Date(0),   // Expire immediately
  });
  res.status(200).json({ success: true, message: "Logged out successfully" });
});
```

### Complete Logout Flow

```
  User clicks "Logout"
        |
        v
  Clear React state (setUser(null), setToken(null))
        |
        v
  Remove token (localStorage.removeItem OR call /api/auth/logout)
        |
        v
  PrivateRoute detects isAuthenticated === false
        |
        v
  Redirect to /login
```

### Important Note on Token Invalidation

JWTs cannot be truly invalidated server-side. Once issued, a token remains valid until expiry. For most apps, removing the token from the client is sufficient. For strict security requirements (banking, healthcare), implement a **token blacklist** using Redis or a database table -- the `protect` middleware checks the blacklist before accepting any token.

---

## 10. Persistent Login

When a user logs in and closes the browser, they expect to remain logged in when they return. This works because localStorage persists across browser sessions.

### How It Works

```
  PERSISTENT LOGIN FLOW

  User logs in --> Token saved to localStorage --> User closes browser
                                                        |
  User reopens app <------------------------------------+
        |
  AuthProvider mounts --> useEffect checks localStorage
        |
        +--- Token found? --> Verify with backend --> Set user state
        |
        +--- No token? --> Show login page
```

### Verifying the Token on App Load

The basic AuthContext from Section 6 reads localStorage on load. A more robust version verifies the token with the backend:

```jsx
// context/AuthContext.jsx (enhanced with token verification)

useEffect(() => {
  const verifyStoredToken = async () => {
    const storedToken = localStorage.getItem("token");

    if (!storedToken) {
      setLoading(false);
      return;
    }

    try {
      const response = await fetch("http://localhost:5000/api/auth/verify", {
        headers: { Authorization: `Bearer ${storedToken}` },
      });

      if (response.ok) {
        const data = await response.json();
        setToken(storedToken);
        setUser(data.user);
      } else {
        // Token expired or invalid -- clean up
        localStorage.removeItem("token");
        localStorage.removeItem("user");
      }
    } catch (error) {
      localStorage.removeItem("token");
      localStorage.removeItem("user");
    }

    setLoading(false);
  };

  verifyStoredToken();
}, []);
```

### Backend Verification Endpoint

```javascript
// routes/auth.js
router.get("/verify", protect, async (req, res) => {
  res.status(200).json({
    success: true,
    user: { id: req.user._id, name: req.user.name, email: req.user.email, role: req.user.role },
  });
});
```

### Handling Expired Tokens Automatically

Create a fetch wrapper that redirects to login when a token expires:

```javascript
// utils/api.js
export async function authFetch(url, options = {}) {
  const token = localStorage.getItem("token");

  const config = {
    ...options,
    headers: {
      "Content-Type": "application/json",
      ...options.headers,
      ...(token && { Authorization: `Bearer ${token}` }),
    },
  };

  const response = await fetch(url, config);

  if (response.status === 401) {
    localStorage.removeItem("token");
    localStorage.removeItem("user");
    window.location.href = "/login";
    return;
  }

  return response;
}
```

```javascript
// Usage in any component:
import { authFetch } from "../utils/api";

const response = await authFetch("http://localhost:5000/api/user/profile");
const data = await response.json();
```

---

## 11. Summary

### Key Concepts

| Concept                        | What It Does                                                        |
|--------------------------------|---------------------------------------------------------------------|
| **Authentication**             | Verifies who the user is (login with email + password)              |
| **Authorization**              | Determines what the user can access (role-based permissions)        |
| **bcrypt**                     | Hashes passwords so they are never stored as plain text             |
| **JWT**                        | A signed token that proves the user's identity                      |
| **AuthContext**                | React Context that shares auth state across all components          |
| **PrivateRoute**               | Blocks unauthenticated users from protected pages                   |
| **protect middleware**         | Express middleware that verifies JWT before route handlers           |
| **authorize middleware**       | Express middleware that checks user role against allowed roles       |
| **httpOnly cookies**           | Secure storage that JavaScript cannot access (prevents XSS)         |
| **Token verification**         | Checking stored tokens on app load for persistent login             |

### Complete File Structure

```
  project/
  +-- client/                        (React frontend)
  |   +-- src/
  |       +-- context/
  |       |   +-- AuthContext.jsx     (Authentication state)
  |       +-- components/
  |       |   +-- PrivateRoute.jsx    (Route protection)
  |       |   +-- AdminRoute.jsx      (Admin-only protection)
  |       +-- pages/
  |       |   +-- Login.jsx
  |       |   +-- Register.jsx
  |       |   +-- Dashboard.jsx
  |       +-- utils/
  |       |   +-- api.js              (Fetch wrapper)
  |       +-- App.jsx
  |
  +-- server/                        (Express backend)
      +-- models/
      |   +-- User.js                (Mongoose schema)
      +-- middleware/
      |   +-- auth.js                (protect + authorize)
      +-- routes/
      |   +-- auth.js                (register, login, logout, verify)
      |   +-- user.js                (profile routes)
      |   +-- admin.js               (admin-only routes)
      +-- server.js
      +-- .env                       (JWT_SECRET, MONGO_URI)
```

### Security Checklist

- [ ] Passwords are hashed with bcrypt before storing
- [ ] JWT secret is in environment variables, never in code
- [ ] Login errors are generic ("Invalid email or password")
- [ ] Tokens have an expiration time
- [ ] Backend routes are protected with middleware, not just frontend
- [ ] User roles are enforced on the backend
- [ ] CORS is configured for your frontend domain only
- [ ] Password is excluded from API responses (`.select("-password")`)
