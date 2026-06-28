# Week 20: React Router & Navigation

> **Prerequisites:** React components, JSX, props, state, useState, useEffect, and useRef from Weeks 16-19.

---

## Table of Contents

1. [What Is Client-Side Routing?](#1-what-is-client-side-routing)
2. [Installing React Router](#2-installing-react-router)
3. [BrowserRouter, Routes, Route -- Setup](#3-browserrouter-routes-route----setup)
4. [Link and NavLink Components](#4-link-and-navlink-components)
5. [NavLink Active Styling](#5-navlink-active-styling)
6. [Dynamic Routes with URL Parameters](#6-dynamic-routes-with-url-parameters)
7. [Nested Routes and Outlet](#7-nested-routes-and-outlet)
8. [Navigate Component and useNavigate Hook](#8-navigate-component-and-usenavigate-hook)
9. [404 Not Found Page](#9-404-not-found-page)
10. [Protected/Private Routes](#10-protectedprivate-routes)
11. [useLocation and useSearchParams Hooks](#11-uselocation-and-usesearchparams-hooks)
12. [Summary](#12-summary)

---

## 1. What Is Client-Side Routing?

### The Problem: Traditional Multi-Page Applications

In a traditional website (called a **Multi-Page Application** or MPA), every time you click a link, your browser sends a request to the server, the server processes it, and sends back an entirely new HTML page. The browser then throws away the current page, loads the new one, and the screen goes white for a moment while this happens.

Think of it like ordering food at a restaurant where the waiter takes your plate away every time you want to add a side dish, walks back to the kitchen, and brings an entirely new plate with everything on it. It works, but it is slow and disruptive.

```
  MULTI-PAGE APPLICATION (MPA) -- Traditional Websites
  =====================================================

  User clicks         Browser sends         Server processes       Browser receives
  "About" link        request to server     the request            ENTIRE new page
       |                    |                    |                       |
       v                    v                    v                       v
  +---------+        +------------+        +----------+          +-----------+
  | Home    | -----> | GET /about | -----> | Server   | -------> | About     |
  | Page    |        | (network)  |        | renders  |          | Page      |
  +---------+        +------------+        | HTML     |          | (full     |
                                           +----------+          |  reload)  |
                                                                 +-----------+
  
  Screen goes white.     Full page download.     Everything re-renders.
  JavaScript reloads.    CSS reloads.             State is lost.
```

### The Solution: Single-Page Applications

A **Single-Page Application** (SPA) works differently. The browser loads a single HTML page once. When you navigate to a different "page," JavaScript intercepts the click, swaps out the content on screen, and updates the URL in the address bar -- all without ever contacting the server for a new page. The browser never reloads. The experience feels instant.

This is like being at a restaurant where the waiter simply swaps the dish on your table without you ever leaving your seat. The table (page shell), the silverware (navigation bar), and your drink (global state) all stay exactly where they are.

```
  SINGLE-PAGE APPLICATION (SPA) -- React Applications
  ====================================================

  User clicks         React Router          React swaps           URL updates
  "About" link        intercepts click      component content     (no reload)
       |                    |                    |                       |
       v                    v                    v                       v
  +---------+        +------------+        +----------+          +-----------+
  | Home    | -----> | JavaScript | -----> | Unmount  | -------> | About     |
  | Page    |        | handles it |        | <Home/>  |          | Page      |
  +---------+        | locally    |        | Mount    |          | displayed |
                     +------------+        | <About/> |          +-----------+
                                           +----------+
  
  NO server request.     NO white screen.     State is preserved.
  NO full reload.        Instant transition.  Only changed part updates.
```

### SPA vs MPA Comparison

| Feature                    | Multi-Page App (MPA)      | Single-Page App (SPA)         |
| -------------------------- | ------------------------- | ----------------------------- |
| **Navigation**             | Full page reload          | Component swap (no reload)    |
| **Speed**                  | Slower (server round-trip)| Faster (instant swap)         |
| **Server requests**        | Every page change         | Only for data (APIs)          |
| **User experience**        | White screen flash        | Smooth, app-like              |
| **URL changes**            | Server handles URLs       | JavaScript manages URLs       |
| **State preservation**     | Lost on every navigation  | Preserved across pages        |
| **Initial load**           | Fast (small HTML)         | Slower (loads entire app JS)  |
| **SEO**                    | Naturally good            | Requires extra work (SSR)     |
| **Examples**               | Wikipedia, news sites     | Gmail, Twitter, Spotify       |

### What Is Client-Side Routing?

**Client-side routing** is the mechanism that makes SPA navigation work. A client-side router:

1. **Intercepts link clicks** so the browser does not send a request to the server.
2. **Reads the URL** to determine which component should be displayed.
3. **Renders the correct component** based on the URL.
4. **Updates the browser's address bar** so the URL reflects the current page (enabling bookmarking and the back button).

In React, the most popular library for client-side routing is **React Router**.

### Real-Life Analogy: A Building with Rooms

Think of a traditional website as a row of separate buildings. To visit a different department, you leave one building, walk outside, and enter another building. Each building has its own walls, furniture, and heating system that all need to load from scratch.

A single-page application is like one large building with many rooms. You walk through a hallway and step into different rooms (pages). The building structure (navbar, footer, layout) stays the same. Only the room contents change. The address on the door (URL) updates so someone can find you.

```
  MPA: Separate Buildings              SPA: One Building, Many Rooms
  ========================              ==============================

  +--------+  +--------+               +---------------------------+
  | Home   |  | About  |               |        NAVBAR             |
  | Bldg   |  | Bldg   |               +---------------------------+
  |        |  |        |               |        |         |        |
  |  (all  |  |  (all  |               | Home   | About   | Blog   |
  |  loads  |  |  loads  |               | Room   | Room    | Room   |
  |  fresh) |  |  fresh) |               |        |         |        |
  +--------+  +--------+               | (only  | (swap   | (swap  |
       ^^          ^^                   |  this   |  this)  |  this) |
   Walk outside  Walk outside           +---------------------------+
   every time    every time             |        FOOTER              |
                                        +---------------------------+
                                        Stay in the same building.
```

---

## 2. Installing React Router

React Router is a third-party library. It is not built into React. You need to install it separately.

### Installation

If you already have a React project (created with Vite or Create React App), open your terminal in the project directory and run:

```bash
npm install react-router-dom
```

This installs the `react-router-dom` package, which is the version of React Router designed for web applications (as opposed to `react-router-native` for React Native mobile apps).

### Verify Installation

After installation, check your `package.json` to confirm it was added:

```json
{
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-router-dom": "^6.20.0"
  }
}
```

You should see `react-router-dom` listed under `dependencies`.

### Import Pattern

Throughout this week, we will import various tools from React Router. The general pattern is:

```javascript
import { BrowserRouter, Routes, Route, Link, NavLink } from "react-router-dom";
```

You import exactly what you need. React Router provides many components and hooks, and we will cover the most important ones.

---

## 3. BrowserRouter, Routes, Route -- Setup

### The Three Core Pieces

React Router requires three components to set up basic routing:

1. **`BrowserRouter`** -- Wraps your entire application and enables routing. It uses the browser's History API to keep the URL in sync with the UI.
2. **`Routes`** -- A container that holds all your route definitions. It looks at the current URL and figures out which route matches.
3. **`Route`** -- Defines a single route. It maps a URL path to a React component.

```
  ROUTING ARCHITECTURE
  =====================

  <BrowserRouter>                    Enables routing for the whole app
       |
       +-- <Routes>                  Container for all routes
              |
              +-- <Route path="/" element={<Home />} />
              |
              +-- <Route path="/about" element={<About />} />
              |
              +-- <Route path="/contact" element={<Contact />} />

  URL: /           --> renders <Home />
  URL: /about      --> renders <About />
  URL: /contact    --> renders <Contact />
```

### Basic Setup

**Step 1: Create your page components.**

```jsx
// src/pages/Home.jsx
function Home() {
  return (
    <div>
      <h1>Home Page</h1>
      <p>Welcome to our website!</p>
    </div>
  );
}

export default Home;
```

```jsx
// src/pages/About.jsx
function About() {
  return (
    <div>
      <h1>About Us</h1>
      <p>We are a team of web developers learning React Router.</p>
    </div>
  );
}

export default About;
```

```jsx
// src/pages/Contact.jsx
function Contact() {
  return (
    <div>
      <h1>Contact Us</h1>
      <p>Email us at hello@example.com</p>
    </div>
  );
}

export default Contact;
```

**Step 2: Set up routing in your App component.**

```jsx
// src/App.jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Home from "./pages/Home";
import About from "./pages/About";
import Contact from "./pages/Contact";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

**How it works:**

1. `<BrowserRouter>` wraps everything and activates the routing system.
2. `<Routes>` examines the current URL.
3. Each `<Route>` checks if its `path` matches the URL. If it does, that route's `element` is rendered.
4. Only one route matches at a time. React Router picks the best match.

If the user visits `http://localhost:5173/about`, the `<About />` component renders. If they visit `/`, the `<Home />` component renders.

### Common Mistake: BrowserRouter Must Wrap Everything

A frequent error is placing `<Routes>` outside of `<BrowserRouter>`. This will crash your application with an error like: **"useRoutes() may be used only in the context of a Router component."**

```jsx
// WRONG -- Routes is outside BrowserRouter
function App() {
  return (
    <div>
      <Routes>
        <Route path="/" element={<Home />} />
      </Routes>
      <BrowserRouter>  {/* This does nothing here */}
      </BrowserRouter>
    </div>
  );
}

// CORRECT -- Routes is inside BrowserRouter
function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
      </Routes>
    </BrowserRouter>
  );
}
```

### Alternative: Wrapping in main.jsx

Many projects wrap `<BrowserRouter>` in the entry file (`main.jsx`) instead of inside `App.jsx`. This keeps `App` clean and ensures routing is available everywhere.

```jsx
// src/main.jsx
import React from "react";
import ReactDOM from "react-dom/client";
import { BrowserRouter } from "react-router-dom";
import App from "./App";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>
);
```

Then in `App.jsx`, you do not need `<BrowserRouter>` again:

```jsx
// src/App.jsx
import { Routes, Route } from "react-router-dom";
import Home from "./pages/Home";
import About from "./pages/About";

function App() {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/about" element={<About />} />
    </Routes>
  );
}

export default App;
```

Either approach works. Just never use `<BrowserRouter>` more than once in your app.

---

## 4. Link and NavLink Components

### The Problem with Anchor Tags in React

In plain HTML, you use `<a href="/about">About</a>` to create links. This works, but in a React SPA, clicking an `<a>` tag causes a **full page reload**. The browser sends a new request to the server, the entire JavaScript application restarts, all component state is lost, and the user sees a white flash.

This defeats the entire purpose of building a single-page application.

```
  <a> TAG IN REACT -- What Happens
  ==================================

  User clicks <a href="/about">

       |
       v
  Browser sends GET /about to server     <-- Full network request
       |
       v
  Server returns index.html              <-- Entire page downloaded
       |
       v
  Browser reloads EVERYTHING             <-- All JavaScript re-executes
       |                                     All state is LOST
       v                                     White screen flash
  React app restarts from scratch
```

### The Solution: Link Component

React Router provides the `<Link>` component as a replacement for `<a>`. It looks and behaves like a regular link, but instead of causing a page reload, it tells React Router to update the URL and swap the component -- all without reloading.

```jsx
import { Link } from "react-router-dom";

function Navbar() {
  return (
    <nav>
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
      <Link to="/contact">Contact</Link>
    </nav>
  );
}
```

**Key differences from `<a>`:**

| Feature        | `<a href="...">`          | `<Link to="...">`           |
| -------------- | ------------------------- | ---------------------------- |
| **Reload**     | Full page reload          | No reload                    |
| **State**      | All state is lost         | State is preserved           |
| **Speed**      | Slow (server round-trip)  | Instant (client-side swap)   |
| **Attribute**  | Uses `href`               | Uses `to`                    |
| **Rendered as**| `<a>` tag in DOM          | `<a>` tag in DOM (but with click handler) |

Under the hood, `<Link>` still renders an `<a>` tag in the actual HTML, so it is accessible and works with right-click "open in new tab." But it intercepts the click event to prevent the default browser navigation.

### When TO Use Regular Anchor Tags

Use `<a>` only for **external links** that go to a different website:

```jsx
function Footer() {
  return (
    <footer>
      {/* Internal link -- use Link */}
      <Link to="/about">About Us</Link>

      {/* External link -- use <a> */}
      <a href="https://github.com" target="_blank" rel="noopener noreferrer">
        GitHub
      </a>
    </footer>
  );
}
```

### NavLink Component

`<NavLink>` is a special version of `<Link>` that knows whether it matches the current URL. This is useful for navigation bars where you want to highlight the active page.

By default, NavLink automatically adds an `active` CSS class to the link when it matches the current route.

```jsx
import { NavLink } from "react-router-dom";

function Navbar() {
  return (
    <nav>
      <NavLink to="/">Home</NavLink>
      <NavLink to="/about">About</NavLink>
      <NavLink to="/contact">Contact</NavLink>
    </nav>
  );
}
```

If the user is on `/about`, the "About" link will have the class `active` in the DOM:

```html
<a href="/" class="">Home</a>
<a href="/about" class="active">About</a>    <!-- Current page -->
<a href="/contact" class="">Contact</a>
```

You can then style it with CSS:

```css
nav a.active {
  color: blue;
  font-weight: bold;
  border-bottom: 2px solid blue;
}
```

---

## 5. NavLink Active Styling

### The className Callback

NavLink accepts a `className` prop that can be a function instead of a string. This function receives an object with an `isActive` property, which you can use to conditionally apply classes.

```jsx
import { NavLink } from "react-router-dom";

function Navbar() {
  return (
    <nav>
      <NavLink
        to="/"
        className={({ isActive }) => (isActive ? "nav-active" : "nav-link")}
      >
        Home
      </NavLink>

      <NavLink
        to="/about"
        className={({ isActive }) => (isActive ? "nav-active" : "nav-link")}
      >
        About
      </NavLink>

      <NavLink
        to="/contact"
        className={({ isActive }) => (isActive ? "nav-active" : "nav-link")}
      >
        Contact
      </NavLink>
    </nav>
  );
}
```

```css
/* styles.css */
.nav-link {
  padding: 8px 16px;
  text-decoration: none;
  color: gray;
}

.nav-active {
  padding: 8px 16px;
  text-decoration: none;
  color: white;
  background-color: #3b82f6;
  border-radius: 4px;
  font-weight: bold;
}
```

### The style Callback

You can also use an inline `style` callback for dynamic styling:

```jsx
<NavLink
  to="/about"
  style={({ isActive }) => ({
    color: isActive ? "white" : "gray",
    backgroundColor: isActive ? "#3b82f6" : "transparent",
    fontWeight: isActive ? "bold" : "normal",
    padding: "8px 16px",
    textDecoration: "none",
    borderRadius: "4px",
  })}
>
  About
</NavLink>
```

### The end Prop

By default, NavLink matches if the current URL **starts with** the `to` path. This means the Home link (`to="/"`) would be "active" on every page because every URL starts with `/`.

The `end` prop tells NavLink to only match when the URL is **exactly** the `to` path.

```jsx
{/* Without end: Active on /, /about, /contact -- everything starts with / */}
<NavLink to="/">Home</NavLink>

{/* With end: Active ONLY on / */}
<NavLink to="/" end>Home</NavLink>
```

### Complete Navbar Example

```jsx
import { NavLink } from "react-router-dom";
import "./Navbar.css";

function Navbar() {
  const linkClass = ({ isActive }) =>
    isActive ? "nav-link active" : "nav-link";

  return (
    <nav className="navbar">
      <div className="navbar-brand">MyApp</div>
      <div className="navbar-links">
        <NavLink to="/" end className={linkClass}>
          Home
        </NavLink>
        <NavLink to="/about" className={linkClass}>
          About
        </NavLink>
        <NavLink to="/products" className={linkClass}>
          Products
        </NavLink>
        <NavLink to="/contact" className={linkClass}>
          Contact
        </NavLink>
      </div>
    </nav>
  );
}

export default Navbar;
```

```css
/* Navbar.css */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 32px;
  background-color: #1f2937;
}

.navbar-brand {
  color: white;
  font-size: 1.5rem;
  font-weight: bold;
}

.navbar-links {
  display: flex;
  gap: 8px;
}

.nav-link {
  color: #9ca3af;
  text-decoration: none;
  padding: 8px 16px;
  border-radius: 6px;
  transition: all 0.2s;
}

.nav-link:hover {
  color: white;
  background-color: #374151;
}

.nav-link.active {
  color: white;
  background-color: #3b82f6;
  font-weight: 600;
}
```

---

## 6. Dynamic Routes with URL Parameters

### The Problem: Hardcoding Every Route

Imagine you are building a blog with 500 posts. You cannot write 500 separate routes:

```jsx
// This is absurd. You would never do this.
<Route path="/post/1" element={<Post id={1} />} />
<Route path="/post/2" element={<Post id={2} />} />
<Route path="/post/3" element={<Post id={3} />} />
// ... 497 more routes
```

### The Solution: URL Parameters

React Router lets you define **dynamic segments** in a route path using the `:paramName` syntax. These segments match any value in that position of the URL.

```jsx
<Route path="/post/:id" element={<PostDetail />} />
```

This single route matches:
- `/post/1`
- `/post/2`
- `/post/hello`
- `/post/anything-here`

The `:id` part is a **URL parameter**. Whatever value appears in that position of the URL is captured and made available to the component.

### useParams Hook

The `useParams` hook lets you access the URL parameters inside the component that the route renders.

```jsx
import { useParams } from "react-router-dom";

function PostDetail() {
  const { id } = useParams();

  return (
    <div>
      <h1>Post #{id}</h1>
      <p>You are viewing post with ID: {id}</p>
    </div>
  );
}
```

If the user visits `/post/42`, the `id` variable will be the string `"42"`.

**Important:** URL parameters are always strings. If you need a number, convert it: `const numericId = Number(id);`

### Real-Life Example: Product Page

```jsx
// src/App.jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import ProductList from "./pages/ProductList";
import ProductDetail from "./pages/ProductDetail";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/products" element={<ProductList />} />
        <Route path="/products/:productId" element={<ProductDetail />} />
      </Routes>
    </BrowserRouter>
  );
}
```

```jsx
// src/pages/ProductList.jsx
import { Link } from "react-router-dom";

const products = [
  { id: 1, name: "Wireless Headphones", price: 79.99 },
  { id: 2, name: "Mechanical Keyboard", price: 129.99 },
  { id: 3, name: "USB-C Hub", price: 49.99 },
];

function ProductList() {
  return (
    <div>
      <h1>Our Products</h1>
      <ul>
        {products.map((product) => (
          <li key={product.id}>
            <Link to={`/products/${product.id}`}>
              {product.name} - ${product.price}
            </Link>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default ProductList;
```

```jsx
// src/pages/ProductDetail.jsx
import { useParams, Link } from "react-router-dom";
import { useState, useEffect } from "react";

const products = [
  { id: 1, name: "Wireless Headphones", price: 79.99, description: "Premium noise-cancelling headphones with 30-hour battery life." },
  { id: 2, name: "Mechanical Keyboard", price: 129.99, description: "Cherry MX switches with RGB backlighting." },
  { id: 3, name: "USB-C Hub", price: 49.99, description: "7-in-1 hub with HDMI, USB-A, and SD card reader." },
];

function ProductDetail() {
  const { productId } = useParams();
  const [product, setProduct] = useState(null);

  useEffect(() => {
    // In a real app, you would fetch from an API:
    // fetch(`/api/products/${productId}`).then(...)
    const found = products.find((p) => p.id === Number(productId));
    setProduct(found);
  }, [productId]);

  if (!product) {
    return <p>Product not found.</p>;
  }

  return (
    <div>
      <Link to="/products">Back to Products</Link>
      <h1>{product.name}</h1>
      <p>Price: ${product.price}</p>
      <p>{product.description}</p>
    </div>
  );
}

export default ProductDetail;
```

```
  DYNAMIC ROUTE FLOW
  ===================

  Route Definition:   /products/:productId

  URL visited:        /products/2
                                ^
                                |
                      productId = "2"

  Inside Component:
  const { productId } = useParams();
  // productId is "2"
  // Find product with id 2 --> "Mechanical Keyboard"
```

### Multiple URL Parameters

You can have multiple dynamic segments in a single route:

```jsx
<Route path="/users/:userId/posts/:postId" element={<UserPost />} />
```

```jsx
function UserPost() {
  const { userId, postId } = useParams();
  // URL: /users/5/posts/12
  // userId = "5", postId = "12"

  return (
    <div>
      <h1>User {userId}, Post {postId}</h1>
    </div>
  );
}
```

---

## 7. Nested Routes and Outlet

### What Are Nested Routes?

Nested routes let you render child components inside a parent component while keeping the parent layout on screen. This is how you build layouts where parts of the page (like a sidebar or header) stay constant while the main content area changes.

### Real-Life Analogy: A Dashboard

Think of a settings dashboard. The sidebar with menu items (Profile, Security, Notifications) stays visible at all times. When you click a menu item, only the main content area on the right changes. The sidebar does not re-render or disappear.

```
  NESTED ROUTES -- Dashboard Layout
  ===================================

  URL: /dashboard/profile
  +--------------------------------------------+
  |              DASHBOARD HEADER              |
  +----------+---------------------------------+
  |          |                                 |
  | Sidebar  |     Profile Content             |
  |          |     (changes based on URL)      |
  | Profile  |                                 |
  | Security |     <Outlet /> renders here     |
  | Billing  |                                 |
  |          |                                 |
  +----------+---------------------------------+

  URL: /dashboard/security
  +--------------------------------------------+
  |              DASHBOARD HEADER              |
  +----------+---------------------------------+
  |          |                                 |
  | Sidebar  |     Security Content            |
  |          |     (swapped in)                |
  | Profile  |                                 |
  | Security |     <Outlet /> renders here     |
  | Billing  |                                 |
  |          |                                 |
  +----------+---------------------------------+
```

### Setting Up Nested Routes

**Step 1: Define nested routes in App.jsx.**

```jsx
// src/App.jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Dashboard from "./pages/Dashboard";
import Profile from "./pages/Profile";
import Security from "./pages/Security";
import Billing from "./pages/Billing";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/dashboard" element={<Dashboard />}>
          {/* These are NESTED routes -- children of /dashboard */}
          <Route path="profile" element={<Profile />} />
          <Route path="security" element={<Security />} />
          <Route path="billing" element={<Billing />} />
        </Route>
      </Routes>
    </BrowserRouter>
  );
}
```

Notice:
- Child routes are placed **inside** the parent `<Route>`.
- Child paths are **relative** -- `path="profile"` means `/dashboard/profile`, not `/profile`.

**Step 2: Use `<Outlet />` in the parent component.**

The `<Outlet />` component is a placeholder that tells React Router: "Render the matching child route here."

```jsx
// src/pages/Dashboard.jsx
import { Outlet, NavLink } from "react-router-dom";

function Dashboard() {
  return (
    <div style={{ display: "flex" }}>
      {/* Sidebar -- always visible */}
      <nav style={{ width: "200px", borderRight: "1px solid #ccc", padding: "16px" }}>
        <h2>Settings</h2>
        <ul style={{ listStyle: "none", padding: 0 }}>
          <li><NavLink to="profile">Profile</NavLink></li>
          <li><NavLink to="security">Security</NavLink></li>
          <li><NavLink to="billing">Billing</NavLink></li>
        </ul>
      </nav>

      {/* Main content -- changes based on URL */}
      <main style={{ flex: 1, padding: "16px" }}>
        <Outlet />
      </main>
    </div>
  );
}

export default Dashboard;
```

```jsx
// src/pages/Profile.jsx
function Profile() {
  return (
    <div>
      <h1>Profile Settings</h1>
      <p>Edit your name, email, and profile picture.</p>
    </div>
  );
}

export default Profile;
```

```jsx
// src/pages/Security.jsx
function Security() {
  return (
    <div>
      <h1>Security Settings</h1>
      <p>Change your password and enable two-factor authentication.</p>
    </div>
  );
}

export default Security;
```

### Index Route

What happens when the user visits `/dashboard` without a child path? Nothing renders in the `<Outlet />`. You can define an **index route** to show default content:

```jsx
<Route path="/dashboard" element={<Dashboard />}>
  <Route index element={<p>Select an option from the sidebar.</p>} />
  <Route path="profile" element={<Profile />} />
  <Route path="security" element={<Security />} />
  <Route path="billing" element={<Billing />} />
</Route>
```

The `index` route matches when the URL is exactly `/dashboard` with no additional path.

```
  NESTED ROUTE MATCHING
  ======================

  URL: /dashboard           --> <Dashboard> + index (default content)
  URL: /dashboard/profile   --> <Dashboard> + <Profile />
  URL: /dashboard/security  --> <Dashboard> + <Security />
  URL: /dashboard/billing   --> <Dashboard> + <Billing />
```

---

## 8. Navigate Component and useNavigate Hook

### Why Programmatic Navigation?

Sometimes you need to navigate the user to a different page without them clicking a link. Common scenarios:

- After a form submission, redirect to a success page.
- After login, redirect to the dashboard.
- After deleting an item, go back to the list.
- After a timer expires, redirect to a timeout page.

### useNavigate Hook

The `useNavigate` hook returns a function that you can call to navigate programmatically.

```jsx
import { useNavigate } from "react-router-dom";

function LoginForm() {
  const navigate = useNavigate();

  function handleSubmit(event) {
    event.preventDefault();

    // Perform login logic (API call, validation, etc.)
    const loginSuccessful = true;

    if (loginSuccessful) {
      // Redirect to dashboard after successful login
      navigate("/dashboard");
    }
  }

  return (
    <form onSubmit={handleSubmit}>
      <input type="email" placeholder="Email" />
      <input type="password" placeholder="Password" />
      <button type="submit">Log In</button>
    </form>
  );
}
```

### navigate Options

```jsx
const navigate = useNavigate();

// Navigate to a path
navigate("/dashboard");

// Navigate and REPLACE the current history entry
// (user cannot press Back to return to the login page)
navigate("/dashboard", { replace: true });

// Go back (like pressing the browser's Back button)
navigate(-1);

// Go forward
navigate(1);

// Go back two pages
navigate(-2);
```

**When to use `replace: true`:** After login or form submission where going "back" to the form would be confusing or cause duplicate submissions.

### Real-Life Example: Contact Form

```jsx
import { useState } from "react";
import { useNavigate } from "react-router-dom";

function ContactForm() {
  const navigate = useNavigate();
  const [formData, setFormData] = useState({ name: "", message: "" });
  const [isSubmitting, setIsSubmitting] = useState(false);

  async function handleSubmit(event) {
    event.preventDefault();
    setIsSubmitting(true);

    // Simulate API call
    await new Promise((resolve) => setTimeout(resolve, 1000));

    console.log("Form submitted:", formData);

    // After successful submission, redirect to thank-you page
    // Using replace: true so user cannot "go back" to re-submit
    navigate("/thank-you", { replace: true });
  }

  return (
    <form onSubmit={handleSubmit}>
      <h1>Contact Us</h1>
      <input
        type="text"
        placeholder="Your name"
        value={formData.name}
        onChange={(e) => setFormData({ ...formData, name: e.target.value })}
      />
      <textarea
        placeholder="Your message"
        value={formData.message}
        onChange={(e) => setFormData({ ...formData, message: e.target.value })}
      />
      <button type="submit" disabled={isSubmitting}>
        {isSubmitting ? "Sending..." : "Send Message"}
      </button>
    </form>
  );
}
```

### Navigate Component (Declarative Redirect)

The `<Navigate>` component is the declarative version of `useNavigate`. When it renders, it immediately redirects the user to the specified path.

```jsx
import { Navigate } from "react-router-dom";

function OldPage() {
  // This page has been moved. Redirect to the new location.
  return <Navigate to="/new-page" replace />;
}
```

A common use case is redirecting old URLs to new ones:

```jsx
<Routes>
  <Route path="/new-page" element={<NewPage />} />
  {/* Old URL redirects to new URL */}
  <Route path="/old-page" element={<Navigate to="/new-page" replace />} />
</Routes>
```

```
  PROGRAMMATIC NAVIGATION FLOW
  ==============================

  User submits form
       |
       v
  handleSubmit() runs
       |
       v
  API call succeeds
       |
       v
  navigate("/dashboard", { replace: true })
       |
       v
  URL changes to /dashboard
  <Dashboard /> renders
  User CANNOT press Back to return to form
```

---

## 9. 404 Not Found Page

### The Problem

What happens when a user visits a URL that does not match any of your routes? By default, React Router renders nothing. The user sees a blank page, which is confusing.

### The Solution: Catch-All Route

React Router provides a special path `"*"` that matches any URL that has not been matched by previous routes. This is called a **catch-all** or **wildcard** route.

```jsx
// src/pages/NotFound.jsx
import { Link } from "react-router-dom";

function NotFound() {
  return (
    <div style={{ textAlign: "center", padding: "80px 20px" }}>
      <h1 style={{ fontSize: "6rem", margin: 0 }}>404</h1>
      <h2>Page Not Found</h2>
      <p>Sorry, the page you are looking for does not exist.</p>
      <Link to="/" style={{ color: "#3b82f6", textDecoration: "underline" }}>
        Go back to Home
      </Link>
    </div>
  );
}

export default NotFound;
```

```jsx
// src/App.jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Home from "./pages/Home";
import About from "./pages/About";
import NotFound from "./pages/NotFound";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        {/* Catch-all route -- must be LAST */}
        <Route path="*" element={<NotFound />} />
      </Routes>
    </BrowserRouter>
  );
}
```

**How it works:**

1. React Router checks each route in order.
2. `/` matches the Home route. `/about` matches the About route.
3. Any other URL (like `/xyz` or `/products/999`) does not match any route.
4. The `path="*"` route catches everything that was not matched.
5. The `<NotFound />` component renders.

```
  CATCH-ALL ROUTE MATCHING
  =========================

  URL: /              --> matches "/"       --> <Home />
  URL: /about         --> matches "/about"  --> <About />
  URL: /xyz           --> no match          --> "*" catches it --> <NotFound />
  URL: /foo/bar/baz   --> no match          --> "*" catches it --> <NotFound />
```

**Important:** Always place the `path="*"` route **last** in your `<Routes>`. If you place it first, it would match every URL before the other routes get a chance.

---

## 10. Protected/Private Routes

### The Problem

Many applications have pages that should only be accessible to logged-in users. If someone who is not authenticated tries to visit `/dashboard`, they should be redirected to the login page instead.

### Real-Life Analogy

Think of a building with a security guard at the entrance. Public areas like the lobby (home page) are open to everyone. But to access the offices (dashboard, settings), you need to show your badge (authentication token). If you do not have a badge, the guard redirects you to the reception desk (login page) to get one.

```
  PROTECTED ROUTE FLOW
  =====================

  User tries to visit /dashboard
       |
       v
  +-------------------+
  | Is user logged in?|
  +-------------------+
       |           |
      YES          NO
       |           |
       v           v
  +---------+  +-----------+
  | Render  |  | Redirect  |
  | Dashboard|  | to /login |
  +---------+  +-----------+
```

### Building a ProtectedRoute Component

```jsx
// src/components/ProtectedRoute.jsx
import { Navigate } from "react-router-dom";

function ProtectedRoute({ isAuthenticated, children }) {
  if (!isAuthenticated) {
    // User is not logged in. Redirect to login page.
    return <Navigate to="/login" replace />;
  }

  // User is logged in. Render the protected content.
  return children;
}

export default ProtectedRoute;
```

### Using ProtectedRoute in Your App

```jsx
// src/App.jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import { useState } from "react";
import Home from "./pages/Home";
import Login from "./pages/Login";
import Dashboard from "./pages/Dashboard";
import Settings from "./pages/Settings";
import ProtectedRoute from "./components/ProtectedRoute";

function App() {
  const [isAuthenticated, setIsAuthenticated] = useState(false);

  return (
    <BrowserRouter>
      <Routes>
        {/* Public routes -- anyone can access */}
        <Route path="/" element={<Home />} />
        <Route
          path="/login"
          element={<Login onLogin={() => setIsAuthenticated(true)} />}
        />

        {/* Protected routes -- only logged-in users */}
        <Route
          path="/dashboard"
          element={
            <ProtectedRoute isAuthenticated={isAuthenticated}>
              <Dashboard />
            </ProtectedRoute>
          }
        />
        <Route
          path="/settings"
          element={
            <ProtectedRoute isAuthenticated={isAuthenticated}>
              <Settings />
            </ProtectedRoute>
          }
        />
      </Routes>
    </BrowserRouter>
  );
}
```

### Login Page

```jsx
// src/pages/Login.jsx
import { useNavigate } from "react-router-dom";

function Login({ onLogin }) {
  const navigate = useNavigate();

  function handleLogin(event) {
    event.preventDefault();
    // In a real app, you would validate credentials with an API
    onLogin(); // Set isAuthenticated to true
    navigate("/dashboard", { replace: true });
  }

  return (
    <form onSubmit={handleLogin}>
      <h1>Login</h1>
      <input type="email" placeholder="Email" />
      <input type="password" placeholder="Password" />
      <button type="submit">Log In</button>
    </form>
  );
}

export default Login;
```

### Protected Route with Layout (Using Outlet)

If you have many protected routes, wrapping each one individually is repetitive. A cleaner approach uses nested routes with `<Outlet>`:

```jsx
// src/components/ProtectedLayout.jsx
import { Navigate, Outlet } from "react-router-dom";

function ProtectedLayout({ isAuthenticated }) {
  if (!isAuthenticated) {
    return <Navigate to="/login" replace />;
  }

  return <Outlet />;
}

export default ProtectedLayout;
```

```jsx
// src/App.jsx
function App() {
  const [isAuthenticated, setIsAuthenticated] = useState(false);

  return (
    <BrowserRouter>
      <Routes>
        {/* Public routes */}
        <Route path="/" element={<Home />} />
        <Route path="/login" element={<Login onLogin={() => setIsAuthenticated(true)} />} />

        {/* All routes inside here are protected */}
        <Route element={<ProtectedLayout isAuthenticated={isAuthenticated} />}>
          <Route path="/dashboard" element={<Dashboard />} />
          <Route path="/settings" element={<Settings />} />
          <Route path="/profile" element={<Profile />} />
        </Route>
      </Routes>
    </BrowserRouter>
  );
}
```

Now every route inside the `<ProtectedLayout>` wrapper is automatically protected. You add a new protected page by simply adding a `<Route>` inside that group.

---

## 11. useLocation and useSearchParams Hooks

### useLocation

The `useLocation` hook returns an object representing the current URL. This is useful when you need to know the current path, read state passed during navigation, or track page changes for analytics.

```jsx
import { useLocation } from "react-router-dom";

function CurrentPage() {
  const location = useLocation();

  console.log(location);
  // {
  //   pathname: "/products",
  //   search: "?category=electronics&sort=price",
  //   hash: "#top",
  //   state: null,
  //   key: "default"
  // }

  return <p>You are on: {location.pathname}</p>;
}
```

### useLocation Properties

| Property     | Description                            | Example                        |
| ------------ | -------------------------------------- | ------------------------------ |
| `pathname`   | The URL path                           | `"/products"`                  |
| `search`     | The query string (including `?`)       | `"?category=electronics"`     |
| `hash`       | The URL fragment (including `#`)       | `"#top"`                       |
| `state`      | Data passed via `navigate()` or `Link` | `{ from: "/cart" }`           |
| `key`        | A unique key for this location         | `"f1a2b3c4"`                   |

### Passing State with Navigation

You can pass hidden data along with navigation that does not appear in the URL:

```jsx
// Sending state
<Link to="/checkout" state={{ from: "/cart", itemCount: 3 }}>
  Proceed to Checkout
</Link>

// Or with useNavigate
navigate("/checkout", { state: { from: "/cart", itemCount: 3 } });
```

```jsx
// Receiving state in the target component
import { useLocation } from "react-router-dom";

function Checkout() {
  const location = useLocation();
  const { from, itemCount } = location.state || {};

  return (
    <div>
      <h1>Checkout</h1>
      {from && <p>You came from: {from}</p>}
      {itemCount && <p>Items in cart: {itemCount}</p>}
    </div>
  );
}
```

### useSearchParams

The `useSearchParams` hook gives you access to the URL's query parameters (the part after `?`). It works like `useState` but for URL query strings.

```
  URL ANATOMY
  ============

  https://mystore.com/products?category=shoes&sort=price&page=2
                       |          |                               
                   pathname     search params (query string)
                                  category = "shoes"
                                  sort     = "price"
                                  page     = "2"
```

### Reading Search Params

```jsx
import { useSearchParams } from "react-router-dom";

function ProductList() {
  const [searchParams] = useSearchParams();

  const category = searchParams.get("category"); // "shoes" or null
  const sort = searchParams.get("sort");          // "price" or null
  const page = searchParams.get("page");          // "2" or null

  return (
    <div>
      <h1>Products</h1>
      {category && <p>Filtering by: {category}</p>}
      {sort && <p>Sorting by: {sort}</p>}
      {page && <p>Page: {page}</p>}
    </div>
  );
}
```

### Setting Search Params

```jsx
import { useSearchParams } from "react-router-dom";

function ProductFilters() {
  const [searchParams, setSearchParams] = useSearchParams();

  function handleCategoryChange(category) {
    // Update the URL to /products?category=shoes
    setSearchParams({ category });
  }

  function handleSortChange(sort) {
    // Preserve existing params and add/update sort
    setSearchParams((prev) => {
      prev.set("sort", sort);
      return prev;
    });
  }

  function clearFilters() {
    setSearchParams({});
  }

  return (
    <div>
      <h2>Filters</h2>
      <button onClick={() => handleCategoryChange("shoes")}>Shoes</button>
      <button onClick={() => handleCategoryChange("shirts")}>Shirts</button>
      <button onClick={() => handleSortChange("price")}>Sort by Price</button>
      <button onClick={() => handleSortChange("name")}>Sort by Name</button>
      <button onClick={clearFilters}>Clear All</button>

      <p>Active category: {searchParams.get("category") || "All"}</p>
      <p>Sort: {searchParams.get("sort") || "Default"}</p>
    </div>
  );
}
```

### Real-Life Example: Search Page

```jsx
import { useState, useEffect } from "react";
import { useSearchParams } from "react-router-dom";

function SearchPage() {
  const [searchParams, setSearchParams] = useSearchParams();
  const [results, setResults] = useState([]);

  // Read the current query from the URL
  const query = searchParams.get("q") || "";

  // Fetch results whenever the query changes
  useEffect(() => {
    if (query) {
      // In a real app, fetch from API
      console.log("Searching for:", query);
      // fetch(`/api/search?q=${query}`).then(...)
    }
  }, [query]);

  function handleSearch(event) {
    event.preventDefault();
    const formData = new FormData(event.target);
    const newQuery = formData.get("search");

    // Update the URL: /search?q=react+router
    setSearchParams({ q: newQuery });
  }

  return (
    <div>
      <h1>Search</h1>
      <form onSubmit={handleSearch}>
        <input name="search" defaultValue={query} placeholder="Search..." />
        <button type="submit">Search</button>
      </form>
      {query && <p>Showing results for: "{query}"</p>}
    </div>
  );
}
```

The beauty of `useSearchParams` is that the search query lives in the URL. Users can bookmark or share search results, and pressing the back button returns to previous search results.

---

## 12. Summary

### What We Covered

This week introduced client-side routing with React Router, enabling multi-page navigation in single-page React applications.

| Concept                | Key Takeaway                                                              |
| ---------------------- | ------------------------------------------------------------------------- |
| **Client-Side Routing** | JavaScript swaps components without page reload, keeping state intact    |
| **BrowserRouter**       | Wraps the app and enables the routing system                             |
| **Routes + Route**      | Define URL-to-component mappings                                         |
| **Link**                | Navigate without page reload (replaces `<a>` for internal links)         |
| **NavLink**             | Link with active state awareness for navigation highlighting             |
| **URL Parameters**      | Dynamic route segments (`:id`) accessed via `useParams()`                |
| **Nested Routes**       | Child routes render inside parent via `<Outlet />`                       |
| **useNavigate**         | Programmatic navigation (after form submit, login, etc.)                 |
| **Navigate**            | Declarative redirect component                                           |
| **path="*"**            | Catch-all route for 404 Not Found pages                                  |
| **Protected Routes**    | Redirect unauthenticated users with `<Navigate to="/login" />`           |
| **useLocation**         | Access current URL info, pathname, search, and passed state              |
| **useSearchParams**     | Read and write URL query parameters like `?category=shoes`               |

### Route Patterns Cheat Sheet

```jsx
import { BrowserRouter, Routes, Route, Navigate, Outlet } from "react-router-dom";

<BrowserRouter>
  <Routes>
    {/* Basic route */}
    <Route path="/" element={<Home />} />

    {/* Static routes */}
    <Route path="/about" element={<About />} />
    <Route path="/contact" element={<Contact />} />

    {/* Dynamic route with URL parameter */}
    <Route path="/products/:id" element={<ProductDetail />} />

    {/* Multiple URL parameters */}
    <Route path="/users/:userId/posts/:postId" element={<UserPost />} />

    {/* Nested routes with layout */}
    <Route path="/dashboard" element={<DashboardLayout />}>
      <Route index element={<DashboardHome />} />
      <Route path="profile" element={<Profile />} />
      <Route path="settings" element={<Settings />} />
    </Route>

    {/* Protected routes group */}
    <Route element={<ProtectedLayout />}>
      <Route path="/admin" element={<Admin />} />
      <Route path="/billing" element={<Billing />} />
    </Route>

    {/* Redirect old URL to new URL */}
    <Route path="/old-page" element={<Navigate to="/new-page" replace />} />

    {/* 404 catch-all (always last) */}
    <Route path="*" element={<NotFound />} />
  </Routes>
</BrowserRouter>
```

### Navigation Cheat Sheet

```jsx
// Declarative navigation (in JSX)
import { Link, NavLink, Navigate } from "react-router-dom";

<Link to="/about">About</Link>
<NavLink to="/about" className={({ isActive }) => isActive ? "active" : ""}>About</NavLink>
<Navigate to="/login" replace />

// Programmatic navigation (in event handlers)
import { useNavigate } from "react-router-dom";

const navigate = useNavigate();
navigate("/dashboard");               // Go to dashboard
navigate("/dashboard", { replace: true }); // Go and replace history
navigate(-1);                          // Go back

// Read URL info
import { useParams, useLocation, useSearchParams } from "react-router-dom";

const { id } = useParams();                          // URL params
const location = useLocation();                      // Full URL info
const [searchParams, setSearchParams] = useSearchParams(); // Query params
```

### Common Mistakes to Avoid

| Mistake                              | Problem                                    | Solution                                      |
| ------------------------------------ | ------------------------------------------ | --------------------------------------------- |
| Using `<a>` for internal links       | Full page reload, state lost               | Use `<Link>` or `<NavLink>` instead           |
| Routes outside BrowserRouter         | Crash: "useRoutes() not in Router context" | Wrap everything in `<BrowserRouter>`          |
| Placing `path="*"` first             | Catches all URLs before other routes match | Always put the catch-all route **last**       |
| Forgetting `<Outlet />` in parent    | Nested child routes render nothing         | Add `<Outlet />` where children should appear |
| Not using `replace` after login      | User can "go back" to login form           | Use `navigate("/dash", { replace: true })`    |
| URL params are numbers not strings   | Comparison fails (`"2" !== 2`)             | Convert with `Number(id)`                     |
| Multiple `<BrowserRouter>` wrappers  | Unexpected routing behavior                | Use `<BrowserRouter>` only once in the app    |

### What Is Next

In Week 21, we will learn advanced React patterns including the Context API for global state management, custom hooks for reusable logic, and performance optimization with `React.memo`, `useMemo`, and `useCallback`. We will bring everything together in a complete multi-page React project.
