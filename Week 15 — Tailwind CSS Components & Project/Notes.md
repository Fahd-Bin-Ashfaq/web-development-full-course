# Week 15 — Tailwind CSS Components & Project

## Table of Contents

1. [Building Reusable Components](#1-building-reusable-components)
2. [Customizing Tailwind Configuration](#2-customizing-tailwind-configuration)
3. [Dark Mode](#3-dark-mode)
4. [Tailwind Plugins & Ecosystem](#4-tailwind-plugins--ecosystem)
5. [Performance](#5-performance)
6. [Common Component Patterns](#6-common-component-patterns)
7. [Week 15 Project: Responsive Landing Page](#7-week-15-project-responsive-landing-page)
8. [Summary](#8-summary)

---

## 1. Building Reusable Components

In Week 14 we learned individual utility classes. Now we combine them to build real UI components.

**Real-Life Example:** Individual LEGO bricks are like utility classes. A completed LEGO spaceship is a component — built from many small pieces, reusable, and recognizable.

### Navbar

```html
<nav class="bg-white shadow-md">
  <div class="max-w-7xl mx-auto px-4 py-3 flex items-center justify-between">
    <!-- Logo -->
    <a href="#" class="text-2xl font-bold text-blue-600">MyBrand</a>

    <!-- Navigation Links -->
    <ul class="hidden md:flex space-x-8">
      <li><a href="#" class="text-gray-700 hover:text-blue-600 transition">Home</a></li>
      <li><a href="#" class="text-gray-700 hover:text-blue-600 transition">About</a></li>
      <li><a href="#" class="text-gray-700 hover:text-blue-600 transition">Services</a></li>
      <li><a href="#" class="text-gray-700 hover:text-blue-600 transition">Contact</a></li>
    </ul>

    <!-- CTA Button -->
    <a href="#" class="hidden md:block bg-blue-600 text-white px-6 py-2 rounded-lg hover:bg-blue-700 transition">
      Get Started
    </a>

    <!-- Mobile Menu Button -->
    <button class="md:hidden text-gray-700">
      <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"/>
      </svg>
    </button>
  </div>
</nav>
```

### Cards

#### Product Card

```html
<div class="max-w-sm bg-white rounded-xl shadow-lg overflow-hidden hover:shadow-xl transition-shadow">
  <img src="product.jpg" alt="Product" class="w-full h-48 object-cover">
  <div class="p-6">
    <span class="text-sm text-blue-600 font-semibold uppercase">New Arrival</span>
    <h3 class="text-xl font-bold text-gray-800 mt-2">Wireless Headphones</h3>
    <p class="text-gray-600 mt-2">Premium sound quality with 30-hour battery life.</p>
    <div class="flex items-center justify-between mt-4">
      <span class="text-2xl font-bold text-gray-900">$99.99</span>
      <button class="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition">
        Add to Cart
      </button>
    </div>
  </div>
</div>
```

#### Profile Card

```html
<div class="max-w-xs bg-white rounded-2xl shadow-lg text-center p-8">
  <img src="avatar.jpg" alt="Profile" class="w-24 h-24 rounded-full mx-auto object-cover border-4 border-blue-100">
  <h3 class="text-xl font-bold mt-4 text-gray-800">Sarah Johnson</h3>
  <p class="text-blue-600 text-sm">Full-Stack Developer</p>
  <p class="text-gray-500 mt-3 text-sm">Building web apps with the MERN stack. Open source contributor.</p>
  <div class="flex justify-center space-x-4 mt-4">
    <a href="#" class="text-gray-400 hover:text-blue-600 transition">GitHub</a>
    <a href="#" class="text-gray-400 hover:text-blue-600 transition">LinkedIn</a>
    <a href="#" class="text-gray-400 hover:text-blue-600 transition">Twitter</a>
  </div>
</div>
```

### Buttons

```html
<!-- Primary -->
<button class="bg-blue-600 text-white px-6 py-2.5 rounded-lg hover:bg-blue-700 active:bg-blue-800 transition font-medium">
  Primary
</button>

<!-- Secondary -->
<button class="bg-gray-200 text-gray-800 px-6 py-2.5 rounded-lg hover:bg-gray-300 transition font-medium">
  Secondary
</button>

<!-- Outline -->
<button class="border-2 border-blue-600 text-blue-600 px-6 py-2.5 rounded-lg hover:bg-blue-600 hover:text-white transition font-medium">
  Outline
</button>

<!-- Danger -->
<button class="bg-red-600 text-white px-6 py-2.5 rounded-lg hover:bg-red-700 transition font-medium">
  Delete
</button>

<!-- Disabled -->
<button class="bg-gray-300 text-gray-500 px-6 py-2.5 rounded-lg cursor-not-allowed font-medium" disabled>
  Disabled
</button>
```

### Forms

```html
<form class="max-w-md mx-auto space-y-4">
  <div>
    <label class="block text-sm font-medium text-gray-700 mb-1">Full Name</label>
    <input type="text" placeholder="John Doe"
      class="w-full px-4 py-2.5 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none transition">
  </div>
  <div>
    <label class="block text-sm font-medium text-gray-700 mb-1">Email</label>
    <input type="email" placeholder="john@example.com"
      class="w-full px-4 py-2.5 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none transition">
  </div>
  <div>
    <label class="block text-sm font-medium text-gray-700 mb-1">Message</label>
    <textarea rows="4" placeholder="Your message..."
      class="w-full px-4 py-2.5 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none transition resize-none"></textarea>
  </div>
  <button type="submit"
    class="w-full bg-blue-600 text-white py-2.5 rounded-lg hover:bg-blue-700 transition font-medium">
    Send Message
  </button>
</form>
```

### Alerts

```html
<!-- Success -->
<div class="bg-green-50 border-l-4 border-green-500 p-4 rounded-r-lg">
  <div class="flex items-center">
    <span class="text-green-600 font-medium">Success!</span>
    <p class="text-green-700 ml-2">Your account has been created successfully.</p>
  </div>
</div>

<!-- Error -->
<div class="bg-red-50 border-l-4 border-red-500 p-4 rounded-r-lg">
  <div class="flex items-center">
    <span class="text-red-600 font-medium">Error!</span>
    <p class="text-red-700 ml-2">Please check your email and password.</p>
  </div>
</div>

<!-- Warning -->
<div class="bg-yellow-50 border-l-4 border-yellow-500 p-4 rounded-r-lg">
  <div class="flex items-center">
    <span class="text-yellow-600 font-medium">Warning!</span>
    <p class="text-yellow-700 ml-2">Your trial expires in 3 days.</p>
  </div>
</div>

<!-- Info -->
<div class="bg-blue-50 border-l-4 border-blue-500 p-4 rounded-r-lg">
  <div class="flex items-center">
    <span class="text-blue-600 font-medium">Info:</span>
    <p class="text-blue-700 ml-2">System maintenance scheduled for tonight.</p>
  </div>
</div>
```

### Badges

```html
<span class="bg-blue-100 text-blue-800 text-xs font-semibold px-2.5 py-0.5 rounded-full">New</span>
<span class="bg-green-100 text-green-800 text-xs font-semibold px-2.5 py-0.5 rounded-full">Active</span>
<span class="bg-red-100 text-red-800 text-xs font-semibold px-2.5 py-0.5 rounded-full">Closed</span>
<span class="bg-yellow-100 text-yellow-800 text-xs font-semibold px-2.5 py-0.5 rounded-full">Pending</span>
```

---

## 2. Customizing Tailwind Configuration

The `tailwind.config.js` file is where you customize the entire design system.

### Basic Configuration

```js
// tailwind.config.js
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {
      // Custom colors
      colors: {
        primary: {
          50: '#eff6ff',
          100: '#dbeafe',
          500: '#3b82f6',
          600: '#2563eb',
          700: '#1d4ed8',
        },
        brand: '#FF6B35',
      },

      // Custom fonts
      fontFamily: {
        heading: ['Poppins', 'sans-serif'],
        body: ['Inter', 'sans-serif'],
      },

      // Custom spacing
      spacing: {
        '128': '32rem',
        '144': '36rem',
      },

      // Custom breakpoints
      screens: {
        'xs': '475px',
        '3xl': '1920px',
      },

      // Custom border radius
      borderRadius: {
        '4xl': '2rem',
      },
    },
  },
  plugins: [],
}
```

### Extend vs Override

| Approach | What It Does | When to Use |
|----------|-------------|-------------|
| `theme.extend.colors` | **Adds** your colors while keeping defaults | Most of the time |
| `theme.colors` | **Replaces** all default colors with yours | When you want a completely custom palette |

### Adding Custom Utilities with @layer

```css
/* In your CSS file */
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer components {
  .btn-primary {
    @apply bg-blue-600 text-white px-6 py-2.5 rounded-lg 
           hover:bg-blue-700 active:bg-blue-800 transition font-medium;
  }

  .card {
    @apply bg-white rounded-xl shadow-lg p-6 hover:shadow-xl transition-shadow;
  }

  .input-field {
    @apply w-full px-4 py-2.5 border border-gray-300 rounded-lg 
           focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none;
  }
}
```

Now you can use these everywhere:

```html
<button class="btn-primary">Click Me</button>
<div class="card">Content here</div>
<input class="input-field" placeholder="Type here...">
```

---

## 3. Dark Mode

Tailwind has built-in dark mode support using the `dark:` prefix.

### Enabling Dark Mode

```js
// tailwind.config.js
export default {
  darkMode: 'class',  // 'class' strategy — toggle with a CSS class
  // ...
}
```

| Strategy | How It Works | Use When |
|----------|-------------|----------|
| `'class'` | Add/remove `dark` class on `<html>` element | You want a manual toggle button |
| `'media'` | Follows user's OS preference automatically | You want automatic detection |

### Using dark: Prefix

```html
<div class="bg-white dark:bg-gray-900 text-gray-800 dark:text-gray-100 min-h-screen">
  <nav class="bg-gray-100 dark:bg-gray-800 p-4">
    <h1 class="text-blue-600 dark:text-blue-400 text-2xl font-bold">My Website</h1>
  </nav>

  <div class="bg-white dark:bg-gray-800 rounded-xl shadow-lg dark:shadow-gray-700/30 p-6 m-4">
    <h2 class="text-gray-800 dark:text-white text-xl font-bold">Card Title</h2>
    <p class="text-gray-600 dark:text-gray-300 mt-2">Card description goes here.</p>
    <button class="bg-blue-600 dark:bg-blue-500 text-white px-4 py-2 rounded-lg mt-4 
                   hover:bg-blue-700 dark:hover:bg-blue-400 transition">
      Action
    </button>
  </div>
</div>
```

### Dark Mode Toggle with JavaScript

```html
<button id="theme-toggle" class="p-2 rounded-lg bg-gray-200 dark:bg-gray-700">
  <span id="light-icon" class="hidden dark:inline">☀️ Light</span>
  <span id="dark-icon" class="inline dark:hidden">🌙 Dark</span>
</button>

<script>
  const toggle = document.getElementById('theme-toggle');

  // Check saved preference or OS preference
  if (localStorage.theme === 'dark' ||
      (!localStorage.theme && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
    document.documentElement.classList.add('dark');
  }

  toggle.addEventListener('click', () => {
    document.documentElement.classList.toggle('dark');
    localStorage.theme = document.documentElement.classList.contains('dark') ? 'dark' : 'light';
  });
</script>
```

### Color Planning for Dark Mode

| Element | Light Mode | Dark Mode |
|---------|-----------|-----------|
| Background | `bg-white` | `dark:bg-gray-900` |
| Card Background | `bg-gray-50` | `dark:bg-gray-800` |
| Primary Text | `text-gray-800` | `dark:text-gray-100` |
| Secondary Text | `text-gray-600` | `dark:text-gray-400` |
| Border | `border-gray-200` | `dark:border-gray-700` |
| Primary Button | `bg-blue-600` | `dark:bg-blue-500` |
| Input Background | `bg-white` | `dark:bg-gray-700` |

---

## 4. Tailwind Plugins & Ecosystem

### Official Plugins

| Plugin | Purpose | Install |
|--------|---------|---------|
| `@tailwindcss/forms` | Better default form styling | `npm install @tailwindcss/forms` |
| `@tailwindcss/typography` | Beautiful prose styling for article/blog content | `npm install @tailwindcss/typography` |
| `@tailwindcss/aspect-ratio` | Control aspect ratios | `npm install @tailwindcss/aspect-ratio` |

### Adding Plugins

```js
// tailwind.config.js
export default {
  // ...
  plugins: [
    require('@tailwindcss/forms'),
    require('@tailwindcss/typography'),
  ],
}
```

### Useful Ecosystem Tools

| Tool | What It Does |
|------|-------------|
| **Heroicons** | Beautiful hand-crafted SVG icons by the Tailwind team |
| **Headless UI** | Unstyled, accessible UI components (dropdown, modal, tabs) |
| **DaisyUI** | Component library built on top of Tailwind |
| **Flowbite** | Tailwind CSS component library |

---

## 5. Performance

### Purging Unused CSS

Tailwind generates thousands of utility classes, but in production only the ones you actually use are included.

```
┌──────────────────────────────────────────────────┐
│              CSS SIZE COMPARISON                 │
│                                                  │
│  Development:  ~3.5 MB  (all utilities)          │
│  Production:   ~10 KB   (only used utilities)    │
│                                                  │
│  Tailwind automatically scans your files         │
│  and removes unused classes in production        │
└──────────────────────────────────────────────────┘
```

### Content Configuration

The `content` array in `tailwind.config.js` tells Tailwind which files to scan:

```js
content: [
  "./index.html",
  "./src/**/*.{js,jsx,ts,tsx}",
  // Add any other file paths that contain Tailwind classes
]
```

### JIT (Just-In-Time) Mode

JIT mode (default in Tailwind v3+) generates styles on-demand during development:

- Faster build times
- Smaller CSS files even in development
- Supports arbitrary values: `w-[137px]`, `bg-[#1da1f2]`, `grid-cols-[1fr_2fr_1fr]`

---

## 6. Common Component Patterns

### Hero Section

```html
<section class="bg-gradient-to-br from-blue-600 to-purple-700 text-white">
  <div class="max-w-7xl mx-auto px-4 py-24 md:py-32 text-center">
    <h1 class="text-4xl md:text-6xl font-bold leading-tight">
      Build Amazing Websites<br>
      <span class="text-blue-200">With Modern Tools</span>
    </h1>
    <p class="text-lg md:text-xl text-blue-100 mt-6 max-w-2xl mx-auto">
      Learn MERN stack development and build professional web applications from scratch.
    </p>
    <div class="mt-10 flex flex-col sm:flex-row gap-4 justify-center">
      <a href="#" class="bg-white text-blue-600 px-8 py-3 rounded-lg font-semibold hover:bg-blue-50 transition">
        Get Started
      </a>
      <a href="#" class="border-2 border-white text-white px-8 py-3 rounded-lg font-semibold hover:bg-white/10 transition">
        Learn More
      </a>
    </div>
  </div>
</section>
```

### Feature Grid

```html
<section class="py-20 bg-gray-50">
  <div class="max-w-7xl mx-auto px-4">
    <h2 class="text-3xl font-bold text-center text-gray-800">Why Choose Us</h2>
    <p class="text-gray-600 text-center mt-3 max-w-xl mx-auto">
      Everything you need to build modern web applications.
    </p>

    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 mt-12">
      <!-- Feature 1 -->
      <div class="bg-white p-8 rounded-xl shadow-sm hover:shadow-md transition">
        <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center">
          <span class="text-blue-600 text-2xl">⚡</span>
        </div>
        <h3 class="text-xl font-semibold mt-4 text-gray-800">Lightning Fast</h3>
        <p class="text-gray-600 mt-2">Optimized for speed with modern build tools and best practices.</p>
      </div>

      <!-- Feature 2 -->
      <div class="bg-white p-8 rounded-xl shadow-sm hover:shadow-md transition">
        <div class="w-12 h-12 bg-green-100 rounded-lg flex items-center justify-center">
          <span class="text-green-600 text-2xl">🔒</span>
        </div>
        <h3 class="text-xl font-semibold mt-4 text-gray-800">Secure</h3>
        <p class="text-gray-600 mt-2">Built with security best practices including JWT authentication.</p>
      </div>

      <!-- Feature 3 -->
      <div class="bg-white p-8 rounded-xl shadow-sm hover:shadow-md transition">
        <div class="w-12 h-12 bg-purple-100 rounded-lg flex items-center justify-center">
          <span class="text-purple-600 text-2xl">📱</span>
        </div>
        <h3 class="text-xl font-semibold mt-4 text-gray-800">Responsive</h3>
        <p class="text-gray-600 mt-2">Looks great on every device from mobile to desktop.</p>
      </div>
    </div>
  </div>
</section>
```

### Testimonial Section

```html
<section class="py-20 bg-white">
  <div class="max-w-7xl mx-auto px-4">
    <h2 class="text-3xl font-bold text-center text-gray-800">What Students Say</h2>

    <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mt-12">
      <div class="bg-gray-50 p-8 rounded-xl">
        <p class="text-gray-600 italic">"This course changed my career. I went from zero coding knowledge to landing my first developer job in 10 months."</p>
        <div class="flex items-center mt-6">
          <div class="w-12 h-12 bg-blue-200 rounded-full flex items-center justify-center font-bold text-blue-700">AK</div>
          <div class="ml-3">
            <p class="font-semibold text-gray-800">Ahmed Khan</p>
            <p class="text-sm text-gray-500">Junior Developer</p>
          </div>
        </div>
      </div>
      <!-- Repeat for more testimonials -->
    </div>
  </div>
</section>
```

### Pricing Table

```html
<section class="py-20 bg-gray-50">
  <div class="max-w-5xl mx-auto px-4">
    <h2 class="text-3xl font-bold text-center text-gray-800">Pricing Plans</h2>

    <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mt-12">
      <!-- Basic -->
      <div class="bg-white rounded-xl shadow-sm p-8 border border-gray-200">
        <h3 class="text-lg font-semibold text-gray-800">Basic</h3>
        <p class="text-4xl font-bold mt-4 text-gray-900">$9<span class="text-lg text-gray-500 font-normal">/mo</span></p>
        <ul class="mt-6 space-y-3">
          <li class="flex items-center text-gray-600">
            <span class="text-green-500 mr-2">✓</span> 5 Projects
          </li>
          <li class="flex items-center text-gray-600">
            <span class="text-green-500 mr-2">✓</span> Basic Support
          </li>
          <li class="flex items-center text-gray-400">
            <span class="mr-2">✗</span> Priority Access
          </li>
        </ul>
        <button class="w-full mt-8 border-2 border-blue-600 text-blue-600 py-2.5 rounded-lg hover:bg-blue-600 hover:text-white transition font-medium">
          Choose Plan
        </button>
      </div>

      <!-- Pro (Featured) -->
      <div class="bg-blue-600 rounded-xl shadow-xl p-8 text-white relative transform md:-translate-y-4">
        <span class="absolute top-0 right-0 bg-yellow-400 text-yellow-900 text-xs font-bold px-3 py-1 rounded-bl-lg rounded-tr-xl">POPULAR</span>
        <h3 class="text-lg font-semibold">Pro</h3>
        <p class="text-4xl font-bold mt-4">$29<span class="text-lg text-blue-200 font-normal">/mo</span></p>
        <ul class="mt-6 space-y-3">
          <li class="flex items-center">
            <span class="text-blue-200 mr-2">✓</span> Unlimited Projects
          </li>
          <li class="flex items-center">
            <span class="text-blue-200 mr-2">✓</span> Priority Support
          </li>
          <li class="flex items-center">
            <span class="text-blue-200 mr-2">✓</span> Priority Access
          </li>
        </ul>
        <button class="w-full mt-8 bg-white text-blue-600 py-2.5 rounded-lg hover:bg-blue-50 transition font-semibold">
          Choose Plan
        </button>
      </div>

      <!-- Enterprise -->
      <div class="bg-white rounded-xl shadow-sm p-8 border border-gray-200">
        <h3 class="text-lg font-semibold text-gray-800">Enterprise</h3>
        <p class="text-4xl font-bold mt-4 text-gray-900">$99<span class="text-lg text-gray-500 font-normal">/mo</span></p>
        <ul class="mt-6 space-y-3">
          <li class="flex items-center text-gray-600">
            <span class="text-green-500 mr-2">✓</span> Everything in Pro
          </li>
          <li class="flex items-center text-gray-600">
            <span class="text-green-500 mr-2">✓</span> Dedicated Manager
          </li>
          <li class="flex items-center text-gray-600">
            <span class="text-green-500 mr-2">✓</span> Custom Solutions
          </li>
        </ul>
        <button class="w-full mt-8 border-2 border-blue-600 text-blue-600 py-2.5 rounded-lg hover:bg-blue-600 hover:text-white transition font-medium">
          Contact Sales
        </button>
      </div>
    </div>
  </div>
</section>
```

### Footer

```html
<footer class="bg-gray-900 text-gray-300">
  <div class="max-w-7xl mx-auto px-4 py-16">
    <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
      <!-- Brand -->
      <div>
        <h3 class="text-white text-xl font-bold">MyBrand</h3>
        <p class="mt-4 text-sm">Building the future of web development, one student at a time.</p>
      </div>

      <!-- Quick Links -->
      <div>
        <h4 class="text-white font-semibold mb-4">Quick Links</h4>
        <ul class="space-y-2 text-sm">
          <li><a href="#" class="hover:text-white transition">Home</a></li>
          <li><a href="#" class="hover:text-white transition">About</a></li>
          <li><a href="#" class="hover:text-white transition">Courses</a></li>
          <li><a href="#" class="hover:text-white transition">Blog</a></li>
        </ul>
      </div>

      <!-- Support -->
      <div>
        <h4 class="text-white font-semibold mb-4">Support</h4>
        <ul class="space-y-2 text-sm">
          <li><a href="#" class="hover:text-white transition">FAQ</a></li>
          <li><a href="#" class="hover:text-white transition">Contact</a></li>
          <li><a href="#" class="hover:text-white transition">Privacy Policy</a></li>
          <li><a href="#" class="hover:text-white transition">Terms of Service</a></li>
        </ul>
      </div>

      <!-- Newsletter -->
      <div>
        <h4 class="text-white font-semibold mb-4">Newsletter</h4>
        <p class="text-sm mb-4">Get the latest updates and resources.</p>
        <form class="flex">
          <input type="email" placeholder="Your email"
            class="flex-1 px-4 py-2 bg-gray-800 rounded-l-lg border border-gray-700 text-sm focus:outline-none focus:border-blue-500">
          <button class="bg-blue-600 px-4 py-2 rounded-r-lg hover:bg-blue-700 transition text-sm text-white">
            Subscribe
          </button>
        </form>
      </div>
    </div>

    <div class="border-t border-gray-800 mt-12 pt-8 text-center text-sm">
      <p>&copy; 2024 MyBrand. All rights reserved.</p>
    </div>
  </div>
</footer>
```

---

## 7. Week 15 Project: Responsive Landing Page

### Project Requirements

Build a **complete responsive landing page** using Tailwind CSS with the following sections:

```
┌─────────────────────────────────────┐
│            NAVBAR                   │
│  Logo    Links...    CTA Button     │
├─────────────────────────────────────┤
│            HERO SECTION             │
│  Headline + Description + Buttons   │
├─────────────────────────────────────┤
│          FEATURES GRID              │
│  [Feature] [Feature] [Feature]      │
├─────────────────────────────────────┤
│         TESTIMONIALS                │
│  [Quote]  [Quote]  [Quote]          │
├─────────────────────────────────────┤
│          PRICING TABLE              │
│  [Basic]  [Pro]  [Enterprise]       │
├─────────────────────────────────────┤
│        CALL TO ACTION (CTA)         │
│  Big heading + Button               │
├─────────────────────────────────────┤
│            FOOTER                   │
│  Links  |  Links  |  Newsletter     │
└─────────────────────────────────────┘
```

### Technical Requirements

1. **Responsive** — must work on mobile, tablet, and desktop
2. **Dark mode** support with a toggle button
3. **Hover effects** on all interactive elements
4. **Gradient** backgrounds on hero section
5. **Smooth transitions** on buttons and cards
6. All components built from the patterns learned in this lesson
7. Clean, organized HTML structure

### File Structure

```
tailwind-landing-page/
├── index.html
├── package.json
├── tailwind.config.js
├── src/
│   └── input.css
└── dist/
    └── output.css
```

---

## 8. Summary

```
┌─────────────────────────────────────────────────────────┐
│           WEEK 15 — KEY TAKEAWAYS                       │
│                                                         │
│  ✓ Build reusable components by combining utilities     │
│    (navbar, cards, buttons, forms, alerts)              │
│                                                         │
│  ✓ Customize Tailwind with tailwind.config.js           │
│    (colors, fonts, spacing, breakpoints)               │
│                                                         │
│  ✓ Use @layer components for repeated class groups      │
│                                                         │
│  ✓ Dark mode with dark: prefix and class strategy       │
│                                                         │
│  ✓ Tailwind auto-purges unused CSS in production        │
│    (3.5MB → ~10KB)                                     │
│                                                         │
│  ✓ Use official plugins for forms, typography           │
│                                                         │
│  ✓ JIT mode supports arbitrary values like w-[137px]   │
└─────────────────────────────────────────────────────────┘
```

### Tailwind CSS Phase Complete!

You have now learned:

| Week | Topic | Skills |
|------|-------|--------|
| Week 14 | Tailwind Basics | Utility classes, responsive, states |
| Week 15 | Components & Project | Building UIs, customization, dark mode |

**Next Week:** We begin **React.js** — building dynamic, interactive user interfaces with components.

---

**Next Week:** Week 16 — Introduction to React
