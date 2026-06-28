# Week 32 — MERN Stack Integration: Practice Questions

**Total Questions: 20** (10 MCQs + 5 Short Answer + 5 Coding Exercises)

---

## Part 1: Multiple Choice Questions (MCQs)

**1. What does MERN stand for?**

- A) MongoDB, Express, React, Next.js
- B) MongoDB, Express, React, Node.js
- C) MySQL, Express, React, Node.js
- D) MongoDB, Ember, React, Node.js

<details>
<summary>Answer</summary>

**B) MongoDB, Express, React, Node.js**

MERN is a popular full-stack JavaScript technology stack used for building modern web applications. MongoDB serves as the NoSQL database for storing data, Express.js is the back-end web application framework that runs on Node.js, React is the front-end library for building user interfaces, and Node.js is the JavaScript runtime environment that allows JavaScript to run on the server side. The key advantage of the MERN stack is that it uses JavaScript across the entire application, from front-end to back-end to database queries, which simplifies development and allows developers to work across the full stack with a single programming language.

</details>

---

**2. What is the primary purpose of CORS (Cross-Origin Resource Sharing)?**

- A) To encrypt data sent between the client and server
- B) To allow or restrict web pages from making requests to a different domain
- C) To compress HTTP responses for faster loading
- D) To cache API responses in the browser

<details>
<summary>Answer</summary>

**B) To allow or restrict web pages from making requests to a different domain**

CORS is a security mechanism implemented by web browsers that controls how web pages in one domain can request resources from another domain. By default, browsers enforce the Same-Origin Policy, which prevents a web page from making requests to a different origin (a combination of protocol, domain, and port). In a MERN stack application, the React front-end typically runs on a different port (such as port 5173 for Vite) than the Express back-end (such as port 5000), which means they are considered different origins. Without proper CORS configuration on the server, the browser will block these cross-origin requests. CORS headers, such as `Access-Control-Allow-Origin`, tell the browser which origins are permitted to access the server's resources.

</details>

---

**3. What is the default development server port for a Vite-based React application?**

- A) 3000
- B) 8080
- C) 5173
- D) 4200

<details>
<summary>Answer</summary>

**C) 5173**

When you create a React application using Vite (with a command like `npm create vite@latest`), the development server starts on port 5173 by default. This is different from Create React App, which uses port 3000 by default. Vite chose port 5173 because the digits spell out "VITE" on a phone keypad. Understanding the default ports is important in full-stack development because you need to configure CORS and proxy settings correctly to allow your front-end and back-end to communicate during development. You can change the default port in the `vite.config.js` file by adding a `server.port` option if needed.

</details>

---

**4. What is a key advantage of using Axios over the native Fetch API?**

- A) Axios is built into all browsers by default
- B) Axios automatically transforms JSON data and provides built-in request/response interceptors
- C) Axios is faster than Fetch because it uses WebSockets
- D) Axios does not require any installation or configuration

<details>
<summary>Answer</summary>

**B) Axios automatically transforms JSON data and provides built-in request/response interceptors**

While the native Fetch API is built into modern browsers and can handle HTTP requests, Axios offers several conveniences that make it popular in production applications. Axios automatically serializes request data to JSON and parses JSON responses, eliminating the need to manually call `response.json()` as you would with Fetch. Axios also provides built-in support for request and response interceptors, which allow you to globally modify requests (such as adding authentication tokens) or handle responses (such as redirecting on 401 errors) before they reach your application code. Additionally, Axios has better error handling out of the box -- it rejects promises for HTTP error status codes (like 404 or 500), whereas Fetch only rejects on network failures and considers HTTP errors as successful responses that must be checked manually.

</details>

---

**5. Why must environment variables in a Vite project be prefixed with `VITE_`?**

- A) It is a JavaScript naming convention for constants
- B) Vite only exposes variables with the `VITE_` prefix to the client-side code for security
- C) The `VITE_` prefix makes the variables load faster
- D) Variables without `VITE_` are automatically deleted during the build process

<details>
<summary>Answer</summary>

**B) Vite only exposes variables with the `VITE_` prefix to the client-side code for security**

Vite uses the `VITE_` prefix as a security mechanism to prevent accidental exposure of sensitive server-side environment variables to the client-side bundle. Since front-end code is sent to and visible in the user's browser, exposing secrets such as database passwords, API keys, or private tokens would be a serious security vulnerability. By requiring the `VITE_` prefix, Vite ensures that developers must explicitly opt in to making a variable available in the browser. For example, `VITE_API_URL=http://localhost:5000` would be accessible in your React code via `import.meta.env.VITE_API_URL`, while a variable like `DB_PASSWORD=secret123` without the prefix would remain inaccessible in the front-end code. This is similar to how Create React App requires the `REACT_APP_` prefix for the same reason.

</details>

---

**6. What is the primary benefit of configuring a proxy in the Vite development server?**

- A) It makes the application run faster in production
- B) It avoids CORS issues during development by forwarding API requests through the dev server
- C) It automatically deploys the application to a cloud server
- D) It enables hot module replacement for CSS files

<details>
<summary>Answer</summary>

**B) It avoids CORS issues during development by forwarding API requests through the dev server**

Configuring a proxy in the Vite development server allows your front-end application to make API requests to the back-end without encountering CORS errors during development. When a proxy is set up, requests matching a certain path (such as `/api`) are intercepted by the Vite dev server and forwarded to your Express back-end server. Since the request is made from the server side (Vite dev server to Express server) rather than from the browser, CORS restrictions do not apply. This means you can write your front-end fetch calls using relative URLs like `/api/users` instead of absolute URLs like `http://localhost:5000/api/users`. The proxy is configured in `vite.config.js` and only applies during development. In production, you would typically serve both front-end and back-end from the same origin or configure proper CORS headers on the server.

</details>

---

**7. Which npm package is used to enable CORS in an Express.js application?**

- A) express-cors
- B) cors
- C) cross-origin
- D) helmet

<details>
<summary>Answer</summary>

**B) cors**

The `cors` package is the standard middleware used to enable Cross-Origin Resource Sharing in Express.js applications. It can be installed with `npm install cors` and then used as middleware with `app.use(cors())`. By default, calling `cors()` without any options allows requests from all origins, which is convenient during development but not recommended for production. For production environments, you should configure specific options such as `cors({ origin: 'https://yourdomain.com' })` to only allow requests from your front-end's domain. The `cors` middleware handles setting the appropriate HTTP headers, including `Access-Control-Allow-Origin`, `Access-Control-Allow-Methods`, and `Access-Control-Allow-Headers`, and it also handles preflight OPTIONS requests automatically. While `helmet` is another popular Express middleware, it is used for setting various security-related HTTP headers and does not handle CORS.

</details>

---

**8. Which of the following is the correct syntax for making a GET request with Axios in a React component?**

- A) `axios.get('/api/data').then(res => res.json()).then(data => setData(data))`
- B) `axios('/api/data').then(res => setData(res.body))`
- C) `axios.get('/api/data').then(res => setData(res.data))`
- D) `axios.fetch('/api/data').then(res => setData(res.data))`

<details>
<summary>Answer</summary>

**C) `axios.get('/api/data').then(res => setData(res.data))`**

In Axios, the response object has a `data` property that contains the parsed response body. Unlike the Fetch API, Axios automatically parses JSON responses, so you do not need to call `.json()` on the response. The correct method for a GET request is `axios.get()`, not `axios.fetch()` (which does not exist). Option A is incorrect because it mixes Fetch API syntax (`.json()`) with Axios. Option B is incorrect because Axios uses `res.data`, not `res.body`. When using `async/await` syntax, the equivalent would be `const res = await axios.get('/api/data'); setData(res.data);`. The `res` object in Axios also includes other useful properties such as `res.status` (the HTTP status code), `res.headers` (the response headers), and `res.config` (the request configuration).

</details>

---

**9. In a typical MERN full-stack project, what is the recommended folder structure?**

- A) All files in a single root directory
- B) Separate `client` (or `frontend`) and `server` (or `backend`) directories within a root project folder
- C) A single `src` folder containing both front-end and back-end code
- D) Separate repositories with no shared configuration

<details>
<summary>Answer</summary>

**B) Separate `client` (or `frontend`) and `server` (or `backend`) directories within a root project folder**

The recommended folder structure for a MERN full-stack application is a monorepo-style layout with clearly separated front-end and back-end directories. A typical structure looks like this: the root directory contains a `client` or `frontend` folder (which holds the Vite/React application with its own `package.json`) and a `server` or `backend` folder (which holds the Express/Node.js application with its own `package.json`). The root may also contain a top-level `package.json` with scripts to run both parts concurrently using a tool like `concurrently`. This separation provides clear boundaries between front-end and back-end code, makes it easier for teams to work on different parts independently, and simplifies deployment since each part can be deployed separately. While separate repositories (option D) can work, they add unnecessary complexity for most projects. Mixing all code in a single directory (options A and C) makes the project harder to maintain and deploy.

</details>

---

**10. What is the correct order of data flow when a user interacts with a MERN stack application?**

- A) MongoDB -> Express -> React -> Node.js
- B) React -> Node.js/Express -> MongoDB -> Express/Node.js -> React
- C) Node.js -> React -> MongoDB -> Express
- D) Express -> MongoDB -> React -> Node.js

<details>
<summary>Answer</summary>

**B) React -> Node.js/Express -> MongoDB -> Express/Node.js -> React**

The data flow in a MERN stack application follows a request-response cycle. First, the user interacts with the React front-end (such as clicking a button or submitting a form), which triggers an HTTP request (using Axios or Fetch) to the Express back-end server running on Node.js. The Express server receives the request, processes it through any middleware (such as authentication or validation), and then interacts with the MongoDB database using an ODM like Mongoose to perform the required database operation (create, read, update, or delete). Once MongoDB returns the result, Express formats the response (typically as JSON) and sends it back to the React front-end over HTTP. Finally, React receives the response and updates the user interface accordingly, often by updating component state with `useState` or a state management library. This full round-trip cycle is the foundation of how all MERN stack applications handle user interactions and data management.

</details>

---

## Part 2: Short Answer Questions

**1. Explain why CORS errors occur in a MERN stack application during development and how they can be resolved.**

<details>
<summary>Answer</summary>

CORS errors occur in a MERN stack application during development because the React front-end and the Express back-end typically run on different ports, making them different "origins" in the eyes of the browser. For example, the Vite development server runs on `http://localhost:5173` while the Express server might run on `http://localhost:5000`. The browser's Same-Origin Policy blocks requests between these two origins as a security measure to prevent malicious websites from accessing resources on other domains.

There are two common ways to resolve CORS issues during development:

**1. Using the `cors` middleware on the Express server:**

```javascript
const cors = require('cors');

// Allow all origins (development only)
app.use(cors());

// Or allow a specific origin (recommended)
app.use(cors({
  origin: 'http://localhost:5173',
  credentials: true
}));
```

**2. Configuring a proxy in `vite.config.js`:**

```javascript
export default defineConfig({
  plugins: [react()],
  server: {
    proxy: {
      '/api': {
        target: 'http://localhost:5000',
        changeOrigin: true
      }
    }
  }
});
```

The proxy approach is often preferred during development because it avoids CORS entirely by routing API requests through the Vite dev server. In production, you would typically serve the React build files from the Express server itself (making them the same origin) or configure specific CORS headers on the server.

</details>

---

**2. Compare storing authentication tokens in `localStorage` versus `httpOnly` cookies. What are the security implications of each approach?**

<details>
<summary>Answer</summary>

Both `localStorage` and `httpOnly` cookies can be used to store authentication tokens (such as JWTs) in a MERN application, but they have significantly different security profiles.

**localStorage:**
- Tokens stored in `localStorage` are accessible via JavaScript using `localStorage.getItem('token')`.
- This makes them vulnerable to Cross-Site Scripting (XSS) attacks. If an attacker injects malicious JavaScript into your application, they can read the token and send it to their own server.
- The developer must manually attach the token to each API request, typically via an Authorization header: `headers: { 'Authorization': 'Bearer ' + token }`.
- Tokens persist until explicitly removed, even after the browser is closed.

**httpOnly Cookies:**
- Cookies with the `httpOnly` flag cannot be accessed by JavaScript (`document.cookie` will not include them), which makes them immune to XSS attacks.
- The browser automatically sends `httpOnly` cookies with every request to the server, so the developer does not need to manually attach them.
- They can be configured with additional security flags: `secure` (only sent over HTTPS), `sameSite` (protects against CSRF attacks), and expiration dates.
- However, they require careful CORS configuration with `credentials: true` on both the client and server.

**Recommendation:** For production applications, `httpOnly` cookies are generally considered more secure because they eliminate the risk of token theft through XSS. However, `localStorage` is simpler to implement and is acceptable for learning projects or applications with strong XSS protections (such as Content Security Policy headers and proper input sanitization).

</details>

---

**3. Why is it beneficial to use a proxy configuration in the Vite development server instead of making direct API calls to the Express back-end?**

<details>
<summary>Answer</summary>

Using a proxy configuration in the Vite development server offers several important benefits over making direct API calls to the Express back-end:

**1. Eliminates CORS Issues:** The most immediate benefit is that a proxy completely avoids CORS errors during development. When the Vite dev server proxies a request, the browser sees the request going to the same origin (`http://localhost:5173`), so no cross-origin restrictions apply. The Vite server then forwards the request to the Express back-end server-to-server, where CORS does not apply.

**2. Cleaner Code with Relative URLs:** With a proxy, you can use relative URLs in your front-end code (such as `/api/users` instead of `http://localhost:5000/api/users`). This means your front-end code does not need to know the back-end's address, making it more portable and easier to deploy.

**3. Smoother Production Transition:** In production, the React build files are often served by the Express server itself, so API calls using relative paths like `/api/users` will work without any changes. Without a proxy, you would need to manage environment-specific API base URLs.

**4. Simplified Environment Configuration:** You do not need to manage different API URLs for different environments in your front-end code, reducing the need for environment variables and conditional logic.

The proxy is configured in `vite.config.js`:

```javascript
server: {
  proxy: {
    '/api': {
      target: 'http://localhost:5000',
      changeOrigin: true
    }
  }
}
```

This tells Vite to forward any request starting with `/api` to `http://localhost:5000`. Note that the proxy only works during development. For production, you must ensure your deployment handles routing correctly.

</details>

---

**4. Explain why Vite requires environment variables to be prefixed with `VITE_` and what would happen if you use a variable without this prefix in your React code.**

<details>
<summary>Answer</summary>

Vite enforces the `VITE_` prefix requirement as a deliberate security measure to protect sensitive information from being exposed in the client-side JavaScript bundle.

**Why the prefix exists:** When Vite builds your React application, it replaces references to `import.meta.env.VITE_*` variables with their actual values in the compiled JavaScript. This JavaScript is then sent to the user's browser, where anyone can inspect it using browser developer tools. If Vite exposed all environment variables without restriction, sensitive server-side secrets (such as database connection strings, private API keys, or encryption secrets) defined in your `.env` file could end up in the browser bundle and be visible to anyone.

**What happens without the prefix:** If you define an environment variable without the `VITE_` prefix (for example, `API_SECRET=mySecretKey123` in your `.env` file) and try to access it in your React code with `import.meta.env.API_SECRET`, the value will be `undefined`. Vite intentionally filters out these variables during the build process, so they never reach the client-side code.

**Practical example:**

```env
# .env file
VITE_API_URL=http://localhost:5000    # Accessible in React
DB_PASSWORD=supersecret               # NOT accessible in React
VITE_APP_TITLE=My MERN App            # Accessible in React
SECRET_KEY=abc123                     # NOT accessible in React
```

```javascript
// In your React component
console.log(import.meta.env.VITE_API_URL);    // "http://localhost:5000"
console.log(import.meta.env.DB_PASSWORD);      // undefined
console.log(import.meta.env.VITE_APP_TITLE);   // "My MERN App"
console.log(import.meta.env.SECRET_KEY);        // undefined
```

This design forces developers to make a conscious decision about which variables should be public, significantly reducing the risk of accidental secret exposure.

</details>

---

**5. Describe the complete data flow that occurs when a user clicks a "Submit" button in a React form and the data is saved to MongoDB. Include all the layers and technologies involved.**

<details>
<summary>Answer</summary>

When a user clicks a "Submit" button in a MERN stack application, the data flows through several layers. Here is the complete journey:

**Step 1 -- React Front-End (User Interaction):**
The user fills in form fields, which are captured in React component state (using `useState` or a form library). When the user clicks "Submit," an `onSubmit` event handler is triggered, which calls `e.preventDefault()` to prevent the default form submission behavior.

**Step 2 -- HTTP Request (React to Express):**
The event handler uses Axios or the Fetch API to send an HTTP POST request to the Express back-end. The form data is serialized as JSON in the request body, and the `Content-Type` header is set to `application/json`.

```javascript
const response = await axios.post('/api/items', {
  name: formData.name,
  description: formData.description
});
```

**Step 3 -- Express Server (Request Processing):**
The Express server receives the request. The `express.json()` middleware parses the JSON request body and makes it available as `req.body`. The request is matched to the appropriate route handler (for example, `router.post('/api/items', controller.createItem)`).

**Step 4 -- Business Logic and Validation:**
The route handler or controller validates the incoming data (checking for required fields, data types, length constraints, etc.). If validation fails, an error response is sent back immediately.

**Step 5 -- Mongoose/MongoDB (Database Operation):**
If validation passes, a Mongoose model is used to create a new document in the MongoDB collection. Mongoose converts the JavaScript object into a MongoDB document, applies any schema-level validation, and executes the `insertOne` operation on the database.

```javascript
const newItem = await Item.create({ name: req.body.name, description: req.body.description });
```

**Step 6 -- Response (Express to React):**
MongoDB returns the saved document (including the generated `_id`). Express sends this data back to the React front-end as a JSON response with an appropriate HTTP status code (typically 201 for a created resource).

**Step 7 -- UI Update (React):**
React receives the response, updates the component state with the new data, and re-renders the UI to reflect the change (such as adding the new item to a displayed list, showing a success message, or redirecting to another page).

Throughout this flow, errors can occur at any stage (network failures, validation errors, database errors), and each layer should handle errors appropriately and communicate them back to the user.

</details>

---

## Part 3: Coding Exercises

**1. Connect a React Component to an Express API**

Write a React component that fetches a list of products from an Express API endpoint (`/api/products`) when the component mounts and displays them in an unordered list.

**Starter Code:**

```jsx
import { useState, useEffect } from 'react';

function ProductList() {
  // TODO: Create state for products

  // TODO: Fetch products from /api/products when component mounts

  return (
    <div>
      <h2>Products</h2>
      {/* TODO: Display products in a <ul> */}
    </div>
  );
}

export default ProductList;
```

<details>
<summary>Solution</summary>

```jsx
import { useState, useEffect } from 'react';
import axios from 'axios';

function ProductList() {
  const [products, setProducts] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchProducts = async () => {
      try {
        const response = await axios.get('/api/products');
        setProducts(response.data);
      } catch (err) {
        setError(err.response?.data?.message || 'Failed to fetch products');
      } finally {
        setLoading(false);
      }
    };

    fetchProducts();
  }, []);

  if (loading) return <p>Loading products...</p>;
  if (error) return <p style={{ color: 'red' }}>Error: {error}</p>;

  return (
    <div>
      <h2>Products</h2>
      {products.length === 0 ? (
        <p>No products found.</p>
      ) : (
        <ul>
          {products.map((product) => (
            <li key={product._id}>
              <strong>{product.name}</strong> - ${product.price}
            </li>
          ))}
        </ul>
      )}
    </div>
  );
}

export default ProductList;
```

**Explanation:**

- `useState` is used to manage three pieces of state: the `products` array, a `loading` boolean, and an `error` message.
- `useEffect` with an empty dependency array (`[]`) ensures the fetch request runs only once when the component first mounts.
- The `async` function is defined inside `useEffect` because the effect callback itself cannot be `async`.
- `axios.get()` sends a GET request to `/api/products`. The response data is accessed via `response.data` (Axios automatically parses JSON).
- The `try/catch/finally` block handles errors gracefully and ensures `loading` is set to `false` regardless of success or failure.
- The component conditionally renders a loading message, an error message, or the list of products using early returns.
- Each product is rendered inside a `<li>` with a unique `key` prop set to `product._id` (the MongoDB document ID).

</details>

---

**2. Set Up CORS in Express with a Specific Origin**

Configure an Express server with the `cors` middleware that only allows requests from `http://localhost:5173` and supports credentials (cookies).

**Starter Code:**

```javascript
const express = require('express');
const app = express();

// TODO: Install and configure CORS middleware
// - Only allow requests from http://localhost:5173
// - Allow credentials (cookies)
// - Allow specific HTTP methods

app.get('/api/data', (req, res) => {
  res.json({ message: 'CORS is configured correctly!' });
});

const PORT = 5000;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

<details>
<summary>Solution</summary>

```javascript
const express = require('express');
const cors = require('cors');
const app = express();

// Configure CORS with specific options
const corsOptions = {
  origin: 'http://localhost:5173',        // Only allow this origin
  credentials: true,                      // Allow cookies and auth headers
  methods: ['GET', 'POST', 'PUT', 'DELETE', 'PATCH'],  // Allowed HTTP methods
  allowedHeaders: ['Content-Type', 'Authorization'],    // Allowed request headers
  optionsSuccessStatus: 200               // For legacy browser support
};

app.use(cors(corsOptions));

// Parse JSON request bodies
app.use(express.json());

app.get('/api/data', (req, res) => {
  res.json({ message: 'CORS is configured correctly!' });
});

const PORT = 5000;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

**Explanation:**

- The `cors` package is imported and used as Express middleware with `app.use(cors(corsOptions))`.
- `origin: 'http://localhost:5173'` restricts API access to only the Vite dev server. Requests from any other origin will be blocked by the browser. For multiple origins, you can pass an array: `origin: ['http://localhost:5173', 'https://myapp.com']`.
- `credentials: true` is required when the front-end needs to send cookies or authentication headers. On the front-end, Axios must also be configured with `withCredentials: true` for this to work.
- `methods` specifies which HTTP methods are allowed for cross-origin requests. This is important for RESTful APIs that use PUT, DELETE, and PATCH methods.
- `allowedHeaders` specifies which request headers the client is allowed to send. `Content-Type` is needed for JSON payloads, and `Authorization` is needed for sending JWT tokens.
- `optionsSuccessStatus: 200` ensures compatibility with older browsers that have issues with the default 204 status code for preflight responses.
- The middleware is applied globally with `app.use()`, meaning all routes will have CORS enabled. You could also apply it to specific routes if needed.

</details>

---

**3. Make an Axios POST Request with Error Handling**

Write a function that sends a POST request to `/api/users/register` with user registration data (name, email, password) and handles both success and various error scenarios.

**Starter Code:**

```javascript
import axios from 'axios';

// TODO: Create an async function called registerUser
// - Accept name, email, and password as parameters
// - Send a POST request to /api/users/register
// - Handle success: return the response data
// - Handle validation errors (400)
// - Handle conflict errors (409 - email already exists)
// - Handle server errors (500)
// - Handle network errors
```

<details>
<summary>Solution</summary>

```javascript
import axios from 'axios';

const registerUser = async (name, email, password) => {
  try {
    const response = await axios.post('/api/users/register', {
      name,
      email,
      password
    });

    // Success - return the user data and token
    console.log('Registration successful!');
    return {
      success: true,
      data: response.data
    };

  } catch (error) {
    // The request was made and the server responded with an error status
    if (error.response) {
      const { status, data } = error.response;

      switch (status) {
        case 400:
          // Validation error
          console.error('Validation failed:', data.message);
          return {
            success: false,
            error: data.message || 'Please check your input and try again.'
          };

        case 409:
          // Conflict - email already exists
          console.error('Email already registered');
          return {
            success: false,
            error: 'An account with this email already exists.'
          };

        case 500:
          // Server error
          console.error('Server error:', data.message);
          return {
            success: false,
            error: 'Something went wrong on the server. Please try again later.'
          };

        default:
          console.error(`Unexpected error (${status}):`, data.message);
          return {
            success: false,
            error: data.message || 'An unexpected error occurred.'
          };
      }

    } else if (error.request) {
      // The request was made but no response was received (network error)
      console.error('Network error - no response received');
      return {
        success: false,
        error: 'Unable to connect to the server. Please check your internet connection.'
      };

    } else {
      // Something went wrong setting up the request
      console.error('Request setup error:', error.message);
      return {
        success: false,
        error: 'An error occurred while preparing the request.'
      };
    }
  }
};

// Usage example in a React component:
// const handleSubmit = async (e) => {
//   e.preventDefault();
//   const result = await registerUser(name, email, password);
//   if (result.success) {
//     // Redirect or show success message
//   } else {
//     setErrorMessage(result.error);
//   }
// };

export default registerUser;
```

**Explanation:**

- The function is declared as `async` so that we can use `await` with the Axios call, resulting in cleaner and more readable code compared to `.then()` chains.
- `axios.post()` takes two arguments: the URL and the data object. Axios automatically serializes the object to JSON and sets the `Content-Type` header.
- Error handling in Axios distinguishes between three scenarios:
  - `error.response` exists when the server responded with an error status code (4xx or 5xx). This object contains `status`, `data`, and `headers`.
  - `error.request` exists when the request was sent but no response was received. This typically indicates a network issue, such as the server being down or the user being offline.
  - If neither exists, the error occurred while setting up the request (such as an invalid URL).
- The function returns a consistent object shape (`{ success, data/error }`) regardless of the outcome, making it easy for the calling component to handle the result.
- A `switch` statement is used to provide user-friendly error messages for different HTTP status codes, rather than exposing raw server errors to the user.

</details>

---

**4. Display API Data in React with Loading and Error States**

Build a React component that fetches user profile data from `/api/users/profile`, displays a loading spinner while fetching, shows an error message if the request fails, and renders the user profile when data is available.

**Starter Code:**

```jsx
import { useState, useEffect } from 'react';
import axios from 'axios';

function UserProfile() {
  // TODO: Set up state for user data, loading, and error

  // TODO: Fetch user profile on component mount

  // TODO: Render loading state

  // TODO: Render error state

  // TODO: Render user profile
  return null;
}

export default UserProfile;
```

<details>
<summary>Solution</summary>

```jsx
import { useState, useEffect } from 'react';
import axios from 'axios';

function UserProfile() {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  const fetchUserProfile = async () => {
    setLoading(true);
    setError(null);

    try {
      const response = await axios.get('/api/users/profile');
      setUser(response.data);
    } catch (err) {
      if (err.response) {
        setError(err.response.data.message || `Server error: ${err.response.status}`);
      } else if (err.request) {
        setError('Unable to reach the server. Please check your connection.');
      } else {
        setError('An unexpected error occurred.');
      }
    } finally {
      setLoading(false);
    }
  };

  useEffect(() => {
    fetchUserProfile();
  }, []);

  // Loading state
  if (loading) {
    return (
      <div style={{ textAlign: 'center', padding: '2rem' }}>
        <div
          style={{
            border: '4px solid #f3f3f3',
            borderTop: '4px solid #3498db',
            borderRadius: '50%',
            width: '40px',
            height: '40px',
            animation: 'spin 1s linear infinite',
            margin: '0 auto'
          }}
        ></div>
        <p>Loading profile...</p>
        <style>{`
          @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
          }
        `}</style>
      </div>
    );
  }

  // Error state
  if (error) {
    return (
      <div style={{
        padding: '1rem',
        backgroundColor: '#fee',
        border: '1px solid #fcc',
        borderRadius: '8px',
        margin: '1rem'
      }}>
        <h3 style={{ color: '#c00' }}>Error Loading Profile</h3>
        <p>{error}</p>
        <button
          onClick={fetchUserProfile}
          style={{
            padding: '0.5rem 1rem',
            backgroundColor: '#3498db',
            color: 'white',
            border: 'none',
            borderRadius: '4px',
            cursor: 'pointer'
          }}
        >
          Try Again
        </button>
      </div>
    );
  }

  // No user data
  if (!user) {
    return <p>No profile data available.</p>;
  }

  // Success state - render user profile
  return (
    <div style={{
      maxWidth: '400px',
      margin: '2rem auto',
      padding: '2rem',
      border: '1px solid #ddd',
      borderRadius: '12px',
      boxShadow: '0 2px 8px rgba(0,0,0,0.1)'
    }}>
      <h2>{user.name}</h2>
      <div style={{ marginTop: '1rem' }}>
        <p><strong>Email:</strong> {user.email}</p>
        <p><strong>Role:</strong> {user.role || 'User'}</p>
        <p><strong>Joined:</strong> {new Date(user.createdAt).toLocaleDateString()}</p>
      </div>
      <button
        onClick={fetchUserProfile}
        style={{
          marginTop: '1rem',
          padding: '0.5rem 1rem',
          backgroundColor: '#2ecc71',
          color: 'white',
          border: 'none',
          borderRadius: '4px',
          cursor: 'pointer'
        }}
      >
        Refresh Profile
      </button>
    </div>
  );
}

export default UserProfile;
```

**Explanation:**

- **Three state variables** manage the component's behavior: `user` holds the profile data (initially `null`), `loading` tracks whether a request is in progress (initially `true`), and `error` stores any error message (initially `null`).
- **The fetch function** is defined outside `useEffect` so it can be reused for the "Try Again" and "Refresh" buttons. It resets `loading` and `error` before each request to ensure the UI reflects the current state.
- **`useEffect`** calls the fetch function once when the component mounts (empty dependency array).
- **Conditional rendering** uses early returns to display the appropriate UI based on the current state. This pattern is cleaner than nested ternary operators and makes the component easier to read and maintain.
- **The loading spinner** is implemented using pure CSS animation, demonstrating that you do not always need a third-party library for simple UI elements.
- **Error handling** provides a user-friendly message and a "Try Again" button, which improves the user experience by allowing recovery without refreshing the entire page.
- **The success state** safely accesses properties using optional chaining and provides default values (such as `user.role || 'User'`), and formats the date using `toLocaleDateString()`.

</details>

---

**5. Build a Full-Stack CRUD Application: Create and Read Items**

Build a simple full-stack feature where users can add new items through a React form and view a list of all items. Write both the Express back-end routes and the React front-end component.

**Starter Code (Back-End):**

```javascript
// server/routes/items.js
const express = require('express');
const router = express.Router();

// TODO: Create an in-memory items array

// TODO: GET /api/items - Return all items

// TODO: POST /api/items - Create a new item (with name and description)

module.exports = router;
```

**Starter Code (Front-End):**

```jsx
// client/src/components/ItemManager.jsx
import { useState, useEffect } from 'react';
import axios from 'axios';

function ItemManager() {
  // TODO: State for items list, form inputs, loading, and error

  // TODO: Fetch all items on mount

  // TODO: Handle form submission to create a new item

  // TODO: Render form and items list
  return null;
}

export default ItemManager;
```

<details>
<summary>Solution</summary>

**Back-End: Express Routes (`server/routes/items.js`)**

```javascript
const express = require('express');
const router = express.Router();

// In-memory storage (replace with MongoDB/Mongoose in production)
let items = [
  { id: 1, name: 'Sample Item', description: 'This is a sample item', createdAt: new Date().toISOString() }
];
let nextId = 2;

// GET /api/items - Return all items
router.get('/', (req, res) => {
  try {
    res.json(items);
  } catch (error) {
    res.status(500).json({ message: 'Failed to fetch items' });
  }
});

// POST /api/items - Create a new item
router.post('/', (req, res) => {
  try {
    const { name, description } = req.body;

    // Validation
    if (!name || !name.trim()) {
      return res.status(400).json({ message: 'Item name is required' });
    }

    if (!description || !description.trim()) {
      return res.status(400).json({ message: 'Item description is required' });
    }

    // Create new item
    const newItem = {
      id: nextId++,
      name: name.trim(),
      description: description.trim(),
      createdAt: new Date().toISOString()
    };

    items.push(newItem);

    res.status(201).json(newItem);
  } catch (error) {
    res.status(500).json({ message: 'Failed to create item' });
  }
});

module.exports = router;
```

**Server Entry Point (`server/index.js`)**

```javascript
const express = require('express');
const cors = require('cors');
const itemRoutes = require('./routes/items');

const app = express();

// Middleware
app.use(cors({ origin: 'http://localhost:5173' }));
app.use(express.json());

// Routes
app.use('/api/items', itemRoutes);

const PORT = 5000;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

**Front-End: React Component (`client/src/components/ItemManager.jsx`)**

```jsx
import { useState, useEffect } from 'react';
import axios from 'axios';

function ItemManager() {
  const [items, setItems] = useState([]);
  const [name, setName] = useState('');
  const [description, setDescription] = useState('');
  const [loading, setLoading] = useState(true);
  const [submitting, setSubmitting] = useState(false);
  const [error, setError] = useState(null);
  const [successMessage, setSuccessMessage] = useState('');

  // Fetch all items on component mount
  useEffect(() => {
    fetchItems();
  }, []);

  const fetchItems = async () => {
    setLoading(true);
    try {
      const response = await axios.get('/api/items');
      setItems(response.data);
      setError(null);
    } catch (err) {
      setError(err.response?.data?.message || 'Failed to fetch items');
    } finally {
      setLoading(false);
    }
  };

  // Handle form submission
  const handleSubmit = async (e) => {
    e.preventDefault();
    setSubmitting(true);
    setError(null);
    setSuccessMessage('');

    try {
      const response = await axios.post('/api/items', { name, description });

      // Add the new item to the list without re-fetching
      setItems((prevItems) => [...prevItems, response.data]);

      // Clear the form
      setName('');
      setDescription('');
      setSuccessMessage('Item created successfully!');

      // Clear success message after 3 seconds
      setTimeout(() => setSuccessMessage(''), 3000);
    } catch (err) {
      setError(err.response?.data?.message || 'Failed to create item');
    } finally {
      setSubmitting(false);
    }
  };

  return (
    <div style={{ maxWidth: '600px', margin: '2rem auto', padding: '0 1rem' }}>
      <h1>Item Manager</h1>

      {/* Add Item Form */}
      <form onSubmit={handleSubmit} style={{
        padding: '1.5rem',
        border: '1px solid #ddd',
        borderRadius: '8px',
        marginBottom: '2rem',
        backgroundColor: '#f9f9f9'
      }}>
        <h2>Add New Item</h2>

        <div style={{ marginBottom: '1rem' }}>
          <label htmlFor="name" style={{ display: 'block', marginBottom: '0.5rem', fontWeight: 'bold' }}>
            Name:
          </label>
          <input
            type="text"
            id="name"
            value={name}
            onChange={(e) => setName(e.target.value)}
            placeholder="Enter item name"
            required
            style={{
              width: '100%',
              padding: '0.5rem',
              borderRadius: '4px',
              border: '1px solid #ccc',
              boxSizing: 'border-box'
            }}
          />
        </div>

        <div style={{ marginBottom: '1rem' }}>
          <label htmlFor="description" style={{ display: 'block', marginBottom: '0.5rem', fontWeight: 'bold' }}>
            Description:
          </label>
          <textarea
            id="description"
            value={description}
            onChange={(e) => setDescription(e.target.value)}
            placeholder="Enter item description"
            required
            rows="3"
            style={{
              width: '100%',
              padding: '0.5rem',
              borderRadius: '4px',
              border: '1px solid #ccc',
              boxSizing: 'border-box'
            }}
          />
        </div>

        <button
          type="submit"
          disabled={submitting}
          style={{
            padding: '0.75rem 1.5rem',
            backgroundColor: submitting ? '#95a5a6' : '#3498db',
            color: 'white',
            border: 'none',
            borderRadius: '4px',
            cursor: submitting ? 'not-allowed' : 'pointer',
            fontSize: '1rem'
          }}
        >
          {submitting ? 'Adding...' : 'Add Item'}
        </button>
      </form>

      {/* Status Messages */}
      {successMessage && (
        <p style={{ color: 'green', padding: '0.5rem', backgroundColor: '#e8f5e9', borderRadius: '4px' }}>
          {successMessage}
        </p>
      )}

      {error && (
        <p style={{ color: 'red', padding: '0.5rem', backgroundColor: '#ffebee', borderRadius: '4px' }}>
          {error}
        </p>
      )}

      {/* Items List */}
      <h2>All Items ({items.length})</h2>

      {loading ? (
        <p>Loading items...</p>
      ) : items.length === 0 ? (
        <p style={{ color: '#666', fontStyle: 'italic' }}>No items yet. Add one above!</p>
      ) : (
        <ul style={{ listStyle: 'none', padding: 0 }}>
          {items.map((item) => (
            <li key={item.id} style={{
              padding: '1rem',
              border: '1px solid #eee',
              borderRadius: '8px',
              marginBottom: '0.75rem',
              backgroundColor: 'white',
              boxShadow: '0 1px 3px rgba(0,0,0,0.08)'
            }}>
              <h3 style={{ margin: '0 0 0.5rem 0' }}>{item.name}</h3>
              <p style={{ margin: '0 0 0.5rem 0', color: '#555' }}>{item.description}</p>
              <small style={{ color: '#999' }}>
                Created: {new Date(item.createdAt).toLocaleString()}
              </small>
            </li>
          ))}
        </ul>
      )}
    </div>
  );
}

export default ItemManager;
```

**Explanation:**

This exercise demonstrates a complete full-stack Create and Read implementation:

**Back-End:**
- An in-memory array simulates a database (in a real application, you would use MongoDB with Mongoose).
- The GET route returns all items as a JSON array.
- The POST route validates the request body, creates a new item with a unique ID and timestamp, adds it to the array, and returns the created item with a 201 status code.
- Both routes include error handling with try/catch blocks.

**Front-End:**
- Six state variables manage the component: `items` (the list), `name` and `description` (form inputs), `loading` (initial fetch state), `submitting` (form submission state), `error`, and `successMessage`.
- `fetchItems` runs on mount to load existing items.
- `handleSubmit` prevents the default form behavior, sends a POST request, and on success uses the functional form of `setItems` to append the new item to the list. This approach (called optimistic updating) avoids an extra GET request.
- The form button is disabled during submission to prevent duplicate submissions, and its text changes to "Adding..." to provide feedback.
- The items list shows a count in the heading and gracefully handles the empty state.
- Each item displays its name, description, and formatted creation date.

</details>

---
