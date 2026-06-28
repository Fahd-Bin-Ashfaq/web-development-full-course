# Week 33 — Authentication in MERN: Practice Questions

**Total Questions: 20** (10 MCQs + 5 Short Answer + 5 Coding Exercises)

---

## Part 1: Multiple Choice Questions (MCQs)

**1. What is the difference between authentication and authorization?**

- A) Authentication encrypts data; authorization decrypts data
- B) Authentication verifies who a user is; authorization determines what they can access
- C) Authentication manages sessions; authorization manages cookies
- D) Authentication and authorization mean the same thing

<details>
<summary>Answer</summary>

**B) Authentication verifies who a user is; authorization determines what they can access**

Authentication is the process of verifying a user's identity, typically through credentials like a username and password. Authorization happens after authentication and determines what resources or actions the authenticated user is permitted to access. For example, logging into a system is authentication, while checking whether that logged-in user has admin privileges to delete other accounts is authorization.
</details>

---

**2. What is the primary purpose of bcrypt in a MERN authentication system?**

- A) To generate JSON Web Tokens
- B) To hash and salt passwords before storing them in the database
- C) To encrypt the entire database
- D) To validate email addresses

<details>
<summary>Answer</summary>

**B) To hash and salt passwords before storing them in the database**

Bcrypt is a password hashing library that converts plain text passwords into irreversible hash strings before they are saved to the database. It automatically generates a random salt (extra random data added to the password before hashing) which ensures that even if two users have the same password, their stored hashes will be different. This protects user credentials in case the database is compromised, because attackers cannot reverse the hash to obtain the original password.
</details>

---

**3. What are the three parts of a JSON Web Token (JWT)?**

- A) Username, password, and token
- B) Header, payload, and signature
- C) Key, value, and expiry
- D) Issuer, audience, and subject

<details>
<summary>Answer</summary>

**B) Header, payload, and signature**

A JWT consists of three Base64-encoded parts separated by dots (`header.payload.signature`). The **header** contains metadata about the token, including the signing algorithm (e.g., HS256) and token type. The **payload** contains the claims -- the actual data stored in the token such as the user ID, email, role, and expiration time. The **signature** is created by combining the encoded header and payload with a secret key, ensuring the token has not been tampered with. When the server receives a JWT, it recalculates the signature using its secret key and compares it to the one in the token to verify authenticity.
</details>

---

**4. Where is the most secure place to store a JWT in a browser-based application?**

- A) `localStorage`
- B) `sessionStorage`
- C) An `httpOnly` cookie
- D) A JavaScript global variable

<details>
<summary>Answer</summary>

**C) An `httpOnly` cookie**

An `httpOnly` cookie is the most secure option because it cannot be accessed by JavaScript running in the browser. This makes it immune to Cross-Site Scripting (XSS) attacks, where an attacker injects malicious JavaScript to steal tokens. Both `localStorage` and `sessionStorage` are accessible via `document.cookie` or the Storage API in JavaScript, which means any XSS vulnerability could allow an attacker to read and exfiltrate the token. A global variable is even worse because it is lost on page refresh and is easily accessible. When using `httpOnly` cookies, the browser automatically sends the cookie with every request to the server, so the token is handled transparently without any client-side JavaScript involvement.
</details>

---

**5. What does `jwt.verify()` return when a valid token is provided?**

- A) A boolean `true`
- B) The encoded token string
- C) The decoded payload object
- D) The secret key used for signing

<details>
<summary>Answer</summary>

**C) The decoded payload object**

When `jwt.verify(token, secretKey)` is called with a valid, non-expired token and the correct secret key, it returns the decoded payload object. This object contains all the claims that were originally encoded into the token, such as the user ID, email, role, and the standard JWT fields like `iat` (issued at) and `exp` (expiration time). If the token is invalid, expired, or was signed with a different secret, `jwt.verify()` throws an error (such as `JsonWebTokenError` or `TokenExpiredError`) rather than returning a value.

```javascript
const decoded = jwt.verify(token, process.env.JWT_SECRET);
// decoded = { userId: "abc123", email: "user@example.com", iat: 1718000000, exp: 1718086400 }
```
</details>

---

**6. What is the main advantage of setting a cookie as `httpOnly`?**

- A) It makes the cookie expire faster
- B) It prevents JavaScript from accessing the cookie, protecting against XSS attacks
- C) It encrypts the cookie value automatically
- D) It allows the cookie to be shared across different domains

<details>
<summary>Answer</summary>

**B) It prevents JavaScript from accessing the cookie, protecting against XSS attacks**

When a cookie is set with the `httpOnly` flag, the browser prevents any client-side JavaScript from reading or modifying that cookie through `document.cookie` or any other API. The cookie is only sent automatically by the browser in HTTP request headers. This is a critical security measure because Cross-Site Scripting (XSS) attacks rely on executing malicious JavaScript in the victim's browser to steal sensitive data like authentication tokens. With `httpOnly` enabled, even if an attacker manages to inject a script, they cannot access the token stored in the cookie.
</details>

---

**7. What does Role-Based Access Control (RBAC) allow you to do?**

- A) Encrypt user passwords based on their role
- B) Restrict access to certain routes or resources based on a user's assigned role
- C) Automatically assign tokens to users based on their email
- D) Create separate databases for each user role

<details>
<summary>Answer</summary>

**B) Restrict access to certain routes or resources based on a user's assigned role**

Role-Based Access Control (RBAC) is a security model where permissions are assigned to roles (such as "admin", "editor", "user") rather than to individual users. Each user is assigned one or more roles, and the application checks the user's role before granting access to specific routes or actions. For example, an "admin" role might have permission to delete users and manage settings, while a "user" role can only view and edit their own profile. In a MERN application, RBAC is typically implemented through middleware that checks the `role` field from the decoded JWT payload before allowing the request to proceed.
</details>

---

**8. What role does middleware play in Express authentication?**

- A) It renders the frontend login page
- B) It intercepts requests to verify tokens and attach user data before reaching protected routes
- C) It creates the database connection for authentication
- D) It hashes passwords during registration

<details>
<summary>Answer</summary>

**B) It intercepts requests to verify tokens and attach user data before reaching protected routes**

In Express, authentication middleware is a function that runs before the route handler for any protected endpoint. It extracts the JWT from the request (typically from the `Authorization` header or a cookie), verifies the token using `jwt.verify()`, and attaches the decoded user information to `req.user`. If the token is missing, invalid, or expired, the middleware sends an error response (usually 401 Unauthorized) and prevents the request from reaching the route handler. This pattern allows you to protect multiple routes by simply adding the middleware function to the route definition, rather than repeating authentication logic in every route handler.

```javascript
app.get("/api/profile", authMiddleware, (req, res) => {
    // req.user is available here because the middleware attached it
    res.json({ user: req.user });
});
```
</details>

---

**9. What is the purpose of React Context in authentication?**

- A) To make API calls to the authentication server
- B) To provide global auth state (user, token, login/logout functions) to all components without prop drilling
- C) To encrypt data before sending it to the backend
- D) To handle routing between login and dashboard pages

<details>
<summary>Answer</summary>

**B) To provide global auth state (user, token, login/logout functions) to all components without prop drilling**

React Context creates a global state container that any component in the component tree can access without passing props through intermediate components (prop drilling). In an authentication system, the AuthContext typically holds the current user object, the authentication token, loading state, and functions like `login()` and `logout()`. Any component that needs to check if a user is logged in, display the user's name, or trigger a logout can consume the context directly using the `useContext` hook. This is far more maintainable than passing `user`, `token`, and `setUser` through every component in the hierarchy.
</details>

---

**10. How should token expiration be handled in a MERN application?**

- A) Tokens should never expire for better user experience
- B) The server should check expiration during verification, and the client should handle 401 responses by redirecting to login
- C) The client should delete the token after a fixed time using `setTimeout`
- D) The database should automatically delete expired tokens

<details>
<summary>Answer</summary>

**B) The server should check expiration during verification, and the client should handle 401 responses by redirecting to login**

Token expiration is a two-sided responsibility. On the server side, JWTs are created with an `expiresIn` option (e.g., `jwt.sign(payload, secret, { expiresIn: "1d" })`), and `jwt.verify()` automatically checks the `exp` claim -- throwing a `TokenExpiredError` if the token has expired. The server then responds with a 401 status code. On the client side (React), the application should intercept 401 responses (often using an Axios interceptor), clear the stored token and user data, and redirect the user to the login page. Tokens should always have an expiration time because if a token is stolen, the attacker's access is limited to the token's remaining lifetime rather than being permanent.
</details>

---

## Part 2: Short Answer Questions

**11. Explain the difference between authentication and authorization with real-world examples from a web application.**

<details>
<summary>Answer</summary>

**Authentication** is the process of verifying a user's identity -- confirming that someone is who they claim to be. It answers the question: "Who are you?" In a web application, authentication typically involves a user submitting their email and password through a login form. The server checks the credentials against the database, and if they match, the user is authenticated and receives a token (like a JWT) as proof of their identity.

**Authorization** is the process of determining what an authenticated user is allowed to do. It answers the question: "What are you permitted to access?" Authorization happens after authentication and checks the user's permissions or role before granting access to specific resources or actions.

**Real-world examples in a web application:**

1. **Authentication:** A user enters their email (`fahad@example.com`) and password on the login page. The server verifies the password hash matches what is stored in MongoDB. If it matches, the user is authenticated and receives a JWT.

2. **Authorization:** After logging in, the authenticated user tries to access the `/admin/dashboard` route. The server checks the user's role from the JWT payload. If the role is `"admin"`, access is granted. If the role is `"user"`, the server responds with 403 Forbidden -- the user is authenticated (we know who they are) but not authorized (they do not have permission).

3. **Another example:** On a blog platform, any authenticated user can create and edit their own posts (authentication is sufficient). However, only users with the `"moderator"` role can delete other users' posts (authorization is required).

The key distinction is that authentication is binary (you are either verified or not), while authorization is granular (different users can have different levels of access even after being authenticated).
</details>

---

**12. Why should passwords never be stored in plain text? What approach should be used instead?**

<details>
<summary>Answer</summary>

Storing passwords in plain text is one of the most dangerous security practices because it creates a single point of catastrophic failure. If an attacker gains access to the database through a breach, SQL injection, or insider threat, they immediately have every user's password in readable form. This is devastating for several reasons:

1. **Mass credential theft:** All user accounts are instantly compromised. Attackers can log in as any user.

2. **Password reuse attacks:** Many users reuse passwords across multiple services. A plain text leak from one application gives attackers access to users' email accounts, banking sites, and other platforms.

3. **No damage limitation:** With plain text storage, there is no way to mitigate the damage after a breach. Every single password must be considered compromised.

4. **Compliance violations:** Storing plain text passwords violates security standards like GDPR, PCI-DSS, and OWASP guidelines, which can result in legal penalties and fines.

**The correct approach is to use bcrypt (or a similar adaptive hashing algorithm) to hash and salt passwords before storing them:**

```javascript
const bcrypt = require("bcrypt");

// During registration -- hash the password
const salt = await bcrypt.genSalt(10);
const hashedPassword = await bcrypt.hash(plainTextPassword, salt);
// Store hashedPassword in database

// During login -- compare the submitted password with the stored hash
const isMatch = await bcrypt.compare(submittedPassword, storedHash);
```

Bcrypt is specifically designed for passwords because it is intentionally slow (controlled by the salt rounds parameter), making brute-force attacks computationally expensive. It also automatically generates a unique salt for each password, so identical passwords produce different hashes. Even if the database is breached, attackers cannot reverse the hashes to obtain the original passwords.
</details>

---

**13. Describe the JWT structure and explain what each of the three parts contains.**

<details>
<summary>Answer</summary>

A JSON Web Token (JWT) is a compact, URL-safe string consisting of three Base64URL-encoded parts separated by dots:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOiI2NjVhYmMxMjMiLCJlbWFpbCI6ImZhaGFkQGV4YW1wbGUuY29tIiwicm9sZSI6InVzZXIiLCJpYXQiOjE3MTgwMDAwMDAsImV4cCI6MTcxODA4NjQwMH0.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

**Part 1: Header**

The header is a JSON object that contains metadata about the token. It specifies the signing algorithm and the token type.

```json
{
    "alg": "HS256",
    "typ": "JWT"
}
```

- `alg` -- The algorithm used to create the signature (e.g., HS256 for HMAC-SHA256, RS256 for RSA-SHA256).
- `typ` -- The type of token, which is always "JWT".

**Part 2: Payload**

The payload is a JSON object containing the "claims" -- the actual data stored in the token. There are three types of claims:

- **Registered claims** (standard fields): `iss` (issuer), `exp` (expiration time), `sub` (subject), `iat` (issued at).
- **Public claims** (commonly used): Custom fields that are widely recognized.
- **Private claims** (application-specific): Custom data relevant to your application.

```json
{
    "userId": "665abc123",
    "email": "fahad@example.com",
    "role": "user",
    "iat": 1718000000,
    "exp": 1718086400
}
```

Important: The payload is encoded, not encrypted. Anyone can decode it and read its contents. Never put sensitive information like passwords or credit card numbers in the payload.

**Part 3: Signature**

The signature is created by taking the encoded header, the encoded payload, and a secret key, then applying the algorithm specified in the header:

```
HMACSHA256(
    base64UrlEncode(header) + "." + base64UrlEncode(payload),
    secret
)
```

The signature serves two purposes: it verifies that the token was issued by a trusted server (because only the server knows the secret key), and it ensures the token has not been tampered with (because changing any character in the header or payload would produce a completely different signature).
</details>

---

**14. Compare `localStorage` and `httpOnly` cookies for storing authentication tokens. What are the security trade-offs of each approach?**

<details>
<summary>Answer</summary>

**localStorage:**

| Aspect | Detail |
|--------|--------|
| Access | Accessible via JavaScript (`localStorage.getItem("token")`) |
| Persistence | Data persists until explicitly removed, even after closing the browser |
| XSS vulnerability | Highly vulnerable -- any XSS attack can read and steal the token |
| CSRF vulnerability | Not vulnerable -- localStorage data is not automatically sent with requests |
| Usage | Token must be manually attached to requests via the `Authorization` header |
| Capacity | ~5-10 MB per origin |

**httpOnly Cookies:**

| Aspect | Detail |
|--------|--------|
| Access | Not accessible via JavaScript -- browser manages it automatically |
| Persistence | Controlled by `expires` or `maxAge` attributes |
| XSS vulnerability | Protected -- JavaScript cannot read the cookie |
| CSRF vulnerability | Vulnerable -- cookies are automatically sent with every request to the domain |
| Usage | Automatically included in requests; no client-side code needed to attach it |
| Capacity | ~4 KB per cookie |

**Security trade-offs:**

- `localStorage` is convenient for single-page applications because you have full control over when and how the token is sent. However, it is fundamentally insecure against XSS attacks. If an attacker injects even a single line of JavaScript into your page (through a comment field, third-party script, or DOM manipulation), they can steal the token with `localStorage.getItem("token")` and send it to their server.

- `httpOnly` cookies are immune to XSS token theft but introduce Cross-Site Request Forgery (CSRF) risk because the browser automatically sends cookies with every request. This can be mitigated by using the `SameSite=Strict` or `SameSite=Lax` cookie attribute and implementing CSRF tokens.

**Recommendation:** For production applications, `httpOnly` cookies with `secure: true` (HTTPS only), `SameSite: "Strict"`, and a short expiration time are generally the more secure choice. XSS vulnerabilities are more common and more difficult to fully prevent than CSRF attacks, and CSRF has well-established mitigation strategies.
</details>

---

**15. Explain how a `PrivateRoute` component works in React to protect authenticated routes.**

<details>
<summary>Answer</summary>

A `PrivateRoute` component is a wrapper that checks whether a user is authenticated before rendering a protected page. If the user is authenticated, the component renders the requested page. If not, it redirects the user to the login page. This pattern ensures that unauthenticated users cannot access pages like dashboards, profiles, or admin panels.

**How it works step by step:**

1. The `PrivateRoute` component consumes the `AuthContext` to access the current authentication state (whether a user is logged in and whether the auth check is still loading).

2. If the authentication state is still loading (e.g., verifying a token on page refresh), it displays a loading indicator to prevent a flash of the login page.

3. If the user is authenticated (`user` exists in context), it renders the child component or the `Outlet` (for nested routes in React Router v6).

4. If the user is not authenticated, it uses the `Navigate` component from React Router to redirect to the `/login` page. The `replace` prop is used so the protected URL is not added to the browser history.

```jsx
import { useContext } from "react";
import { Navigate, Outlet } from "react-router-dom";
import { AuthContext } from "../context/AuthContext";

function PrivateRoute() {
    const { user, loading } = useContext(AuthContext);

    if (loading) {
        return <div>Loading...</div>;
    }

    return user ? <Outlet /> : <Navigate to="/login" replace />;
}
```

**Usage in the router:**

```jsx
<Routes>
    <Route path="/login" element={<Login />} />
    <Route path="/register" element={<Register />} />

    {/* Protected routes */}
    <Route element={<PrivateRoute />}>
        <Route path="/dashboard" element={<Dashboard />} />
        <Route path="/profile" element={<Profile />} />
        <Route path="/settings" element={<Settings />} />
    </Route>
</Routes>
```

All routes nested inside `<PrivateRoute />` are automatically protected. When a user navigates to `/dashboard`, React Router renders `PrivateRoute` first. If the user is logged in, `Outlet` renders the `Dashboard` component. If not, the user is redirected to `/login`. This provides a clean, declarative way to protect multiple routes without repeating authentication checks in every page component.
</details>

---

## Part 3: Coding Exercises

**16. Create a User model with Mongoose that includes `name`, `email`, and `password` fields with proper validation. The email should be unique and validated for correct format. The password should be at least 6 characters.**

**Starter Code:**

```javascript
const mongoose = require("mongoose");

const userSchema = new mongoose.Schema({
    // TODO: Define the name field (required, trimmed)
    // TODO: Define the email field (required, unique, lowercase, validated)
    // TODO: Define the password field (required, minimum length)
});

module.exports = mongoose.model("User", userSchema);
```

<details>
<summary>Solution</summary>

```javascript
const mongoose = require("mongoose");

const userSchema = new mongoose.Schema(
    {
        name: {
            type: String,
            required: [true, "Name is required"],
            trim: true,
            minlength: [2, "Name must be at least 2 characters"],
            maxlength: [50, "Name cannot exceed 50 characters"]
        },
        email: {
            type: String,
            required: [true, "Email is required"],
            unique: true,
            lowercase: true,
            trim: true,
            match: [
                /^[^\s@]+@[^\s@]+\.[^\s@]+$/,
                "Please enter a valid email address"
            ]
        },
        password: {
            type: String,
            required: [true, "Password is required"],
            minlength: [6, "Password must be at least 6 characters"],
            select: false // Exclude password from query results by default
        }
    },
    {
        timestamps: true // Adds createdAt and updatedAt fields automatically
    }
);

module.exports = mongoose.model("User", userSchema);
```

**Key points explained:**

1. **`required: [true, "message"]`** -- The array syntax provides a custom error message when the field is missing.

2. **`unique: true`** on email -- This creates a MongoDB unique index, preventing duplicate email addresses. Note that this is not a Mongoose validator; it is a MongoDB constraint. If a duplicate email is submitted, MongoDB throws an error with code `11000`.

3. **`lowercase: true`** -- Automatically converts the email to lowercase before saving, ensuring `User@Example.com` and `user@example.com` are treated as the same email.

4. **`match: [regex, "message"]`** -- Validates the email format using a regular expression. The regex `^[^\s@]+@[^\s@]+\.[^\s@]+$` checks for a basic email pattern (characters before @, a domain, and a TLD).

5. **`select: false`** on password -- This is a critical security measure. By default, whenever you query users (`User.find()`, `User.findById()`), the password field will be excluded from the results. When you need the password (e.g., during login), you explicitly request it with `User.findOne({ email }).select("+password")`.

6. **`timestamps: true`** -- Mongoose automatically adds and maintains `createdAt` and `updatedAt` fields on every document.
</details>

---

**17. Write an Express registration route that accepts `name`, `email`, and `password` from the request body, hashes the password with bcrypt, saves the user to the database, and returns a JWT.**

**Starter Code:**

```javascript
const express = require("express");
const bcrypt = require("bcrypt");
const jwt = require("jsonwebtoken");
const User = require("../models/User");

const router = express.Router();

// POST /api/auth/register
router.post("/register", async (req, res) => {
    // TODO: Extract name, email, password from req.body
    // TODO: Check if user already exists
    // TODO: Hash the password with bcrypt
    // TODO: Create the user in the database
    // TODO: Generate a JWT
    // TODO: Send the response with the token
});

module.exports = router;
```

<details>
<summary>Solution</summary>

```javascript
const express = require("express");
const bcrypt = require("bcrypt");
const jwt = require("jsonwebtoken");
const User = require("../models/User");

const router = express.Router();

// POST /api/auth/register
router.post("/register", async (req, res) => {
    try {
        const { name, email, password } = req.body;

        // 1. Validate required fields
        if (!name || !email || !password) {
            return res.status(400).json({
                success: false,
                error: "Name, email, and password are required"
            });
        }

        // 2. Check if user already exists
        const existingUser = await User.findOne({ email });
        if (existingUser) {
            return res.status(400).json({
                success: false,
                error: "A user with this email already exists"
            });
        }

        // 3. Hash the password
        const salt = await bcrypt.genSalt(10);
        const hashedPassword = await bcrypt.hash(password, salt);

        // 4. Create user in database
        const user = await User.create({
            name,
            email,
            password: hashedPassword
        });

        // 5. Generate JWT
        const token = jwt.sign(
            { userId: user._id, email: user.email },
            process.env.JWT_SECRET,
            { expiresIn: "7d" }
        );

        // 6. Send response (exclude password from the response)
        res.status(201).json({
            success: true,
            token,
            user: {
                id: user._id,
                name: user.name,
                email: user.email
            }
        });
    } catch (error) {
        // Handle Mongoose validation errors
        if (error.name === "ValidationError") {
            const messages = Object.values(error.errors).map(err => err.message);
            return res.status(400).json({
                success: false,
                errors: messages
            });
        }

        // Handle duplicate key error (unique email constraint)
        if (error.code === 11000) {
            return res.status(400).json({
                success: false,
                error: "A user with this email already exists"
            });
        }

        console.error("Registration error:", error.message);
        res.status(500).json({
            success: false,
            error: "Server error during registration"
        });
    }
});

module.exports = router;
```

**How the registration flow works:**

1. The client sends a POST request with `name`, `email`, and `password` in the request body.
2. The server validates that all required fields are present.
3. It checks the database for an existing user with the same email to prevent duplicates.
4. The plain text password is hashed using bcrypt with 10 salt rounds. The `salt` adds random data to the password before hashing, so identical passwords produce different hashes.
5. The user document is created in MongoDB with the hashed password (never the plain text).
6. A JWT is generated containing the user's ID and email, signed with a secret key, and set to expire in 7 days.
7. The response includes the token and user data (without the password). The client stores this token and uses it for subsequent authenticated requests.

**Environment variable required:**
```
JWT_SECRET=your_super_secret_key_here_make_it_long_and_random
```
</details>

---

**18. Write a JWT authentication middleware for Express that extracts the token from the `Authorization` header, verifies it, and attaches the decoded user to `req.user`. Include proper error handling for missing, invalid, and expired tokens.**

**Starter Code:**

```javascript
const jwt = require("jsonwebtoken");
const User = require("../models/User");

const authMiddleware = async (req, res, next) => {
    // TODO: Extract token from Authorization header
    // TODO: Verify the token
    // TODO: Find the user in the database
    // TODO: Attach user to req.user
    // TODO: Call next()
    // TODO: Handle errors (missing token, invalid token, expired token)
};

module.exports = authMiddleware;
```

<details>
<summary>Solution</summary>

```javascript
const jwt = require("jsonwebtoken");
const User = require("../models/User");

const authMiddleware = async (req, res, next) => {
    try {
        // 1. Extract token from Authorization header
        const authHeader = req.headers.authorization;

        if (!authHeader || !authHeader.startsWith("Bearer ")) {
            return res.status(401).json({
                success: false,
                error: "Access denied. No token provided."
            });
        }

        // Remove "Bearer " prefix to get the actual token
        const token = authHeader.split(" ")[1];

        if (!token) {
            return res.status(401).json({
                success: false,
                error: "Access denied. Token is empty."
            });
        }

        // 2. Verify the token
        const decoded = jwt.verify(token, process.env.JWT_SECRET);

        // 3. Find the user in database (verify they still exist)
        const user = await User.findById(decoded.userId).select("-password");

        if (!user) {
            return res.status(401).json({
                success: false,
                error: "Token is valid but user no longer exists."
            });
        }

        // 4. Attach user to request object
        req.user = user;

        // 5. Proceed to the next middleware or route handler
        next();
    } catch (error) {
        // Handle specific JWT errors
        if (error.name === "TokenExpiredError") {
            return res.status(401).json({
                success: false,
                error: "Token has expired. Please log in again."
            });
        }

        if (error.name === "JsonWebTokenError") {
            return res.status(401).json({
                success: false,
                error: "Invalid token. Authentication failed."
            });
        }

        console.error("Auth middleware error:", error.message);
        res.status(500).json({
            success: false,
            error: "Server error during authentication."
        });
    }
};

module.exports = authMiddleware;
```

**Usage in routes:**

```javascript
const authMiddleware = require("../middleware/authMiddleware");

// Protect a single route
router.get("/profile", authMiddleware, (req, res) => {
    res.json({ success: true, user: req.user });
});

// Protect all routes in a router
router.use(authMiddleware); // Every route defined after this line is protected
router.get("/dashboard", getDashboard);
router.put("/settings", updateSettings);
```

**How the middleware works:**

1. The client sends a request with the header `Authorization: Bearer <token>`.
2. The middleware checks for the presence and correct format of the header.
3. `jwt.verify()` decodes the token and validates its signature and expiration. If the token was tampered with or has expired, it throws an error.
4. The middleware queries the database to confirm the user still exists. This handles the edge case where a user was deleted but their token has not yet expired.
5. The user object (without the password) is attached to `req.user`, making it available to all subsequent middleware and route handlers.
6. `next()` is called to pass control to the next function in the chain.
</details>

---

**19. Create an `AuthContext` in React that manages user authentication state, provides `login` and `logout` functions, and persists the authentication state across page refreshes using `localStorage`.**

**Starter Code:**

```jsx
import { createContext, useState, useEffect } from "react";

export const AuthContext = createContext();

export function AuthProvider({ children }) {
    // TODO: Initialize user and token state
    // TODO: Check localStorage on mount for existing auth data
    // TODO: Create login function (call API, store token, set user)
    // TODO: Create logout function (clear token, clear user)
    // TODO: Provide state and functions through context

    return (
        <AuthContext.Provider value={/* TODO */}>
            {children}
        </AuthContext.Provider>
    );
}
```

<details>
<summary>Solution</summary>

```jsx
import { createContext, useState, useEffect } from "react";
import axios from "axios";

export const AuthContext = createContext();

export function AuthProvider({ children }) {
    const [user, setUser] = useState(null);
    const [token, setToken] = useState(null);
    const [loading, setLoading] = useState(true);

    // On mount, check localStorage for existing auth data
    useEffect(() => {
        const storedToken = localStorage.getItem("token");
        const storedUser = localStorage.getItem("user");

        if (storedToken && storedUser) {
            setToken(storedToken);
            setUser(JSON.parse(storedUser));

            // Set default Authorization header for all future requests
            axios.defaults.headers.common["Authorization"] = `Bearer ${storedToken}`;
        }

        setLoading(false);
    }, []);

    // Login function
    const login = async (email, password) => {
        try {
            const response = await axios.post("/api/auth/login", {
                email,
                password
            });

            const { token: newToken, user: userData } = response.data;

            // Update state
            setToken(newToken);
            setUser(userData);

            // Persist to localStorage
            localStorage.setItem("token", newToken);
            localStorage.setItem("user", JSON.stringify(userData));

            // Set Authorization header for all future Axios requests
            axios.defaults.headers.common["Authorization"] = `Bearer ${newToken}`;

            return { success: true };
        } catch (error) {
            const message =
                error.response?.data?.error || "Login failed. Please try again.";
            return { success: false, error: message };
        }
    };

    // Logout function
    const logout = () => {
        // Clear state
        setUser(null);
        setToken(null);

        // Clear localStorage
        localStorage.removeItem("token");
        localStorage.removeItem("user");

        // Remove Authorization header
        delete axios.defaults.headers.common["Authorization"];
    };

    return (
        <AuthContext.Provider
            value={{
                user,
                token,
                loading,
                isAuthenticated: !!user,
                login,
                logout
            }}
        >
            {children}
        </AuthContext.Provider>
    );
}
```

**How to use the AuthProvider in your application:**

**main.jsx (or index.jsx):**

```jsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import { BrowserRouter } from "react-router-dom";
import { AuthProvider } from "./context/AuthContext";
import App from "./App";

createRoot(document.getElementById("root")).render(
    <StrictMode>
        <BrowserRouter>
            <AuthProvider>
                <App />
            </AuthProvider>
        </BrowserRouter>
    </StrictMode>
);
```

**Using context in a component (e.g., Navbar):**

```jsx
import { useContext } from "react";
import { AuthContext } from "../context/AuthContext";

function Navbar() {
    const { user, isAuthenticated, logout } = useContext(AuthContext);

    return (
        <nav>
            {isAuthenticated ? (
                <>
                    <span>Welcome, {user.name}</span>
                    <button onClick={logout}>Logout</button>
                </>
            ) : (
                <a href="/login">Login</a>
            )}
        </nav>
    );
}
```

**Key design decisions explained:**

1. **`loading` state** -- When the page loads, we need to check `localStorage` for an existing token before rendering. Without `loading`, the app would briefly show the login page before recognizing the user is already authenticated (a "flash" problem). Components like `PrivateRoute` check `loading` and show a spinner until the auth state is determined.

2. **`isAuthenticated` derived value** -- A boolean convenience value (`!!user`) that components can check directly instead of writing `user !== null` everywhere.

3. **Axios default headers** -- Setting `axios.defaults.headers.common["Authorization"]` ensures that every Axios request automatically includes the token. This eliminates the need to manually attach the token in every API call.

4. **Error handling in `login`** -- The function returns a result object (`{ success, error }`) instead of throwing, allowing the login form to display error messages without needing try/catch.
</details>

---

**20. Build a complete login flow that includes a React login form component, an Express login route, and JWT generation. The form should call the API, store the token, and redirect to the dashboard on success.**

**Starter Code:**

**Frontend -- LoginPage.jsx:**

```jsx
import { useState, useContext } from "react";
import { useNavigate } from "react-router-dom";
import { AuthContext } from "../context/AuthContext";

function LoginPage() {
    // TODO: Create state for email, password, error, and loading
    // TODO: Handle form submission (call login from context)
    // TODO: Redirect to dashboard on success
    // TODO: Display error messages

    return (
        <div>
            <h2>Login</h2>
            {/* TODO: Build the login form */}
        </div>
    );
}

export default LoginPage;
```

**Backend -- authRoutes.js:**

```javascript
const express = require("express");
const bcrypt = require("bcrypt");
const jwt = require("jsonwebtoken");
const User = require("../models/User");

const router = express.Router();

// POST /api/auth/login
router.post("/login", async (req, res) => {
    // TODO: Extract email and password from req.body
    // TODO: Find user by email (include password field)
    // TODO: Compare passwords with bcrypt
    // TODO: Generate JWT
    // TODO: Send response with token and user data
});

module.exports = router;
```

<details>
<summary>Solution</summary>

**Backend -- authRoutes.js:**

```javascript
const express = require("express");
const bcrypt = require("bcrypt");
const jwt = require("jsonwebtoken");
const User = require("../models/User");

const router = express.Router();

// POST /api/auth/login
router.post("/login", async (req, res) => {
    try {
        const { email, password } = req.body;

        // 1. Validate required fields
        if (!email || !password) {
            return res.status(400).json({
                success: false,
                error: "Email and password are required"
            });
        }

        // 2. Find user by email (explicitly include password field)
        const user = await User.findOne({ email }).select("+password");

        if (!user) {
            return res.status(401).json({
                success: false,
                error: "Invalid email or password"
            });
        }

        // 3. Compare submitted password with stored hash
        const isMatch = await bcrypt.compare(password, user.password);

        if (!isMatch) {
            return res.status(401).json({
                success: false,
                error: "Invalid email or password"
            });
        }

        // 4. Generate JWT
        const token = jwt.sign(
            { userId: user._id, email: user.email },
            process.env.JWT_SECRET,
            { expiresIn: "7d" }
        );

        // 5. Send response (exclude password)
        res.status(200).json({
            success: true,
            token,
            user: {
                id: user._id,
                name: user.name,
                email: user.email
            }
        });
    } catch (error) {
        console.error("Login error:", error.message);
        res.status(500).json({
            success: false,
            error: "Server error during login"
        });
    }
});

module.exports = router;
```

**Frontend -- LoginPage.jsx:**

```jsx
import { useState, useContext } from "react";
import { useNavigate, Link } from "react-router-dom";
import { AuthContext } from "../context/AuthContext";

function LoginPage() {
    const [email, setEmail] = useState("");
    const [password, setPassword] = useState("");
    const [error, setError] = useState("");
    const [loading, setLoading] = useState(false);

    const { login } = useContext(AuthContext);
    const navigate = useNavigate();

    const handleSubmit = async (e) => {
        e.preventDefault();
        setError("");

        // Basic client-side validation
        if (!email || !password) {
            setError("Please fill in all fields");
            return;
        }

        setLoading(true);

        const result = await login(email, password);

        if (result.success) {
            navigate("/dashboard");
        } else {
            setError(result.error);
            setLoading(false);
        }
    };

    return (
        <div style={{ maxWidth: "400px", margin: "100px auto", padding: "20px" }}>
            <h2>Login</h2>

            {error && (
                <div style={{
                    padding: "10px",
                    marginBottom: "15px",
                    backgroundColor: "#f8d7da",
                    color: "#721c24",
                    borderRadius: "4px"
                }}>
                    {error}
                </div>
            )}

            <form onSubmit={handleSubmit}>
                <div style={{ marginBottom: "15px" }}>
                    <label htmlFor="email">Email</label>
                    <input
                        id="email"
                        type="email"
                        value={email}
                        onChange={(e) => setEmail(e.target.value)}
                        placeholder="Enter your email"
                        disabled={loading}
                        style={{
                            width: "100%",
                            padding: "8px",
                            marginTop: "5px",
                            boxSizing: "border-box"
                        }}
                    />
                </div>

                <div style={{ marginBottom: "15px" }}>
                    <label htmlFor="password">Password</label>
                    <input
                        id="password"
                        type="password"
                        value={password}
                        onChange={(e) => setPassword(e.target.value)}
                        placeholder="Enter your password"
                        disabled={loading}
                        style={{
                            width: "100%",
                            padding: "8px",
                            marginTop: "5px",
                            boxSizing: "border-box"
                        }}
                    />
                </div>

                <button
                    type="submit"
                    disabled={loading}
                    style={{
                        width: "100%",
                        padding: "10px",
                        backgroundColor: loading ? "#ccc" : "#007bff",
                        color: "white",
                        border: "none",
                        borderRadius: "4px",
                        cursor: loading ? "not-allowed" : "pointer"
                    }}
                >
                    {loading ? "Logging in..." : "Login"}
                </button>
            </form>

            <p style={{ marginTop: "15px", textAlign: "center" }}>
                Don't have an account? <Link to="/register">Register</Link>
            </p>
        </div>
    );
}

export default LoginPage;
```

**How the complete login flow works end-to-end:**

1. **User fills the form:** The user enters their email and password in the React form. Each input is controlled by React state (`email`, `password`).

2. **Form submission:** When the form is submitted, `handleSubmit` is called. It prevents the default browser form behavior with `e.preventDefault()`, clears any previous error messages, and validates that both fields are filled.

3. **Context login function:** The `login()` function from `AuthContext` is called with the email and password. Inside this function, an Axios POST request is sent to `/api/auth/login`.

4. **Server receives the request:** The Express route handler extracts `email` and `password` from `req.body`.

5. **User lookup:** The server queries MongoDB for a user with the submitted email, using `.select("+password")` to include the password field (which is excluded by default in the schema).

6. **Password comparison:** `bcrypt.compare()` hashes the submitted password with the same salt used during registration and compares it to the stored hash. This is a one-way comparison -- the stored hash is never decrypted.

7. **Token generation:** If the password matches, the server creates a JWT containing the user's ID and email, signed with the server's secret key and set to expire in 7 days.

8. **Response:** The server sends back the token and user data (without the password).

9. **Client stores the token:** The `login()` function in AuthContext stores the token and user data in `localStorage` and sets the Axios default `Authorization` header for future requests.

10. **Redirect:** Back in `LoginPage`, if `login()` returned `{ success: true }`, `navigate("/dashboard")` redirects the user to the dashboard.

11. **Subsequent requests:** All future API calls automatically include the `Authorization: Bearer <token>` header. The `authMiddleware` on the server verifies this token before granting access to protected routes.

**Security notes:**
- The error message "Invalid email or password" is intentionally vague. Telling the user whether the email or password was wrong would let attackers enumerate valid email addresses.
- The `loading` state disables the form during the API call, preventing duplicate submissions.
- The `type="password"` attribute on the password input hides the characters as the user types.
</details>

---

*End of Week 33 Practice Questions.*
