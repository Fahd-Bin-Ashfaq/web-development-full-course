# Week 20 -- React Router & Navigation: Practice Questions

**Total Questions: 20** (10 MCQs + 5 Short Answer + 5 Coding Exercises)

---

## Part 1: Multiple Choice Questions (MCQs)

**1. What is the primary advantage of client-side routing in a Single-Page Application?**

- A) It eliminates the need for a web server
- B) It navigates between views without a full page reload, preserving state
- C) It makes the website work without JavaScript
- D) It automatically handles SEO for all pages

<details>
<summary>Answer</summary>

**B) It navigates between views without a full page reload, preserving state**

Client-side routing uses JavaScript to swap components and update the URL without sending a new request to the server. The browser never reloads, the screen never flashes white, and all application state (form inputs, scroll position, fetched data) is preserved across navigation.
</details>

---

**2. Which component must wrap your entire application to enable React Router?**

- A) `<Routes>`
- B) `<Route>`
- C) `<BrowserRouter>`
- D) `<RouterProvider>`

<details>
<summary>Answer</summary>

**C) `<BrowserRouter>`**

`<BrowserRouter>` provides the routing context that all other React Router components depend on. It uses the browser's History API to keep the URL in sync with the rendered components. Without it, components like `<Routes>`, `<Link>`, and hooks like `useNavigate` will throw an error.
</details>

---

**3. Why should you use `<Link to="/about">` instead of `<a href="/about">` in a React application?**

- A) `<Link>` is faster because it uses WebSockets
- B) `<a>` tags are not valid HTML in React
- C) `<Link>` prevents a full page reload and preserves application state
- D) `<Link>` automatically adds SEO metadata

<details>
<summary>Answer</summary>

**C) `<Link>` prevents a full page reload and preserves application state**

When you click a regular `<a>` tag, the browser sends a new HTTP request to the server and reloads the entire page. All JavaScript re-executes, all component state is lost, and the user sees a white screen flash. `<Link>` intercepts the click, updates the URL, and tells React Router to swap the rendered component -- all without a page reload. The `<a>` tag is perfectly valid HTML; the issue is that it triggers the default browser navigation behavior which destroys the SPA experience.
</details>

---

**4. What is the difference between `<Link>` and `<NavLink>`?**

- A) `<NavLink>` can navigate to external URLs; `<Link>` cannot
- B) `<NavLink>` automatically knows if it matches the current URL and can apply active styling
- C) `<Link>` is for navigation; `<NavLink>` is for forms
- D) There is no difference; they are interchangeable

<details>
<summary>Answer</summary>

**B) `<NavLink>` automatically knows if it matches the current URL and can apply active styling**

`<NavLink>` is a special version of `<Link>` that is aware of whether its `to` path matches the current URL. When it matches, it adds an `active` CSS class by default, and its `className` and `style` props accept callback functions that receive `{ isActive }` as an argument. This makes it ideal for navigation bars where you want to highlight the current page.
</details>

---

**5. What does the `useParams` hook return?**

```jsx
// Route definition:
<Route path="/products/:productId" element={<ProductDetail />} />

// URL visited: /products/42
```

- A) `{ productId: 42 }` (a number)
- B) `{ productId: "42" }` (a string)
- C) `["42"]` (an array)
- D) `"42"` (a plain string)

<details>
<summary>Answer</summary>

**B) `{ productId: "42" }` (a string)**

`useParams` returns an object where each key corresponds to a named URL parameter defined in the route path (`:productId`), and each value is a **string**. URL parameters are always strings, even if they look like numbers. If you need a numeric value, you must convert it explicitly using `Number(productId)` or `parseInt(productId, 10)`.
</details>

---

**6. What is the purpose of the `<Outlet />` component in nested routes?**

- A) It defines where child routes should be rendered inside a parent layout
- B) It creates an exit point from the application
- C) It redirects users to the parent route
- D) It catches errors thrown by child components

<details>
<summary>Answer</summary>

**A) It defines where child routes should be rendered inside a parent layout**

When you have nested routes (child `<Route>` elements inside a parent `<Route>`), the parent component needs a way to say "render the matching child here." `<Outlet />` is that placeholder. It acts like a window in the parent layout where different child components appear based on the URL. The parent layout (navbar, sidebar, footer) stays on screen while only the `<Outlet />` area changes.
</details>

---

**7. Which approach correctly performs programmatic navigation after a form submission?**

- A)
```jsx
window.location.href = "/success";
```

- B)
```jsx
<Link to="/success" />
```

- C)
```jsx
const navigate = useNavigate();
navigate("/success", { replace: true });
```

- D)
```jsx
<Route path="/success" element={<Success />} />
```

<details>
<summary>Answer</summary>

**C)**
```jsx
const navigate = useNavigate();
navigate("/success", { replace: true });
```

`useNavigate` returns a function that you can call inside event handlers to navigate programmatically. Option A uses `window.location.href` which causes a full page reload, losing all state. Option B is a component, not a function call, and cannot be used inside a handler. Option D defines a route but does not navigate to it. Using `{ replace: true }` after a form submission prevents the user from pressing the back button and re-submitting.
</details>

---

**8. What does the route `path="*"` match?**

- A) Only the root URL `/`
- B) Only URLs with exactly one path segment
- C) Any URL that has not been matched by other defined routes
- D) All URLs, even those that match other routes

<details>
<summary>Answer</summary>

**C) Any URL that has not been matched by other defined routes**

The `path="*"` is a catch-all (wildcard) route. React Router evaluates routes and picks the best match. If no other route matches the current URL, the `*` route catches it. This is typically used to render a 404 Not Found page. It should always be placed as the last route in your `<Routes>` to ensure other routes have a chance to match first.
</details>

---

**9. What happens when an unauthenticated user tries to access a protected route that uses `<Navigate to="/login" replace />`?**

- A) The protected page renders normally
- B) The application crashes with an error
- C) The user is immediately redirected to the `/login` page
- D) A pop-up asks the user to log in

<details>
<summary>Answer</summary>

**C) The user is immediately redirected to the `/login` page**

The `<Navigate>` component is a declarative redirect. When it renders, it immediately navigates to the specified `to` path. In a protected route pattern, a check determines if the user is authenticated. If not, `<Navigate to="/login" replace />` renders instead of the protected content, sending the user to the login page. The `replace` prop replaces the current history entry so pressing Back does not return to the protected page.
</details>

---

**10. What does `useSearchParams` allow you to do?**

- A) Search for components in the React tree
- B) Read and write URL query parameters (e.g., `?category=shoes&sort=price`)
- C) Search through an array of objects in state
- D) Find and replace text in the DOM

<details>
<summary>Answer</summary>

**B) Read and write URL query parameters (e.g., `?category=shoes&sort=price`)**

`useSearchParams` returns a pair `[searchParams, setSearchParams]` that works similarly to `useState` but is synchronized with the URL query string. `searchParams.get("category")` reads the value of the `category` parameter, and `setSearchParams({ category: "shoes" })` updates the URL. This is ideal for filters, search queries, and pagination where the state should be reflected in the URL so users can bookmark or share links.
</details>

---

## Part 2: Short Answer Questions

**1. Explain the difference between a Multi-Page Application (MPA) and a Single-Page Application (SPA) in terms of how navigation works.**

<details>
<summary>Answer</summary>

In a **Multi-Page Application**, every navigation action (clicking a link, submitting a form) triggers a full HTTP request to the server. The server processes the request and returns an entirely new HTML document. The browser discards the current page, downloads and renders the new page from scratch. This causes a visible white screen flash, all JavaScript re-executes, and any client-side state (form inputs, scroll position) is lost.

In a **Single-Page Application**, the server sends a single HTML page along with a JavaScript bundle on the initial load. After that, navigation is handled entirely by JavaScript on the client side. When the user clicks a link, client-side routing intercepts the click, prevents the browser from making a server request, swaps the rendered component, and updates the URL using the browser's History API. The page never reloads, state is preserved, and transitions feel instantaneous. Server requests are only made for data (API calls), not for entire pages.
</details>

---

**2. What is the purpose of the `end` prop on a `<NavLink>`? Give a specific scenario where omitting it causes a problem.**

<details>
<summary>Answer</summary>

The `end` prop restricts NavLink matching to an **exact** path match. Without `end`, NavLink uses a "starts with" comparison, meaning it considers itself active if the current URL begins with its `to` path.

A concrete problem occurs with the Home link: `<NavLink to="/">Home</NavLink>`. Since every URL starts with `/` (for example, `/about`, `/products`, `/contact`), this NavLink would be marked as "active" on every single page. The Home link would always appear highlighted, making the active indicator meaningless.

Adding `<NavLink to="/" end>Home</NavLink>` tells React Router to only mark this link as active when the URL is exactly `/`, not when it merely starts with `/`. This is almost always necessary for root-level links.
</details>

---

**3. How do nested routes and `<Outlet />` work together? Describe the rendering process when a user visits `/dashboard/settings`.**

<details>
<summary>Answer</summary>

Nested routes create a parent-child relationship between route definitions. The parent route renders a layout component, and `<Outlet />` inside that layout acts as a placeholder where the matched child route's component will appear.

When a user visits `/dashboard/settings`:

1. React Router matches the parent route `path="/dashboard"` and renders its element (e.g., `<DashboardLayout />`).
2. `<DashboardLayout />` contains the persistent UI (sidebar, header) and an `<Outlet />` component somewhere in its JSX.
3. React Router then matches the child route `path="settings"` (which is relative, meaning `/dashboard/settings`).
4. The child route's element (`<Settings />`) is rendered **inside** the `<Outlet />` placeholder.
5. The result is the Dashboard layout displayed on screen with the Settings content inserted where `<Outlet />` is placed.

If the user navigates to `/dashboard/profile`, the Dashboard layout stays mounted and only the content inside `<Outlet />` changes from `<Settings />` to `<Profile />`. The sidebar and header do not re-render.
</details>

---

**4. What is the difference between `useNavigate` (the hook) and `<Navigate>` (the component)? When would you use each?**

<details>
<summary>Answer</summary>

**`useNavigate`** is a hook that returns a function. You call this function inside event handlers, async callbacks, or other imperative logic to navigate programmatically. It is used when navigation is triggered by code execution, not by rendering.

Example use cases: redirecting after a form submission, navigating after an API call completes, going back in response to a button click.

```jsx
const navigate = useNavigate();
navigate("/dashboard", { replace: true });
```

**`<Navigate>`** is a component. When it renders, it immediately redirects the user. It is declarative -- you place it in your JSX, and the redirect happens as part of the render cycle.

Example use cases: redirecting old URLs to new ones, redirecting in conditional rendering (e.g., inside a ProtectedRoute when the user is not authenticated), showing a default redirect for an index route.

```jsx
if (!isAuthenticated) {
  return <Navigate to="/login" replace />;
}
```

In short: use `useNavigate` when you need to navigate in response to an **event** (form submit, button click, API response). Use `<Navigate>` when you need to redirect as part of the **render output** (conditional rendering, route redirection).
</details>

---

**5. Why are URL parameters always strings, and how should you handle a situation where you need a numeric ID from a URL parameter?**

<details>
<summary>Answer</summary>

URL parameters are always strings because URLs are inherently text-based. The browser's address bar contains a string, and React Router extracts segments of that string. There is no type information in a URL -- `/products/42` is just the text characters "4" and "2", not the number forty-two.

When you call `useParams()`, every value in the returned object is a string. If your application logic requires a number (for example, to compare against numeric IDs in an array or to send to an API that expects a number), you must convert it explicitly:

```jsx
const { id } = useParams();         // id is "42" (string)
const numericId = Number(id);        // numericId is 42 (number)

// Now comparisons work correctly:
const product = products.find((p) => p.id === numericId);  // Correct
// Without conversion:
const wrong = products.find((p) => p.id === id);           // Fails: 42 !== "42"
```

You can also use `parseInt(id, 10)` for integer conversion. Additionally, it is good practice to handle the case where the parameter is not a valid number (e.g., the user types `/products/abc`), by checking `isNaN(numericId)` and displaying an error message or redirecting to a 404 page.
</details>

---

## Part 3: Coding Exercises

**Exercise 1: Basic Three-Page App with Routing**

Create a React application with three pages (Home, About, Contact) and a navigation bar. Use React Router to handle navigation between pages.

Requirements:
- Set up `BrowserRouter`, `Routes`, and `Route` for three pages
- Create a `Navbar` component with `Link` components
- Each page should display a heading and a short paragraph
- The Navbar should appear on all pages

<details>
<summary>Solution</summary>

```jsx
// src/pages/Home.jsx
function Home() {
  return (
    <div>
      <h1>Home</h1>
      <p>Welcome to our website. Browse around using the navigation above.</p>
    </div>
  );
}
export default Home;

// src/pages/About.jsx
function About() {
  return (
    <div>
      <h1>About Us</h1>
      <p>We are a small team building web applications with React.</p>
    </div>
  );
}
export default About;

// src/pages/Contact.jsx
function Contact() {
  return (
    <div>
      <h1>Contact</h1>
      <p>Reach us at contact@example.com or call +1-555-0100.</p>
    </div>
  );
}
export default Contact;

// src/components/Navbar.jsx
import { Link } from "react-router-dom";

function Navbar() {
  return (
    <nav style={{ display: "flex", gap: "16px", padding: "16px", backgroundColor: "#f3f4f6" }}>
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
      <Link to="/contact">Contact</Link>
    </nav>
  );
}
export default Navbar;

// src/App.jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Navbar from "./components/Navbar";
import Home from "./pages/Home";
import About from "./pages/About";
import Contact from "./pages/Contact";

function App() {
  return (
    <BrowserRouter>
      <Navbar />
      <div style={{ padding: "20px" }}>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
          <Route path="/contact" element={<Contact />} />
        </Routes>
      </div>
    </BrowserRouter>
  );
}

export default App;
```

**Key points:**
- `<Navbar />` is placed **inside** `<BrowserRouter>` but **outside** `<Routes>`, so it appears on every page.
- Each `<Link>` uses the `to` prop instead of `href` to prevent page reloads.
- The `<Routes>` block determines which page component renders based on the URL.
</details>

---

**Exercise 2: Dynamic Routes with Product Details**

Create a product listing page that links to individual product detail pages using dynamic routes and `useParams`.

Requirements:
- Create an array of at least 4 products with `id`, `name`, `price`, and `description`
- `ProductList` page displays all products with links to their detail pages
- `ProductDetail` page uses `useParams` to get the product ID and display the product information
- Handle the case where a product ID does not exist

<details>
<summary>Solution</summary>

```jsx
// src/data/products.js
const products = [
  { id: 1, name: "Laptop Stand", price: 39.99, description: "Ergonomic aluminum stand that raises your laptop to eye level." },
  { id: 2, name: "Wireless Mouse", price: 24.99, description: "Compact wireless mouse with silent clicks and USB-C charging." },
  { id: 3, name: "Desk Lamp", price: 54.99, description: "LED desk lamp with adjustable brightness and color temperature." },
  { id: 4, name: "Webcam HD", price: 69.99, description: "1080p webcam with built-in microphone and auto-focus." },
];

export default products;

// src/pages/ProductList.jsx
import { Link } from "react-router-dom";
import products from "../data/products";

function ProductList() {
  return (
    <div>
      <h1>Our Products</h1>
      <div style={{ display: "grid", gap: "16px" }}>
        {products.map((product) => (
          <div key={product.id} style={{ border: "1px solid #e5e7eb", padding: "16px", borderRadius: "8px" }}>
            <h3>{product.name}</h3>
            <p>${product.price}</p>
            <Link to={`/products/${product.id}`}>View Details</Link>
          </div>
        ))}
      </div>
    </div>
  );
}

export default ProductList;

// src/pages/ProductDetail.jsx
import { useParams, Link } from "react-router-dom";
import products from "../data/products";

function ProductDetail() {
  const { productId } = useParams();
  const product = products.find((p) => p.id === Number(productId));

  if (!product) {
    return (
      <div>
        <h1>Product Not Found</h1>
        <p>No product exists with ID "{productId}".</p>
        <Link to="/products">Back to Products</Link>
      </div>
    );
  }

  return (
    <div>
      <Link to="/products">&#8592; Back to Products</Link>
      <h1>{product.name}</h1>
      <p style={{ fontSize: "1.5rem", color: "#16a34a" }}>${product.price}</p>
      <p>{product.description}</p>
      <button style={{ marginTop: "16px", padding: "8px 24px" }}>Add to Cart</button>
    </div>
  );
}

export default ProductDetail;

// src/App.jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import ProductList from "./pages/ProductList";
import ProductDetail from "./pages/ProductDetail";

function App() {
  return (
    <BrowserRouter>
      <div style={{ padding: "20px" }}>
        <Routes>
          <Route path="/products" element={<ProductList />} />
          <Route path="/products/:productId" element={<ProductDetail />} />
        </Routes>
      </div>
    </BrowserRouter>
  );
}

export default App;
```

**Key points:**
- The route `/products/:productId` captures any value after `/products/` as the `productId` parameter.
- `useParams()` returns `{ productId: "3" }` (always a string), so `Number(productId)` is necessary for comparison.
- The component gracefully handles invalid IDs by checking if the product was found and displaying a fallback message.
</details>

---

**Exercise 3: Navbar with Active Styling Using NavLink**

Build a navigation bar that highlights the current page using `NavLink` with the `className` callback.

Requirements:
- Use `NavLink` instead of `Link`
- Use the `className` callback to apply an "active" class when the link matches the current route
- Use the `end` prop on the Home link to prevent it from always being active
- Style the active link with a distinct background color and text color

<details>
<summary>Solution</summary>

```jsx
// src/components/Navbar.jsx
import { NavLink } from "react-router-dom";

function Navbar() {
  const getLinkClass = ({ isActive }) =>
    isActive ? "navbar-link navbar-link-active" : "navbar-link";

  return (
    <nav style={{
      display: "flex",
      alignItems: "center",
      gap: "8px",
      padding: "12px 24px",
      backgroundColor: "#1e293b",
    }}>
      <span style={{ color: "white", fontWeight: "bold", fontSize: "1.2rem", marginRight: "24px" }}>
        MyApp
      </span>
      <NavLink to="/" end className={getLinkClass}>
        Home
      </NavLink>
      <NavLink to="/services" className={getLinkClass}>
        Services
      </NavLink>
      <NavLink to="/portfolio" className={getLinkClass}>
        Portfolio
      </NavLink>
      <NavLink to="/contact" className={getLinkClass}>
        Contact
      </NavLink>
    </nav>
  );
}

export default Navbar;

// src/App.jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Navbar from "./components/Navbar";
import "./App.css";

function App() {
  return (
    <BrowserRouter>
      <Navbar />
      <main style={{ padding: "24px" }}>
        <Routes>
          <Route path="/" element={<h1>Home Page</h1>} />
          <Route path="/services" element={<h1>Services Page</h1>} />
          <Route path="/portfolio" element={<h1>Portfolio Page</h1>} />
          <Route path="/contact" element={<h1>Contact Page</h1>} />
        </Routes>
      </main>
    </BrowserRouter>
  );
}

export default App;
```

```css
/* src/App.css */
.navbar-link {
  color: #94a3b8;
  text-decoration: none;
  padding: 8px 16px;
  border-radius: 6px;
  font-size: 0.95rem;
  transition: background-color 0.2s, color 0.2s;
}

.navbar-link:hover {
  color: #e2e8f0;
  background-color: #334155;
}

.navbar-link-active {
  color: white;
  background-color: #3b82f6;
  font-weight: 600;
}
```

**Key points:**
- `getLinkClass` is a function that receives `{ isActive }` and returns the appropriate class name.
- The `end` prop on the Home NavLink (`to="/"`) ensures it is only marked active when the URL is exactly `/`, not on every page.
- The same `getLinkClass` function is reused for all NavLinks, keeping the code DRY.
</details>

---

**Exercise 4: 404 Not Found Page**

Add a 404 Not Found page to an existing React Router setup that catches all unmatched URLs.

Requirements:
- Create a `NotFound` component with a "404" heading, a message, and a link back to the home page
- Use the `path="*"` catch-all route
- Ensure it is the last route in the `<Routes>` block

<details>
<summary>Solution</summary>

```jsx
// src/pages/NotFound.jsx
import { Link } from "react-router-dom";

function NotFound() {
  return (
    <div style={{
      display: "flex",
      flexDirection: "column",
      alignItems: "center",
      justifyContent: "center",
      minHeight: "60vh",
      textAlign: "center",
      padding: "20px",
    }}>
      <h1 style={{ fontSize: "8rem", margin: "0", color: "#e5e7eb" }}>404</h1>
      <h2 style={{ marginTop: "0" }}>Page Not Found</h2>
      <p style={{ color: "#6b7280", maxWidth: "400px" }}>
        The page you are looking for might have been removed, had its name
        changed, or is temporarily unavailable.
      </p>
      <Link
        to="/"
        style={{
          marginTop: "16px",
          padding: "12px 24px",
          backgroundColor: "#3b82f6",
          color: "white",
          textDecoration: "none",
          borderRadius: "8px",
        }}
      >
        Return to Home
      </Link>
    </div>
  );
}

export default NotFound;

// src/App.jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Home from "./pages/Home";
import About from "./pages/About";
import Contact from "./pages/Contact";
import NotFound from "./pages/NotFound";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
        {/* Catch-all: must be the LAST route */}
        <Route path="*" element={<NotFound />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

**Key points:**
- `path="*"` acts as a wildcard that matches any URL not already handled by a previous route.
- It must be the **last** `<Route>` inside `<Routes>`. If placed first, it would intercept all URLs before other routes could match.
- The `NotFound` component provides a `<Link to="/">` so users can easily navigate back to the home page without manually editing the URL.
</details>

---

**Exercise 5: Protected Route with Authentication**

Implement a protected route system where unauthenticated users are redirected to a login page, and authenticated users can access a dashboard.

Requirements:
- Create a `ProtectedRoute` component that checks authentication
- If not authenticated, redirect to `/login`
- Create a `Login` page with a button that sets the user as authenticated
- Create a `Dashboard` page that is only accessible when authenticated
- Use `useNavigate` with `replace: true` after login

<details>
<summary>Solution</summary>

```jsx
// src/components/ProtectedRoute.jsx
import { Navigate } from "react-router-dom";

function ProtectedRoute({ isAuthenticated, children }) {
  if (!isAuthenticated) {
    return <Navigate to="/login" replace />;
  }
  return children;
}

export default ProtectedRoute;

// src/pages/Login.jsx
import { useNavigate } from "react-router-dom";

function Login({ onLogin }) {
  const navigate = useNavigate();

  function handleLogin(event) {
    event.preventDefault();
    // In a real app, validate credentials via API
    onLogin();
    navigate("/dashboard", { replace: true });
  }

  return (
    <div style={{ maxWidth: "400px", margin: "40px auto", padding: "20px" }}>
      <h1>Login</h1>
      <form onSubmit={handleLogin}>
        <div style={{ marginBottom: "12px" }}>
          <label>Email</label>
          <input type="email" placeholder="you@example.com" style={{ display: "block", width: "100%", padding: "8px" }} />
        </div>
        <div style={{ marginBottom: "12px" }}>
          <label>Password</label>
          <input type="password" placeholder="********" style={{ display: "block", width: "100%", padding: "8px" }} />
        </div>
        <button type="submit" style={{ padding: "10px 24px", backgroundColor: "#3b82f6", color: "white", border: "none", borderRadius: "6px", cursor: "pointer" }}>
          Log In
        </button>
      </form>
    </div>
  );
}

export default Login;

// src/pages/Dashboard.jsx
function Dashboard({ onLogout }) {
  return (
    <div style={{ padding: "20px" }}>
      <h1>Dashboard</h1>
      <p>Welcome! You are logged in. This page is protected.</p>
      <button onClick={onLogout} style={{ padding: "8px 16px", marginTop: "12px" }}>
        Log Out
      </button>
    </div>
  );
}

export default Dashboard;

// src/App.jsx
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";
import { useState } from "react";
import Login from "./pages/Login";
import Dashboard from "./pages/Dashboard";
import ProtectedRoute from "./components/ProtectedRoute";

function App() {
  const [isAuthenticated, setIsAuthenticated] = useState(false);

  return (
    <BrowserRouter>
      <nav style={{ padding: "12px 20px", backgroundColor: "#f3f4f6", display: "flex", gap: "16px" }}>
        <Link to="/">Home</Link>
        <Link to="/dashboard">Dashboard</Link>
        {!isAuthenticated ? (
          <Link to="/login">Login</Link>
        ) : (
          <span style={{ color: "green" }}>Logged In</span>
        )}
      </nav>

      <Routes>
        <Route path="/" element={<h1 style={{ padding: "20px" }}>Home - Public Page</h1>} />
        <Route
          path="/login"
          element={<Login onLogin={() => setIsAuthenticated(true)} />}
        />
        <Route
          path="/dashboard"
          element={
            <ProtectedRoute isAuthenticated={isAuthenticated}>
              <Dashboard onLogout={() => setIsAuthenticated(false)} />
            </ProtectedRoute>
          }
        />
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

**Key points:**
- `ProtectedRoute` checks `isAuthenticated`. If false, it renders `<Navigate to="/login" replace />`, redirecting the user.
- `replace` prevents the protected URL from appearing in browser history, so pressing Back does not loop back to the redirect.
- After successful login, `navigate("/dashboard", { replace: true })` sends the user to the dashboard and replaces the login page in history.
- The `onLogout` callback resets `isAuthenticated` to `false`, which immediately triggers the redirect on any protected page.
</details>
