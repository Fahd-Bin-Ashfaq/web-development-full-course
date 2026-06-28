# Week 2 — HTML Links, Images & Lists

A comprehensive guide to hyperlinks, images, and lists in HTML. This document builds on the
HTML fundamentals covered in Week 1 (basic tags, document structure, text formatting) and
introduces the elements that turn a static page into a connected, media-rich experience.

**Course:** MERN Stack Full Course
**Level:** Beginner
**Prerequisites:** Week 1 — HTML Basics (document structure, headings, paragraphs, text tags)

---

## Table of Contents

1. [Hyperlinks — The `<a>` Tag](#1-hyperlinks--the-a-tag)
   - 1.1 [What Are Hyperlinks and Why Do They Matter?](#11-what-are-hyperlinks-and-why-do-they-matter)
   - 1.2 [The `href` Attribute](#12-the-href-attribute)
   - 1.3 [Opening Links in a New Tab](#13-opening-links-in-a-new-tab)
   - 1.4 [Internal Links (Same-Page Anchors)](#14-internal-links-same-page-anchors)
   - 1.5 [External Links](#15-external-links)
   - 1.6 [Email Links — `mailto:`](#16-email-links--mailto)
   - 1.7 [Phone Links — `tel:`](#17-phone-links--tel)
   - 1.8 [Download Links](#18-download-links)
2. [Images — The `<img>` Tag](#2-images--the-img-tag)
   - 2.1 [Why Images Matter on the Web](#21-why-images-matter-on-the-web)
   - 2.2 [`src` and `alt` Attributes](#22-src-and-alt-attributes)
   - 2.3 [`width` and `height` Attributes](#23-width-and-height-attributes)
   - 2.4 [Image Formats Comparison](#24-image-formats-comparison)
   - 2.5 [Relative vs Absolute Paths](#25-relative-vs-absolute-paths)
   - 2.6 [Image as a Link](#26-image-as-a-link)
3. [Lists](#3-lists)
   - 3.1 [Unordered Lists](#31-unordered-lists)
   - 3.2 [Ordered Lists](#32-ordered-lists)
   - 3.3 [Nested Lists](#33-nested-lists)
   - 3.4 [Description Lists](#34-description-lists)
   - 3.5 [Real-Life Use Cases](#35-real-life-use-cases)
4. [HTML Comments](#4-html-comments)
5. [Summary](#5-summary)

---

## 1. Hyperlinks — The `<a>` Tag

### 1.1 What Are Hyperlinks and Why Do They Matter?

A **hyperlink** (commonly called a "link") is a clickable reference that takes the user from
one resource to another. Hyperlinks are the reason the internet is called the **World Wide Web**
-- billions of pages linked together like threads in a spider web.

Without hyperlinks, every webpage would be a dead end. You would have to memorize and type
every URL manually. Links make navigation, discovery, and the entire user experience possible.

**Real-life analogy:** Think of a library where every book has sticky notes pointing to related
books on other shelves. You follow the sticky note, pick up the next book, and find more sticky
notes inside it. That chain of references is exactly what hyperlinks do for the web.

```
The World Wide Web — Pages Connected by Hyperlinks
====================================================

          +----------------+
          |   Google.com   |
          +-------+--------+
                  |
       +----------+----------+
       |                     |
+------v-------+    +--------v------+
| Wikipedia.org|    | YouTube.com   |
+------+-------+    +-------+-------+
       |                    |
  +----v----+          +----v----+
  | Page A  |--------->| Page B  |
  +----+----+          +----+----+
       |                    |
       +------+      +------+
              |      |
         +----v------v----+
         |   Your Page    |
         +----------------+

Every arrow is a hyperlink.
The "web" is this network of connections.
```

### 1.2 The `href` Attribute

The `href` (Hypertext REFerence) attribute specifies the destination URL of the link. It is the
most important attribute of the `<a>` tag.

```html
<a href="https://www.google.com">Go to Google</a>
```

**How it renders:** The text "Go to Google" appears as a clickable link (usually blue and
underlined by default). Clicking it takes the user to `https://www.google.com`.

| Part of the tag       | Purpose                                      |
|-----------------------|----------------------------------------------|
| `<a>`                 | The anchor element (creates a hyperlink)      |
| `href="..."`          | The destination URL                           |
| Text between tags     | The clickable text the user sees              |
| `</a>`                | Closing tag                                   |

**Important:** An `<a>` tag without an `href` attribute is not a functioning hyperlink. It will
render as plain text.

```html
<!-- This is NOT a working link -->
<a>Click me</a>

<!-- This IS a working link -->
<a href="https://example.com">Click me</a>
```

### 1.3 Opening Links in a New Tab

By default, clicking a link navigates away from the current page. To open the link in a new
browser tab instead, use the `target` attribute.

```html
<a href="https://www.google.com" target="_blank" rel="noopener noreferrer">
  Open Google in a new tab
</a>
```

| Attribute                   | Purpose                                                  |
|-----------------------------|----------------------------------------------------------|
| `target="_blank"`           | Opens the link in a new browser tab or window            |
| `rel="noopener noreferrer"` | Security measure — prevents the new page from accessing  |
|                             | your page via `window.opener` and stops the browser from |
|                             | sending the referrer header                              |

**Common `target` values:**

| Value       | Behavior                                       |
|-------------|-------------------------------------------------|
| `_self`     | Opens in the same tab (default)                 |
| `_blank`    | Opens in a new tab                              |
| `_parent`   | Opens in the parent frame                       |
| `_top`      | Opens in the full body of the window            |

**Security note:** Always pair `target="_blank"` with `rel="noopener noreferrer"`. Without it,
the destination page can potentially manipulate your original page through JavaScript — a
vulnerability known as **reverse tabnapping**. Modern browsers handle `noopener` by default for
`target="_blank"`, but adding the attribute explicitly is still considered best practice.

### 1.4 Internal Links (Same-Page Anchors)

Internal links let users jump to a specific section within the same page. This is useful for
long pages, documentation, or any content with a table of contents.

**How it works:**

1. Add an `id` attribute to the target element (the section you want to jump to).
2. Create a link with `href="#id-value"`.

```html
<!-- Navigation at the top -->
<nav>
  <a href="#about">About Us</a>
  <a href="#services">Our Services</a>
  <a href="#contact">Contact</a>
</nav>

<!-- Sections further down the page -->
<section id="about">
  <h2>About Us</h2>
  <p>We are a web development agency...</p>
</section>

<section id="services">
  <h2>Our Services</h2>
  <p>We offer frontend, backend, and full-stack development...</p>
</section>

<section id="contact">
  <h2>Contact</h2>
  <p>Email us at hello@agency.com</p>
</section>
```

```
How Internal Links Work
========================

  User clicks       Browser scrolls
  "#services"       down to the
   link             matching id
     |                  |
     v                  v
+----------+     +--------------+
| Click me |---->| id="services"|
| #services|     | Our Services |
+----------+     | ...content...|
                  +--------------+
```

**Back-to-top link** (very common pattern):

```html
<!-- At the bottom of the page -->
<a href="#top">Back to Top</a>

<!-- At the top of the page -->
<body id="top">
```

### 1.5 External Links

External links point to a different website entirely. They use a full (absolute) URL including
the protocol (`https://`).

```html
<!-- Link to an external website -->
<a href="https://developer.mozilla.org">MDN Web Docs</a>

<!-- Link to an external website, new tab -->
<a href="https://stackoverflow.com" target="_blank" rel="noopener noreferrer">
  Stack Overflow
</a>
```

**Best practices for external links:**

- Use descriptive link text (avoid "click here").
- Consider opening external links in a new tab so users do not leave your site.
- Always include the protocol (`https://`), not just `www.example.com`.

```html
<!-- Bad practice -->
<a href="https://google.com">Click here</a>

<!-- Good practice -->
<a href="https://google.com" target="_blank" rel="noopener noreferrer">
  Search on Google
</a>
```

### 1.6 Email Links — `mailto:`

The `mailto:` protocol creates a link that opens the user's default email application with a
new message pre-filled.

```html
<!-- Basic email link -->
<a href="mailto:info@example.com">Email Us</a>

<!-- With subject line -->
<a href="mailto:info@example.com?subject=Hello%20There">Email with Subject</a>

<!-- With subject and body -->
<a href="mailto:info@example.com?subject=Inquiry&body=Hi%2C%20I%20have%20a%20question.">
  Send an Inquiry
</a>

<!-- Multiple recipients -->
<a href="mailto:hr@example.com,admin@example.com?subject=Job%20Application">
  Apply Now
</a>
```

| Parameter  | Purpose                           | Example                                  |
|------------|-----------------------------------|------------------------------------------|
| `subject`  | Pre-fills the email subject line  | `?subject=Hello`                         |
| `body`     | Pre-fills the email body          | `?body=Dear%20Sir`                       |
| `cc`       | Carbon copy recipients            | `?cc=manager@example.com`                |
| `bcc`      | Blind carbon copy recipients      | `?bcc=archive@example.com`               |

**Note:** Spaces and special characters in `subject` and `body` must be URL-encoded
(`%20` for space, `%2C` for comma, etc.).

**Real-life example:** A business website "Contact Us" section:

```html
<h2>Get in Touch</h2>
<p>Have questions? <a href="mailto:support@myshop.com?subject=Support%20Request">
   Email our support team</a>.</p>
```

### 1.7 Phone Links — `tel:`

The `tel:` protocol creates a clickable phone number. On mobile devices, tapping the link
initiates a phone call. On desktops, it may open a calling application (Skype, FaceTime, etc.).

```html
<!-- Basic phone link -->
<a href="tel:+12025551234">Call Us: (202) 555-1234</a>

<!-- Pakistan number format -->
<a href="tel:+923001234567">Call: 0300-1234567</a>
```

**Best practices:**

- Always use the international format with the `+` country code.
- Display the number in a human-readable format in the link text.
- Phone links are most useful on mobile-responsive websites.

**Real-life example:** A restaurant website footer:

```html
<footer>
  <p>Reservations: <a href="tel:+923211234567">0321-1234567</a></p>
  <p>Email: <a href="mailto:reserve@restaurant.pk">reserve@restaurant.pk</a></p>
</footer>
```

### 1.8 Download Links

The `download` attribute tells the browser to download the linked file instead of navigating
to it.

```html
<!-- Download a PDF -->
<a href="/files/brochure.pdf" download>Download Brochure</a>

<!-- Download with a custom filename -->
<a href="/files/report-2024-q1.pdf" download="Quarterly-Report.pdf">
  Download Q1 Report
</a>

<!-- Download an image -->
<a href="/images/logo.png" download="company-logo.png">
  Download Our Logo
</a>
```

| Attribute             | Purpose                                                     |
|-----------------------|-------------------------------------------------------------|
| `download`            | Triggers download instead of navigation                     |
| `download="name.ext"` | Triggers download and suggests a filename for the saved file |

**Note:** The `download` attribute only works for same-origin URLs (files on your own server)
or `blob:` and `data:` URLs. Cross-origin downloads may be blocked by the browser for security.

---

### Quick Reference — All Link Types

```
+--------------------+----------------------------+----------------------------------+
| Link Type          | href Value                 | Example                          |
+--------------------+----------------------------+----------------------------------+
| External           | https://example.com        | Go to another website            |
| Internal (anchor)  | #section-id                | Jump within the same page        |
| Relative page      | about.html                 | Navigate to a local page         |
| Email              | mailto:user@example.com    | Open email client                |
| Phone              | tel:+1234567890            | Initiate phone call              |
| Download           | file.pdf (with download)   | Download a file                  |
+--------------------+----------------------------+----------------------------------+
```

---

## 2. Images — The `<img>` Tag

### 2.1 Why Images Matter on the Web

Images are essential to the web experience. A page full of text without any visual elements
feels dull and is harder to engage with. Images serve multiple purposes:

- **Convey information** — charts, infographics, diagrams, screenshots
- **Enhance aesthetics** — hero banners, backgrounds, icons
- **Build trust** — team photos, product images, logos
- **Improve comprehension** — a picture is often worth a thousand words

**Real-life example:** Imagine an e-commerce site selling shoes but without any product photos.
No one would buy. Images are not decoration — they are content.

### 2.2 `src` and `alt` Attributes

The `<img>` tag is a **self-closing** (void) tag. It has no closing tag.

```html
<img src="photo.jpg" alt="A golden retriever playing in a park">
```

| Attribute | Required | Purpose                                                       |
|-----------|----------|---------------------------------------------------------------|
| `src`     | Yes      | The path or URL to the image file                             |
| `alt`     | Yes      | Alternative text describing the image                         |

**Why `alt` is crucial:**

1. **Accessibility:** Screen readers (used by visually impaired users) read the `alt` text
   aloud. Without it, the user has no idea what the image shows.
2. **Broken images:** If the image fails to load (wrong path, slow network), the browser
   displays the `alt` text instead.
3. **SEO:** Search engines cannot "see" images. They rely on `alt` text to understand and
   index image content.

```
What happens when an image fails to load?
==========================================

WITH alt text:                    WITHOUT alt text:
+---------------------------+     +---------------------------+
|  [x] A golden retriever   |     |  [x]                      |
|      playing in a park     |     |                           |
+---------------------------+     +---------------------------+
  User understands                  User sees nothing useful
  what was supposed                 (just a broken icon)
  to appear
```

**Writing good alt text:**

```html
<!-- Bad: vague or missing -->
<img src="dog.jpg" alt="image">
<img src="dog.jpg" alt="">
<img src="dog.jpg">

<!-- Good: descriptive -->
<img src="dog.jpg" alt="A golden retriever playing fetch in a park on a sunny day">

<!-- Decorative images: use empty alt (not missing, but explicitly empty) -->
<img src="decorative-border.png" alt="">
```

**Rule of thumb:** Close your eyes and have someone read the `alt` text to you. Can you
picture the image? If yes, the `alt` text is good.

### 2.3 `width` and `height` Attributes

You can control the display size of an image directly in HTML.

```html
<!-- Set exact dimensions in pixels -->
<img src="logo.png" alt="Company Logo" width="200" height="100">

<!-- Set only width (height adjusts proportionally) -->
<img src="banner.jpg" alt="Welcome Banner" width="800">
```

| Attribute | Purpose                              | Value        |
|-----------|--------------------------------------|--------------|
| `width`   | Sets the display width of the image  | Pixels (number) |
| `height`  | Sets the display height of the image | Pixels (number) |

**Why specify width and height?**

- **Prevents layout shift:** When the browser loads a page, it does not know the image
  dimensions until the image file is downloaded. Without explicit dimensions, the page layout
  jumps around as images load. This is called **Cumulative Layout Shift (CLS)** and hurts
  user experience and SEO.
- **Performance hint:** Specifying dimensions lets the browser reserve the correct space before
  the image loads.

**Best practice:** Set dimensions in HTML for layout stability, but use CSS for responsive
sizing.

```html
<!-- HTML sets the intrinsic size -->
<img src="photo.jpg" alt="Team photo" width="600" height="400">
```

```css
/* CSS makes it responsive */
img {
  max-width: 100%;
  height: auto;
}
```

### 2.4 Image Formats Comparison

Choosing the right image format matters for quality, file size, and browser support.

| Format | Full Name                         | Best For                            | Transparency | Animation | Typical Size |
|--------|-----------------------------------|-------------------------------------|:------------:|:---------:|:------------:|
| JPEG   | Joint Photographic Experts Group  | Photographs, complex images         | No           | No        | Medium       |
| PNG    | Portable Network Graphics         | Logos, icons, images with text      | Yes          | No        | Large        |
| GIF    | Graphics Interchange Format       | Simple animations, small icons      | Yes (1-bit)  | Yes       | Small-Medium |
| SVG    | Scalable Vector Graphics          | Icons, logos, illustrations         | Yes          | Yes*      | Very Small   |
| WebP   | Web Picture format (by Google)    | General-purpose (replaces JPEG/PNG) | Yes          | Yes       | Small        |

*SVG supports animation via CSS/JavaScript, not frame-based animation like GIF.

**When to use each format:**

```
Choosing the Right Image Format
=================================

Is it a photograph?
  |
  +-- YES --> Is file size critical?
  |             |
  |             +-- YES --> Use WebP (best compression)
  |             +-- NO  --> Use JPEG (widest support)
  |
  +-- NO  --> Does it need transparency?
                |
                +-- YES --> Is it an icon/logo/illustration?
                |             |
                |             +-- YES --> Use SVG (scalable, tiny file)
                |             +-- NO  --> Use PNG or WebP
                |
                +-- NO  --> Does it need animation?
                              |
                              +-- YES --> Use GIF (simple) or WebP (better quality)
                              +-- NO  --> Use SVG, PNG, or WebP
```

### 2.5 Relative vs Absolute Paths

Understanding file paths is essential for linking images (and any other resource).

**Absolute path:** The full URL, starting from the protocol. Works from anywhere.

```html
<img src="https://www.example.com/images/logo.png" alt="Logo">
```

**Relative path:** A path relative to the current HTML file's location. Shorter and more
portable.

```html
<img src="images/logo.png" alt="Logo">
<img src="../images/logo.png" alt="Logo">
```

```
Project Folder Structure
=========================

my-website/
  |
  +-- index.html
  +-- about/
  |     +-- team.html
  |
  +-- images/
  |     +-- logo.png
  |     +-- banner.jpg
  |
  +-- css/
        +-- style.css


From index.html to logo.png:
  <img src="images/logo.png">
  (Go INTO the images folder)

From about/team.html to logo.png:
  <img src="../images/logo.png">
  (Go UP one level with "..", then INTO images)

Absolute path (works from any file):
  <img src="https://www.mysite.com/images/logo.png">
```

| Path Type | Example                                      | Pros                         | Cons                        |
|-----------|----------------------------------------------|------------------------------|-----------------------------|
| Relative  | `images/logo.png`                            | Short, portable, works locally | Breaks if file moves        |
| Absolute  | `https://www.example.com/images/logo.png`    | Always works regardless of page | Longer, not portable       |
| Root-relative | `/images/logo.png`                       | Works from any page on the same site | Does not work when opening files directly |

### 2.6 Image as a Link

You can wrap an `<img>` tag inside an `<a>` tag to make the image clickable.

```html
<!-- Clicking the logo takes the user to the homepage -->
<a href="index.html">
  <img src="images/logo.png" alt="Company Logo - Go to Homepage" width="150">
</a>

<!-- Clicking a product image opens the product page -->
<a href="products/shoes.html">
  <img src="images/shoe-red.jpg" alt="Red running shoes - View details" width="300">
</a>

<!-- Image linking to an external site -->
<a href="https://github.com" target="_blank" rel="noopener noreferrer">
  <img src="images/github-icon.svg" alt="Visit our GitHub profile" width="40">
</a>
```

```
Image as a Link — How it works
================================

+----------------------------------+
|  <a href="index.html">          |
|    +------------------------+    |
|    |                        |    |
|    |    [ Company Logo ]    |  <-- Entire image is clickable
|    |      (img tag)         |    |
|    +------------------------+    |
|  </a>                           |
+----------------------------------+
       |
       | User clicks the image
       v
  Browser navigates to index.html
```

**Tip:** When an image is used as a link, the `alt` text should describe both the image and the
action. For example: `alt="Company Logo - Go to Homepage"`.

---

## 3. Lists

Lists are used to group related items together. HTML provides three types of lists, each suited
for different kinds of content.

### 3.1 Unordered Lists

An **unordered list** displays items with bullet points. Use it when the order of items does
not matter.

```html
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
  <li>React</li>
</ul>
```

**Output:**

```
  * HTML
  * CSS
  * JavaScript
  * React
```

**The `type` attribute** changes the bullet style:

| `type` Value | Bullet Style          | Example    |
|--------------|-----------------------|------------|
| `disc`       | Filled circle (default) | ●        |
| `circle`     | Hollow circle         | ○          |
| `square`     | Filled square         | ■          |

```html
<ul type="square">
  <li>MongoDB</li>
  <li>Express</li>
  <li>React</li>
  <li>Node.js</li>
</ul>
```

**Note:** In modern HTML, the `type` attribute on `<ul>` is considered presentational. It is
better to use CSS `list-style-type` for styling. However, knowing the attribute is useful for
understanding legacy code and quick prototyping.

```css
/* CSS approach (preferred) */
ul {
  list-style-type: square;
}
```

### 3.2 Ordered Lists

An **ordered list** displays items with numbers (or letters/roman numerals). Use it when the
sequence matters.

```html
<ol>
  <li>Plan the project</li>
  <li>Set up the development environment</li>
  <li>Write HTML structure</li>
  <li>Add CSS styling</li>
  <li>Implement JavaScript logic</li>
</ol>
```

**Output:**

```
  1. Plan the project
  2. Set up the development environment
  3. Write HTML structure
  4. Add CSS styling
  5. Implement JavaScript logic
```

**The `type` attribute** changes the numbering style:

| `type` Value | Numbering Style            | Example            |
|--------------|----------------------------|--------------------|
| `1`          | Numbers (default)          | 1, 2, 3, 4        |
| `A`          | Uppercase letters          | A, B, C, D        |
| `a`          | Lowercase letters          | a, b, c, d        |
| `I`          | Uppercase Roman numerals   | I, II, III, IV     |
| `i`          | Lowercase Roman numerals   | i, ii, iii, iv     |

**The `start` attribute** changes the starting number:

```html
<!-- Starts counting from 5 -->
<ol start="5">
  <li>Deploy to staging</li>
  <li>Run QA tests</li>
  <li>Deploy to production</li>
</ol>
```

**Output:**

```
  5. Deploy to staging
  6. Run QA tests
  7. Deploy to production
```

**The `reversed` attribute** counts backwards:

```html
<ol reversed>
  <li>Gold Medal</li>
  <li>Silver Medal</li>
  <li>Bronze Medal</li>
</ol>
```

**Output:**

```
  3. Gold Medal
  2. Silver Medal
  1. Bronze Medal
```

**Combined example:**

```html
<ol type="A" start="3">
  <li>Third item labeled C</li>
  <li>Fourth item labeled D</li>
  <li>Fifth item labeled E</li>
</ol>
```

**Output:**

```
  C. Third item labeled C
  D. Fourth item labeled D
  E. Fifth item labeled E
```

### 3.3 Nested Lists

Lists can be placed inside other lists to create multi-level hierarchies. This is called
**nesting**. The inner list must be placed inside an `<li>` element of the outer list.

```html
<ul>
  <li>Frontend
    <ul>
      <li>HTML</li>
      <li>CSS</li>
      <li>JavaScript
        <ul>
          <li>React</li>
          <li>Angular</li>
          <li>Vue</li>
        </ul>
      </li>
    </ul>
  </li>
  <li>Backend
    <ul>
      <li>Node.js</li>
      <li>Express</li>
      <li>Python (Django)</li>
    </ul>
  </li>
  <li>Database
    <ul>
      <li>MongoDB</li>
      <li>PostgreSQL</li>
    </ul>
  </li>
</ul>
```

```
Visual Representation of Nested Lists
=======================================

Web Development
  |
  +-- Frontend
  |     |
  |     +-- HTML
  |     +-- CSS
  |     +-- JavaScript
  |           |
  |           +-- React
  |           +-- Angular
  |           +-- Vue
  |
  +-- Backend
  |     |
  |     +-- Node.js
  |     +-- Express
  |     +-- Python (Django)
  |
  +-- Database
        |
        +-- MongoDB
        +-- PostgreSQL
```

**You can also mix ordered and unordered lists:**

```html
<ol>
  <li>Prepare ingredients
    <ul>
      <li>2 eggs</li>
      <li>1 cup flour</li>
      <li>1/2 cup sugar</li>
    </ul>
  </li>
  <li>Mix everything together</li>
  <li>Bake at 180 C for 25 minutes</li>
</ol>
```

```
Output:

  1. Prepare ingredients
       * 2 eggs
       * 1 cup flour
       * 1/2 cup sugar
  2. Mix everything together
  3. Bake at 180 C for 25 minutes
```

### 3.4 Description Lists

A **description list** is used for term-definition pairs (like a glossary or FAQ). It uses
three tags:

| Tag    | Purpose                                 |
|--------|-----------------------------------------|
| `<dl>` | Description List — the container        |
| `<dt>` | Description Term — the word or concept  |
| `<dd>` | Description Details — the definition    |

```html
<dl>
  <dt>HTML</dt>
  <dd>HyperText Markup Language — the structure of web pages.</dd>

  <dt>CSS</dt>
  <dd>Cascading Style Sheets — controls the visual presentation.</dd>

  <dt>JavaScript</dt>
  <dd>A programming language that adds interactivity to web pages.</dd>

  <dt>MERN</dt>
  <dd>A full-stack development stack: MongoDB, Express, React, Node.js.</dd>
</dl>
```

**Output:**

```
  HTML
      HyperText Markup Language -- the structure of web pages.

  CSS
      Cascading Style Sheets -- controls the visual presentation.

  JavaScript
      A programming language that adds interactivity to web pages.

  MERN
      A full-stack development stack: MongoDB, Express, React, Node.js.
```

**A term can have multiple definitions:**

```html
<dl>
  <dt>Node.js</dt>
  <dd>A JavaScript runtime built on Chrome's V8 engine.</dd>
  <dd>Used for building server-side applications.</dd>
  <dd>Enables JavaScript to run outside the browser.</dd>
</dl>
```

### 3.5 Real-Life Use Cases

Lists are everywhere on the web. Here are practical examples of where each type is used.

**1. Navigation menus (Unordered List)**

Almost every website navigation bar is built with a `<ul>`. CSS removes the bullets and
displays items horizontally.

```html
<nav>
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/about">About</a></li>
    <li><a href="/services">Services</a></li>
    <li><a href="/contact">Contact</a></li>
  </ul>
</nav>
```

```
How a nav menu is built from a <ul>
=====================================

Raw HTML (with bullets):        After CSS styling:

  * Home                        Home  |  About  |  Services  |  Contact
  * About                       =========================================
  * Services
  * Contact
```

**2. Feature/pricing lists (Unordered List)**

```html
<h3>Pro Plan - $29/month</h3>
<ul>
  <li>Unlimited projects</li>
  <li>Priority support</li>
  <li>Custom domain</li>
  <li>Analytics dashboard</li>
</ul>
```

**3. Step-by-step instructions (Ordered List)**

```html
<h3>How to Create a GitHub Repository</h3>
<ol>
  <li>Log in to your GitHub account</li>
  <li>Click the "+" icon in the top right corner</li>
  <li>Select "New repository"</li>
  <li>Enter a repository name and description</li>
  <li>Choose Public or Private</li>
  <li>Click "Create repository"</li>
</ol>
```

**4. FAQ / Glossary (Description List)**

```html
<h3>Frequently Asked Questions</h3>
<dl>
  <dt>How long is the course?</dt>
  <dd>The MERN stack course runs for 16 weeks.</dd>

  <dt>Do I need prior programming experience?</dt>
  <dd>No. We start from the basics and build up gradually.</dd>

  <dt>What will I build?</dt>
  <dd>You will build multiple projects including a portfolio site,
      a blog, and a full-stack e-commerce application.</dd>
</dl>
```

**5. Breadcrumb navigation (Ordered List)**

```html
<nav aria-label="Breadcrumb">
  <ol>
    <li><a href="/">Home</a></li>
    <li><a href="/courses">Courses</a></li>
    <li><a href="/courses/mern">MERN Stack</a></li>
    <li>Week 2</li>
  </ol>
</nav>
```

```
Breadcrumb output (after CSS):

  Home  >  Courses  >  MERN Stack  >  Week 2
```

---

## 4. HTML Comments

HTML comments are notes in the code that are **invisible to the user** but visible to anyone
reading the source code. The browser completely ignores comments when rendering the page.

```html
<!-- This is a comment. It will not appear on the page. -->

<h1>Welcome to Our Website</h1>

<!-- TODO: Add a hero image here -->

<p>This paragraph is visible to the user.</p>

<!-- 
  Multi-line comment:
  The section below is for the navigation.
  It will be styled later with CSS.
-->
<nav>
  <a href="/">Home</a>
  <a href="/about">About</a>
</nav>
```

### When and Why to Use Comments

| Use Case                          | Example                                           |
|-----------------------------------|----------------------------------------------------|
| Explain complex or non-obvious code | `<!-- Flexbox container for card layout -->`     |
| Mark sections of a large page     | `<!-- ====== HEADER SECTION ====== -->`            |
| Leave notes for teammates         | `<!-- TODO: Replace placeholder images -->`        |
| Temporarily disable code          | `<!-- <p>This text is hidden for now</p> -->`      |
| Document decisions                | `<!-- Using table here for email template compat -->` |

**Temporarily disabling code (commenting out):**

```html
<!-- <img src="old-banner.jpg" alt="Old promotional banner"> -->
<img src="new-banner.jpg" alt="Summer sale banner">
```

**Important notes about comments:**

- Comments are still visible in the page source code (right-click > View Page Source). Never
  put passwords, API keys, or sensitive information in comments.
- Excessive commenting clutters the code. Comment the "why," not the "what." If the code is
  self-explanatory, a comment is unnecessary.

```html
<!-- Bad: states the obvious -->
<!-- This is a paragraph -->
<p>Hello World</p>

<!-- Good: explains the reason -->
<!-- Using a div instead of section because this content is purely decorative -->
<div class="decorative-strip"></div>
```

---

## 5. Summary

This week covered three fundamental building blocks of HTML that transform static text into
a rich, interactive, and navigable web experience.

### Key Concepts at a Glance

| Topic              | Tags / Attributes                          | Key Takeaway                                     |
|--------------------|--------------------------------------------|--------------------------------------------------|
| Hyperlinks         | `<a>`, `href`, `target`, `rel`, `download` | Links connect pages — they are the web's backbone |
| Images             | `<img>`, `src`, `alt`, `width`, `height`   | Always use `alt` for accessibility and SEO        |
| Unordered Lists    | `<ul>`, `<li>`, `type`                     | Bulleted items — order does not matter            |
| Ordered Lists      | `<ol>`, `<li>`, `type`, `start`, `reversed`| Numbered items — sequence matters                 |
| Description Lists  | `<dl>`, `<dt>`, `<dd>`                     | Term-definition pairs (glossaries, FAQs)          |
| Nested Lists       | Lists inside `<li>` elements               | Create multi-level hierarchies                    |
| Image Formats      | JPEG, PNG, GIF, SVG, WebP                  | Choose based on content type and requirements     |
| File Paths         | Relative, Absolute, Root-relative          | Understand path resolution for linking resources  |
| HTML Comments      | `<!-- -->`                                 | Document code, never store sensitive data         |

### What Comes Next

In the upcoming weeks, you will learn:

- **HTML Tables** — Structuring tabular data with rows and columns
- **HTML Forms** — Collecting user input (text fields, dropdowns, buttons)
- **CSS Fundamentals** — Styling everything you have built so far

The links, images, and lists you learned today will appear in virtually every web project you
build throughout this MERN stack course and beyond.

---

**Author:** Fahad Ahmed
**Purpose:** MERN Stack Full Course — Week 2 Lecture Notes
**Level:** Beginner
