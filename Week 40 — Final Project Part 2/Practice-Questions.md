# Week 40 — Final Course Comprehensive Review

**Total Review Questions: 20** (10 MCQs + 5 Short Answer + 5 Coding Challenges)

This final review covers the **entire 40-week course** -- from HTML fundamentals through full-stack MERN deployment. These questions test your understanding of every major topic you have studied.

---

## Part 1: Multiple Choice Questions (10 MCQs)

---

**Question 1 (HTML): Which HTML element is the correct way to define a navigation section in HTML5?**

- A) `<div id="nav">`
- B) `<navigation>`
- C) `<nav>`
- D) `<menu>`

<details>
<summary>Answer</summary>

**Correct Answer: C**

The `<nav>` element is a semantic HTML5 element specifically designed to wrap a section of navigation links. It tells browsers and screen readers that the content inside is a navigation block.

- **A** is wrong because `<div id="nav">` has no semantic meaning. It is a generic container with an arbitrary ID.
- **B** is wrong because `<navigation>` is not a valid HTML element.
- **D** is wrong because `<menu>` is designed for interactive command menus (like context menus), not page navigation.

```html
<!-- Correct usage -->
<nav>
  <a href="/">Home</a>
  <a href="/about">About</a>
  <a href="/contact">Contact</a>
</nav>
```

</details>

---

**Question 2 (CSS): What does `display: grid; grid-template-columns: repeat(3, 1fr);` do?**

- A) Creates 3 rows of equal height
- B) Creates 3 columns of equal width that share the available space
- C) Creates a single column repeated 3 times with fixed width
- D) Creates a 3x3 grid of equal cells

<details>
<summary>Answer</summary>

**Correct Answer: B**

This CSS creates a grid container with 3 columns, each taking up an equal fraction (`1fr`) of the available space.

Breaking it down:
- `display: grid` -- Makes the element a grid container.
- `grid-template-columns` -- Defines the column structure.
- `repeat(3, 1fr)` -- Shorthand for `1fr 1fr 1fr`, meaning 3 columns that each take 1 fraction of the available width.

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}

/*
Result:
+----------+----------+----------+
| Column 1 | Column 2 | Column 3 |
| (1/3)    | (1/3)    | (1/3)    |
+----------+----------+----------+
*/
```

- **A** is wrong because `grid-template-columns` defines columns, not rows. Use `grid-template-rows` for rows.
- **C** is wrong because `1fr` is a flexible unit, not a fixed width.
- **D** is wrong because this only defines columns. The number of rows depends on how many child elements exist.

</details>

---

**Question 3 (JavaScript): What is the output of the following code?**

```javascript
const fruits = ['apple', 'banana', 'cherry'];
const [first, ...rest] = fruits;
console.log(rest);
```

- A) `['apple']`
- B) `['banana', 'cherry']`
- C) `'banana'`
- D) `['apple', 'banana', 'cherry']`

<details>
<summary>Answer</summary>

**Correct Answer: B**

This uses **destructuring assignment** with the **rest operator** (`...`).

- `const [first, ...rest] = fruits;` -- Takes the first element and assigns it to `first` (`'apple'`). The `...rest` collects all remaining elements into a new array called `rest`.
- So `first` is `'apple'` and `rest` is `['banana', 'cherry']`.

```
Original array:  ['apple', 'banana', 'cherry']
                    |         |         |
                  first    ...rest (collects the rest)
                    |         |
                 'apple'   ['banana', 'cherry']
```

- **A** is wrong because `first` gets `'apple'`, not `rest`.
- **C** is wrong because the rest operator always produces an array, not a single string.
- **D** is wrong because `first` already took the first element out.

</details>

---

**Question 4 (Git): You are working on a feature branch and want to get the latest changes from `main` into your branch. Which command is the safest approach?**

- A) `git push origin main`
- B) `git merge main` (while on your feature branch)
- C) `git reset --hard main`
- D) `git checkout main`

<details>
<summary>Answer</summary>

**Correct Answer: B**

To bring the latest changes from `main` into your feature branch:

1. First, make sure `main` is up to date: `git checkout main && git pull`
2. Switch back to your feature branch: `git checkout feature-branch`
3. Merge main into your branch: `git merge main`

This preserves your feature branch work and adds the new changes from `main`.

- **A** is wrong because `git push` sends your local changes TO the remote. It does not bring changes into your branch.
- **C** is wrong because `git reset --hard main` is destructive -- it would erase all your feature branch changes and make your branch identical to `main`.
- **D** is wrong because `git checkout main` switches to the main branch but does not merge anything.

```
Before merge:
  main:     A -- B -- C
                  \
  feature:         D -- E  (your work)

After "git merge main" on feature branch:
  main:     A -- B -- C
                  \     \
  feature:         D -- E -- M  (merge commit)
```

</details>

---

**Question 5 (Tailwind CSS): What does the class `md:grid-cols-3` mean in Tailwind CSS?**

- A) Always use 3 grid columns
- B) Use 3 grid columns on medium screens (768px) and above
- C) Use 3 grid columns on screens smaller than medium
- D) Use 3 grid columns only on exactly medium-sized screens

<details>
<summary>Answer</summary>

**Correct Answer: B**

In Tailwind CSS, responsive prefixes like `md:` are **minimum-width breakpoints**. The `md:` prefix applies the style at 768px and above.

```
Tailwind Responsive Prefixes (Mobile-First):
=============================================

Default (no prefix) = 0px+     (all screens)
sm:                 = 640px+   (small screens and up)
md:                 = 768px+   (medium screens and up)
lg:                 = 1024px+  (large screens and up)
xl:                 = 1280px+  (extra large screens and up)
```

So `md:grid-cols-3` means: "Apply `grid-template-columns: repeat(3, 1fr)` when the viewport is 768px or wider."

A common pattern is:

```html
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
  <!-- 1 column on mobile, 2 on tablet, 3 on desktop -->
</div>
```

- **A** is wrong because the `md:` prefix makes it conditional, not unconditional.
- **C** is wrong because `md:` applies to screens **above** 768px, not below.
- **D** is wrong because Tailwind breakpoints are minimum-width, meaning the style applies at 768px **and larger**, not only at exactly 768px.

</details>

---

**Question 6 (React): What is the purpose of the `useEffect` cleanup function?**

```javascript
useEffect(() => {
  const timer = setInterval(() => console.log('tick'), 1000);

  return () => clearInterval(timer);  // <-- What is this?
}, []);
```

- A) It runs before the effect function executes
- B) It runs when the component unmounts or before the effect re-runs, to clean up resources
- C) It runs only when an error occurs in the effect
- D) It replaces the effect function on the second render

<details>
<summary>Answer</summary>

**Correct Answer: B**

The cleanup function (the function returned from `useEffect`) runs in two situations:

1. **When the component unmounts** (is removed from the screen)
2. **Before the effect re-runs** (if dependencies change)

Its purpose is to **clean up side effects** to prevent memory leaks. In this example, if we set up an interval timer but never clear it, the timer keeps running even after the component is gone -- consuming memory and potentially causing errors.

```
Component Lifecycle with useEffect:
=====================================

Component mounts
    |
    v
useEffect runs --> setInterval starts (tick, tick, tick...)
    |
    v
Component unmounts (user navigates away)
    |
    v
Cleanup function runs --> clearInterval stops the timer
    |
    v
No memory leak!
```

Common things to clean up:
- `clearInterval` / `clearTimeout` (timers)
- `removeEventListener` (event listeners)
- Abort fetch requests (via `AbortController`)
- Unsubscribe from WebSocket connections

</details>

---

**Question 7 (Node.js/Express): In Express, what is middleware?**

- A) A database that sits between the frontend and backend
- B) A function that has access to the request, response, and next objects, and can modify the request/response cycle
- C) A type of HTTP request method
- D) A frontend library for making API calls

<details>
<summary>Answer</summary>

**Correct Answer: B**

Middleware in Express is a function with the signature `(req, res, next)`. It sits between the incoming request and the final route handler, and can:

- **Read or modify** the request object (`req`)
- **Send a response** early (`res.json()`)
- **Pass control** to the next middleware (`next()`)

```
REQUEST FLOW THROUGH MIDDLEWARE
================================

Client Request
    |
    v
[cors()]           --> Adds CORS headers
    |
    v
[express.json()]   --> Parses JSON body into req.body
    |
    v
[protect()]        --> Checks JWT token, adds req.user
    |
    v
[Route Handler]    --> Your controller function
    |
    v
[errorHandler()]   --> Catches any errors
    |
    v
Response sent to client
```

```javascript
// Example: Custom logging middleware
const logger = (req, res, next) => {
  console.log(`${req.method} ${req.path}`);
  next();  // MUST call next() or the request hangs
};

app.use(logger);  // Applied to ALL routes
```

- **A** is wrong because middleware is a function, not a database.
- **C** is wrong because HTTP methods are GET, POST, PUT, DELETE, etc. -- middleware is not a method.
- **D** is wrong because middleware runs on the server, not the frontend.

</details>

---

**Question 8 (MongoDB): What does the following Mongoose query do?**

```javascript
const posts = await Post.find({ published: true })
  .populate('author', 'name email')
  .sort({ createdAt: -1 })
  .limit(10);
```

- A) Finds all posts, populates the author field, sorts randomly, and returns 10
- B) Finds published posts, replaces the author ObjectId with the author's name and email, sorts by newest first, and returns up to 10 results
- C) Finds 10 posts, filters by published status, and joins with the User table
- D) Creates 10 new published posts with author information

<details>
<summary>Answer</summary>

**Correct Answer: B**

Breaking down each part of the query chain:

1. `Post.find({ published: true })` -- Filters to only documents where `published` is `true`.
2. `.populate('author', 'name email')` -- The `author` field stores an ObjectId reference to a User document. `populate` replaces that ObjectId with the actual user data, but only the `name` and `email` fields (not the password or other fields).
3. `.sort({ createdAt: -1 })` -- Sorts results by `createdAt` in **descending** order (`-1` means newest first, `1` would mean oldest first).
4. `.limit(10)` -- Returns a maximum of 10 documents.

```
Before populate:
{ title: "My Post", author: "507f1f77bcf86cd799439011" }

After populate('author', 'name email'):
{ title: "My Post", author: { name: "John", email: "john@mail.com" } }
```

- **A** is wrong because `{ createdAt: -1 }` sorts by newest first, not randomly.
- **C** is wrong because MongoDB is not a relational database with "tables." It uses collections and documents. Also, `find` does not create documents.
- **D** is wrong because `find` reads documents, it does not create them.

</details>

---

**Question 9 (MERN Integration): In a MERN application, which of the following correctly describes the data flow when a user submits a contact form?**

- A) React form --> MongoDB directly --> Express processes --> Response to browser
- B) React form --> Express API endpoint --> Mongoose validates and saves to MongoDB --> Express sends response --> React updates UI
- C) React form --> Express middleware --> React Router --> MongoDB
- D) React form --> Vercel serverless function --> MongoDB Atlas

<details>
<summary>Answer</summary>

**Correct Answer: B**

The correct data flow in a MERN application follows this sequence:

```
MERN DATA FLOW: Contact Form Submission
=========================================

1. USER fills out the form in the React frontend
   |
   v
2. REACT calls: axios.post('/api/contacts', { name, email, message })
   |
   v
3. EXPRESS receives the POST request at /api/contacts route
   |
   v
4. CONTROLLER function runs: Contact.create(req.body)
   |
   v
5. MONGOOSE validates the data against the Contact schema
   |-- If validation fails: returns error to Express
   |-- If validation passes: continues
   |
   v
6. MONGODB saves the document to the "contacts" collection
   |
   v
7. MONGOOSE returns the created document to the controller
   |
   v
8. EXPRESS sends JSON response: { success: true, data: contact }
   |
   v
9. REACT receives the response and updates the UI
   (shows "Message sent successfully!")
```

- **A** is wrong because React never communicates directly with MongoDB. All database operations go through the Express backend.
- **C** is wrong because React Router handles frontend page navigation, not data flow to the database.
- **D** is wrong because in a standard MERN stack, Express on Render (or similar) handles the backend, not Vercel serverless functions.

</details>

---

**Question 10 (Deployment): Why do single-page applications (SPAs) built with React need special server configuration for routing in production?**

- A) React applications cannot be deployed to production servers
- B) React Router handles routing on the client side, but when users refresh or directly visit a URL, the server looks for a file at that path and returns 404 because the file does not exist
- C) React applications require a separate server for each route
- D) Browser security policies block React routing in production environments

<details>
<summary>Answer</summary>

**Correct Answer: B**

In a React SPA, routing is handled entirely in JavaScript by React Router. The server only has one HTML file (`index.html`). When a user navigates within the app (clicking links), React Router intercepts the navigation and renders the correct component without contacting the server.

However, when a user **refreshes the page** or **types a URL directly** (e.g., `yoursite.com/blog/123`), the browser sends a request to the server for `/blog/123`. The server looks for a file or folder called `/blog/123`, cannot find one, and returns a 404 error.

The fix is to configure the server to serve `index.html` for ALL routes, letting React Router handle the routing client-side.

```
THE SPA ROUTING PROBLEM
========================

User visits: yoursite.com/blog/123

WITHOUT server configuration:
  Server looks for: /blog/123/index.html
  Server response: 404 NOT FOUND (file does not exist)

WITH server configuration (rewrites):
  Server sees: /blog/123
  Server serves: /index.html (for ALL routes)
  React Router reads URL: /blog/123
  React Router renders: <SinglePost id="123" />

Vercel fix (vercel.json):
  { "rewrites": [{ "source": "/(.*)", "destination": "/index.html" }] }
```

- **A** is wrong because React apps are deployed to production all the time.
- **C** is wrong because SPAs are specifically designed to run on a single server with a single entry point.
- **D** is wrong because browser security policies do not interfere with client-side routing.

</details>

---

## Part 2: Short Answer Questions (5 Questions)

---

**Question 11: Explain the complete data flow when a logged-in user creates a new blog post in a MERN application. Trace the journey from the form submission to the data appearing on the blog page.**

<details>
<summary>Answer</summary>

The complete data flow for creating a blog post involves six stages across three layers (frontend, backend, database):

**Stage 1 -- User Interaction (Frontend)**
The admin fills out the blog post form (title, content, tags, image URL) and clicks "Create Post." The React component calls the `createPost` service function.

**Stage 2 -- API Request (Frontend to Backend)**
The service function uses Axios to send a POST request to `/api/posts`. The Axios interceptor automatically attaches the JWT token from localStorage to the `Authorization` header: `Bearer <token>`.

**Stage 3 -- Authentication (Backend)**
Express routes the request to `postRoutes.js`, which passes it through the `protect` middleware. The middleware extracts the token, verifies it with `jwt.verify()`, finds the user in the database by the decoded ID, and attaches the user object to `req.user`. If the token is invalid or missing, a 401 response is returned and the request stops here.

**Stage 4 -- Business Logic (Backend)**
The `createPost` controller function runs. It adds `req.user._id` as the `author` field, then calls `Post.create(req.body)`. Mongoose validates the data against the Post schema (required fields, type checks, max lengths). If validation fails, an error is thrown and caught by the error handler middleware.

**Stage 5 -- Database (MongoDB)**
Mongoose converts the JavaScript object to BSON and sends an insert operation to MongoDB. MongoDB stores the document in the `posts` collection and returns the created document with a generated `_id` and timestamps.

**Stage 6 -- Response and UI Update (Backend to Frontend)**
Express sends a 201 JSON response with the created post data. React receives the response, and the component either navigates to the blog page or refreshes the post list. When a visitor navigates to the blog page, React calls `GET /api/posts?published=true`, and the new post (if published) appears in the list.

```
Form Submit --> Axios POST /api/posts (with JWT)
  --> Express Router --> protect middleware (verify JWT)
  --> createPost controller --> Post.create() --> Mongoose validation
  --> MongoDB insert --> Document saved
  --> 201 Response --> React updates UI --> Post visible on blog
```

</details>

---

**Question 12: Describe the authentication flow in a MERN application. How does a user log in, how is their session maintained, and how are protected routes secured?**

<details>
<summary>Answer</summary>

Authentication in a MERN application uses **JWT (JSON Web Tokens)** and follows three phases:

**Phase 1 -- Login**
The user submits their email and password via a login form. React sends a POST request to `/api/auth/login`. The Express controller finds the user by email, uses `bcrypt.compare()` to check the entered password against the stored hash, and if they match, generates a JWT using `jwt.sign({ id: user._id }, JWT_SECRET, { expiresIn: '30d' })`. The token and user data are sent back in the response.

**Phase 2 -- Session Maintenance**
React stores the JWT token and user object in `localStorage`. The `AuthContext` reads from localStorage on app load to restore the session. An Axios request interceptor automatically attaches the token to every API request as `Authorization: Bearer <token>`. This means the user stays "logged in" across page refreshes and browser sessions until the token expires or they manually log out.

**Phase 3 -- Route Protection**
On the backend, protected routes use the `protect` middleware. This middleware extracts the token from the Authorization header, verifies it with `jwt.verify()`, and finds the associated user. If the token is missing, expired, or invalid, a 401 response is returned. On the frontend, a `ProtectedRoute` component checks the AuthContext for a logged-in user. If no user exists, it redirects to the login page using `<Navigate to="/login" />`.

Logout clears the token and user from localStorage and resets the AuthContext state. Since JWTs are stateless (the server does not store sessions), logging out is purely a client-side action.

</details>

---

**Question 13: Explain your approach to making a web application responsive. What strategy do you follow, what tools do you use, and how do you test responsiveness?**

<details>
<summary>Answer</summary>

The approach to responsive design follows the **mobile-first** strategy:

**Strategy: Mobile-First Design**
Start by designing for the smallest screen (320px), then progressively add layout complexity for larger screens. This ensures the core content and functionality work on every device, and larger screens get enhanced layouts rather than degraded ones.

**Tools:**
1. **Tailwind CSS responsive prefixes** -- Use `md:`, `lg:`, `xl:` prefixes to apply styles at specific breakpoints. For example: `class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3"` starts with 1 column on mobile, 2 on tablets, and 3 on desktops.
2. **Flexbox and CSS Grid** -- Flexbox for one-dimensional layouts (navbar items, card rows). Grid for two-dimensional layouts (project grids, dashboard panels).
3. **Relative units** -- Use `rem`, `em`, `%`, and `vw/vh` instead of fixed `px` values for fonts and spacing. Tailwind handles this by default.
4. **Viewport meta tag** -- `<meta name="viewport" content="width=device-width, initial-scale=1.0">` ensures proper scaling on mobile devices.

**Testing:**
1. **Chrome DevTools Device Toolbar** (F12 > toggle device icon) -- Simulate specific devices (iPhone, iPad, etc.) and test at arbitrary widths.
2. **Test at three key widths** -- 390px (mobile), 768px (tablet), and 1280px (desktop).
3. **Check for:** horizontal scrollbars, overlapping text, unreadable fonts, untappable buttons (minimum 44x44px), images that overflow their containers, and navigation that works at all sizes.
4. **Test on a real mobile device** if possible -- emulators do not always catch touch-specific issues.

</details>

---

**Question 14: You are designing a REST API for a bookstore application. Define 5 endpoints for managing books, following RESTful conventions. Include the HTTP method, route, request body (if applicable), and response.**

<details>
<summary>Answer</summary>

Here are 5 RESTful endpoints for a bookstore API:

**1. GET /api/books -- List all books**
- Request body: None
- Query parameters: `?genre=fiction&page=1&limit=10`
- Response (200): `{ "success": true, "data": [{ "_id": "...", "title": "The Great Gatsby", "author": "F. Scott Fitzgerald", "genre": "fiction", "price": 12.99, "inStock": true }], "pagination": { "page": 1, "pages": 5, "total": 48 } }`

**2. GET /api/books/:id -- Get a single book**
- Request body: None
- Response (200): `{ "success": true, "data": { "_id": "...", "title": "The Great Gatsby", "author": "F. Scott Fitzgerald", "genre": "fiction", "price": 12.99, "isbn": "978-0743273565", "description": "...", "inStock": true } }`
- Response (404): `{ "success": false, "message": "Book not found" }`

**3. POST /api/books -- Create a new book** (requires authentication)
- Request body: `{ "title": "New Book", "author": "Author Name", "genre": "fiction", "price": 15.99, "isbn": "978-...", "description": "A great book", "inStock": true }`
- Response (201): `{ "success": true, "data": { "_id": "...", ...createdBook } }`
- Response (400): `{ "success": false, "message": "Title is required" }`

**4. PUT /api/books/:id -- Update an existing book** (requires authentication)
- Request body: `{ "price": 10.99, "inStock": false }` (partial update)
- Response (200): `{ "success": true, "data": { ...updatedBook } }`
- Response (404): `{ "success": false, "message": "Book not found" }`

**5. DELETE /api/books/:id -- Delete a book** (requires authentication)
- Request body: None
- Response (200): `{ "success": true, "message": "Book deleted successfully" }`
- Response (404): `{ "success": false, "message": "Book not found" }`

Key RESTful conventions followed: resource-based URLs (nouns, not verbs), HTTP methods indicate the action, consistent response format, proper status codes (200, 201, 400, 404), and stateless authentication via JWT.

</details>

---

**Question 15: You need to deploy a MERN application. Describe your deployment strategy, including where you would host each part, what environment variables you need, and what could go wrong.**

<details>
<summary>Answer</summary>

**Deployment Architecture:**

The application has three components that need separate hosting:

1. **Frontend (React)** -- Deploy to **Vercel**. Vercel is optimized for frontend frameworks, provides automatic HTTPS, global CDN, and zero-configuration deployment for Vite/React projects. Configure `vercel.json` with rewrites to handle client-side routing.

2. **Backend (Express/Node.js)** -- Deploy to **Render**. Render provides free tier hosting for Node.js web services, automatic deploys from GitHub, and built-in HTTPS. Set the start command to `node server.js` and the build command to `npm install`.

3. **Database (MongoDB)** -- Use **MongoDB Atlas** (managed cloud database). Create a production cluster, configure network access to allow connections from Render (0.0.0.0/0 for free tier), and create a database user with read/write permissions.

**Environment Variables:**

Backend (set in Render dashboard):
- `MONGO_URI` -- MongoDB Atlas connection string
- `JWT_SECRET` -- A long, random, secret string for signing tokens
- `JWT_EXPIRE` -- Token expiration (e.g., `30d`)
- `CLIENT_URL` -- The Vercel frontend URL (for CORS)
- `PORT` -- Usually set automatically by Render

Frontend (set in Vercel dashboard):
- `VITE_API_URL` -- The Render backend URL (e.g., `https://api.onrender.com/api`)

**What Could Go Wrong:**

1. **CORS errors** -- The backend must explicitly allow the frontend's production domain. Set `cors({ origin: process.env.CLIENT_URL })`.
2. **Environment variables not set** -- If `MONGO_URI` is missing in production, the app crashes on startup. Double-check every variable in the hosting dashboard.
3. **404 on page refresh** -- Without the `vercel.json` rewrites configuration, React Router routes return 404 when accessed directly.
4. **Mixed content errors** -- If the frontend is on HTTPS but the API URL uses HTTP, the browser blocks the requests. Ensure both use HTTPS.
5. **Cold starts on free tier** -- Render free tier services spin down after inactivity. The first request after inactivity may take 30-60 seconds. This is normal for free hosting.
6. **MongoDB Atlas IP whitelist** -- If network access is not set to allow all IPs (0.0.0.0/0), Render cannot connect to the database.

</details>

---

## Part 3: Coding Challenges (5 Challenges)

---

**Challenge 1 (HTML): Build a Registration Form**

Create an HTML registration form with the following fields: full name, email, password, confirm password, date of birth (date picker), gender (radio buttons: Male, Female, Other), agree to terms (checkbox), and a submit button. Use proper semantic HTML with labels and fieldsets.

<details>
<summary>Answer</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Registration Form</title>
</head>
<body>

  <main>
    <h1>Create Your Account</h1>

    <form action="/api/auth/register" method="POST" id="registerForm">

      <!-- Personal Information -->
      <fieldset>
        <legend>Personal Information</legend>

        <div>
          <label for="fullName">Full Name:</label>
          <input type="text" id="fullName" name="fullName"
                 placeholder="John Doe" required minlength="2" maxlength="50">
        </div>

        <div>
          <label for="email">Email Address:</label>
          <input type="email" id="email" name="email"
                 placeholder="john@example.com" required>
        </div>

        <div>
          <label for="dob">Date of Birth:</label>
          <input type="date" id="dob" name="dob" required>
        </div>

        <div>
          <label>Gender:</label>
          <input type="radio" id="male" name="gender" value="male">
          <label for="male">Male</label>

          <input type="radio" id="female" name="gender" value="female">
          <label for="female">Female</label>

          <input type="radio" id="other" name="gender" value="other">
          <label for="other">Other</label>
        </div>
      </fieldset>

      <!-- Security -->
      <fieldset>
        <legend>Security</legend>

        <div>
          <label for="password">Password:</label>
          <input type="password" id="password" name="password"
                 required minlength="6" placeholder="At least 6 characters">
        </div>

        <div>
          <label for="confirmPassword">Confirm Password:</label>
          <input type="password" id="confirmPassword" name="confirmPassword"
                 required minlength="6" placeholder="Re-enter your password">
        </div>
      </fieldset>

      <!-- Terms -->
      <div>
        <input type="checkbox" id="terms" name="terms" required>
        <label for="terms">I agree to the Terms and Conditions</label>
      </div>

      <button type="submit">Create Account</button>

    </form>
  </main>

</body>
</html>
```

Key HTML best practices demonstrated:
- **Semantic elements:** `<main>`, `<form>`, `<fieldset>`, `<legend>`
- **Accessible labels:** Every input has a `<label>` with matching `for`/`id` attributes
- **Input types:** `text`, `email`, `date`, `password`, `radio`, `checkbox` -- each provides appropriate browser behavior and mobile keyboards
- **Validation attributes:** `required`, `minlength`, `maxlength`, `type="email"` for built-in browser validation
- **Logical grouping:** Related fields are grouped with `<fieldset>` and `<legend>`

</details>

---

**Challenge 2 (Tailwind CSS): Style the Registration Form**

Using Tailwind CSS utility classes, style the registration form from Challenge 1 to be responsive, modern, and professional. The form should be centered, have a card-like appearance, and work on both mobile and desktop.

<details>
<summary>Answer</summary>

```html
<div class="min-h-screen bg-gray-100 dark:bg-gray-900 flex items-center justify-center px-4 py-8">

  <div class="w-full max-w-md bg-white dark:bg-gray-800 rounded-xl shadow-lg p-8">

    <h1 class="text-2xl font-bold text-center text-gray-800 dark:text-white mb-6">
      Create Your Account
    </h1>

    <form id="registerForm" class="space-y-5">

      <!-- Personal Information -->
      <fieldset class="space-y-4">
        <legend class="text-lg font-semibold text-gray-700 dark:text-gray-300 mb-2">
          Personal Information
        </legend>

        <div>
          <label for="fullName"
                 class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">
            Full Name
          </label>
          <input type="text" id="fullName" name="fullName"
                 placeholder="John Doe" required minlength="2"
                 class="w-full px-4 py-2 border border-gray-300 dark:border-gray-600
                        rounded-lg bg-white dark:bg-gray-700 text-gray-900 dark:text-white
                        focus:ring-2 focus:ring-blue-500 focus:border-transparent
                        outline-none transition">
        </div>

        <div>
          <label for="email"
                 class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">
            Email Address
          </label>
          <input type="email" id="email" name="email"
                 placeholder="john@example.com" required
                 class="w-full px-4 py-2 border border-gray-300 dark:border-gray-600
                        rounded-lg bg-white dark:bg-gray-700 text-gray-900 dark:text-white
                        focus:ring-2 focus:ring-blue-500 focus:border-transparent
                        outline-none transition">
        </div>

        <div>
          <label for="dob"
                 class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">
            Date of Birth
          </label>
          <input type="date" id="dob" name="dob" required
                 class="w-full px-4 py-2 border border-gray-300 dark:border-gray-600
                        rounded-lg bg-white dark:bg-gray-700 text-gray-900 dark:text-white
                        focus:ring-2 focus:ring-blue-500 focus:border-transparent
                        outline-none transition">
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">
            Gender
          </label>
          <div class="flex gap-6">
            <label class="flex items-center gap-2 cursor-pointer">
              <input type="radio" name="gender" value="male"
                     class="w-4 h-4 text-blue-600">
              <span class="text-gray-700 dark:text-gray-300">Male</span>
            </label>
            <label class="flex items-center gap-2 cursor-pointer">
              <input type="radio" name="gender" value="female"
                     class="w-4 h-4 text-blue-600">
              <span class="text-gray-700 dark:text-gray-300">Female</span>
            </label>
            <label class="flex items-center gap-2 cursor-pointer">
              <input type="radio" name="gender" value="other"
                     class="w-4 h-4 text-blue-600">
              <span class="text-gray-700 dark:text-gray-300">Other</span>
            </label>
          </div>
        </div>
      </fieldset>

      <!-- Security -->
      <fieldset class="space-y-4">
        <legend class="text-lg font-semibold text-gray-700 dark:text-gray-300 mb-2">
          Security
        </legend>

        <div>
          <label for="password"
                 class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">
            Password
          </label>
          <input type="password" id="password" name="password"
                 required minlength="6" placeholder="At least 6 characters"
                 class="w-full px-4 py-2 border border-gray-300 dark:border-gray-600
                        rounded-lg bg-white dark:bg-gray-700 text-gray-900 dark:text-white
                        focus:ring-2 focus:ring-blue-500 focus:border-transparent
                        outline-none transition">
        </div>

        <div>
          <label for="confirmPassword"
                 class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">
            Confirm Password
          </label>
          <input type="password" id="confirmPassword" name="confirmPassword"
                 required minlength="6" placeholder="Re-enter your password"
                 class="w-full px-4 py-2 border border-gray-300 dark:border-gray-600
                        rounded-lg bg-white dark:bg-gray-700 text-gray-900 dark:text-white
                        focus:ring-2 focus:ring-blue-500 focus:border-transparent
                        outline-none transition">
        </div>
      </fieldset>

      <!-- Terms -->
      <div class="flex items-center gap-2">
        <input type="checkbox" id="terms" name="terms" required
               class="w-4 h-4 text-blue-600 rounded">
        <label for="terms" class="text-sm text-gray-600 dark:text-gray-400">
          I agree to the <a href="#" class="text-blue-600 hover:underline">Terms and Conditions</a>
        </label>
      </div>

      <!-- Submit Button -->
      <button type="submit"
              class="w-full bg-blue-600 hover:bg-blue-700 text-white font-semibold
                     py-3 rounded-lg transition duration-200
                     focus:ring-4 focus:ring-blue-300 dark:focus:ring-blue-800">
        Create Account
      </button>

    </form>

    <p class="text-center text-sm text-gray-500 dark:text-gray-400 mt-4">
      Already have an account?
      <a href="/login" class="text-blue-600 hover:underline">Log in</a>
    </p>

  </div>
</div>
```

Key Tailwind techniques demonstrated:
- **Centering:** `flex items-center justify-center min-h-screen` centers the card on the page
- **Card design:** `bg-white rounded-xl shadow-lg p-8` creates a floating card effect
- **Dark mode:** `dark:bg-gray-800`, `dark:text-white` classes toggle with system preference
- **Form inputs:** Consistent styling with `w-full px-4 py-2 border rounded-lg` and focus states using `focus:ring-2 focus:ring-blue-500`
- **Spacing:** `space-y-5` and `space-y-4` for consistent vertical spacing
- **Responsive:** `max-w-md` constrains width on desktop while `w-full px-4` ensures full width on mobile
- **Transitions:** `transition duration-200` for smooth hover and focus effects

</details>

---

**Challenge 3 (JavaScript): Add Client-Side Validation**

Write a JavaScript validation function for the registration form. It should validate: name is at least 2 characters, email has a valid format, password is at least 6 characters, confirm password matches password, date of birth makes the user at least 13 years old, and terms checkbox is checked. Display error messages next to each invalid field.

<details>
<summary>Answer</summary>

```javascript
// Form validation for the registration form

function validateForm(event) {
  event.preventDefault();  // Prevent form submission

  // Clear all previous error messages
  clearErrors();

  // Get form values
  const name = document.getElementById('fullName').value.trim();
  const email = document.getElementById('email').value.trim();
  const password = document.getElementById('password').value;
  const confirmPassword = document.getElementById('confirmPassword').value;
  const dob = document.getElementById('dob').value;
  const terms = document.getElementById('terms').checked;

  let isValid = true;  // Track overall form validity

  // 1. Validate name (at least 2 characters)
  if (name.length < 2) {
    showError('fullName', 'Name must be at least 2 characters long');
    isValid = false;
  }

  // 2. Validate email format
  const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!emailPattern.test(email)) {
    showError('email', 'Please enter a valid email address');
    isValid = false;
  }

  // 3. Validate password (at least 6 characters)
  if (password.length < 6) {
    showError('password', 'Password must be at least 6 characters long');
    isValid = false;
  }

  // 4. Validate confirm password (must match password)
  if (password !== confirmPassword) {
    showError('confirmPassword', 'Passwords do not match');
    isValid = false;
  }

  // 5. Validate date of birth (user must be at least 13 years old)
  if (dob) {
    const birthDate = new Date(dob);
    const today = new Date();
    const age = today.getFullYear() - birthDate.getFullYear();
    const monthDiff = today.getMonth() - birthDate.getMonth();

    // Adjust age if birthday has not occurred yet this year
    const adjustedAge = (monthDiff < 0 ||
      (monthDiff === 0 && today.getDate() < birthDate.getDate()))
      ? age - 1
      : age;

    if (adjustedAge < 13) {
      showError('dob', 'You must be at least 13 years old to register');
      isValid = false;
    }
  } else {
    showError('dob', 'Date of birth is required');
    isValid = false;
  }

  // 6. Validate terms checkbox
  if (!terms) {
    showError('terms', 'You must agree to the Terms and Conditions');
    isValid = false;
  }

  // If all validations pass, submit the form
  if (isValid) {
    console.log('Form is valid! Submitting...');
    console.log({ name, email, password, dob, terms });

    // In a real app, you would send this data to the backend:
    // fetch('/api/auth/register', {
    //   method: 'POST',
    //   headers: { 'Content-Type': 'application/json' },
    //   body: JSON.stringify({ name, email, password, dob })
    // });

    alert('Registration successful!');
  }

  return isValid;
}

// Display an error message below a specific field
function showError(fieldId, message) {
  const field = document.getElementById(fieldId);
  const errorElement = document.createElement('p');

  errorElement.textContent = message;
  errorElement.className = 'error-message';
  errorElement.style.color = '#dc2626';       // Red text
  errorElement.style.fontSize = '0.875rem';   // Small text
  errorElement.style.marginTop = '4px';

  // Add red border to the field
  field.style.borderColor = '#dc2626';

  // Insert the error message after the field
  field.parentNode.appendChild(errorElement);
}

// Clear all error messages and red borders
function clearErrors() {
  // Remove all error message elements
  const errors = document.querySelectorAll('.error-message');
  errors.forEach(error => error.remove());

  // Reset border colors on all inputs
  const inputs = document.querySelectorAll('input');
  inputs.forEach(input => {
    input.style.borderColor = '';
  });
}

// Attach the validation function to the form
document.getElementById('registerForm').addEventListener('submit', validateForm);
```

Key concepts demonstrated:
- **`event.preventDefault()`** stops the form from submitting and reloading the page
- **Regular expression** (`/^[^\s@]+@[^\s@]+\.[^\s@]+$/`) for email validation
- **Date arithmetic** to calculate age from date of birth, including month/day adjustment
- **DOM manipulation** to dynamically create and insert error messages
- **Clearing previous errors** before re-validating to prevent duplicate messages
- **Separation of concerns** with helper functions (`showError`, `clearErrors`)

</details>

---

**Challenge 4 (Express): Create a Complete REST Endpoint**

Write an Express.js endpoint for a `GET /api/books` route that: accepts query parameters for `genre`, `page`, and `limit`; queries MongoDB using Mongoose; returns paginated results sorted by newest first; includes pagination metadata in the response; and handles errors gracefully.

<details>
<summary>Answer</summary>

```javascript
// server/models/Book.js
const mongoose = require('mongoose');

const bookSchema = new mongoose.Schema({
  title: {
    type: String,
    required: [true, 'Book title is required'],
    trim: true
  },
  author: {
    type: String,
    required: [true, 'Author name is required'],
    trim: true
  },
  genre: {
    type: String,
    required: true,
    enum: ['fiction', 'non-fiction', 'science', 'technology', 'history', 'biography'],
    lowercase: true
  },
  price: {
    type: Number,
    required: true,
    min: [0, 'Price cannot be negative']
  },
  isbn: {
    type: String,
    unique: true
  },
  description: String,
  inStock: {
    type: Boolean,
    default: true
  }
}, { timestamps: true });

module.exports = mongoose.model('Book', bookSchema);


// server/controllers/bookController.js
const Book = require('../models/Book');

const getBooks = async (req, res) => {
  try {
    // Extract and parse query parameters with defaults
    const {
      genre,
      page = 1,
      limit = 10,
      sortBy = 'createdAt',
      order = 'desc'
    } = req.query;

    // Validate pagination values
    const pageNum = Math.max(1, parseInt(page));           // Minimum page 1
    const limitNum = Math.min(50, Math.max(1, parseInt(limit))); // Between 1 and 50

    // Build the query filter
    const filter = {};
    if (genre) {
      filter.genre = genre.toLowerCase();
    }

    // Build the sort object
    const sortOrder = order === 'asc' ? 1 : -1;
    const sortObj = { [sortBy]: sortOrder };

    // Calculate skip value for pagination
    const skip = (pageNum - 1) * limitNum;

    // Execute query and count in parallel for better performance
    const [books, totalCount] = await Promise.all([
      Book.find(filter)
        .sort(sortObj)
        .skip(skip)
        .limit(limitNum)
        .select('-__v'),    // Exclude the __v field from results
      Book.countDocuments(filter)
    ]);

    // Calculate pagination metadata
    const totalPages = Math.ceil(totalCount / limitNum);

    // Send response
    res.status(200).json({
      success: true,
      data: books,
      pagination: {
        currentPage: pageNum,
        totalPages: totalPages,
        totalItems: totalCount,
        itemsPerPage: limitNum,
        hasNextPage: pageNum < totalPages,
        hasPrevPage: pageNum > 1
      }
    });

  } catch (error) {
    // Handle specific Mongoose errors
    if (error.name === 'CastError') {
      return res.status(400).json({
        success: false,
        message: 'Invalid query parameter format'
      });
    }

    // Generic server error
    console.error('Error in getBooks:', error.message);
    res.status(500).json({
      success: false,
      message: 'An error occurred while fetching books'
    });
  }
};

module.exports = { getBooks };


// server/routes/bookRoutes.js
const express = require('express');
const router = express.Router();
const { getBooks } = require('../controllers/bookController');

router.get('/', getBooks);

module.exports = router;


// Usage in server.js:
// app.use('/api/books', require('./routes/bookRoutes'));
```

**Example API calls and responses:**

```
GET /api/books
--> Returns first 10 books, sorted by newest

GET /api/books?genre=fiction&page=2&limit=5
--> Returns books 6-10 in the fiction genre

GET /api/books?sortBy=price&order=asc&limit=20
--> Returns 20 cheapest books

Response:
{
  "success": true,
  "data": [
    {
      "_id": "64a...",
      "title": "The Great Gatsby",
      "author": "F. Scott Fitzgerald",
      "genre": "fiction",
      "price": 12.99,
      "inStock": true,
      "createdAt": "2026-01-15T10:30:00Z"
    }
  ],
  "pagination": {
    "currentPage": 1,
    "totalPages": 5,
    "totalItems": 48,
    "itemsPerPage": 10,
    "hasNextPage": true,
    "hasPrevPage": false
  }
}
```

Key concepts demonstrated:
- **Query parameter parsing** with defaults and validation
- **Dynamic filter building** based on optional parameters
- **Parallel queries** with `Promise.all` for better performance
- **Pagination metadata** with helper booleans (`hasNextPage`, `hasPrevPage`)
- **Error handling** with specific Mongoose error types
- **Input sanitization** (clamping limit between 1-50, ensuring page >= 1)
- **Clean response format** with consistent `success` and `data` structure

</details>

---

**Challenge 5 (Mongoose): Write Complex Database Queries**

Write Mongoose queries for the following scenarios using a `Post` model with fields: `title`, `content`, `author` (ObjectId ref), `tags` (array), `published` (boolean), `views` (number), `createdAt` (date). Write queries to: (a) find the 5 most viewed published posts, (b) find all posts by a specific author that contain a specific tag, (c) update the view count of a post by incrementing it by 1, (d) find posts created in the last 7 days, and (e) get the total number of posts and average views grouped by each tag.

<details>
<summary>Answer</summary>

```javascript
const mongoose = require('mongoose');
const Post = require('./models/Post');

// ============================================
// (a) Find the 5 most viewed published posts
// ============================================
const getTopPosts = async () => {
  const topPosts = await Post.find({ published: true })
    .sort({ views: -1 })        // Sort by views descending (highest first)
    .limit(5)                    // Return only 5 results
    .populate('author', 'name')  // Include author's name
    .select('title views tags createdAt');  // Only return these fields

  return topPosts;
};

// Result example:
// [
//   { title: "React Hooks Guide", views: 1523, tags: ["react"], ... },
//   { title: "CSS Grid Tutorial", views: 982, tags: ["css"], ... },
//   ...
// ]


// ============================================
// (b) Find all posts by a specific author
//     that contain a specific tag
// ============================================
const getPostsByAuthorAndTag = async (authorId, tag) => {
  const posts = await Post.find({
    author: authorId,            // Match the author's ObjectId
    tags: tag,                   // MongoDB checks if the array contains this value
    published: true              // Only published posts
  })
    .sort({ createdAt: -1 })     // Newest first
    .populate('author', 'name email');

  return posts;
};

// Usage: getPostsByAuthorAndTag('507f1f77bcf86cd799439011', 'javascript')
// Finds all published posts by that author tagged with "javascript"


// ============================================
// (c) Increment the view count by 1
//     (atomic operation -- safe for concurrent requests)
// ============================================
const incrementViews = async (postId) => {
  const updatedPost = await Post.findByIdAndUpdate(
    postId,
    { $inc: { views: 1 } },     // $inc atomically increments the field
    { new: true }                // Return the updated document
  );

  return updatedPost;
};

// Why $inc instead of reading, adding 1, and saving?
// $inc is ATOMIC -- if 100 users view the post simultaneously,
// each increment happens safely. With read-modify-write, some
// increments could be lost (race condition).


// ============================================
// (d) Find posts created in the last 7 days
// ============================================
const getRecentPosts = async () => {
  const sevenDaysAgo = new Date();
  sevenDaysAgo.setDate(sevenDaysAgo.getDate() - 7);

  const recentPosts = await Post.find({
    createdAt: { $gte: sevenDaysAgo },  // $gte = greater than or equal
    published: true
  })
    .sort({ createdAt: -1 })
    .populate('author', 'name');

  return recentPosts;
};

// $gte: sevenDaysAgo means "createdAt >= 7 days ago"
// Other date operators: $gt (after), $lt (before), $lte (before or on)


// ============================================
// (e) Get total posts and average views
//     grouped by each tag
// ============================================
const getStatsByTag = async () => {
  const stats = await Post.aggregate([
    // Stage 1: Only include published posts
    { $match: { published: true } },

    // Stage 2: Unwind the tags array
    // If a post has tags: ["react", "javascript"],
    // it creates 2 documents -- one for each tag
    { $unwind: '$tags' },

    // Stage 3: Group by tag and calculate stats
    {
      $group: {
        _id: '$tags',                              // Group by tag name
        totalPosts: { $sum: 1 },                   // Count posts per tag
        averageViews: { $avg: '$views' },          // Average views per tag
        totalViews: { $sum: '$views' },            // Total views per tag
        mostViewed: { $max: '$views' }             // Highest view count
      }
    },

    // Stage 4: Sort by total posts descending
    { $sort: { totalPosts: -1 } },

    // Stage 5: Rename _id to "tag" for cleaner output
    {
      $project: {
        _id: 0,
        tag: '$_id',
        totalPosts: 1,
        averageViews: { $round: ['$averageViews', 0] },  // Round to integer
        totalViews: 1,
        mostViewed: 1
      }
    }
  ]);

  return stats;
};

// Result example:
// [
//   { tag: "react", totalPosts: 15, averageViews: 342, totalViews: 5130, mostViewed: 1523 },
//   { tag: "javascript", totalPosts: 12, averageViews: 287, totalViews: 3444, mostViewed: 982 },
//   { tag: "css", totalPosts: 8, averageViews: 198, totalViews: 1584, mostViewed: 654 },
//   ...
// ]
```

Key Mongoose/MongoDB concepts demonstrated:

- **Query chaining:** `.find().sort().limit().populate().select()` -- each method narrows or shapes the query
- **Array field matching:** `{ tags: "javascript" }` automatically checks if the array contains the value
- **Atomic operations:** `$inc` safely increments a counter without race conditions
- **Date comparisons:** `$gte` with a calculated date for time-based filtering
- **Aggregation pipeline:** Multi-stage data transformation with `$match`, `$unwind`, `$group`, `$sort`, `$project`
- **`$unwind`:** Flattens arrays so each array element becomes its own document -- essential for grouping by array values
- **Population:** Replacing ObjectId references with actual document data from related collections

</details>

---

## Final Score

**Total Questions: 20**

| Section | Questions | Your Score |
|---------|-----------|------------|
| Multiple Choice (MCQs) | 10 | ___ / 10 |
| Short Answer | 5 | ___ / 5 |
| Coding Challenges | 5 | ___ / 5 |
| **Total** | **20** | **___ / 20** |

### Scoring Guide

| Score | Rating | What It Means |
|-------|--------|---------------|
| 18-20 | Excellent | You have mastered the full-stack curriculum. You are ready for professional work. |
| 14-17 | Good | Strong understanding with a few gaps. Review the topics where you struggled. |
| 10-13 | Fair | You understand the fundamentals but need more practice with advanced concepts. |
| Below 10 | Needs Review | Go back and review the weekly notes for the topics you missed. Focus on building more projects. |

---

*Congratulations on completing the 40-week Full-Stack Web Development Course! You are now a MERN developer.*
