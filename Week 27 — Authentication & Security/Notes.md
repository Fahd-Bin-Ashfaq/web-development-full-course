# Week 27: Authentication & Security

A comprehensive guide to implementing user authentication, password security, JSON Web Tokens, protected routes, and security best practices in Express.js applications. This document builds on the CRUD API and middleware concepts from Weeks 25-26 and completes the backend fundamentals phase of the course.

---

## Table of Contents

1. [Authentication vs Authorization](#1-authentication-vs-authorization)
   - [Understanding the Difference](#11-understanding-the-difference)
   - [Authentication and Authorization Flow](#12-authentication-and-authorization-flow)
2. [Password Hashing with bcrypt](#2-password-hashing-with-bcrypt)
   - [Why Hash Passwords?](#21-why-hash-passwords)
   - [How bcrypt Works](#22-how-bcrypt-works)
   - [Hashing a Password](#23-hashing-a-password)
   - [Comparing Passwords](#24-comparing-passwords)
3. [JSON Web Tokens (JWT)](#3-json-web-tokens-jwt)
   - [What is a JWT?](#31-what-is-a-jwt)
   - [JWT Structure Diagram](#32-jwt-structure-diagram)
   - [JWT Authentication Flow](#33-jwt-authentication-flow)
   - [Generating a JWT](#34-generating-a-jwt)
   - [Verifying a JWT](#35-verifying-a-jwt)
4. [Registration Endpoint](#4-registration-endpoint)
5. [Login Endpoint](#5-login-endpoint)
6. [Protecting Routes with JWT Middleware](#6-protecting-routes-with-jwt-middleware)
7. [Role-Based Access Control](#7-role-based-access-control)
   - [Admin vs User Roles](#71-admin-vs-user-roles)
   - [Role Authorization Middleware](#72-role-authorization-middleware)
8. [Security Best Practices](#8-security-best-practices)
   - [Helmet](#81-helmet)
   - [Rate Limiting](#82-rate-limiting)
   - [CORS Configuration](#83-cors-configuration)
   - [Input Sanitization](#84-input-sanitization)
   - [HTTPS](#85-https)
   - [Environment Variables](#86-environment-variables)
9. [Week 27 Project: Complete REST API with Authentication](#9-week-27-project-complete-rest-api-with-authentication)
10. [Summary](#10-summary)

---

## 1. Authentication vs Authorization

### 1.1 Understanding the Difference

**Authentication** and **Authorization** are two separate security concepts that are often confused. They work together but serve different purposes.

| Aspect             | Authentication                          | Authorization                            |
|--------------------|-----------------------------------------|------------------------------------------|
| **Question**       | "Who are you?"                          | "What are you allowed to do?"            |
| **Purpose**        | Verify the identity of the user         | Determine the permissions of the user    |
| **When**           | Happens first (login)                   | Happens after authentication             |
| **How**            | Credentials (email + password, token)   | Roles, permissions, access levels        |
| **Failure**        | 401 Unauthorized                        | 403 Forbidden                            |
| **Real-life**      | Showing your ID at a building entrance  | Your ID card grants access to floor 3 only |

**Real-Life Analogy: An Office Building**

```
+----------------------------------------------------------------+
|                     OFFICE BUILDING                              |
+----------------------------------------------------------------+
|                                                                  |
|  STEP 1: AUTHENTICATION                                         |
|  +--------------------------+                                    |
|  |  RECEPTION DESK          |                                    |
|  |                          |                                    |
|  |  Guard: "Show me your    |                                    |
|  |         employee ID."    |                                    |
|  |                          |                                    |
|  |  You: *shows ID badge*   |                                    |
|  |                          |                                    |
|  |  Guard: "OK, you are     |                                    |
|  |         Fahad from IT."  |                                    |
|  +--------------------------+                                    |
|        |                                                         |
|        v                                                         |
|  STEP 2: AUTHORIZATION                                           |
|  +--------------------------+      +--------------------------+  |
|  |  FLOOR 3: IT DEPARTMENT  |      |  FLOOR 5: CEO OFFICE     |  |
|  |                          |      |                          |  |
|  |  Your badge works here.  |      |  ACCESS DENIED.          |  |
|  |  ACCESS GRANTED.         |      |  You are authenticated   |  |
|  |                          |      |  but not authorized.     |  |
|  +--------------------------+      +--------------------------+  |
|                                                                  |
+----------------------------------------------------------------+
```

- **Authentication** = The guard confirms your identity (you are who you say you are).
- **Authorization** = Your badge only opens certain doors (you can only access what you are allowed to).

### 1.2 Authentication and Authorization Flow

```
Client                                       Server
------                                       ------

1. REGISTRATION
   POST /api/auth/register
   { email, password }    --------->    Hash password with bcrypt
                                        Save user to database
                          <---------    Return JWT token

2. LOGIN
   POST /api/auth/login
   { email, password }    --------->    Find user by email
                                        Compare password with bcrypt
                          <---------    Return JWT token

3. AUTHENTICATED REQUEST
   GET /api/profile
   Authorization:
   Bearer <token>         --------->    Verify JWT token (Authentication)
                                        Check user role (Authorization)
                          <---------    Return protected data

4. UNAUTHORIZED REQUEST
   GET /api/admin/users
   Authorization:
   Bearer <user-token>    --------->    Verify JWT token (Authentication OK)
                                        Check role: "user" !== "admin"
                          <---------    403 Forbidden (Authorization FAILED)
```

---

## 2. Password Hashing with bcrypt

### 2.1 Why Hash Passwords?

**Never store passwords in plain text.** If your database is breached, every user's password is exposed.

```
PLAIN TEXT (Dangerous):              HASHED (Secure):
-----------------------              -----------------
| email          | password   |      | email          | password                           |
|----------------|------------|      |----------------|-------------------------------------|
| fahad@mail.com | mypass123  |      | fahad@mail.com | $2b$10$N9qo8uLOick...Yfm0fzMep  |
| sara@mail.com  | abc456     |      | sara@mail.com  | $2b$10$IhR7yvz0X8k...Q5JYT3afR  |

If database is stolen:              If database is stolen:
Attacker sees all passwords.         Attacker sees random strings.
All accounts compromised.            Passwords cannot be reversed.
```

**Hashing** is a one-way process. You can convert a password into a hash, but you cannot convert the hash back into the password. Even the application itself does not know the original password -- it can only compare.

### 2.2 How bcrypt Works

bcrypt adds a **salt** (random data) to the password before hashing. This means even if two users have the same password, their hashes will be different.

```
Password: "mypass123"

Without salt:                        With salt (bcrypt):
hash("mypass123") = abc123           hash("mypass123" + "random_salt_1") = xyz789
hash("mypass123") = abc123           hash("mypass123" + "random_salt_2") = def456
(Same password = same hash)          (Same password = different hash!)
```

The **salt rounds** parameter (also called the cost factor) controls how many times the hashing algorithm runs. Higher rounds = more secure but slower.

| Salt Rounds | Time to Hash | Security Level |
|-------------|-------------|----------------|
| 8           | ~40ms       | Minimum        |
| 10          | ~130ms      | Recommended    |
| 12          | ~500ms      | Strong         |
| 14          | ~2 seconds  | Very strong    |

### 2.3 Hashing a Password

```bash
npm install bcrypt
```

```javascript
const bcrypt = require("bcrypt");

async function hashPassword(plainPassword) {
    const saltRounds = 10;

    // Method 1: Auto-generate salt and hash
    const hashedPassword = await bcrypt.hash(plainPassword, saltRounds);

    console.log("Original:", plainPassword);
    console.log("Hashed:", hashedPassword);

    return hashedPassword;
}

hashPassword("mySecurePassword123");
// Original: mySecurePassword123
// Hashed: $2b$10$N9qo8uLOickgx2ZMRZoMyeIjZAgcfl7p92ldGxad68LJZdL17lhWy
```

**Anatomy of a bcrypt hash:**
```
$2b$10$N9qo8uLOickgx2ZMRZoMyeIjZAgcfl7p92ldGxad68LJZdL17lhWy
 |   |  |                     |
 |   |  |                     +-- Hash result (31 characters)
 |   |  +-- Salt (22 characters)
 |   +-- Cost factor (10 rounds)
 +-- Algorithm version (2b = bcrypt)
```

### 2.4 Comparing Passwords

When a user logs in, you compare the plain text password they entered with the hashed password stored in the database.

```javascript
async function checkPassword(plainPassword, hashedPassword) {
    const isMatch = await bcrypt.compare(plainPassword, hashedPassword);

    if (isMatch) {
        console.log("Password is correct!");
    } else {
        console.log("Password is wrong!");
    }

    return isMatch;
}

// Usage
const stored = "$2b$10$N9qo8uLOickgx2ZMRZoMyeIjZAgcfl7p92ldGxad68LJZdL17lhWy";
checkPassword("mySecurePassword123", stored); // true
checkPassword("wrongPassword", stored);       // false
```

**Important:** `bcrypt.compare()` does NOT decrypt the hash. It hashes the input password with the same salt (embedded in the stored hash) and checks if the results match.

---

## 3. JSON Web Tokens (JWT)

### 3.1 What is a JWT?

A JSON Web Token (JWT) is a compact, self-contained string that securely represents claims (information) between two parties. In web applications, JWTs are used to authenticate users without storing session data on the server.

**Real-Life Analogy: A Concert Wristband**

When you arrive at a music festival, you show your ticket (login). The staff verifies it and gives you a wristband (JWT). For the rest of the event, you just show your wristband -- no one checks the ticket again. The wristband itself proves you are allowed in.

### 3.2 JWT Structure Diagram

A JWT consists of three parts separated by dots: `header.payload.signature`

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEsImVtYWlsIjoiZmFoYWRAZXhhbXBsZS5jb20iLCJyb2xlIjoiYWRtaW4iLCJpYXQiOjE3MTg0NTY3ODksImV4cCI6MTcxODQ2MDM4OX0.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
|___________________________________|_______________________________________________________________________________|___________________________________________|
            HEADER                                                PAYLOAD                                                      SIGNATURE


+----------------------------------------------------------------------+
|                           JWT STRUCTURE                               |
+----------------------------------------------------------------------+
|                                                                        |
|  PART 1: HEADER (Algorithm + Token Type)                               |
|  +----------------------------------+                                  |
|  |  {                               |                                  |
|  |    "alg": "HS256",               |  Algorithm: HMAC SHA-256         |
|  |    "typ": "JWT"                  |  Type: JSON Web Token            |
|  |  }                               |                                  |
|  +----------------------------------+                                  |
|                    |                                                   |
|                    v                                                   |
|  PART 2: PAYLOAD (Data / Claims)                                       |
|  +----------------------------------+                                  |
|  |  {                               |                                  |
|  |    "userId": 1,                  |  Who is this user?               |
|  |    "email": "fahad@example.com", |  Custom data (claims)            |
|  |    "role": "admin",              |  User's role                     |
|  |    "iat": 1718456789,            |  Issued At (timestamp)           |
|  |    "exp": 1718460389             |  Expires At (timestamp)          |
|  |  }                               |                                  |
|  +----------------------------------+                                  |
|                    |                                                   |
|                    v                                                   |
|  PART 3: SIGNATURE (Verification)                                      |
|  +----------------------------------+                                  |
|  |  HMACSHA256(                     |                                  |
|  |    base64(header) + "." +        |  Created using the header,       |
|  |    base64(payload),              |  payload, and a SECRET KEY       |
|  |    your-secret-key               |  that only the server knows.     |
|  |  )                               |                                  |
|  +----------------------------------+                                  |
|                                                                        |
+----------------------------------------------------------------------+
```

**Key points:**
- The **header** and **payload** are Base64-encoded (not encrypted). Anyone can decode and read them.
- The **signature** ensures the token has not been tampered with. If someone changes the payload, the signature will not match.
- **Never put sensitive data** (passwords, credit card numbers) in the payload because it is not encrypted.

### 3.3 JWT Authentication Flow

```
+----------------------------------------------------------------+
|                    JWT AUTHENTICATION FLOW                       |
+----------------------------------------------------------------+
|                                                                  |
|  1. USER LOGS IN                                                 |
|     Client ----> POST /api/auth/login                            |
|                  { email: "fahad@mail.com", password: "123" }    |
|                                                                  |
|  2. SERVER VERIFIES CREDENTIALS                                  |
|     Server: Find user by email                                   |
|     Server: Compare password with bcrypt                         |
|     Server: Credentials valid!                                   |
|                                                                  |
|  3. SERVER CREATES JWT                                           |
|     Server: jwt.sign({ userId: 1, role: "admin" }, SECRET)      |
|     Server ----> { token: "eyJhbGci..." }                        |
|                                                                  |
|  4. CLIENT STORES TOKEN                                          |
|     Client: Save token in localStorage or cookie                 |
|                                                                  |
|  5. CLIENT SENDS TOKEN WITH EVERY REQUEST                        |
|     Client ----> GET /api/profile                                |
|                  Headers: { Authorization: "Bearer eyJhbGci..." }|
|                                                                  |
|  6. SERVER VERIFIES TOKEN                                        |
|     Middleware: Extract token from header                        |
|     Middleware: jwt.verify(token, SECRET)                        |
|     Middleware: Token valid! Attach user to req                  |
|     Route handler: Send protected data                           |
|     Server ----> { user: { id: 1, name: "Fahad" } }             |
|                                                                  |
+----------------------------------------------------------------+
```

### 3.4 Generating a JWT

```bash
npm install jsonwebtoken
```

```javascript
const jwt = require("jsonwebtoken");

// Secret key -- MUST be stored in environment variables in production
const JWT_SECRET = "your-super-secret-key-change-in-production";
const JWT_EXPIRES_IN = "1h"; // Token expires in 1 hour

function generateToken(user) {
    const payload = {
        userId: user.id,
        email: user.email,
        role: user.role
    };

    const token = jwt.sign(payload, JWT_SECRET, {
        expiresIn: JWT_EXPIRES_IN
    });

    return token;
}

// Usage
const token = generateToken({ id: 1, email: "fahad@example.com", role: "admin" });
console.log(token);
// eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjE...
```

### 3.5 Verifying a JWT

```javascript
function verifyToken(token) {
    try {
        const decoded = jwt.verify(token, JWT_SECRET);
        console.log("Token is valid:", decoded);
        return decoded;
    } catch (err) {
        if (err.name === "TokenExpiredError") {
            console.log("Token has expired");
        } else if (err.name === "JsonWebTokenError") {
            console.log("Token is invalid");
        }
        return null;
    }
}

// Usage
const decoded = verifyToken(token);
// { userId: 1, email: "fahad@example.com", role: "admin", iat: 1718456789, exp: 1718460389 }
```

---

## 4. Registration Endpoint

The registration endpoint creates a new user account. It hashes the password, saves the user, and returns a JWT token so the user is immediately logged in after registration.

```javascript
const express = require("express");
const bcrypt = require("bcrypt");
const jwt = require("jsonwebtoken");

const app = express();
app.use(express.json());

const JWT_SECRET = process.env.JWT_SECRET || "your-secret-key";
const JWT_EXPIRES_IN = "24h";

// In-memory users (replace with database in production)
let users = [];
let nextId = 1;

// ---------- REGISTER ----------
app.post("/api/auth/register", async (req, res) => {
    try {
        const { name, email, password } = req.body;

        // 1. Validate input
        if (!name || !email || !password) {
            return res.status(400).json({
                success: false,
                error: "Name, email, and password are required"
            });
        }

        if (password.length < 6) {
            return res.status(400).json({
                success: false,
                error: "Password must be at least 6 characters"
            });
        }

        // 2. Check if user already exists
        const existingUser = users.find(u => u.email === email);
        if (existingUser) {
            return res.status(400).json({
                success: false,
                error: "Email is already registered"
            });
        }

        // 3. Hash the password
        const saltRounds = 10;
        const hashedPassword = await bcrypt.hash(password, saltRounds);

        // 4. Save the user
        const newUser = {
            id: nextId++,
            name,
            email,
            password: hashedPassword,   // Store the HASH, never the plain password
            role: "user"                // Default role
        };
        users.push(newUser);

        // 5. Generate JWT token
        const token = jwt.sign(
            { userId: newUser.id, email: newUser.email, role: newUser.role },
            JWT_SECRET,
            { expiresIn: JWT_EXPIRES_IN }
        );

        // 6. Send response (exclude password from response)
        res.status(201).json({
            success: true,
            token,
            user: {
                id: newUser.id,
                name: newUser.name,
                email: newUser.email,
                role: newUser.role
            }
        });

    } catch (err) {
        res.status(500).json({ success: false, error: "Server error" });
    }
});
```

**Registration flow:**

```
Client sends:                         Server does:
{                                     1. Validate fields
  "name": "Fahad",                    2. Check email not taken
  "email": "fahad@mail.com",          3. Hash password: "pass123"
  "password": "pass123"                  --> "$2b$10$N9qo8u..."
}                                     4. Save user with hashed password
                                      5. Generate JWT token
                                      6. Return token + user info

Server responds:
{
  "success": true,
  "token": "eyJhbGci...",
  "user": {
    "id": 1,
    "name": "Fahad",
    "email": "fahad@mail.com",
    "role": "user"
  }
}
```

---

## 5. Login Endpoint

The login endpoint verifies the user's credentials and returns a JWT token.

```javascript
// ---------- LOGIN ----------
app.post("/api/auth/login", async (req, res) => {
    try {
        const { email, password } = req.body;

        // 1. Validate input
        if (!email || !password) {
            return res.status(400).json({
                success: false,
                error: "Email and password are required"
            });
        }

        // 2. Find user by email
        const user = users.find(u => u.email === email);
        if (!user) {
            return res.status(401).json({
                success: false,
                error: "Invalid email or password"
            });
        }

        // 3. Compare password with stored hash
        const isMatch = await bcrypt.compare(password, user.password);
        if (!isMatch) {
            return res.status(401).json({
                success: false,
                error: "Invalid email or password"
            });
        }

        // 4. Generate JWT token
        const token = jwt.sign(
            { userId: user.id, email: user.email, role: user.role },
            JWT_SECRET,
            { expiresIn: JWT_EXPIRES_IN }
        );

        // 5. Send response
        res.status(200).json({
            success: true,
            token,
            user: {
                id: user.id,
                name: user.name,
                email: user.email,
                role: user.role
            }
        });

    } catch (err) {
        res.status(500).json({ success: false, error: "Server error" });
    }
});
```

**Security note:** When login fails, always return the same generic error message ("Invalid email or password") regardless of whether the email or the password was wrong. This prevents attackers from discovering which emails are registered in your system.

```
WRONG (reveals information):          RIGHT (generic message):
"Email not found"                     "Invalid email or password"
"Password is incorrect"               "Invalid email or password"

Attacker learns which                 Attacker cannot tell if the email
emails exist in your system.          exists or if the password is wrong.
```

---

## 6. Protecting Routes with JWT Middleware

Create a middleware that extracts and verifies the JWT from the `Authorization` header.

```javascript
// middleware/auth.js
const jwt = require("jsonwebtoken");
const JWT_SECRET = process.env.JWT_SECRET || "your-secret-key";

function authenticate(req, res, next) {
    // 1. Get the Authorization header
    const authHeader = req.headers["authorization"];

    // 2. Check if header exists and has correct format
    if (!authHeader || !authHeader.startsWith("Bearer ")) {
        return res.status(401).json({
            success: false,
            error: "Access denied. No token provided."
        });
    }

    // 3. Extract the token (remove "Bearer " prefix)
    const token = authHeader.split(" ")[1];

    try {
        // 4. Verify the token
        const decoded = jwt.verify(token, JWT_SECRET);

        // 5. Attach user info to the request object
        req.user = decoded;

        // 6. Continue to the next middleware/route
        next();

    } catch (err) {
        if (err.name === "TokenExpiredError") {
            return res.status(401).json({
                success: false,
                error: "Token has expired. Please log in again."
            });
        }
        return res.status(401).json({
            success: false,
            error: "Invalid token."
        });
    }
}

module.exports = authenticate;
```

**Using the middleware:**

```javascript
const authenticate = require("./middleware/auth");

// PUBLIC routes -- no authentication needed
app.post("/api/auth/register", registerHandler);
app.post("/api/auth/login", loginHandler);

// PROTECTED routes -- authentication required
app.get("/api/profile", authenticate, (req, res) => {
    // req.user is available because authenticate middleware set it
    const user = users.find(u => u.id === req.user.userId);

    res.json({
        success: true,
        data: {
            id: user.id,
            name: user.name,
            email: user.email,
            role: user.role
        }
    });
});

app.put("/api/profile", authenticate, (req, res) => {
    // Update the logged-in user's profile
    const user = users.find(u => u.id === req.user.userId);
    const { name } = req.body;

    if (name) user.name = name;

    res.json({ success: true, data: { id: user.id, name: user.name, email: user.email } });
});
```

**How the Authorization header works:**

```
Client request:
GET /api/profile HTTP/1.1
Host: localhost:3000
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...

                       |       |
                       |       +-- The actual JWT token
                       +-- The word "Bearer" (authentication scheme)

Middleware extracts:
const authHeader = "Bearer eyJhbGci...";
const token = authHeader.split(" ")[1]; // "eyJhbGci..."
```

---

## 7. Role-Based Access Control

### 7.1 Admin vs User Roles

Different users need different levels of access. A regular user should be able to view their own profile but should not be able to delete other users' accounts.

```
+--------------------------------------------------+
|           ROLE-BASED ACCESS                       |
+--------------------------------------------------+
|                                                    |
|  ADMIN                       USER                  |
|  -----                       ----                  |
|  View all users              View own profile      |
|  Delete any user             Edit own profile      |
|  Edit any product            View products         |
|  View system stats           Place orders          |
|  Manage roles                View own orders       |
|                                                    |
|  GET /api/admin/users   OK   GET /api/profile  OK  |
|  DELETE /api/users/5    OK   DELETE /api/users  NO |
|  GET /api/admin/stats   OK   GET /api/admin    NO  |
|                                                    |
+--------------------------------------------------+
```

### 7.2 Role Authorization Middleware

After authentication (verifying identity), authorization checks whether the user has the right role.

```javascript
// middleware/authorize.js
function authorize(...allowedRoles) {
    return (req, res, next) => {
        // req.user is set by the authenticate middleware
        if (!req.user) {
            return res.status(401).json({
                success: false,
                error: "Authentication required"
            });
        }

        if (!allowedRoles.includes(req.user.role)) {
            return res.status(403).json({
                success: false,
                error: "You do not have permission to access this resource"
            });
        }

        next();
    };
}

module.exports = authorize;
```

**Using both authentication and authorization:**

```javascript
const authenticate = require("./middleware/auth");
const authorize = require("./middleware/authorize");

// Any authenticated user can access
app.get("/api/profile", authenticate, (req, res) => {
    res.json({ user: req.user });
});

// Only admins can access
app.get("/api/admin/users", authenticate, authorize("admin"), (req, res) => {
    res.json({ success: true, data: users });
});

// Only admins can delete users
app.delete("/api/admin/users/:id", authenticate, authorize("admin"), (req, res) => {
    const index = users.findIndex(u => u.id === parseInt(req.params.id));
    if (index === -1) {
        return res.status(404).json({ success: false, error: "User not found" });
    }
    users.splice(index, 1);
    res.status(204).send();
});

// Admins and moderators can access
app.put("/api/posts/:id/approve",
    authenticate,
    authorize("admin", "moderator"),
    (req, res) => {
        res.json({ message: "Post approved" });
    }
);
```

**Middleware chain flow:**

```
Request: GET /api/admin/users
Headers: Authorization: Bearer <token>

     authenticate               authorize("admin")          Route Handler
     ------------               ------------------          -------------
     Extract token              Check req.user.role         Send user list
     Verify with JWT            "admin" in ["admin"]?
     Set req.user = {           YES --> next()
       userId: 1,                                           res.json(users)
       role: "admin"
     }
     next()

Request: GET /api/admin/users (regular user)
Headers: Authorization: Bearer <user-token>

     authenticate               authorize("admin")
     ------------               ------------------
     Token valid                Check req.user.role
     req.user = {               "user" in ["admin"]?
       userId: 2,               NO --> 403 Forbidden
       role: "user"             "You do not have permission..."
     }
     next()                     (request stops here)
```

---

## 8. Security Best Practices

### 8.1 Helmet

Helmet sets security-related HTTP headers to protect against common web vulnerabilities.

```bash
npm install helmet
```

```javascript
const helmet = require("helmet");
app.use(helmet());
```

### 8.2 Rate Limiting

Rate limiting prevents abuse by limiting how many requests a client can make in a given time period. This protects against brute-force attacks on login endpoints and denial-of-service attacks.

```bash
npm install express-rate-limit
```

```javascript
const rateLimit = require("express-rate-limit");

// General rate limiter: 100 requests per 15 minutes
const generalLimiter = rateLimit({
    windowMs: 15 * 60 * 1000,   // 15 minutes
    max: 100,                    // Limit each IP to 100 requests per window
    message: {
        success: false,
        error: "Too many requests. Please try again later."
    }
});

// Strict rate limiter for auth routes: 5 attempts per 15 minutes
const authLimiter = rateLimit({
    windowMs: 15 * 60 * 1000,
    max: 5,
    message: {
        success: false,
        error: "Too many login attempts. Please try again in 15 minutes."
    }
});

// Apply rate limiters
app.use("/api/", generalLimiter);               // All API routes
app.use("/api/auth/login", authLimiter);         // Login route (stricter)
app.use("/api/auth/register", authLimiter);      // Register route (stricter)
```

### 8.3 CORS Configuration

In production, restrict CORS to only allow requests from your frontend domain.

```javascript
const cors = require("cors");

app.use(cors({
    origin: process.env.FRONTEND_URL || "http://localhost:3000",
    methods: ["GET", "POST", "PUT", "DELETE"],
    allowedHeaders: ["Content-Type", "Authorization"],
    credentials: true
}));
```

### 8.4 Input Sanitization

Sanitization removes or escapes potentially dangerous characters from user input to prevent injection attacks.

```bash
npm install express-mongo-sanitize xss-clean
```

```javascript
const mongoSanitize = require("express-mongo-sanitize");
const xss = require("xss-clean");

// Prevent NoSQL injection attacks
// Removes $ and . from req.body, req.query, and req.params
app.use(mongoSanitize());

// Prevent XSS (Cross-Site Scripting) attacks
// Sanitizes user input in req.body, req.query, and req.params
app.use(xss());
```

**What these prevent:**
```
Without mongoSanitize:                  With mongoSanitize:
POST /api/auth/login                    POST /api/auth/login
{                                       {
  "email": { "$gt": "" },                "email": { "gt": "" },    // $ removed
  "password": { "$gt": "" }              "password": { "gt": "" }  // $ removed
}                                       }
This could bypass authentication!       Injection attempt neutralized.

Without xss:                            With xss:
POST /api/comments                      POST /api/comments
{                                       {
  "text": "<script>alert('hack')</script>"   "text": "&lt;script&gt;alert('hack')&lt;/script&gt;"
}                                       }
Script would execute in browser!        Script tags are escaped and harmless.
```

### 8.5 HTTPS

Always use HTTPS in production to encrypt data in transit.

```
HTTP (Not Secure):                      HTTPS (Secure):
-------------------                     -----------------
Client --> "password123" --> Server     Client --> [encrypted] --> Server
                                        
Anyone on the network can               Data is encrypted. Even if
read the password.                      intercepted, it cannot be read.
```

In development, HTTP is fine. In production, use a reverse proxy like Nginx or a hosting platform (Heroku, Railway, Render) that provides HTTPS automatically.

### 8.6 Environment Variables

Never hardcode secrets (JWT keys, database passwords, API keys) in your source code. Use environment variables.

```bash
npm install dotenv
```

**`.env` file (never commit this to Git):**
```
PORT=3000
JWT_SECRET=your-very-long-random-secret-key-here-minimum-32-chars
JWT_EXPIRES_IN=24h
FRONTEND_URL=http://localhost:3000
```

**`.gitignore` (add .env):**
```
node_modules/
.env
```

**Usage in code:**
```javascript
require("dotenv").config();

const JWT_SECRET = process.env.JWT_SECRET;
const PORT = process.env.PORT || 3000;
```

**Security checklist:**

```
+--------------------------------------------------+
|           SECURITY CHECKLIST                      |
+--------------------------------------------------+
| [x] Hash passwords with bcrypt (10+ rounds)      |
| [x] Use JWT with expiration for authentication   |
| [x] Store secrets in environment variables        |
| [x] Use Helmet for security headers              |
| [x] Rate limit login and registration endpoints  |
| [x] Configure CORS for production                |
| [x] Sanitize input (NoSQL injection, XSS)        |
| [x] Use HTTPS in production                      |
| [x] Return generic error messages on login fail  |
| [x] Never send passwords in API responses        |
| [x] Add .env to .gitignore                       |
+--------------------------------------------------+
```

---

## 9. Week 27 Project: Complete REST API with Authentication

Build a complete REST API for a note-taking application with user authentication, protected routes, and role-based access.

**Project requirements:**
- User registration and login with JWT
- Password hashing with bcrypt
- Protected CRUD routes for notes (each user sees only their own notes)
- Admin route to view all users
- Security middleware (helmet, cors, rate limiting)

```javascript
// ---------- COMPLETE PROJECT: Notes API with Auth ----------

const express = require("express");
const bcrypt = require("bcrypt");
const jwt = require("jsonwebtoken");
const helmet = require("helmet");
const cors = require("cors");
const rateLimit = require("express-rate-limit");

const app = express();

// ---------- CONFIGURATION ----------
const JWT_SECRET = process.env.JWT_SECRET || "dev-secret-change-in-production";
const JWT_EXPIRES_IN = "24h";
const PORT = process.env.PORT || 3000;

// ---------- SECURITY MIDDLEWARE ----------
app.use(helmet());
app.use(cors());
app.use(express.json({ limit: "10kb" })); // Limit body size

const authLimiter = rateLimit({
    windowMs: 15 * 60 * 1000,
    max: 10,
    message: { success: false, error: "Too many attempts. Try again later." }
});

// ---------- DATA STORES ----------
let users = [
    {
        id: 1,
        name: "Admin User",
        email: "admin@example.com",
        password: "$2b$10$abcdefghijklmnopqrstuuABCDEFGHIJKLMNOPQRSTUVWXYZ12", // pre-hashed
        role: "admin"
    }
];
let notes = [];
let nextUserId = 2;
let nextNoteId = 1;

// ---------- HELPER: Generate Token ----------
function generateToken(user) {
    return jwt.sign(
        { userId: user.id, email: user.email, role: user.role },
        JWT_SECRET,
        { expiresIn: JWT_EXPIRES_IN }
    );
}

// ---------- MIDDLEWARE: Authenticate ----------
function authenticate(req, res, next) {
    const authHeader = req.headers["authorization"];

    if (!authHeader || !authHeader.startsWith("Bearer ")) {
        return res.status(401).json({ success: false, error: "No token provided" });
    }

    const token = authHeader.split(" ")[1];

    try {
        req.user = jwt.verify(token, JWT_SECRET);
        next();
    } catch (err) {
        return res.status(401).json({ success: false, error: "Invalid or expired token" });
    }
}

// ---------- MIDDLEWARE: Authorize ----------
function authorize(...roles) {
    return (req, res, next) => {
        if (!roles.includes(req.user.role)) {
            return res.status(403).json({ success: false, error: "Access denied" });
        }
        next();
    };
}

// ========== AUTH ROUTES ==========

// Register
app.post("/api/auth/register", authLimiter, async (req, res) => {
    try {
        const { name, email, password } = req.body;

        if (!name || !email || !password) {
            return res.status(400).json({ success: false, error: "All fields required" });
        }

        if (password.length < 6) {
            return res.status(400).json({ success: false, error: "Password min 6 characters" });
        }

        if (users.find(u => u.email === email)) {
            return res.status(400).json({ success: false, error: "Email already registered" });
        }

        const hashedPassword = await bcrypt.hash(password, 10);

        const user = {
            id: nextUserId++,
            name,
            email,
            password: hashedPassword,
            role: "user"
        };
        users.push(user);

        const token = generateToken(user);

        res.status(201).json({
            success: true,
            token,
            user: { id: user.id, name: user.name, email: user.email, role: user.role }
        });
    } catch (err) {
        res.status(500).json({ success: false, error: "Server error" });
    }
});

// Login
app.post("/api/auth/login", authLimiter, async (req, res) => {
    try {
        const { email, password } = req.body;

        if (!email || !password) {
            return res.status(400).json({ success: false, error: "Email and password required" });
        }

        const user = users.find(u => u.email === email);
        if (!user) {
            return res.status(401).json({ success: false, error: "Invalid email or password" });
        }

        const isMatch = await bcrypt.compare(password, user.password);
        if (!isMatch) {
            return res.status(401).json({ success: false, error: "Invalid email or password" });
        }

        const token = generateToken(user);

        res.status(200).json({
            success: true,
            token,
            user: { id: user.id, name: user.name, email: user.email, role: user.role }
        });
    } catch (err) {
        res.status(500).json({ success: false, error: "Server error" });
    }
});

// ========== NOTES ROUTES (Protected) ==========

// Get my notes
app.get("/api/notes", authenticate, (req, res) => {
    const myNotes = notes.filter(n => n.userId === req.user.userId);
    res.json({ success: true, count: myNotes.length, data: myNotes });
});

// Get one of my notes
app.get("/api/notes/:id", authenticate, (req, res) => {
    const note = notes.find(
        n => n.id === parseInt(req.params.id) && n.userId === req.user.userId
    );

    if (!note) {
        return res.status(404).json({ success: false, error: "Note not found" });
    }

    res.json({ success: true, data: note });
});

// Create a note
app.post("/api/notes", authenticate, (req, res) => {
    const { title, content } = req.body;

    if (!title || !content) {
        return res.status(400).json({ success: false, error: "Title and content required" });
    }

    const note = {
        id: nextNoteId++,
        userId: req.user.userId,
        title,
        content,
        createdAt: new Date().toISOString()
    };
    notes.push(note);

    res.status(201).json({ success: true, data: note });
});

// Update a note
app.put("/api/notes/:id", authenticate, (req, res) => {
    const note = notes.find(
        n => n.id === parseInt(req.params.id) && n.userId === req.user.userId
    );

    if (!note) {
        return res.status(404).json({ success: false, error: "Note not found" });
    }

    const { title, content } = req.body;
    if (title) note.title = title;
    if (content) note.content = content;

    res.json({ success: true, data: note });
});

// Delete a note
app.delete("/api/notes/:id", authenticate, (req, res) => {
    const index = notes.findIndex(
        n => n.id === parseInt(req.params.id) && n.userId === req.user.userId
    );

    if (index === -1) {
        return res.status(404).json({ success: false, error: "Note not found" });
    }

    notes.splice(index, 1);
    res.status(204).send();
});

// ========== ADMIN ROUTES ==========

// Get all users (admin only)
app.get("/api/admin/users", authenticate, authorize("admin"), (req, res) => {
    const safeUsers = users.map(u => ({
        id: u.id,
        name: u.name,
        email: u.email,
        role: u.role
    }));
    res.json({ success: true, count: safeUsers.length, data: safeUsers });
});

// ========== ERROR HANDLER ==========

app.use((err, req, res, next) => {
    console.error(err.message);
    res.status(500).json({ success: false, error: "Internal server error" });
});

// ========== START ==========
app.listen(PORT, () => {
    console.log(`Notes API running on http://localhost:${PORT}`);
});
```

**API endpoints summary:**

```
PUBLIC:
  POST   /api/auth/register      Register a new user
  POST   /api/auth/login         Login and get token

PROTECTED (requires JWT):
  GET    /api/notes              Get my notes
  GET    /api/notes/:id          Get one of my notes
  POST   /api/notes              Create a note
  PUT    /api/notes/:id          Update my note
  DELETE /api/notes/:id          Delete my note

ADMIN ONLY (requires JWT + admin role):
  GET    /api/admin/users        Get all users
```

---

## 10. Summary

| Topic                     | Key Takeaway                                                                   |
|---------------------------|--------------------------------------------------------------------------------|
| **Authentication**        | Verifies identity ("who are you?") -- uses email/password and JWT              |
| **Authorization**         | Checks permissions ("what can you do?") -- uses roles (admin, user)            |
| **bcrypt**                | One-way password hashing with salt; use 10+ rounds                             |
| **JWT**                   | Self-contained token with header.payload.signature; verified with secret key   |
| **Registration**          | Hash password, save user, return JWT token                                     |
| **Login**                 | Compare password with bcrypt, return JWT token on success                      |
| **Auth Middleware**       | Extracts and verifies JWT from Authorization header, attaches user to `req`    |
| **Role-Based Access**     | `authorize("admin")` middleware checks `req.user.role` after authentication    |
| **Helmet**                | Sets security headers (XSS protection, clickjacking prevention, etc.)          |
| **Rate Limiting**         | Limits requests per IP to prevent brute-force and DoS attacks                  |
| **Input Sanitization**    | Removes dangerous characters to prevent NoSQL injection and XSS               |
| **Environment Variables** | Store secrets in `.env` files, never in source code                            |

---

*This completes the backend fundamentals phase (Weeks 22-27). Next, we will connect our Express API to a MongoDB database and build a full-stack MERN application.*
