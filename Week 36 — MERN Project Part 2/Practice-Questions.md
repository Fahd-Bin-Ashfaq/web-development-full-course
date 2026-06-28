# Week 36 — MERN Project Part 2: Completion Checklist & Phase Review

**Total Review Questions: 15** (10 MCQs + 5 Coding Exercises)

---

## Part 1: Project Completion Checklist

Use this checklist to verify your MERN project is fully complete before submission. Check off each item as you finish it.

### Authentication

- [ ] User can register with name, email, password
- [ ] User can login and receive JWT
- [ ] User can logout (token cleared)
- [ ] Protected routes redirect to login
- [ ] Login persists on page refresh

### CRUD Operations

- [ ] Create new items with form validation
- [ ] Read/display all items in list/grid
- [ ] View single item details
- [ ] Update existing items with pre-filled form
- [ ] Delete items with confirmation dialog

### Advanced Features

- [ ] Search functionality with debounce
- [ ] Filter by status/category
- [ ] Sort by date/priority
- [ ] Pagination working
- [ ] Loading states on all operations
- [ ] Error handling with user-friendly messages

### UI/UX

- [ ] Styled with Tailwind CSS
- [ ] Responsive on mobile, tablet, desktop
- [ ] Consistent color scheme
- [ ] Proper navigation
- [ ] Empty states (no items found)
- [ ] Success/error notifications

### Code Quality

- [ ] Environment variables used (no hardcoded secrets)
- [ ] Passwords hashed with bcrypt
- [ ] Input validation on frontend and backend
- [ ] Proper error handling in try/catch
- [ ] Clean folder structure
- [ ] Code comments where needed

---

## Part 2: MERN Phase Review (Weeks 32-36)

This section reviews the entire MERN phase of the course, covering integration, authentication, advanced features, and project building.

---

### Multiple Choice Questions

---

**Question 1: In the MERN stack, what role does each component play?**

- A) MongoDB handles routing, Express handles data, React handles server logic, Node.js handles UI
- B) MongoDB is the database, Express is the backend framework, React is the frontend library, Node.js is the runtime environment
- C) MongoDB is the frontend, Express is the database, React is the runtime, Node.js is the framework
- D) MongoDB handles authentication, Express handles styling, React handles APIs, Node.js handles storage

<details>
<summary>Answer</summary>

**Correct Answer: B**

The MERN stack is a full-stack JavaScript architecture where each technology serves a distinct purpose:

- **MongoDB** is a NoSQL document database that stores data in flexible, JSON-like documents (BSON). It serves as the data persistence layer.
- **Express.js** is a minimal and flexible Node.js web application framework that provides routing, middleware support, and HTTP utility methods. It serves as the backend/server framework.
- **React** is a JavaScript library for building user interfaces. It handles the frontend, rendering components and managing the view layer that users interact with.
- **Node.js** is a JavaScript runtime built on Chrome's V8 engine. It allows JavaScript to run on the server side, providing the environment in which Express operates.

Together, they allow developers to use JavaScript across the entire application stack, from database queries to server logic to client-side rendering.
</details>

---

**Question 2: What is the purpose of CORS (Cross-Origin Resource Sharing), and how is it typically configured in a MERN application?**

- A) CORS encrypts data between the client and server to prevent hacking
- B) CORS allows the backend to specify which frontend origins are permitted to make requests, preventing unauthorized cross-origin access
- C) CORS is a database security feature that restricts which collections can be queried
- D) CORS is a React feature that manages component rendering across different routes

<details>
<summary>Answer</summary>

**Correct Answer: B**

CORS is a security mechanism enforced by web browsers. By default, browsers block requests made from one origin (e.g., `http://localhost:3000`) to a different origin (e.g., `http://localhost:5000`). This is called the Same-Origin Policy.

In a MERN application, the React frontend typically runs on a different port than the Express backend during development. Without CORS configuration, the browser would block API requests from React to Express.

To enable CORS in Express, you install and use the `cors` middleware:

```js
const cors = require('cors');

app.use(cors({
  origin: 'http://localhost:3000', // Allow only your React app
  credentials: true               // Allow cookies/auth headers
}));
```

You can also allow multiple origins or use `origin: '*'` during development (not recommended for production). CORS headers like `Access-Control-Allow-Origin` and `Access-Control-Allow-Methods` are sent in the server's response, telling the browser which cross-origin requests are permitted.
</details>

---

**Question 3: In a MERN application, what is the difference between bcrypt and JWT?**

- A) bcrypt is used to create tokens, JWT is used to hash passwords
- B) bcrypt is a frontend library, JWT is a backend library
- C) bcrypt is used to hash passwords for secure storage, JWT is used to create tokens for authenticating users across requests
- D) bcrypt and JWT serve the same purpose and are interchangeable

<details>
<summary>Answer</summary>

**Correct Answer: C**

bcrypt and JWT serve two completely different purposes in authentication:

**bcrypt** is a password-hashing library. When a user registers, their plain-text password is hashed using bcrypt before being stored in the database. This ensures that even if the database is compromised, the actual passwords are not exposed. bcrypt uses a salt (random data) and multiple rounds of hashing to make brute-force attacks extremely difficult.

```js
const hashedPassword = await bcrypt.hash(password, 10); // Hash with 10 salt rounds
const isMatch = await bcrypt.compare(password, hashedPassword); // Compare during login
```

**JWT (JSON Web Token)** is a token-based authentication mechanism. After a user successfully logs in (password verified with bcrypt), the server creates a JWT containing the user's ID and other claims. This token is sent to the client and included in subsequent requests (usually in the `Authorization` header) to prove the user's identity without requiring them to send their password again.

```js
const token = jwt.sign({ userId: user._id }, process.env.JWT_SECRET, { expiresIn: '7d' });
```

In summary: bcrypt secures the password at rest, JWT secures the session in transit.
</details>

---

**Question 4: What is the purpose of Multer middleware in an Express application?**

- A) Multer is used to validate JSON request bodies
- B) Multer is used to handle file uploads by parsing multipart/form-data requests
- C) Multer is used to compress response data before sending it to the client
- D) Multer is used to manage database connections in Express

<details>
<summary>Answer</summary>

**Correct Answer: B**

Multer is a Node.js middleware specifically designed for handling `multipart/form-data`, which is the encoding type used when forms include file uploads. Express's built-in `express.json()` middleware cannot parse file uploads, so Multer fills that gap.

When a user uploads a file (such as a profile picture or document), the browser sends the data as `multipart/form-data`. Multer intercepts this request, processes the file, and makes it available on `req.file` (single file) or `req.files` (multiple files).

```js
const multer = require('multer');

const storage = multer.diskStorage({
  destination: (req, file, cb) => cb(null, 'uploads/'),
  filename: (req, file, cb) => cb(null, Date.now() + '-' + file.originalname)
});

const upload = multer({ storage });

app.post('/api/upload', upload.single('image'), (req, res) => {
  res.json({ filePath: req.file.path });
});
```

Multer supports configuration options for file size limits, file type filtering, storage destinations (disk or memory), and handling multiple file fields. It is essential for any MERN application that requires image uploads, document attachments, or any form of file handling.
</details>

---

**Question 5: In MongoDB, how is the `$regex` operator used, and what is a common use case?**

- A) `$regex` is used to delete documents matching a pattern
- B) `$regex` is used to perform pattern-based string matching in queries, commonly used for search functionality
- C) `$regex` is used to validate schema types in MongoDB collections
- D) `$regex` is used to sort documents alphabetically

<details>
<summary>Answer</summary>

**Correct Answer: B**

The `$regex` operator in MongoDB allows you to perform regular expression (pattern-based) matching on string fields. It is one of the most common ways to implement search functionality in a MERN application.

For example, if you want to find all products whose name contains the word "phone" (case-insensitive):

```js
const products = await Product.find({
  name: { $regex: searchTerm, $options: 'i' }
});
```

- `$regex: searchTerm` specifies the pattern to match against.
- `$options: 'i'` makes the search case-insensitive.

Common use cases include:

1. **Search bars**: Finding documents where a field contains the user's search query.
2. **Autocomplete**: Matching documents that start with certain characters using `^` (e.g., `$regex: '^app'`).
3. **Filtering**: Finding documents that match specific patterns in fields like email domains or categories.

It is important to note that `$regex` queries on large collections without proper indexing can be slow. For production applications with heavy search requirements, consider using MongoDB Atlas Search or a dedicated search engine like Elasticsearch.
</details>

---

**Question 6: How do `skip` and `limit` work together to implement pagination in MongoDB?**

- A) `skip` sets the maximum number of documents, `limit` sets the starting point
- B) `skip` bypasses a specified number of documents, `limit` restricts how many documents are returned, enabling page-based data retrieval
- C) `skip` removes documents from the collection, `limit` caps the collection size
- D) `skip` and `limit` are used only for sorting, not pagination

<details>
<summary>Answer</summary>

**Correct Answer: B**

Pagination is the process of dividing a large dataset into smaller pages. In MongoDB, `skip` and `limit` work together to achieve this:

- **`skip(n)`** tells MongoDB to bypass the first `n` documents in the result set.
- **`limit(n)`** tells MongoDB to return at most `n` documents.

The formula for pagination is:

```
skip = (page - 1) * limit
```

For example, with 10 items per page:
- **Page 1**: `skip(0).limit(10)` returns documents 1-10
- **Page 2**: `skip(10).limit(10)` returns documents 11-20
- **Page 3**: `skip(20).limit(10)` returns documents 21-30

Here is a typical Express route implementing pagination:

```js
app.get('/api/items', async (req, res) => {
  const page = parseInt(req.query.page) || 1;
  const limit = parseInt(req.query.limit) || 10;
  const skip = (page - 1) * limit;

  const items = await Item.find().skip(skip).limit(limit).sort({ createdAt: -1 });
  const total = await Item.countDocuments();

  res.json({
    items,
    currentPage: page,
    totalPages: Math.ceil(total / limit),
    totalItems: total
  });
});
```

This approach allows the frontend to request specific pages of data and display pagination controls (Previous, Next, page numbers) to the user.
</details>

---

**Question 7: What is the purpose of AuthContext in a React MERN application?**

- A) AuthContext is used to style authentication forms with CSS
- B) AuthContext provides a global state for authentication data (user info, tokens, login/logout functions) accessible to any component without prop drilling
- C) AuthContext is an Express middleware that validates JWT tokens
- D) AuthContext is a MongoDB collection that stores user sessions

<details>
<summary>Answer</summary>

**Correct Answer: B**

AuthContext leverages React's Context API to create a global authentication state that any component in the application can access without passing props through multiple levels (prop drilling).

In a typical MERN application, many components need to know whether a user is logged in, who the user is, or need access to login/logout functions. Without Context, you would have to pass this data as props from parent to child through every intermediate component.

AuthContext typically provides:

1. **User state**: The currently logged-in user's information.
2. **Token**: The JWT token for making authenticated API requests.
3. **Login function**: Sends credentials to the API, stores the token, and updates the user state.
4. **Logout function**: Clears the token and user state.
5. **Loading state**: Indicates whether authentication status is being checked (e.g., on page refresh).

```jsx
const AuthContext = createContext();

export function AuthProvider({ children }) {
  const [user, setUser] = useState(null);
  const [token, setToken] = useState(localStorage.getItem('token'));

  const login = async (email, password) => { /* ... */ };
  const logout = () => { /* ... */ };

  return (
    <AuthContext.Provider value={{ user, token, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
}

export const useAuth = () => useContext(AuthContext);
```

Any component can then call `const { user, login, logout } = useAuth()` to access authentication state and functions.
</details>

---

**Question 8: What does a PrivateRoute component do when an unauthenticated user tries to access a protected page?**

- A) It displays the protected page but hides sensitive data
- B) It throws an error and crashes the application
- C) It redirects the user to the login page, preventing access to the protected content
- D) It sends a request to the server to delete the user's account

<details>
<summary>Answer</summary>

**Correct Answer: C**

A PrivateRoute (also called a Protected Route) is a wrapper component that checks whether a user is authenticated before rendering the requested page. If the user is not authenticated, it redirects them to the login page instead of showing the protected content.

This is a client-side guard that works alongside server-side authentication (JWT verification). Even though the server protects API endpoints, PrivateRoute improves user experience by preventing unauthenticated users from seeing pages that would be useless without data.

A typical implementation using React Router v6:

```jsx
import { Navigate } from 'react-router-dom';
import { useAuth } from '../context/AuthContext';

function PrivateRoute({ children }) {
  const { token, loading } = useAuth();

  if (loading) return <div>Loading...</div>;

  return token ? children : <Navigate to="/login" replace />;
}

// Usage in routes:
<Route path="/dashboard" element={
  <PrivateRoute>
    <Dashboard />
  </PrivateRoute>
} />
```

Key behaviors:
- If the user has a valid token, the child component (protected page) is rendered normally.
- If the user does not have a token, they are redirected to `/login`.
- The `replace` prop prevents the protected URL from appearing in browser history, so pressing "Back" after redirect does not loop back to the protected route.
- A loading state is checked first to avoid premature redirects while authentication status is being verified (e.g., on page refresh).
</details>

---

**Question 9: When is FormData used instead of a regular JSON object in a MERN application?**

- A) FormData is used whenever you send any data to the server
- B) FormData is used when the request includes file uploads, because files cannot be sent as JSON
- C) FormData is used only for GET requests
- D) FormData is a MongoDB data format for storing documents

<details>
<summary>Answer</summary>

**Correct Answer: B**

FormData is a built-in browser API that constructs a set of key-value pairs representing form fields and their values, including files. It is necessary when your request includes file uploads because files (binary data) cannot be serialized into JSON format.

When you send a regular JSON request, you set the `Content-Type` to `application/json` and send a stringified object. However, files need to be sent as `multipart/form-data`, which is exactly what FormData produces.

```jsx
// Regular JSON request (no files):
const response = await fetch('/api/items', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ title: 'My Item', description: 'Details' })
});

// FormData request (with files):
const formData = new FormData();
formData.append('title', 'My Item');
formData.append('description', 'Details');
formData.append('image', fileInput.files[0]); // File object

const response = await fetch('/api/items', {
  method: 'POST',
  headers: { 'Authorization': `Bearer ${token}` },
  // Do NOT set Content-Type header - browser sets it automatically with boundary
  body: formData
});
```

Important notes:
- When using FormData, do **not** manually set the `Content-Type` header. The browser automatically sets it to `multipart/form-data` with a unique boundary string that separates each field.
- On the Express side, you need Multer (or a similar middleware) to parse `multipart/form-data` requests. `express.json()` cannot handle this format.
- FormData can include both text fields and file fields in the same request.
</details>

---

**Question 10: In a complete MERN application, what is the correct order of the full data flow when a user submits a form?**

- A) MongoDB -> Express -> React -> Node.js
- B) React component captures input -> Axios/Fetch sends HTTP request -> Express route receives request -> Mongoose model saves to MongoDB -> Response sent back to React
- C) Express sends data to React -> React stores in MongoDB -> MongoDB sends to Node.js
- D) Node.js compiles the form -> MongoDB validates the data -> Express renders the page -> React stores the result

<details>
<summary>Answer</summary>

**Correct Answer: B**

The complete data flow in a MERN application follows a clear request-response cycle:

1. **React (Frontend)**: The user fills out a form. React captures the input values using state (e.g., `useState`). When the form is submitted, an event handler prevents the default form submission and prepares the data.

2. **HTTP Request (Axios/Fetch)**: The React component sends an HTTP request (POST, PUT, etc.) to the Express backend. This request includes the form data in the body and any authentication headers (JWT token).

3. **Express (Backend)**: The Express server receives the request at the matching route. Middleware processes the request first (e.g., `express.json()` parses the body, `auth` middleware verifies the JWT token, validation middleware checks the data).

4. **Mongoose/MongoDB (Database)**: The Express route handler uses a Mongoose model to interact with MongoDB. For a form submission, it typically creates a new document: `const item = await Item.create(req.body)`.

5. **Response**: MongoDB confirms the operation. Express sends a response back to React (e.g., the created document, a success message, or an error). React receives the response and updates the UI accordingly (e.g., redirects to a list page, shows a success notification, or displays validation errors).

```
User Input -> React State -> fetch/axios POST -> Express Route -> Mongoose Model -> MongoDB
                                                                                      |
User sees update <- React updates UI <- Response received <- Express sends response <--+
```

This full cycle demonstrates how JavaScript flows seamlessly across the entire stack in a MERN application.
</details>

---

### Coding Exercises

---

**Exercise 1: Build a Complete Express API with Auth Middleware and CRUD Routes**

You are building a Task Manager API. Given the following Mongoose schema, create a complete Express setup with JWT authentication middleware and full CRUD routes for tasks. Each task belongs to a specific user.

**Schema:**

```js
const taskSchema = new mongoose.Schema({
  title: { type: String, required: true },
  description: { type: String },
  status: { type: String, enum: ['pending', 'in-progress', 'completed'], default: 'pending' },
  priority: { type: String, enum: ['low', 'medium', 'high'], default: 'medium' },
  user: { type: mongoose.Schema.Types.ObjectId, ref: 'User', required: true },
}, { timestamps: true });
```

**Requirements:**
- Auth middleware that verifies JWT from the Authorization header
- GET `/api/tasks` - Get all tasks for the logged-in user (with optional status filter)
- GET `/api/tasks/:id` - Get a single task (only if it belongs to the user)
- POST `/api/tasks` - Create a new task
- PUT `/api/tasks/:id` - Update a task (only if it belongs to the user)
- DELETE `/api/tasks/:id` - Delete a task (only if it belongs to the user)

**Starter Code:**

```js
const express = require('express');
const jwt = require('jsonwebtoken');
const mongoose = require('mongoose');

const app = express();
app.use(express.json());

// Task model (assume already defined as above)
const Task = mongoose.model('Task', taskSchema);

// TODO: Create auth middleware

// TODO: Create CRUD routes

app.listen(5000, () => console.log('Server running on port 5000'));
```

<details>
<summary>Solution</summary>

```js
const express = require('express');
const jwt = require('jsonwebtoken');
const mongoose = require('mongoose');

const app = express();
app.use(express.json());

// ========================
// Mongoose Schema & Model
// ========================
const taskSchema = new mongoose.Schema({
  title: { type: String, required: true },
  description: { type: String },
  status: { type: String, enum: ['pending', 'in-progress', 'completed'], default: 'pending' },
  priority: { type: String, enum: ['low', 'medium', 'high'], default: 'medium' },
  user: { type: mongoose.Schema.Types.ObjectId, ref: 'User', required: true },
}, { timestamps: true });

const Task = mongoose.model('Task', taskSchema);

// ========================
// Auth Middleware
// ========================
// This middleware extracts the JWT from the Authorization header,
// verifies it, and attaches the decoded user data to req.user.
const auth = (req, res, next) => {
  try {
    // The token is expected in the format: "Bearer <token>"
    const authHeader = req.header('Authorization');

    if (!authHeader || !authHeader.startsWith('Bearer ')) {
      return res.status(401).json({ message: 'No token provided, authorization denied' });
    }

    const token = authHeader.replace('Bearer ', '');
    const decoded = jwt.verify(token, process.env.JWT_SECRET);

    // Attach the user's ID from the token payload to the request object
    // This makes it available in all subsequent route handlers
    req.user = decoded;
    next();
  } catch (error) {
    res.status(401).json({ message: 'Token is not valid' });
  }
};

// ========================
// CRUD Routes
// ========================

// GET /api/tasks - Get all tasks for the logged-in user
// Supports optional query parameter: ?status=pending
app.get('/api/tasks', auth, async (req, res) => {
  try {
    // Build a filter object. Always filter by the logged-in user's ID.
    const filter = { user: req.user.userId };

    // If a status query parameter is provided, add it to the filter
    if (req.query.status) {
      filter.status = req.query.status;
    }

    const tasks = await Task.find(filter).sort({ createdAt: -1 });

    res.json({
      count: tasks.length,
      tasks
    });
  } catch (error) {
    res.status(500).json({ message: 'Server error', error: error.message });
  }
});

// GET /api/tasks/:id - Get a single task by ID
// Only returns the task if it belongs to the logged-in user
app.get('/api/tasks/:id', auth, async (req, res) => {
  try {
    const task = await Task.findOne({
      _id: req.params.id,
      user: req.user.userId  // Ensures the task belongs to this user
    });

    if (!task) {
      return res.status(404).json({ message: 'Task not found' });
    }

    res.json(task);
  } catch (error) {
    res.status(500).json({ message: 'Server error', error: error.message });
  }
});

// POST /api/tasks - Create a new task
// Automatically assigns the task to the logged-in user
app.post('/api/tasks', auth, async (req, res) => {
  try {
    const { title, description, status, priority } = req.body;

    // Validate required fields
    if (!title) {
      return res.status(400).json({ message: 'Title is required' });
    }

    const task = await Task.create({
      title,
      description,
      status,
      priority,
      user: req.user.userId  // Associate the task with the logged-in user
    });

    res.status(201).json({
      message: 'Task created successfully',
      task
    });
  } catch (error) {
    // Handle Mongoose validation errors
    if (error.name === 'ValidationError') {
      return res.status(400).json({ message: error.message });
    }
    res.status(500).json({ message: 'Server error', error: error.message });
  }
});

// PUT /api/tasks/:id - Update an existing task
// Only allows updating if the task belongs to the logged-in user
app.put('/api/tasks/:id', auth, async (req, res) => {
  try {
    const { title, description, status, priority } = req.body;

    // findOneAndUpdate with both _id and user ensures ownership
    const task = await Task.findOneAndUpdate(
      { _id: req.params.id, user: req.user.userId },
      { title, description, status, priority },
      { new: true, runValidators: true }  // Return updated doc, run schema validators
    );

    if (!task) {
      return res.status(404).json({ message: 'Task not found or unauthorized' });
    }

    res.json({
      message: 'Task updated successfully',
      task
    });
  } catch (error) {
    if (error.name === 'ValidationError') {
      return res.status(400).json({ message: error.message });
    }
    res.status(500).json({ message: 'Server error', error: error.message });
  }
});

// DELETE /api/tasks/:id - Delete a task
// Only allows deleting if the task belongs to the logged-in user
app.delete('/api/tasks/:id', auth, async (req, res) => {
  try {
    const task = await Task.findOneAndDelete({
      _id: req.params.id,
      user: req.user.userId  // Ensures the task belongs to this user
    });

    if (!task) {
      return res.status(404).json({ message: 'Task not found or unauthorized' });
    }

    res.json({
      message: 'Task deleted successfully',
      deletedTask: task
    });
  } catch (error) {
    res.status(500).json({ message: 'Server error', error: error.message });
  }
});

// ========================
// Server Start
// ========================
app.listen(5000, () => console.log('Server running on port 5000'));
```

**Key concepts demonstrated:**

1. **Auth Middleware**: Extracts the token from the `Authorization` header, verifies it with `jwt.verify()`, and attaches the decoded payload to `req.user`. If the token is missing or invalid, the request is rejected with a 401 status.

2. **Ownership Filtering**: Every query includes `user: req.user.userId` to ensure users can only access their own tasks. This is critical for data security.

3. **Validation**: The route checks for required fields before creating a task, and `runValidators: true` on updates ensures Mongoose schema validations (like enum values) are enforced on updates as well.

4. **Error Handling**: Each route is wrapped in try/catch. Mongoose validation errors return 400 (client error), while unexpected errors return 500 (server error).

5. **Query Filtering**: The GET route supports optional filtering via query parameters, building the filter object dynamically.
</details>

---

**Exercise 2: Create a React AuthContext with Login, Logout, and Persistent Auth**

Build a complete `AuthContext` that provides authentication state throughout your React application. The context should handle login, logout, and persist the user's session across page refreshes using localStorage.

**Requirements:**
- Store the JWT token in localStorage
- On app load, check localStorage for an existing token and validate it by fetching user data
- Provide `login`, `register`, and `logout` functions
- Expose a `loading` state for initial auth check
- Expose the current `user` object and `token`

**Starter Code:**

```jsx
import { createContext, useContext, useState, useEffect } from 'react';

const AuthContext = createContext();

export function AuthProvider({ children }) {
  // TODO: Implement auth state and functions

  return (
    <AuthContext.Provider value={{}}>
      {children}
    </AuthContext.Provider>
  );
}

export const useAuth = () => useContext(AuthContext);
```

<details>
<summary>Solution</summary>

```jsx
import { createContext, useContext, useState, useEffect } from 'react';

const AuthContext = createContext();

const API_URL = 'http://localhost:5000/api';

export function AuthProvider({ children }) {
  // ========================
  // State Management
  // ========================
  const [user, setUser] = useState(null);           // Current user object
  const [token, setToken] = useState(               // JWT token
    localStorage.getItem('token')                    // Initialize from localStorage
  );
  const [loading, setLoading] = useState(true);      // Loading state for initial auth check

  // ========================
  // Persistent Auth Check
  // ========================
  // When the app loads, check if there is a stored token and validate it
  // by fetching the current user's data from the server.
  useEffect(() => {
    const loadUser = async () => {
      if (!token) {
        setLoading(false);
        return;
      }

      try {
        const response = await fetch(`${API_URL}/auth/me`, {
          headers: {
            'Authorization': `Bearer ${token}`
          }
        });

        if (response.ok) {
          const data = await response.json();
          setUser(data.user);
        } else {
          // Token is invalid or expired - clean up
          localStorage.removeItem('token');
          setToken(null);
          setUser(null);
        }
      } catch (error) {
        console.error('Failed to load user:', error);
        // Network error - clean up stored auth data
        localStorage.removeItem('token');
        setToken(null);
        setUser(null);
      } finally {
        setLoading(false);
      }
    };

    loadUser();
  }, [token]);

  // ========================
  // Register Function
  // ========================
  // Sends registration data to the server, stores the returned token,
  // and sets the user state.
  const register = async (name, email, password) => {
    const response = await fetch(`${API_URL}/auth/register`, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ name, email, password })
    });

    const data = await response.json();

    if (!response.ok) {
      // Throw the server's error message so the component can display it
      throw new Error(data.message || 'Registration failed');
    }

    // Store the token in localStorage for persistence across page refreshes
    localStorage.setItem('token', data.token);
    setToken(data.token);
    setUser(data.user);

    return data;
  };

  // ========================
  // Login Function
  // ========================
  // Sends credentials to the server, stores the returned token,
  // and sets the user state.
  const login = async (email, password) => {
    const response = await fetch(`${API_URL}/auth/login`, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ email, password })
    });

    const data = await response.json();

    if (!response.ok) {
      throw new Error(data.message || 'Login failed');
    }

    // Store token in localStorage so it survives page refreshes
    localStorage.setItem('token', data.token);
    setToken(data.token);
    setUser(data.user);

    return data;
  };

  // ========================
  // Logout Function
  // ========================
  // Clears the token from localStorage and resets all auth state.
  const logout = () => {
    localStorage.removeItem('token');
    setToken(null);
    setUser(null);
  };

  // ========================
  // Context Value
  // ========================
  // All components that consume this context will have access to these values.
  const value = {
    user,       // The current user object (null if not logged in)
    token,      // The JWT token (null if not logged in)
    loading,    // True while checking for existing auth on app load
    login,      // Function to log in: login(email, password)
    register,   // Function to register: register(name, email, password)
    logout,     // Function to log out: logout()
    isAuthenticated: !!token  // Convenience boolean for quick auth checks
  };

  return (
    <AuthContext.Provider value={value}>
      {children}
    </AuthContext.Provider>
  );
}

// Custom hook for consuming the auth context.
// Components call: const { user, login, logout } = useAuth();
export const useAuth = () => {
  const context = useContext(AuthContext);
  if (!context) {
    throw new Error('useAuth must be used within an AuthProvider');
  }
  return context;
};
```

**How to use this in your app:**

```jsx
// App.jsx - Wrap your entire app with AuthProvider
import { AuthProvider } from './context/AuthContext';
import { BrowserRouter, Routes, Route } from 'react-router-dom';

function App() {
  return (
    <AuthProvider>
      <BrowserRouter>
        <Routes>
          <Route path="/login" element={<Login />} />
          <Route path="/dashboard" element={
            <PrivateRoute><Dashboard /></PrivateRoute>
          } />
        </Routes>
      </BrowserRouter>
    </AuthProvider>
  );
}
```

```jsx
// Login.jsx - Consuming the context
import { useAuth } from '../context/AuthContext';
import { useState } from 'react';
import { useNavigate } from 'react-router-dom';

function Login() {
  const { login } = useAuth();
  const navigate = useNavigate();
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [error, setError] = useState('');

  const handleSubmit = async (e) => {
    e.preventDefault();
    try {
      await login(email, password);
      navigate('/dashboard');
    } catch (err) {
      setError(err.message);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      {error && <p className="text-red-500">{error}</p>}
      <input value={email} onChange={(e) => setEmail(e.target.value)} />
      <input type="password" value={password} onChange={(e) => setPassword(e.target.value)} />
      <button type="submit">Login</button>
    </form>
  );
}
```

**Key concepts demonstrated:**

1. **Persistent Auth**: The token is stored in `localStorage` and checked on every app load via the `useEffect` hook. This ensures that if the user refreshes the page, they remain logged in.

2. **Token Validation**: Simply having a token in `localStorage` is not enough. The `useEffect` makes an API call to `/auth/me` to verify the token is still valid. If the server rejects it (expired, tampered), the auth state is cleared.

3. **Loading State**: The `loading` flag prevents the app from rendering protected routes before the auth check completes. Without this, a valid user would briefly see the login page before being redirected to the dashboard.

4. **Error Handling**: Both `login` and `register` throw errors with the server's message, allowing components to catch and display them to the user.

5. **Custom Hook Safety**: The `useAuth` hook throws a descriptive error if used outside of `AuthProvider`, making debugging easier during development.
</details>

---

**Exercise 3: Build a React Component with Fetch, Display, Search, and Pagination**

Create a React component that fetches products from an API, displays them in a grid, implements search with debounce, and supports pagination.

**Requirements:**
- Fetch products from `/api/products` with query parameters for search, page, and limit
- Display products in a responsive grid
- Search input with 500ms debounce (does not fire an API call on every keystroke)
- Pagination controls (Previous, page numbers, Next)
- Loading and error states

**Starter Code:**

```jsx
import { useState, useEffect } from 'react';

function ProductList() {
  // TODO: Implement state, fetching, search with debounce, and pagination

  return (
    <div>
      {/* TODO: Search input, product grid, pagination controls */}
    </div>
  );
}

export default ProductList;
```

<details>
<summary>Solution</summary>

```jsx
import { useState, useEffect, useCallback } from 'react';

function ProductList() {
  // ========================
  // State
  // ========================
  const [products, setProducts] = useState([]);      // Array of product objects
  const [loading, setLoading] = useState(true);       // Loading indicator
  const [error, setError] = useState(null);           // Error message
  const [searchTerm, setSearchTerm] = useState('');   // What the user types
  const [debouncedSearch, setDebouncedSearch] = useState(''); // Debounced value sent to API
  const [currentPage, setCurrentPage] = useState(1);  // Current page number
  const [totalPages, setTotalPages] = useState(1);    // Total number of pages
  const limit = 12;                                    // Products per page

  // ========================
  // Debounce Search Input
  // ========================
  // This useEffect sets a 500ms timer whenever searchTerm changes.
  // If the user types again within 500ms, the previous timer is cleared
  // and a new one starts. This prevents API calls on every keystroke.
  useEffect(() => {
    const timer = setTimeout(() => {
      setDebouncedSearch(searchTerm);
      setCurrentPage(1); // Reset to page 1 when search changes
    }, 500);

    // Cleanup: clear the timer if searchTerm changes before 500ms
    return () => clearTimeout(timer);
  }, [searchTerm]);

  // ========================
  // Fetch Products
  // ========================
  // Runs whenever the debounced search term or current page changes.
  const fetchProducts = useCallback(async () => {
    setLoading(true);
    setError(null);

    try {
      const params = new URLSearchParams({
        page: currentPage.toString(),
        limit: limit.toString(),
      });

      // Only add search param if there is a search term
      if (debouncedSearch) {
        params.append('search', debouncedSearch);
      }

      const response = await fetch(`/api/products?${params}`);

      if (!response.ok) {
        throw new Error('Failed to fetch products');
      }

      const data = await response.json();

      setProducts(data.products);
      setTotalPages(data.totalPages);
    } catch (err) {
      setError(err.message);
      setProducts([]);
    } finally {
      setLoading(false);
    }
  }, [currentPage, debouncedSearch]);

  useEffect(() => {
    fetchProducts();
  }, [fetchProducts]);

  // ========================
  // Pagination Handlers
  // ========================
  const goToPage = (page) => {
    if (page >= 1 && page <= totalPages) {
      setCurrentPage(page);
      window.scrollTo({ top: 0, behavior: 'smooth' });
    }
  };

  // Generate an array of page numbers to display
  // Shows at most 5 page buttons centered around the current page
  const getPageNumbers = () => {
    const pages = [];
    const maxVisible = 5;
    let start = Math.max(1, currentPage - Math.floor(maxVisible / 2));
    let end = Math.min(totalPages, start + maxVisible - 1);

    // Adjust start if we are near the end
    if (end - start + 1 < maxVisible) {
      start = Math.max(1, end - maxVisible + 1);
    }

    for (let i = start; i <= end; i++) {
      pages.push(i);
    }

    return pages;
  };

  // ========================
  // Render
  // ========================
  return (
    <div className="max-w-7xl mx-auto px-4 py-8">
      {/* Page Title */}
      <h1 className="text-3xl font-bold text-gray-800 mb-8">Products</h1>

      {/* Search Input */}
      <div className="mb-6">
        <input
          type="text"
          placeholder="Search products..."
          value={searchTerm}
          onChange={(e) => setSearchTerm(e.target.value)}
          className="w-full max-w-md px-4 py-2 border border-gray-300 rounded-lg
                     focus:outline-none focus:ring-2 focus:ring-blue-500"
        />
        {searchTerm !== debouncedSearch && (
          <span className="ml-2 text-sm text-gray-400">Searching...</span>
        )}
      </div>

      {/* Error State */}
      {error && (
        <div className="bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded mb-6">
          <p>{error}</p>
          <button
            onClick={fetchProducts}
            className="mt-2 text-sm underline hover:no-underline"
          >
            Try Again
          </button>
        </div>
      )}

      {/* Loading State */}
      {loading && (
        <div className="flex justify-center items-center py-20">
          <div className="animate-spin rounded-full h-12 w-12 border-b-2 border-blue-500"></div>
        </div>
      )}

      {/* Empty State */}
      {!loading && !error && products.length === 0 && (
        <div className="text-center py-20 text-gray-500">
          <p className="text-xl mb-2">No products found</p>
          {debouncedSearch && (
            <p className="text-sm">
              No results for "{debouncedSearch}".
              <button
                onClick={() => setSearchTerm('')}
                className="text-blue-500 underline ml-1"
              >
                Clear search
              </button>
            </p>
          )}
        </div>
      )}

      {/* Product Grid */}
      {!loading && !error && products.length > 0 && (
        <>
          <div className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
            {products.map((product) => (
              <div
                key={product._id}
                className="bg-white rounded-lg shadow-md overflow-hidden
                           hover:shadow-lg transition-shadow duration-300"
              >
                {product.image && (
                  <img
                    src={product.image}
                    alt={product.name}
                    className="w-full h-48 object-cover"
                  />
                )}
                <div className="p-4">
                  <h3 className="text-lg font-semibold text-gray-800 mb-1">
                    {product.name}
                  </h3>
                  <p className="text-gray-500 text-sm mb-2 line-clamp-2">
                    {product.description}
                  </p>
                  <div className="flex justify-between items-center">
                    <span className="text-xl font-bold text-blue-600">
                      ${product.price?.toFixed(2)}
                    </span>
                    <span className="text-xs bg-green-100 text-green-800 px-2 py-1 rounded">
                      {product.category}
                    </span>
                  </div>
                </div>
              </div>
            ))}
          </div>

          {/* Pagination Controls */}
          {totalPages > 1 && (
            <div className="flex justify-center items-center gap-2 mt-8">
              {/* Previous Button */}
              <button
                onClick={() => goToPage(currentPage - 1)}
                disabled={currentPage === 1}
                className="px-4 py-2 rounded-lg border border-gray-300
                           disabled:opacity-50 disabled:cursor-not-allowed
                           hover:bg-gray-100 transition-colors"
              >
                Previous
              </button>

              {/* Page Number Buttons */}
              {getPageNumbers().map((page) => (
                <button
                  key={page}
                  onClick={() => goToPage(page)}
                  className={`px-4 py-2 rounded-lg transition-colors ${
                    page === currentPage
                      ? 'bg-blue-500 text-white'
                      : 'border border-gray-300 hover:bg-gray-100'
                  }`}
                >
                  {page}
                </button>
              ))}

              {/* Next Button */}
              <button
                onClick={() => goToPage(currentPage + 1)}
                disabled={currentPage === totalPages}
                className="px-4 py-2 rounded-lg border border-gray-300
                           disabled:opacity-50 disabled:cursor-not-allowed
                           hover:bg-gray-100 transition-colors"
              >
                Next
              </button>
            </div>
          )}

          {/* Page Info */}
          <p className="text-center text-sm text-gray-500 mt-4">
            Page {currentPage} of {totalPages}
          </p>
        </>
      )}
    </div>
  );
}

export default ProductList;
```

**Key concepts demonstrated:**

1. **Debounce Pattern**: The search input uses a two-state approach: `searchTerm` updates immediately as the user types (keeping the input responsive), while `debouncedSearch` only updates after 500ms of inactivity. The API call is triggered by `debouncedSearch`, not `searchTerm`. This prevents excessive API calls while maintaining a smooth user experience.

2. **URLSearchParams**: Instead of manually concatenating query strings, `URLSearchParams` builds the query string properly, handling encoding and formatting automatically.

3. **useCallback for fetchProducts**: The fetch function is wrapped in `useCallback` with its dependencies listed. This ensures the function reference only changes when `currentPage` or `debouncedSearch` changes, preventing unnecessary re-renders and fetch cycles.

4. **Multiple UI States**: The component handles four distinct states: loading (spinner), error (error message with retry), empty (no results message), and success (product grid). This provides a polished user experience for every scenario.

5. **Smart Pagination**: The `getPageNumbers` function generates a sliding window of page buttons centered around the current page. This prevents rendering hundreds of page buttons for large datasets while still showing relevant navigation options.

6. **Responsive Grid**: The Tailwind CSS grid classes (`grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4`) create a responsive layout that adapts from a single column on mobile to four columns on large screens.
</details>

---

**Exercise 4: Create a File Upload Feature (React FormData + Express Multer Route)**

Build both the frontend React component and the backend Express route for uploading a profile picture. The React component should allow users to select an image, preview it, and upload it. The Express route should use Multer to handle the upload.

**Requirements:**
- React: File input, image preview before upload, upload button, progress/status feedback
- Express: Multer configuration with file size limit (5MB) and image-only filter
- Handle errors for invalid file types and oversized files

**Starter Code (React):**

```jsx
function ProfilePicUpload() {
  // TODO: Implement file selection, preview, and upload

  return (
    <div>
      {/* TODO: File input, preview, upload button */}
    </div>
  );
}
```

**Starter Code (Express):**

```js
const express = require('express');
const multer = require('multer');
const path = require('path');
const router = express.Router();

// TODO: Configure multer storage, file filter, and size limit
// TODO: Create upload route
```

<details>
<summary>Solution</summary>

**Express Backend (uploadRoutes.js):**

```js
const express = require('express');
const multer = require('multer');
const path = require('path');
const router = express.Router();

// ========================
// Multer Configuration
// ========================

// Storage configuration: defines WHERE and HOW files are saved
const storage = multer.diskStorage({
  // Set the destination folder for uploaded files
  destination: (req, file, cb) => {
    cb(null, 'uploads/profiles/');
  },
  // Generate a unique filename to prevent overwriting
  // Format: userId-timestamp.extension (e.g., 64a1b2c3d4-1687654321000.jpg)
  filename: (req, file, cb) => {
    const uniqueName = `${req.user.userId}-${Date.now()}${path.extname(file.originalname)}`;
    cb(null, uniqueName);
  }
});

// File filter: only allow image files (JPEG, PNG, GIF, WebP)
const fileFilter = (req, file, cb) => {
  const allowedTypes = ['image/jpeg', 'image/png', 'image/gif', 'image/webp'];

  if (allowedTypes.includes(file.mimetype)) {
    cb(null, true);   // Accept the file
  } else {
    cb(new Error('Only image files (JPEG, PNG, GIF, WebP) are allowed'), false);
  }
};

// Create the multer instance with storage, filter, and size limit
const upload = multer({
  storage,
  fileFilter,
  limits: {
    fileSize: 5 * 1024 * 1024  // 5MB limit (5 * 1024KB * 1024B)
  }
});

// ========================
// Upload Route
// ========================
// POST /api/upload/profile - Upload a profile picture
// The 'profilePic' string must match the field name used in FormData.append()
router.post('/profile', upload.single('profilePic'), async (req, res) => {
  try {
    // If multer did not find a file in the request
    if (!req.file) {
      return res.status(400).json({ message: 'No file uploaded' });
    }

    // Build the file URL that the frontend can use to display the image
    const fileUrl = `/uploads/profiles/${req.file.filename}`;

    // Optionally update the user's profile picture in the database
    // await User.findByIdAndUpdate(req.user.userId, { profilePic: fileUrl });

    res.json({
      message: 'Profile picture uploaded successfully',
      fileUrl,
      file: {
        filename: req.file.filename,
        size: req.file.size,
        mimetype: req.file.mimetype
      }
    });
  } catch (error) {
    res.status(500).json({ message: 'Upload failed', error: error.message });
  }
});

// ========================
// Error Handling Middleware
// ========================
// Multer errors (file too large, wrong type) are caught here
router.use((err, req, res, next) => {
  if (err instanceof multer.MulterError) {
    // Multer-specific errors
    if (err.code === 'LIMIT_FILE_SIZE') {
      return res.status(400).json({
        message: 'File is too large. Maximum size is 5MB.'
      });
    }
    return res.status(400).json({ message: err.message });
  }

  if (err) {
    // Custom errors (e.g., from fileFilter)
    return res.status(400).json({ message: err.message });
  }

  next();
});

module.exports = router;
```

**React Frontend (ProfilePicUpload.jsx):**

```jsx
import { useState } from 'react';
import { useAuth } from '../context/AuthContext';

function ProfilePicUpload() {
  // ========================
  // State
  // ========================
  const [selectedFile, setSelectedFile] = useState(null);  // The File object
  const [preview, setPreview] = useState(null);            // Base64 preview URL
  const [uploading, setUploading] = useState(false);       // Upload in progress
  const [uploadedUrl, setUploadedUrl] = useState(null);    // URL returned by server
  const [error, setError] = useState(null);                // Error message
  const { token } = useAuth();

  // ========================
  // File Selection Handler
  // ========================
  const handleFileSelect = (e) => {
    const file = e.target.files[0];
    setError(null);
    setUploadedUrl(null);

    if (!file) {
      setSelectedFile(null);
      setPreview(null);
      return;
    }

    // Client-side validation: check file type
    const allowedTypes = ['image/jpeg', 'image/png', 'image/gif', 'image/webp'];
    if (!allowedTypes.includes(file.type)) {
      setError('Please select an image file (JPEG, PNG, GIF, or WebP)');
      setSelectedFile(null);
      setPreview(null);
      return;
    }

    // Client-side validation: check file size (5MB)
    if (file.size > 5 * 1024 * 1024) {
      setError('File is too large. Maximum size is 5MB.');
      setSelectedFile(null);
      setPreview(null);
      return;
    }

    setSelectedFile(file);

    // Create a preview using FileReader
    // FileReader reads the file and converts it to a base64 data URL
    // that can be used as an image src for preview
    const reader = new FileReader();
    reader.onloadend = () => {
      setPreview(reader.result);
    };
    reader.readAsDataURL(file);
  };

  // ========================
  // Upload Handler
  // ========================
  const handleUpload = async () => {
    if (!selectedFile) {
      setError('Please select a file first');
      return;
    }

    setUploading(true);
    setError(null);

    try {
      // Create FormData and append the file
      // The key 'profilePic' must match what Multer expects: upload.single('profilePic')
      const formData = new FormData();
      formData.append('profilePic', selectedFile);

      const response = await fetch('/api/upload/profile', {
        method: 'POST',
        headers: {
          // Include the auth token for protected routes
          'Authorization': `Bearer ${token}`
          // Do NOT set Content-Type header!
          // The browser automatically sets it to multipart/form-data
          // with the correct boundary string
        },
        body: formData
      });

      const data = await response.json();

      if (!response.ok) {
        throw new Error(data.message || 'Upload failed');
      }

      setUploadedUrl(data.fileUrl);
      setSelectedFile(null);
      // Keep the preview showing the uploaded image
    } catch (err) {
      setError(err.message);
    } finally {
      setUploading(false);
    }
  };

  // ========================
  // Remove Selection
  // ========================
  const handleRemove = () => {
    setSelectedFile(null);
    setPreview(null);
    setError(null);
    setUploadedUrl(null);
  };

  // ========================
  // Render
  // ========================
  return (
    <div className="max-w-md mx-auto p-6 bg-white rounded-lg shadow-md">
      <h2 className="text-2xl font-bold text-gray-800 mb-4">Profile Picture</h2>

      {/* Image Preview */}
      <div className="mb-4 flex justify-center">
        {preview ? (
          <img
            src={preview}
            alt="Preview"
            className="w-40 h-40 rounded-full object-cover border-4 border-blue-200"
          />
        ) : (
          <div className="w-40 h-40 rounded-full bg-gray-200 flex items-center
                          justify-center text-gray-400 border-4 border-gray-300">
            <span className="text-sm">No image</span>
          </div>
        )}
      </div>

      {/* File Input */}
      <div className="mb-4">
        <label className="block w-full cursor-pointer">
          <span className="block text-center py-3 px-4 bg-gray-100 border-2 border-dashed
                           border-gray-300 rounded-lg hover:bg-gray-50 transition-colors">
            {selectedFile ? selectedFile.name : 'Click to select an image'}
          </span>
          <input
            type="file"
            accept="image/jpeg,image/png,image/gif,image/webp"
            onChange={handleFileSelect}
            className="hidden"
          />
        </label>
        <p className="text-xs text-gray-500 mt-1">
          Accepted formats: JPEG, PNG, GIF, WebP. Max size: 5MB.
        </p>
      </div>

      {/* Error Message */}
      {error && (
        <div className="mb-4 p-3 bg-red-100 border border-red-400 text-red-700 rounded text-sm">
          {error}
        </div>
      )}

      {/* Success Message */}
      {uploadedUrl && (
        <div className="mb-4 p-3 bg-green-100 border border-green-400 text-green-700 rounded text-sm">
          Profile picture uploaded successfully!
        </div>
      )}

      {/* Action Buttons */}
      <div className="flex gap-3">
        <button
          onClick={handleUpload}
          disabled={!selectedFile || uploading}
          className="flex-1 py-2 px-4 bg-blue-500 text-white rounded-lg
                     hover:bg-blue-600 disabled:opacity-50 disabled:cursor-not-allowed
                     transition-colors"
        >
          {uploading ? 'Uploading...' : 'Upload'}
        </button>

        {(selectedFile || preview) && (
          <button
            onClick={handleRemove}
            disabled={uploading}
            className="py-2 px-4 bg-gray-200 text-gray-700 rounded-lg
                       hover:bg-gray-300 disabled:opacity-50 transition-colors"
          >
            Remove
          </button>
        )}
      </div>
    </div>
  );
}

export default ProfilePicUpload;
```

**Key concepts demonstrated:**

1. **FormData API**: FormData is used instead of JSON because files are binary data that cannot be JSON-serialized. The `append` method adds both the file and any additional text fields. The key name (`'profilePic'`) must match the field name in Multer's `upload.single('profilePic')`.

2. **No Content-Type Header**: When sending FormData, you must NOT manually set the `Content-Type` header. The browser automatically sets it to `multipart/form-data` with a unique boundary string that tells the server where each field starts and ends. Setting it manually breaks the upload.

3. **FileReader for Preview**: `FileReader.readAsDataURL()` converts the selected file into a base64-encoded string that can be used as an image `src`. This lets users see their image before uploading it, improving the user experience.

4. **Client-Side Validation**: The component validates file type and size before uploading, providing instant feedback. However, server-side validation (Multer's `fileFilter` and `limits`) is still essential because client-side checks can be bypassed.

5. **Multer Error Handling**: The Express error-handling middleware catches Multer-specific errors (like `LIMIT_FILE_SIZE`) and custom errors (from `fileFilter`) and returns appropriate error messages. Without this middleware, Multer errors would cause unhandled exceptions.

6. **Unique Filenames**: The `diskStorage` configuration generates filenames using the user ID and timestamp, preventing filename collisions when multiple users upload files with the same name.
</details>

---

**Exercise 5: Build a Complete Mini MERN Feature: React Form to Express Route to MongoDB to Display**

Build a complete "Add Note" feature that spans the entire MERN stack. Create a React form that submits a note, an Express route that saves it to MongoDB, and then display the saved note back in the UI. This exercise ties together everything from Weeks 32-36.

**Requirements:**
- React form with title and content fields
- Form validation (both fields required, title max 100 chars)
- Express POST route that validates and saves to MongoDB
- After successful save, display the new note in a list of existing notes
- Error handling at every layer
- Use AuthContext for the token

**Starter Code (React - AddNote.jsx):**

```jsx
function AddNote() {
  // TODO: Form state, validation, submit handler, notes list

  return (
    <div>
      {/* TODO: Form and notes list */}
    </div>
  );
}
```

**Starter Code (Express - noteRoutes.js):**

```js
const express = require('express');
const router = express.Router();

// TODO: Note model, routes for creating and fetching notes
```

<details>
<summary>Solution</summary>

**MongoDB Model (Note.js):**

```js
const mongoose = require('mongoose');

const noteSchema = new mongoose.Schema({
  title: {
    type: String,
    required: [true, 'Title is required'],
    trim: true,
    maxlength: [100, 'Title cannot exceed 100 characters']
  },
  content: {
    type: String,
    required: [true, 'Content is required'],
    trim: true
  },
  user: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User',
    required: true
  }
}, {
  timestamps: true  // Automatically adds createdAt and updatedAt fields
});

module.exports = mongoose.model('Note', noteSchema);
```

**Express Routes (noteRoutes.js):**

```js
const express = require('express');
const router = express.Router();
const Note = require('../models/Note');
const auth = require('../middleware/auth');

// ========================
// GET /api/notes
// ========================
// Fetch all notes for the authenticated user, sorted by newest first
router.get('/', auth, async (req, res) => {
  try {
    const notes = await Note.find({ user: req.user.userId })
      .sort({ createdAt: -1 });

    res.json({
      count: notes.length,
      notes
    });
  } catch (error) {
    console.error('Error fetching notes:', error);
    res.status(500).json({ message: 'Failed to fetch notes' });
  }
});

// ========================
// POST /api/notes
// ========================
// Create a new note for the authenticated user
router.post('/', auth, async (req, res) => {
  try {
    const { title, content } = req.body;

    // ---- Server-side validation ----
    // Even though the frontend validates, ALWAYS validate on the server too.
    // Frontend validation can be bypassed with developer tools or API clients.
    const errors = [];

    if (!title || !title.trim()) {
      errors.push('Title is required');
    } else if (title.trim().length > 100) {
      errors.push('Title cannot exceed 100 characters');
    }

    if (!content || !content.trim()) {
      errors.push('Content is required');
    }

    if (errors.length > 0) {
      return res.status(400).json({
        message: 'Validation failed',
        errors
      });
    }

    // ---- Create the note ----
    const note = await Note.create({
      title: title.trim(),
      content: content.trim(),
      user: req.user.userId
    });

    res.status(201).json({
      message: 'Note created successfully',
      note
    });
  } catch (error) {
    // Handle Mongoose validation errors (e.g., enum violations, type mismatches)
    if (error.name === 'ValidationError') {
      const messages = Object.values(error.errors).map(err => err.message);
      return res.status(400).json({
        message: 'Validation failed',
        errors: messages
      });
    }

    console.error('Error creating note:', error);
    res.status(500).json({ message: 'Failed to create note' });
  }
});

module.exports = router;
```

**React Component (AddNote.jsx):**

```jsx
import { useState, useEffect } from 'react';
import { useAuth } from '../context/AuthContext';

function AddNote() {
  // ========================
  // State
  // ========================
  const [notes, setNotes] = useState([]);           // List of all notes
  const [title, setTitle] = useState('');            // Form: title field
  const [content, setContent] = useState('');        // Form: content field
  const [errors, setErrors] = useState({});          // Form validation errors
  const [submitError, setSubmitError] = useState(''); // Server error message
  const [loading, setLoading] = useState(true);      // Loading notes
  const [submitting, setSubmitting] = useState(false); // Submitting form
  const [success, setSuccess] = useState('');         // Success message
  const { token } = useAuth();

  // ========================
  // Fetch Existing Notes
  // ========================
  useEffect(() => {
    fetchNotes();
  }, []);

  const fetchNotes = async () => {
    try {
      const response = await fetch('/api/notes', {
        headers: {
          'Authorization': `Bearer ${token}`
        }
      });

      if (!response.ok) throw new Error('Failed to fetch notes');

      const data = await response.json();
      setNotes(data.notes);
    } catch (error) {
      console.error('Error loading notes:', error);
    } finally {
      setLoading(false);
    }
  };

  // ========================
  // Client-Side Validation
  // ========================
  const validate = () => {
    const newErrors = {};

    if (!title.trim()) {
      newErrors.title = 'Title is required';
    } else if (title.trim().length > 100) {
      newErrors.title = 'Title cannot exceed 100 characters';
    }

    if (!content.trim()) {
      newErrors.content = 'Content is required';
    }

    setErrors(newErrors);
    return Object.keys(newErrors).length === 0; // Returns true if no errors
  };

  // ========================
  // Form Submit Handler
  // ========================
  const handleSubmit = async (e) => {
    e.preventDefault();
    setSubmitError('');
    setSuccess('');

    // Run client-side validation first
    if (!validate()) return;

    setSubmitting(true);

    try {
      const response = await fetch('/api/notes', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'Authorization': `Bearer ${token}`
        },
        body: JSON.stringify({
          title: title.trim(),
          content: content.trim()
        })
      });

      const data = await response.json();

      if (!response.ok) {
        // Display server validation errors or general error message
        throw new Error(data.errors?.join(', ') || data.message || 'Failed to create note');
      }

      // Success: add the new note to the top of the list
      // This avoids a full refetch - the server returns the created note
      setNotes(prevNotes => [data.note, ...prevNotes]);

      // Clear the form
      setTitle('');
      setContent('');
      setErrors({});

      // Show success message, auto-clear after 3 seconds
      setSuccess('Note created successfully!');
      setTimeout(() => setSuccess(''), 3000);
    } catch (error) {
      setSubmitError(error.message);
    } finally {
      setSubmitting(false);
    }
  };

  // ========================
  // Render
  // ========================
  return (
    <div className="max-w-4xl mx-auto px-4 py-8">
      <h1 className="text-3xl font-bold text-gray-800 mb-8">My Notes</h1>

      {/* ==================== */}
      {/* Note Creation Form   */}
      {/* ==================== */}
      <div className="bg-white rounded-lg shadow-md p-6 mb-8">
        <h2 className="text-xl font-semibold text-gray-700 mb-4">Add New Note</h2>

        <form onSubmit={handleSubmit}>
          {/* Title Field */}
          <div className="mb-4">
            <label
              htmlFor="title"
              className="block text-sm font-medium text-gray-700 mb-1"
            >
              Title
            </label>
            <input
              id="title"
              type="text"
              value={title}
              onChange={(e) => {
                setTitle(e.target.value);
                if (errors.title) setErrors(prev => ({ ...prev, title: '' }));
              }}
              placeholder="Enter note title"
              className={`w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2
                ${errors.title
                  ? 'border-red-500 focus:ring-red-300'
                  : 'border-gray-300 focus:ring-blue-300'
                }`}
              maxLength={100}
            />
            <div className="flex justify-between mt-1">
              {errors.title && (
                <span className="text-red-500 text-sm">{errors.title}</span>
              )}
              <span className="text-gray-400 text-xs ml-auto">
                {title.length}/100
              </span>
            </div>
          </div>

          {/* Content Field */}
          <div className="mb-4">
            <label
              htmlFor="content"
              className="block text-sm font-medium text-gray-700 mb-1"
            >
              Content
            </label>
            <textarea
              id="content"
              value={content}
              onChange={(e) => {
                setContent(e.target.value);
                if (errors.content) setErrors(prev => ({ ...prev, content: '' }));
              }}
              placeholder="Write your note here..."
              rows={4}
              className={`w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2
                          resize-vertical
                ${errors.content
                  ? 'border-red-500 focus:ring-red-300'
                  : 'border-gray-300 focus:ring-blue-300'
                }`}
            />
            {errors.content && (
              <span className="text-red-500 text-sm">{errors.content}</span>
            )}
          </div>

          {/* Server Error */}
          {submitError && (
            <div className="mb-4 p-3 bg-red-100 border border-red-400 text-red-700 rounded text-sm">
              {submitError}
            </div>
          )}

          {/* Success Message */}
          {success && (
            <div className="mb-4 p-3 bg-green-100 border border-green-400 text-green-700
                            rounded text-sm">
              {success}
            </div>
          )}

          {/* Submit Button */}
          <button
            type="submit"
            disabled={submitting}
            className="w-full py-2 px-4 bg-blue-500 text-white font-semibold rounded-lg
                       hover:bg-blue-600 disabled:opacity-50 disabled:cursor-not-allowed
                       transition-colors"
          >
            {submitting ? 'Saving...' : 'Save Note'}
          </button>
        </form>
      </div>

      {/* ==================== */}
      {/* Notes List            */}
      {/* ==================== */}
      <div>
        <h2 className="text-xl font-semibold text-gray-700 mb-4">
          Your Notes ({notes.length})
        </h2>

        {/* Loading State */}
        {loading && (
          <div className="text-center py-8 text-gray-500">Loading notes...</div>
        )}

        {/* Empty State */}
        {!loading && notes.length === 0 && (
          <div className="text-center py-12 bg-gray-50 rounded-lg">
            <p className="text-gray-500 text-lg">No notes yet</p>
            <p className="text-gray-400 text-sm mt-1">
              Create your first note using the form above.
            </p>
          </div>
        )}

        {/* Notes Grid */}
        {!loading && notes.length > 0 && (
          <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
            {notes.map((note) => (
              <div
                key={note._id}
                className="bg-white rounded-lg shadow-sm border border-gray-200 p-4
                           hover:shadow-md transition-shadow"
              >
                <h3 className="text-lg font-semibold text-gray-800 mb-2">
                  {note.title}
                </h3>
                <p className="text-gray-600 text-sm whitespace-pre-wrap">
                  {note.content}
                </p>
                <p className="text-xs text-gray-400 mt-3">
                  {new Date(note.createdAt).toLocaleDateString('en-US', {
                    year: 'numeric',
                    month: 'short',
                    day: 'numeric',
                    hour: '2-digit',
                    minute: '2-digit'
                  })}
                </p>
              </div>
            ))}
          </div>
        )}
      </div>
    </div>
  );
}

export default AddNote;
```

**Key concepts demonstrated (Full MERN Data Flow):**

1. **React Form with Validation**: The component manages form state with `useState` and validates input before submission. The `onChange` handlers clear field-specific errors as the user types, providing immediate feedback. The character counter on the title field guides the user before they hit the limit.

2. **HTTP Request to Express**: When the form is submitted, `fetch` sends a POST request with the note data as JSON and the JWT token in the Authorization header. The request follows the standard pattern: prevent default form behavior, validate, send request, handle response.

3. **Express Route with Server Validation**: The POST route validates the incoming data independently of the frontend. This is crucial because frontend validation can be bypassed. The route trims whitespace, checks required fields and length limits, and returns structured error messages.

4. **Mongoose to MongoDB**: The `Note.create()` method saves the document to MongoDB. Mongoose applies schema validation (required fields, maxlength, trimming) as an additional safety layer. The `timestamps: true` option automatically adds `createdAt` and `updatedAt` fields.

5. **Response Back to React**: The server responds with the created note object. React adds this note to the existing list using `setNotes(prevNotes => [data.note, ...prevNotes])`. This optimistic update avoids a full refetch, making the UI feel instant. The spread operator `...prevNotes` preserves existing notes while the new note appears at the top.

6. **Error Handling at Every Layer**: Errors are handled at four levels: client-side validation (immediate feedback), network errors (try/catch in fetch), server validation errors (400 responses with messages), and server errors (500 responses for unexpected failures). Each layer provides appropriate feedback to the user.

7. **Complete Data Flow Summary**:
   ```
   User types in form
       -> React state updates (useState)
       -> Form submitted (onSubmit)
       -> Client validation runs
       -> fetch POST /api/notes (with JWT header)
       -> Express auth middleware verifies JWT
       -> Express route validates request body
       -> Mongoose Note.create() saves to MongoDB
       -> MongoDB stores the document
       -> Express sends 201 response with the note
       -> React receives response
       -> React updates notes list (setNotes)
       -> User sees the new note in the grid
   ```
</details>
