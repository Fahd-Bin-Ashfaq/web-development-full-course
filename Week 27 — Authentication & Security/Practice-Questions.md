# Week 27: Authentication & Security - Practice Questions

**Total Questions: 30**

| Section | Topic                                          | Questions |
|---------|------------------------------------------------|-----------|
| A       | Multiple Choice Questions                      | 10        |
| B       | Short Answer Questions                         | 5         |
| C       | Coding Exercises                               | 5         |
| D       | Backend Phase Review (Weeks 22-27)             | 10        |

---

## Section A: Multiple Choice Questions (10)

**Q1.** What is the difference between authentication and authorization?

- A) Authentication checks permissions; authorization verifies identity
- B) Authentication verifies identity; authorization checks permissions
- C) They are the same thing
- D) Authentication is for admins; authorization is for regular users

<details>
<summary>Answer</summary>

**B) Authentication verifies identity; authorization checks permissions**

Authentication answers the question "Who are you?" by verifying credentials (email/password, token). Authorization answers "What are you allowed to do?" by checking the user's role or permissions. Authentication always happens first; authorization happens after the identity is confirmed.
</details>

---

**Q2.** Why should passwords never be stored as plain text in a database?

- A) Plain text takes up more storage space
- B) Plain text passwords are slower to read
- C) If the database is breached, all passwords are immediately exposed
- D) Plain text cannot be compared with user input

<details>
<summary>Answer</summary>

**C) If the database is breached, all passwords are immediately exposed**

If an attacker gains access to a database that stores plain text passwords, every user's password is immediately readable. With hashed passwords, the attacker sees random strings that cannot be reversed into the original passwords. Hashing is a one-way process.
</details>

---

**Q3.** What does bcrypt's "salt" do?

- A) Encrypts the password so it can be decrypted later
- B) Adds random data to the password before hashing, making identical passwords produce different hashes
- C) Compresses the password to save storage space
- D) Converts the password to Base64 encoding

<details>
<summary>Answer</summary>

**B) Adds random data to the password before hashing, making identical passwords produce different hashes**

A salt is random data that is combined with the password before the hashing algorithm runs. Even if two users have the same password ("password123"), their hashes will be different because each gets a unique salt. This prevents attackers from using pre-computed hash tables (rainbow tables) to crack passwords.
</details>

---

**Q4.** A JWT consists of three parts. What are they?

- A) Username, Password, Token
- B) Header, Payload, Signature
- C) Key, Value, Hash
- D) Encrypt, Decrypt, Verify

<details>
<summary>Answer</summary>

**B) Header, Payload, Signature**

A JWT has three parts separated by dots: `header.payload.signature`. The **header** specifies the algorithm and token type. The **payload** contains the claims (user data like userId, role, expiration). The **signature** is created using the header, payload, and a secret key -- it ensures the token has not been tampered with.
</details>

---

**Q5.** What HTTP status code should be returned when an authenticated user tries to access a resource they do not have permission for?

- A) `401 Unauthorized`
- B) `403 Forbidden`
- C) `404 Not Found`
- D) `400 Bad Request`

<details>
<summary>Answer</summary>

**B) `403 Forbidden`**

`403 Forbidden` means the server knows who the user is (authentication succeeded) but the user does not have the required permissions (authorization failed). For example, a regular user trying to access an admin-only endpoint. `401 Unauthorized` is used when the user is not authenticated at all (no token or invalid token).
</details>

---

**Q6.** Which of the following should NEVER be included in a JWT payload?

- A) User ID
- B) User email
- C) User role
- D) User password

<details>
<summary>Answer</summary>

**D) User password**

The JWT payload is Base64-encoded, **not encrypted**. Anyone who obtains the token can decode and read the payload. Therefore, sensitive information like passwords, credit card numbers, or secret keys must never be placed in the payload. Only non-sensitive identifiers (userId, email, role) and metadata (issued at, expiration) should be included.
</details>

---

**Q7.** What does `bcrypt.compare()` do internally?

- A) Decrypts the stored hash back to plain text and compares the strings
- B) Hashes the input password with the same salt from the stored hash and checks if the results match
- C) Converts both passwords to Base64 and compares them
- D) Sends both passwords to an external service for verification

<details>
<summary>Answer</summary>

**B) Hashes the input password with the same salt from the stored hash and checks if the results match**

bcrypt hashes are not reversible -- they cannot be decrypted. Instead, `bcrypt.compare()` extracts the salt and cost factor from the stored hash string, hashes the input password using those same parameters, and then checks if the resulting hash matches the stored hash. If they match, the passwords are the same.
</details>

---

**Q8.** What is the purpose of the `expiresIn` option when generating a JWT?

- A) It sets how long the user's session lasts on the server
- B) It determines when the token becomes invalid, forcing the user to log in again
- C) It sets the maximum number of requests the token can be used for
- D) It controls how long the token takes to generate

<details>
<summary>Answer</summary>

**B) It determines when the token becomes invalid, forcing the user to log in again**

The `expiresIn` option (e.g., `"1h"`, `"24h"`, `"7d"`) adds an `exp` (expiration) claim to the JWT payload. When `jwt.verify()` is called, it checks the current time against the expiration time. If the token has expired, verification fails with a `TokenExpiredError`. This limits the damage if a token is stolen.
</details>

---

**Q9.** What does the `express-rate-limit` middleware protect against?

- A) SQL injection attacks
- B) Brute-force login attempts and denial-of-service attacks
- C) Cross-site scripting (XSS)
- D) Man-in-the-middle attacks

<details>
<summary>Answer</summary>

**B) Brute-force login attempts and denial-of-service attacks**

Rate limiting restricts the number of requests a client (identified by IP address) can make within a time window. On a login endpoint, it prevents attackers from trying thousands of password combinations. On general routes, it prevents a single client from overwhelming the server with excessive requests.
</details>

---

**Q10.** Why should login error messages be generic (e.g., "Invalid email or password") rather than specific?

- A) Specific messages are harder to code
- B) Generic messages prevent attackers from discovering which emails are registered in the system
- C) Generic messages load faster
- D) Specific messages violate HTTP standards

<details>
<summary>Answer</summary>

**B) Generic messages prevent attackers from discovering which emails are registered in the system**

If the server returns "Email not found" for a wrong email and "Password is incorrect" for a wrong password, an attacker can use the different messages to enumerate which email addresses are registered. With a generic message like "Invalid email or password," the attacker cannot determine whether the email exists or the password is wrong.
</details>

---

## Section B: Short Answer Questions (5)

**Q11.** Explain the complete JWT authentication flow from login to accessing a protected route. Include what the client and server do at each step.

<details>
<summary>Answer</summary>

**Step 1 -- Login Request:** The client sends a POST request to `/api/auth/login` with the user's email and password in the request body.

**Step 2 -- Server Verifies Credentials:** The server finds the user by email in the database, then uses `bcrypt.compare()` to check if the submitted password matches the stored hash. If either the email is not found or the password does not match, the server returns `401` with a generic error.

**Step 3 -- Server Generates JWT:** If credentials are valid, the server creates a JWT using `jwt.sign()` with the user's ID, email, and role in the payload, signed with a secret key and an expiration time.

**Step 4 -- Client Stores Token:** The client receives the JWT in the response and stores it (typically in localStorage, sessionStorage, or an HTTP-only cookie).

**Step 5 -- Client Sends Token with Requests:** For every subsequent request to a protected route, the client includes the token in the `Authorization` header: `Authorization: Bearer <token>`.

**Step 6 -- Server Verifies Token:** The authentication middleware extracts the token from the header, verifies it using `jwt.verify()` with the same secret key, and attaches the decoded payload (userId, role) to `req.user`. If verification fails, the server returns `401`.

**Step 7 -- Route Handler Executes:** With `req.user` set, the route handler can identify the user and return the appropriate data.
</details>

---

**Q12.** What is the difference between hashing and encryption? Why is hashing preferred for passwords?

<details>
<summary>Answer</summary>

**Hashing** is a one-way process. Once data is hashed, it cannot be converted back to the original. The same input always produces the same output (deterministic), but the output cannot be reversed.

**Encryption** is a two-way process. Data is encrypted with a key and can be decrypted back to the original using the same key (symmetric) or a paired key (asymmetric).

```
Hashing:    "password123"  -->  "$2b$10$abc..."  -->  CANNOT go back
Encryption: "password123"  -->  "x7f9k2m..."     -->  CAN go back with the key
```

**Hashing is preferred for passwords** because:
1. The server never needs to know the original password -- it only needs to verify that a submitted password produces the same hash.
2. If the database is breached, hashed passwords cannot be reversed.
3. With encryption, anyone who obtains the encryption key can decrypt all passwords. With hashing, there is no key to steal.
4. bcrypt adds a unique salt to each password, so even identical passwords produce different hashes, preventing rainbow table attacks.
</details>

---

**Q13.** Explain how role-based access control (RBAC) works in an Express application. How do the `authenticate` and `authorize` middleware work together?

<details>
<summary>Answer</summary>

Role-based access control assigns each user a role (such as "user", "admin", or "moderator") and restricts access to routes based on that role.

**The `authenticate` middleware** runs first and handles authentication. It extracts the JWT from the `Authorization` header, verifies it, and attaches the decoded payload (including the user's role) to `req.user`. If the token is missing or invalid, it returns `401`.

**The `authorize` middleware** runs after `authenticate` and handles authorization. It receives a list of allowed roles as arguments and checks if `req.user.role` is in that list. If the user's role is not allowed, it returns `403 Forbidden`. If it is allowed, it calls `next()`.

```javascript
// The middleware chain in action:
app.delete("/api/users/:id",
    authenticate,           // Step 1: Is the user logged in? (sets req.user)
    authorize("admin"),     // Step 2: Is the user an admin? (checks req.user.role)
    deleteUserHandler       // Step 3: Execute the delete logic
);
```

This two-step approach keeps authentication and authorization separate and reusable. The `authenticate` middleware is used on all protected routes, while `authorize` is only added where specific roles are required.
</details>

---

**Q14.** What are the security risks of using a weak or short JWT secret key? What makes a good secret key?

<details>
<summary>Answer</summary>

**Risks of a weak secret key:**

1. **Token forgery:** If the secret is short or predictable (like "secret" or "123456"), an attacker can guess or brute-force it. Once they have the secret, they can create their own valid JWT tokens with any payload (userId, role: "admin") and gain unauthorized access.

2. **Token tampering:** With the secret key, an attacker can modify an existing token's payload (changing their role from "user" to "admin") and re-sign it with a valid signature.

**A good secret key should be:**
- At least 32 characters long (64+ recommended)
- Randomly generated (not a dictionary word or common phrase)
- Stored in environment variables, never hardcoded in source code
- Different for each environment (development, staging, production)

**Example of generating a strong key:**
```bash
node -e "console.log(require('crypto').randomBytes(64).toString('hex'))"
```

This produces a 128-character random hexadecimal string that is practically impossible to guess or brute-force.
</details>

---

**Q15.** List and explain five security best practices for a production Express API. For each, explain what attack it prevents.

<details>
<summary>Answer</summary>

1. **Helmet** -- Sets security-related HTTP headers. Prevents: XSS attacks (via `X-XSS-Protection`), clickjacking (via `X-Frame-Options`), MIME type sniffing (via `X-Content-Type-Options`).

2. **Rate Limiting (express-rate-limit)** -- Limits the number of requests per IP address within a time window. Prevents: brute-force password attacks on login endpoints and denial-of-service (DoS) attacks that overwhelm the server.

3. **CORS Configuration** -- Restricts which domains can make requests to the API. Prevents: unauthorized websites from making requests to your API on behalf of users, which could lead to data theft via cross-site request forgery.

4. **Input Sanitization (express-mongo-sanitize, xss-clean)** -- Removes dangerous characters from user input. Prevents: NoSQL injection (where attackers use `$gt`, `$ne` operators to bypass authentication) and cross-site scripting (where attackers inject `<script>` tags to execute code in other users' browsers).

5. **Environment Variables (dotenv)** -- Stores sensitive configuration (JWT secret, database passwords, API keys) outside the source code. Prevents: credential exposure if the source code is leaked or the repository is public. Secrets in `.env` files are excluded from version control via `.gitignore`.
</details>

---

## Section C: Coding Exercises (5)

**Q16.** Write a function that takes a plain text password, hashes it with bcrypt (10 salt rounds), and then demonstrates verifying the password by comparing the correct password and a wrong password against the hash.

<details>
<summary>Answer</summary>

```javascript
const bcrypt = require("bcrypt");

async function demonstrateHashing() {
    const plainPassword = "mySecretPassword123";
    const saltRounds = 10;

    // Step 1: Hash the password
    console.log("Original password:", plainPassword);

    const hashedPassword = await bcrypt.hash(plainPassword, saltRounds);
    console.log("Hashed password:", hashedPassword);

    // Step 2: Compare with correct password
    const correctMatch = await bcrypt.compare("mySecretPassword123", hashedPassword);
    console.log("Correct password match:", correctMatch); // true

    // Step 3: Compare with wrong password
    const wrongMatch = await bcrypt.compare("wrongPassword", hashedPassword);
    console.log("Wrong password match:", wrongMatch); // false

    // Step 4: Show that same password produces different hashes (due to salt)
    const hash1 = await bcrypt.hash("samePassword", saltRounds);
    const hash2 = await bcrypt.hash("samePassword", saltRounds);
    console.log("Hash 1:", hash1);
    console.log("Hash 2:", hash2);
    console.log("Same password, same hash?", hash1 === hash2); // false (different salts)

    // But both still match the original password
    console.log("Hash 1 matches:", await bcrypt.compare("samePassword", hash1)); // true
    console.log("Hash 2 matches:", await bcrypt.compare("samePassword", hash2)); // true
}

demonstrateHashing();
```

**Expected output:**
```
Original password: mySecretPassword123
Hashed password: $2b$10$N9qo8uLOickgx2ZMRZoMye...
Correct password match: true
Wrong password match: false
Hash 1: $2b$10$abc...
Hash 2: $2b$10$xyz...
Same password, same hash? false
Hash 1 matches: true
Hash 2 matches: true
```
</details>

---

**Q17.** Write a complete JWT utility module (`jwtUtils.js`) that exports two functions: `generateToken(user)` that creates a JWT with userId, email, and role claims that expires in 24 hours, and `verifyToken(token)` that verifies and returns the decoded payload or throws an error.

<details>
<summary>Answer</summary>

```javascript
// jwtUtils.js
const jwt = require("jsonwebtoken");

const JWT_SECRET = process.env.JWT_SECRET || "dev-secret-key-change-in-production";
const JWT_EXPIRES_IN = "24h";

/**
 * Generate a JWT for a user
 * @param {Object} user - User object with id, email, role
 * @returns {string} JWT token
 */
function generateToken(user) {
    if (!user || !user.id || !user.email || !user.role) {
        throw new Error("User must have id, email, and role properties");
    }

    const payload = {
        userId: user.id,
        email: user.email,
        role: user.role
    };

    return jwt.sign(payload, JWT_SECRET, { expiresIn: JWT_EXPIRES_IN });
}

/**
 * Verify a JWT and return the decoded payload
 * @param {string} token - JWT token string
 * @returns {Object} Decoded payload
 * @throws {Error} If token is invalid or expired
 */
function verifyToken(token) {
    if (!token) {
        throw new Error("Token is required");
    }

    try {
        const decoded = jwt.verify(token, JWT_SECRET);
        return decoded;
    } catch (err) {
        if (err.name === "TokenExpiredError") {
            throw new Error("Token has expired");
        } else if (err.name === "JsonWebTokenError") {
            throw new Error("Token is invalid");
        }
        throw err;
    }
}

module.exports = { generateToken, verifyToken };
```

**Usage example (test.js):**

```javascript
const { generateToken, verifyToken } = require("./jwtUtils");

// Generate a token
const user = { id: 1, email: "fahad@example.com", role: "admin" };
const token = generateToken(user);
console.log("Token:", token);

// Verify a valid token
const decoded = verifyToken(token);
console.log("Decoded:", decoded);
// { userId: 1, email: "fahad@example.com", role: "admin", iat: ..., exp: ... }

// Verify an invalid token
try {
    verifyToken("invalid.token.here");
} catch (err) {
    console.log("Error:", err.message); // "Token is invalid"
}
```
</details>

---

**Q18.** Create an `authenticate` middleware that extracts the JWT from the Authorization header, verifies it, and attaches the user data to `req.user`. Handle three error cases: missing token, expired token, and invalid token. Each should return the appropriate error message and status code.

<details>
<summary>Answer</summary>

```javascript
// middleware/authenticate.js
const jwt = require("jsonwebtoken");

const JWT_SECRET = process.env.JWT_SECRET || "dev-secret-key";

function authenticate(req, res, next) {
    // 1. Get the Authorization header
    const authHeader = req.headers["authorization"];

    // 2. Check if header exists
    if (!authHeader) {
        return res.status(401).json({
            success: false,
            error: "Access denied. No authorization header provided."
        });
    }

    // 3. Check if header has correct format (Bearer <token>)
    if (!authHeader.startsWith("Bearer ")) {
        return res.status(401).json({
            success: false,
            error: "Invalid authorization format. Use: Bearer <token>"
        });
    }

    // 4. Extract the token
    const token = authHeader.split(" ")[1];

    if (!token || token === "undefined" || token === "null") {
        return res.status(401).json({
            success: false,
            error: "Access denied. Token is empty."
        });
    }

    // 5. Verify the token
    try {
        const decoded = jwt.verify(token, JWT_SECRET);

        // 6. Attach user data to request
        req.user = {
            userId: decoded.userId,
            email: decoded.email,
            role: decoded.role
        };

        // 7. Continue to next middleware or route handler
        next();

    } catch (err) {
        // Handle specific JWT errors
        if (err.name === "TokenExpiredError") {
            return res.status(401).json({
                success: false,
                error: "Token has expired. Please log in again."
            });
        }

        if (err.name === "JsonWebTokenError") {
            return res.status(401).json({
                success: false,
                error: "Invalid token. Please log in again."
            });
        }

        // Unexpected error
        return res.status(500).json({
            success: false,
            error: "Authentication failed due to a server error."
        });
    }
}

module.exports = authenticate;
```

**Usage in Express app:**

```javascript
const express = require("express");
const authenticate = require("./middleware/authenticate");

const app = express();
app.use(express.json());

// Public route
app.get("/api/public", (req, res) => {
    res.json({ message: "This is public" });
});

// Protected route
app.get("/api/profile", authenticate, (req, res) => {
    res.json({
        success: true,
        message: "You are authenticated",
        user: req.user
    });
});

app.listen(3000);
```

**Test scenarios:**
```
1. No header:         --> 401 "Access denied. No authorization header provided."
2. Wrong format:      --> 401 "Invalid authorization format. Use: Bearer <token>"
3. Expired token:     --> 401 "Token has expired. Please log in again."
4. Tampered token:    --> 401 "Invalid token. Please log in again."
5. Valid token:       --> 200 { user: { userId, email, role } }
```
</details>

---

**Q19.** Build a set of protected routes for a user profile system. Include: GET `/api/profile` (returns the logged-in user's data), PUT `/api/profile` (updates the user's name), and DELETE `/api/profile` (deletes the user's account). All routes must require authentication. Use the authenticate middleware from Q18.

<details>
<summary>Answer</summary>

```javascript
const express = require("express");
const bcrypt = require("bcrypt");
const jwt = require("jsonwebtoken");

const app = express();
app.use(express.json());

const JWT_SECRET = process.env.JWT_SECRET || "dev-secret-key";

// ---------- IN-MEMORY DATA ----------
let users = [
    {
        id: 1,
        name: "Fahad Ahmed",
        email: "fahad@example.com",
        password: "$2b$10$examplehashedpassword", // pre-hashed
        role: "user"
    },
    {
        id: 2,
        name: "Sara Khan",
        email: "sara@example.com",
        password: "$2b$10$examplehashedpassword2",
        role: "user"
    }
];

// ---------- AUTHENTICATE MIDDLEWARE ----------
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

// ---------- PROFILE ROUTES ----------

// GET /api/profile - Get current user's profile
app.get("/api/profile", authenticate, (req, res) => {
    const user = users.find(u => u.id === req.user.userId);

    if (!user) {
        return res.status(404).json({ success: false, error: "User not found" });
    }

    // Return user data WITHOUT the password
    res.status(200).json({
        success: true,
        data: {
            id: user.id,
            name: user.name,
            email: user.email,
            role: user.role
        }
    });
});

// PUT /api/profile - Update current user's name
app.put("/api/profile", authenticate, (req, res) => {
    const user = users.find(u => u.id === req.user.userId);

    if (!user) {
        return res.status(404).json({ success: false, error: "User not found" });
    }

    const { name } = req.body;

    if (!name || name.trim().length < 2) {
        return res.status(400).json({
            success: false,
            error: "Name is required and must be at least 2 characters"
        });
    }

    user.name = name.trim();

    res.status(200).json({
        success: true,
        message: "Profile updated successfully",
        data: {
            id: user.id,
            name: user.name,
            email: user.email,
            role: user.role
        }
    });
});

// DELETE /api/profile - Delete current user's account
app.delete("/api/profile", authenticate, (req, res) => {
    const index = users.findIndex(u => u.id === req.user.userId);

    if (index === -1) {
        return res.status(404).json({ success: false, error: "User not found" });
    }

    users.splice(index, 1);

    res.status(200).json({
        success: true,
        message: "Account deleted successfully"
    });
});

// ---------- START ----------
app.listen(3000, () => {
    console.log("Profile API running on http://localhost:3000");
});
```

**Key security principles demonstrated:**
1. All routes use `authenticate` middleware -- no profile route is accessible without a valid JWT.
2. Users can only access their own data -- `req.user.userId` from the JWT determines which user's data to return.
3. Passwords are never included in responses.
4. The DELETE route removes the user's own account only -- they cannot delete other users.
</details>

---

**Q20.** Build a complete authentication system with registration, login, an authorize middleware for role-based access, and a protected admin route. Include proper password hashing, JWT generation, and error handling.

<details>
<summary>Answer</summary>

```javascript
const express = require("express");
const bcrypt = require("bcrypt");
const jwt = require("jsonwebtoken");

const app = express();
app.use(express.json());

const JWT_SECRET = process.env.JWT_SECRET || "dev-secret-key-change-me";
const JWT_EXPIRES_IN = "24h";
const SALT_ROUNDS = 10;

// ---------- DATA STORE ----------
let users = [];
let nextId = 1;

// ---------- HELPER ----------
function generateToken(user) {
    return jwt.sign(
        { userId: user.id, email: user.email, role: user.role },
        JWT_SECRET,
        { expiresIn: JWT_EXPIRES_IN }
    );
}

// ---------- AUTHENTICATE MIDDLEWARE ----------
function authenticate(req, res, next) {
    const authHeader = req.headers["authorization"];

    if (!authHeader || !authHeader.startsWith("Bearer ")) {
        return res.status(401).json({
            success: false,
            error: "Access denied. No token provided."
        });
    }

    try {
        const token = authHeader.split(" ")[1];
        req.user = jwt.verify(token, JWT_SECRET);
        next();
    } catch (err) {
        const message = err.name === "TokenExpiredError"
            ? "Token expired. Please log in again."
            : "Invalid token.";
        return res.status(401).json({ success: false, error: message });
    }
}

// ---------- AUTHORIZE MIDDLEWARE ----------
function authorize(...allowedRoles) {
    return (req, res, next) => {
        if (!allowedRoles.includes(req.user.role)) {
            return res.status(403).json({
                success: false,
                error: `Access denied. Required role: ${allowedRoles.join(" or ")}`
            });
        }
        next();
    };
}

// ========== ROUTES ==========

// POST /api/auth/register
app.post("/api/auth/register", async (req, res) => {
    try {
        const { name, email, password, role } = req.body;

        // Validation
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

        // Check duplicate email
        if (users.find(u => u.email === email)) {
            return res.status(400).json({
                success: false,
                error: "Email is already registered"
            });
        }

        // Hash password and create user
        const hashedPassword = await bcrypt.hash(password, SALT_ROUNDS);

        const user = {
            id: nextId++,
            name,
            email,
            password: hashedPassword,
            role: role === "admin" ? "admin" : "user" // Only allow admin if explicitly set
        };
        users.push(user);

        const token = generateToken(user);

        res.status(201).json({
            success: true,
            token,
            user: { id: user.id, name: user.name, email: user.email, role: user.role }
        });

    } catch (err) {
        res.status(500).json({ success: false, error: "Server error during registration" });
    }
});

// POST /api/auth/login
app.post("/api/auth/login", async (req, res) => {
    try {
        const { email, password } = req.body;

        if (!email || !password) {
            return res.status(400).json({
                success: false,
                error: "Email and password are required"
            });
        }

        const user = users.find(u => u.email === email);

        if (!user || !(await bcrypt.compare(password, user.password))) {
            return res.status(401).json({
                success: false,
                error: "Invalid email or password"
            });
        }

        const token = generateToken(user);

        res.status(200).json({
            success: true,
            token,
            user: { id: user.id, name: user.name, email: user.email, role: user.role }
        });

    } catch (err) {
        res.status(500).json({ success: false, error: "Server error during login" });
    }
});

// GET /api/profile (any authenticated user)
app.get("/api/profile", authenticate, (req, res) => {
    const user = users.find(u => u.id === req.user.userId);

    if (!user) {
        return res.status(404).json({ success: false, error: "User not found" });
    }

    res.json({
        success: true,
        data: { id: user.id, name: user.name, email: user.email, role: user.role }
    });
});

// GET /api/admin/users (admin only)
app.get("/api/admin/users",
    authenticate,
    authorize("admin"),
    (req, res) => {
        const safeUsers = users.map(u => ({
            id: u.id,
            name: u.name,
            email: u.email,
            role: u.role
        }));

        res.json({ success: true, count: safeUsers.length, data: safeUsers });
    }
);

// DELETE /api/admin/users/:id (admin only)
app.delete("/api/admin/users/:id",
    authenticate,
    authorize("admin"),
    (req, res) => {
        const targetId = parseInt(req.params.id);

        // Prevent admin from deleting themselves
        if (targetId === req.user.userId) {
            return res.status(400).json({
                success: false,
                error: "You cannot delete your own account from the admin panel"
            });
        }

        const index = users.findIndex(u => u.id === targetId);
        if (index === -1) {
            return res.status(404).json({ success: false, error: "User not found" });
        }

        const deletedUser = users[index];
        users.splice(index, 1);

        res.json({
            success: true,
            message: `User ${deletedUser.email} deleted successfully`
        });
    }
);

// ========== ERROR HANDLER ==========
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).json({ success: false, error: "Internal server error" });
});

app.listen(3000, () => console.log("Auth API running on http://localhost:3000"));
```

**Testing sequence:**
```
1. Register: POST /api/auth/register
   Body: { "name": "Fahad", "email": "fahad@mail.com", "password": "pass123", "role": "admin" }
   Expect: 201 + token

2. Login: POST /api/auth/login
   Body: { "email": "fahad@mail.com", "password": "pass123" }
   Expect: 200 + token

3. Profile: GET /api/profile
   Headers: Authorization: Bearer <token>
   Expect: 200 + user data

4. Admin route: GET /api/admin/users
   Headers: Authorization: Bearer <admin-token>
   Expect: 200 + list of users

5. Admin route with user token: GET /api/admin/users
   Headers: Authorization: Bearer <user-token>
   Expect: 403 Forbidden
```
</details>

---

## Section D: Backend Phase Review (Weeks 22-27) (10)

**Q21.** What is Node.js, and how does it differ from running JavaScript in a browser?

<details>
<summary>Answer</summary>

Node.js is a JavaScript runtime environment built on Chrome's V8 engine that allows JavaScript to run outside the browser, on a server. In the browser, JavaScript has access to the DOM, window object, and browser APIs (localStorage, fetch). In Node.js, JavaScript has access to server-side capabilities: the file system (`fs`), network operations (`http`), operating system information (`os`), and environment variables. Node.js does not have a DOM or `window` object. It uses `global` instead of `window` and provides `require()` / `import` for modules.
</details>

---

**Q22.** What is npm, and what is the difference between `dependencies` and `devDependencies` in `package.json`?

<details>
<summary>Answer</summary>

npm (Node Package Manager) is the default package manager for Node.js. It allows you to install, manage, and share reusable JavaScript packages.

**`dependencies`** are packages required for the application to run in production. They are installed with `npm install <package>`. Examples: `express`, `bcrypt`, `jsonwebtoken`.

**`devDependencies`** are packages only needed during development (testing, linting, building). They are installed with `npm install --save-dev <package>`. Examples: `nodemon`, `jest`, `eslint`. They are not installed when `NODE_ENV=production`.
</details>

---

**Q23.** What is Express.js, and why is it used instead of Node.js's built-in `http` module?

<details>
<summary>Answer</summary>

Express.js is a minimal and flexible web framework for Node.js that simplifies building web servers and APIs. While Node.js's built-in `http` module can create a server, it requires manual handling of URL parsing, request methods, body parsing, and response formatting.

Express provides: a clean routing system (`app.get()`, `app.post()`), middleware support for request processing, built-in body parsing, static file serving, error handling, and a massive ecosystem of third-party middleware. What takes 30+ lines with the `http` module often takes 5 lines with Express.
</details>

---

**Q24.** Explain the purpose of middleware in Express. Give three examples of different types of middleware.

<details>
<summary>Answer</summary>

Middleware functions sit between the incoming request and the final route handler. They have access to `req`, `res`, and `next()`, and can inspect, modify, or reject requests before they reach the route.

Three types:
1. **Built-in middleware:** `express.json()` -- parses JSON request bodies and makes them available on `req.body`.
2. **Custom middleware:** An authentication middleware that checks for a JWT in the Authorization header and rejects requests without a valid token.
3. **Third-party middleware:** `cors` -- adds Cross-Origin Resource Sharing headers to responses, allowing frontend applications on different domains to call the API.

Middleware runs in the order it is registered, and each must call `next()` to pass control forward or send a response to end the chain.
</details>

---

**Q25.** What does REST stand for, and what are the four main HTTP methods used in a RESTful API? Map each to a CRUD operation.

<details>
<summary>Answer</summary>

REST stands for **Representational State Transfer**. It is an architectural style for designing APIs that uses standard HTTP methods and structured URLs to manage resources.

| HTTP Method | CRUD Operation | Example                              |
|-------------|----------------|---------------------------------------|
| `GET`       | **Read**       | `GET /api/users` -- retrieve all users |
| `POST`      | **Create**     | `POST /api/users` -- create a new user |
| `PUT`       | **Update**     | `PUT /api/users/5` -- update user 5    |
| `DELETE`    | **Delete**     | `DELETE /api/users/5` -- delete user 5 |

RESTful URLs use plural nouns (not verbs), and the HTTP method determines the action. The same URL `/api/users` can handle multiple operations depending on the method used.
</details>

---

**Q26.** How does Joi validation work, and why is it better than manual validation with `if` statements?

<details>
<summary>Answer</summary>

Joi lets you define a **schema** -- a set of rules for your data -- and validate incoming data against it. You call `schema.validate(data)` and get back either the validated data or an error object with detailed messages.

Joi is better than manual validation because:
1. **Less code:** A schema with 5 rules replaces 10-15 `if` statements.
2. **Readability:** Rules are declarative (`.min(3).max(100).required()`) and self-documenting.
3. **Reusability:** The same schema can be used for both POST and PUT routes via middleware.
4. **Custom messages:** Each rule can have a custom error message via `.messages()`.
5. **Sanitization:** The `stripUnknown` option removes unexpected fields automatically.
6. **Multiple errors:** With `abortEarly: false`, all validation errors are returned at once instead of one at a time.
</details>

---

**Q27.** Explain the MVC pattern and the responsibility of each layer. Why is it important for larger applications?

<details>
<summary>Answer</summary>

MVC separates an application into three layers:

**Model** -- Handles data and data operations. Defines the data structure and provides functions to read, write, update, and delete data. In a database application, models define schemas and execute queries.

**Controller** -- Handles request logic. Receives the HTTP request, calls the appropriate model functions, and sends back the response. Controllers contain the business logic.

**Routes (View in traditional MVC)** -- Maps URLs to controller functions. In an API, the "View" layer is the JSON response; in a full-stack app, it would be HTML templates.

MVC is important for larger applications because it enforces separation of concerns -- each file has one responsibility. This makes the codebase easier to navigate, easier to test (you can test controllers without a database), and easier for teams to work on simultaneously (one developer works on models while another works on controllers).
</details>

---

**Q28.** What is the difference between `express.json()` and `express.urlencoded()`? When would you use each?

<details>
<summary>Answer</summary>

**`express.json()`** parses request bodies with `Content-Type: application/json`. This is the format used by most API clients (Postman, React apps using `fetch`, mobile apps). The parsed data is available on `req.body` as a JavaScript object.

**`express.urlencoded({ extended: true })`** parses request bodies with `Content-Type: application/x-www-form-urlencoded`. This is the format used by traditional HTML forms when submitted. The data arrives as key-value pairs like `name=Fahad&email=fahad@mail.com`.

In a modern API that serves a React or mobile frontend, `express.json()` is almost always sufficient. Add `express.urlencoded()` if your API also accepts submissions from traditional HTML forms. Most developers include both by default.
</details>

---

**Q29.** What is the purpose of the `express-rate-limit` package, and how would you configure different rate limits for general API routes vs authentication routes?

<details>
<summary>Answer</summary>

`express-rate-limit` restricts how many requests an IP address can make within a time window. It protects against brute-force attacks and denial-of-service.

Authentication routes need stricter limits because attackers may try many password combinations rapidly. General API routes can have more relaxed limits for normal usage.

```javascript
const rateLimit = require("express-rate-limit");

// General: 100 requests per 15 minutes
const generalLimiter = rateLimit({
    windowMs: 15 * 60 * 1000,
    max: 100,
    message: { error: "Too many requests" }
});

// Auth: 5 attempts per 15 minutes (much stricter)
const authLimiter = rateLimit({
    windowMs: 15 * 60 * 1000,
    max: 5,
    message: { error: "Too many login attempts" }
});

app.use("/api/", generalLimiter);
app.use("/api/auth/login", authLimiter);
app.use("/api/auth/register", authLimiter);
```

This allows normal users to make 100 API calls per 15 minutes but limits login/register attempts to 5, making brute-force attacks impractical.
</details>

---

**Q30.** Describe the complete flow of a user request from login to accessing a protected route in a MERN stack application. Include what happens at each step on both the client and server side.

<details>
<summary>Answer</summary>

**Step 1 -- User submits login form (Client):**
The React frontend sends a POST request to `/api/auth/login` with the email and password in the JSON body using `fetch` or `axios`.

**Step 2 -- Server receives the request (Server):**
Express receives the request. `express.json()` middleware parses the body. The request passes through `cors` and rate limiting middleware.

**Step 3 -- Server validates credentials (Server):**
The login route handler finds the user by email in the database. It uses `bcrypt.compare()` to check the password against the stored hash. If either check fails, it returns `401` with a generic error.

**Step 4 -- Server generates JWT (Server):**
If credentials are valid, the server creates a JWT using `jwt.sign()` with the user's ID and role, signed with the secret key. The token and user data (excluding password) are sent in the response.

**Step 5 -- Client stores the token (Client):**
React receives the response, extracts the token, and stores it (in localStorage, a state management store, or a cookie). The user is redirected to the dashboard.

**Step 6 -- Client makes an authenticated request (Client):**
When the user navigates to a protected page, React sends a GET request to `/api/profile` with the header `Authorization: Bearer <token>`.

**Step 7 -- Server verifies the token (Server):**
The `authenticate` middleware extracts the token from the header, calls `jwt.verify()`, and attaches the decoded user data to `req.user`. If verification fails, it returns `401`.

**Step 8 -- Authorization check (Server, if applicable):**
If the route requires a specific role, the `authorize` middleware checks `req.user.role` against the allowed roles. If unauthorized, it returns `403`.

**Step 9 -- Route handler responds (Server):**
The route handler uses `req.user.userId` to fetch the user's specific data and sends it in the response.

**Step 10 -- Client displays the data (Client):**
React receives the data and renders it on the page. If the token has expired (401 response), React redirects the user to the login page.
</details>

---

*End of Week 27 Practice Questions and Backend Phase Review.*
