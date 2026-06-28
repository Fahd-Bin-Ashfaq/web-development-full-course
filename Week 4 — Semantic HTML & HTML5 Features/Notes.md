# Week 4 -- Semantic HTML & HTML5 Features

> **MERN Stack Course**
> By this point you know basic tags, headings, paragraphs, links, images, lists, tables, and forms from Weeks 1-3. This week we give your pages *meaning* with semantic HTML, add audio and video, embed external content, explore new HTML5 input types, and put it all together in a multi-page website project.

---

## Table of Contents

1. [Semantic HTML](#1-semantic-html)
   - [What Is Semantic HTML?](#what-is-semantic-html)
   - [Why Semantic HTML Matters](#why-semantic-html-matters)
   - [Semantic Tags In Detail](#semantic-tags-in-detail)
   - [Complete Page Layout Diagram](#complete-page-layout-diagram)
2. [HTML5 Multimedia](#2-html5-multimedia)
   - [The audio Tag](#the-audio-tag)
   - [The video Tag](#the-video-tag)
   - [The source Tag and Format Support](#the-source-tag-and-format-support)
3. [Embedding External Content](#3-embedding-external-content)
   - [The iframe Tag](#the-iframe-tag)
   - [Security Considerations](#security-considerations)
4. [HTML5 New Input Types](#4-html5-new-input-types)
5. [HTML Best Practices](#5-html-best-practices)
6. [Week 4 Project -- Build a Complete Multi-Page Website](#6-week-4-project----build-a-complete-multi-page-website)
7. [Summary -- What We Learned in HTML (Weeks 1-4 Recap)](#7-summary----what-we-learned-in-html-weeks-1-4-recap)

---

## 1. Semantic HTML

### What Is Semantic HTML?

**Semantic** means "relating to meaning." In HTML, a semantic element clearly describes its purpose to both the browser and the developer reading the code.

| Aspect          | Non-Semantic (Generic) | Semantic                |
|-----------------|------------------------|-------------------------|
| Tag example     | `<div>`, `<span>`      | `<header>`, `<article>` |
| Meaning         | None -- just a box     | Describes the content   |
| Accessibility   | Screen readers guess   | Screen readers announce |
| SEO             | Search engines guess   | Search engines understand |
| Readability     | Requires class names   | Self-documenting        |

#### The "Div Soup" Problem

Before HTML5 semantic tags existed, every page looked like this:

```
  NON-SEMANTIC ("Div Soup")             SEMANTIC HTML5
  ===========================           ===========================

  <div class="header">                  <header>
    <div class="nav">                     <nav>
      ...                                   ...
    </div>                                </nav>
  </div>                                </header>

  <div class="main">                    <main>
    <div class="article">                 <article>
      <div class="section">                 <section>
        ...                                   ...
      </div>                                </section>
    </div>                                </article>
    <div class="sidebar">                 <aside>
      ...                                   ...
    </div>                                </aside>
  </div>                                </main>

  <div class="footer">                  <footer>
    ...                                   ...
  </div>                                </footer>
```

Both produce the same visual result, but the semantic version tells the browser, screen readers, and search engines what each section actually *is*.

**Real-life analogy:** Imagine a filing cabinet. Non-semantic HTML is like throwing every document into one drawer labeled "stuff." Semantic HTML is like having drawers labeled "Invoices," "Contracts," and "Reports" -- anyone can find what they need immediately.

---

### Why Semantic HTML Matters

#### 1. Accessibility

Screen readers (used by visually impaired users) rely on semantic tags to navigate a page. When a screen reader encounters `<nav>`, it announces "navigation region" so the user can skip to it or past it. A `<div class="nav">` provides no such hint.

#### 2. SEO (Search Engine Optimization)

Search engines like Google use semantic tags to understand page structure. Content inside `<article>` is treated as the primary content, while content inside `<aside>` is recognized as supplementary. This helps search engines index your pages more accurately and can improve your ranking.

#### 3. Code Readability and Maintenance

When you (or a teammate) return to code six months later, `<header>` immediately communicates its purpose. `<div class="hdr-wrap-outer">` requires you to read class names, check CSS, and guess.

---

### Semantic Tags In Detail

#### `<header>` -- Site or Section Header

The `<header>` element represents introductory content or a group of navigational aids. A page can have multiple `<header>` elements (one for the site, one for each `<article>`, etc.).

```
  +-----------------------------------------------+
  | <header>                                       |
  |   Logo    Site Title    Navigation Links       |
  +-----------------------------------------------+
```

```html
<header>
  <h1>My Travel Blog</h1>
  <p>Exploring the world, one city at a time</p>
</header>
```

**Real-life example:** The header is like the masthead of a newspaper -- the name, logo, and date at the top of the front page.

---

#### `<nav>` -- Navigation Links

The `<nav>` element wraps a set of navigation links. It is typically used for the main site menu, but can also appear in a footer or sidebar for secondary navigation.

```
  +-----------------------------------------------+
  | <nav>                                          |
  |   Home  |  About  |  Services  |  Contact     |
  +-----------------------------------------------+
```

```html
<nav>
  <ul>
    <li><a href="index.html">Home</a></li>
    <li><a href="about.html">About</a></li>
    <li><a href="services.html">Services</a></li>
    <li><a href="contact.html">Contact</a></li>
  </ul>
</nav>
```

**Real-life example:** The table of contents in a book. It tells you what sections exist and lets you jump directly to them.

---

#### `<main>` -- Main Content

The `<main>` element wraps the dominant content of the page. There must be only **one** `<main>` per page, and it must not be nested inside `<header>`, `<footer>`, `<nav>`, or `<aside>`.

```
  +-----------------------------------------------+
  |                  <header>                      |
  +-----------------------------------------------+
  |                   <nav>                        |
  +-----------------------------------------------+
  |                                               |
  |                  <main>                        |
  |    (This is where your primary content goes)   |
  |                                               |
  +-----------------------------------------------+
  |                  <footer>                      |
  +-----------------------------------------------+
```

```html
<main>
  <h2>Welcome to Our Restaurant</h2>
  <p>We serve authentic Italian cuisine made with fresh ingredients.</p>
</main>
```

**Real-life example:** The main stage at a concert. There might be side stages and food stalls, but the main stage is where the headline act performs.

---

#### `<section>` -- Thematic Grouping

The `<section>` element groups related content under a common theme. Each `<section>` should typically have its own heading.

```
  +-----------------------------------------------+
  | <section>                                      |
  |   <h2>Our Menu</h2>                           |
  |   Appetizers, Main Courses, Desserts ...       |
  +-----------------------------------------------+
  | <section>                                      |
  |   <h2>Customer Reviews</h2>                   |
  |   Review 1, Review 2, Review 3 ...            |
  +-----------------------------------------------+
```

```html
<section>
  <h2>Our Services</h2>
  <p>We offer web development, mobile apps, and cloud solutions.</p>
</section>

<section>
  <h2>Our Team</h2>
  <p>Meet the talented people behind our products.</p>
</section>
```

**Real-life example:** Chapters in a textbook. Each chapter covers a distinct topic but belongs to the same book.

---

#### `<article>` -- Independent Content

The `<article>` element represents a self-contained composition that could be distributed independently -- a blog post, a news story, a forum thread, or a product card.

```
  +-----------------------------------------------+
  | <article>                                      |
  |   <h2>How to Learn JavaScript</h2>            |
  |   <p>Published: June 25, 2026</p>             |
  |   <p>JavaScript is the language of ...</p>     |
  +-----------------------------------------------+
```

```html
<article>
  <h2>How to Learn JavaScript in 2026</h2>
  <p><time datetime="2026-06-25">June 25, 2026</time></p>
  <p>JavaScript remains the most popular programming language for web
     development. Here is a step-by-step guide to getting started...</p>
</article>
```

**Real-life example:** A single article in a magazine. You could tear it out and it would still make complete sense on its own.

---

#### `<aside>` -- Sidebar or Supplementary Content

The `<aside>` element contains content that is tangentially related to the content around it -- sidebars, pull quotes, advertisements, or related links.

```
  +----------------------------------+----------+
  |                                  | <aside>  |
  |           <main>                 |  Related |
  |    (Primary content area)        |  Links   |
  |                                  |  Ads     |
  |                                  |  Tips    |
  +----------------------------------+----------+
```

```html
<aside>
  <h3>Related Articles</h3>
  <ul>
    <li><a href="#">Understanding CSS Grid</a></li>
    <li><a href="#">JavaScript for Beginners</a></li>
  </ul>
</aside>
```

**Real-life example:** The sidebar in a newspaper. While the main article is about the election results, the sidebar shows a brief bio of the candidates.

---

#### `<footer>` -- Footer

The `<footer>` element represents the footer of its nearest sectioning ancestor. A page footer typically contains copyright information, contact details, and secondary navigation.

```
  +-----------------------------------------------+
  | <footer>                                       |
  |   Copyright 2026  |  Privacy  |  Terms         |
  |   Contact: info@example.com                    |
  +-----------------------------------------------+
```

```html
<footer>
  <p>&copy; 2026 My Company. All rights reserved.</p>
  <nav>
    <a href="privacy.html">Privacy Policy</a> |
    <a href="terms.html">Terms of Service</a>
  </nav>
</footer>
```

**Real-life example:** The bottom of a letter -- the closing, signature, and contact information.

---

#### `<figure>` and `<figcaption>` -- Images with Captions

The `<figure>` element wraps self-contained content like images, diagrams, or code snippets. The `<figcaption>` provides a caption for the figure.

```
  +-----------------------------------------------+
  | <figure>                                       |
  |  +-------------------------------------------+ |
  |  |                                           | |
  |  |           [ Image Here ]                  | |
  |  |                                           | |
  |  +-------------------------------------------+ |
  |  <figcaption>                                  |
  |    A sunset over the mountains                 |
  |  </figcaption>                                 |
  +-----------------------------------------------+
```

```html
<figure>
  <img src="sunset.jpg" alt="A golden sunset over snow-capped mountains">
  <figcaption>A sunset over the Rocky Mountains, Colorado.</figcaption>
</figure>
```

**Real-life example:** A photo in a textbook with a caption beneath it explaining what the image shows.

---

#### `<details>` and `<summary>` -- Collapsible Content

The `<details>` element creates a disclosure widget that the user can open and close. The `<summary>` element provides the visible heading for the widget. No JavaScript required.

```
  CLOSED STATE:                     OPEN STATE:
  +---------------------------+     +---------------------------+
  | > What is HTML?           |     | v What is HTML?           |
  +---------------------------+     |                           |
                                    |   HTML stands for Hyper   |
                                    |   Text Markup Language.   |
                                    |   It is used to create    |
                                    |   web pages.              |
                                    +---------------------------+
```

```html
<details>
  <summary>What is HTML?</summary>
  <p>HTML stands for HyperText Markup Language. It is the standard
     language for creating web pages and web applications.</p>
</details>

<details open>
  <summary>What is CSS?</summary>
  <p>CSS stands for Cascading Style Sheets. It controls the
     presentation and layout of HTML elements.</p>
</details>
```

> **Note:** Adding the `open` attribute makes the details section expanded by default.

**Real-life example:** An FAQ page where each question can be clicked to reveal the answer. This is exactly what `<details>` and `<summary>` were designed for.

---

#### `<time>` -- Date and Time

The `<time>` element represents a specific date, time, or duration. The `datetime` attribute provides a machine-readable value, while the text content is the human-readable version.

```html
<p>The event starts on
   <time datetime="2026-07-15T09:00">July 15, 2026 at 9:00 AM</time>.
</p>

<p>Registration deadline:
   <time datetime="2026-07-01">July 1, 2026</time>.
</p>

<p>The workshop lasts
   <time datetime="PT2H30M">2 hours and 30 minutes</time>.
</p>
```

The `datetime` attribute uses standard formats:
- Date: `YYYY-MM-DD` (e.g., `2026-07-15`)
- Time: `HH:MM` (e.g., `09:00`)
- Date and time: `YYYY-MM-DDTHH:MM` (e.g., `2026-07-15T09:00`)
- Duration: `PT` followed by hours and minutes (e.g., `PT2H30M`)

**Real-life example:** Calendar entries. Humans read "July 15 at 9 AM," but your calendar app stores `2026-07-15T09:00` so it can set alarms and convert time zones.

---

### Complete Page Layout Diagram

Here is how all the semantic tags come together to form a well-structured page:

```
+================================================================+
|                        <header>                                 |
|   +----------------------------------------------------------+ |
|   |  LOGO        Site Title                                   | |
|   +----------------------------------------------------------+ |
|   |                    <nav>                                  | |
|   |   Home  |  About  |  Blog  |  Contact                    | |
|   +----------------------------------------------------------+ |
+================================================================+
|                                                                 |
|                        <main>                                   |
|                                                                 |
|   +------------------------------------------+ +-----------+   |
|   |            <article>                      | |  <aside>  |   |
|   |                                           | |           |   |
|   |   <h2>Blog Post Title</h2>               | |  Related  |   |
|   |                                           | |  Posts    |   |
|   |   +----------------------------------+    | |           |   |
|   |   | <section>                        |    | |  Popular  |   |
|   |   |   <h3>Introduction</h3>          |    | |  Tags     |   |
|   |   |   <p>Content here...</p>         |    | |           |   |
|   |   +----------------------------------+    | |  Ad       |   |
|   |                                           | |  Banner   |   |
|   |   +----------------------------------+    | |           |   |
|   |   | <section>                        |    | |           |   |
|   |   |   <h3>Main Points</h3>           |    | |           |   |
|   |   |   <p>Content here...</p>         |    | |           |   |
|   |   |                                  |    | |           |   |
|   |   |   +----------------------------+ |    | |           |   |
|   |   |   | <figure>                   | |    | |           |   |
|   |   |   |   [ Image ]               | |    | |           |   |
|   |   |   |   <figcaption>            | |    | |           |   |
|   |   |   |     Caption text          | |    | |           |   |
|   |   |   +----------------------------+ |    | |           |   |
|   |   +----------------------------------+    | |           |   |
|   |                                           | |           |   |
|   +-------------------------------------------+ +-----------+   |
|                                                                 |
+=================================================================+
|                        <footer>                                 |
|   Copyright 2026  |  Privacy Policy  |  Terms  |  Contact      |
+=================================================================+
```

#### Full Code Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Blog</title>
</head>
<body>

  <header>
    <h1>My Travel Blog</h1>
    <p>Exploring the world, one city at a time</p>
    <nav>
      <ul>
        <li><a href="index.html">Home</a></li>
        <li><a href="about.html">About</a></li>
        <li><a href="blog.html">Blog</a></li>
        <li><a href="contact.html">Contact</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <article>
      <h2>A Week in Tokyo</h2>
      <p>Published on <time datetime="2026-06-20">June 20, 2026</time></p>

      <section>
        <h3>Getting There</h3>
        <p>We flew from Karachi to Tokyo Narita Airport, a 10-hour flight
           with one layover in Bangkok.</p>
      </section>

      <section>
        <h3>Day 1: Shibuya and Shinjuku</h3>
        <p>Our first stop was the famous Shibuya Crossing...</p>

        <figure>
          <img src="shibuya.jpg" alt="Crowds crossing at Shibuya intersection at night">
          <figcaption>Shibuya Crossing at night -- the busiest intersection in the world.</figcaption>
        </figure>
      </section>

      <details>
        <summary>Travel Tips for Tokyo</summary>
        <ul>
          <li>Get a Suica card for trains and buses</li>
          <li>Download Google Translate with Japanese offline</li>
          <li>Carry cash -- many small shops do not accept cards</li>
        </ul>
      </details>
    </article>

    <aside>
      <h3>Related Posts</h3>
      <ul>
        <li><a href="#">5 Days in Seoul</a></li>
        <li><a href="#">Backpacking Through Vietnam</a></li>
      </ul>
    </aside>
  </main>

  <footer>
    <p>&copy; 2026 My Travel Blog. All rights reserved.</p>
    <nav>
      <a href="privacy.html">Privacy Policy</a> |
      <a href="terms.html">Terms of Service</a>
    </nav>
  </footer>

</body>
</html>
```

---

## 2. HTML5 Multimedia

Before HTML5, playing audio or video on a web page required third-party plugins like Adobe Flash. HTML5 introduced native `<audio>` and `<video>` elements, making multimedia a built-in part of the web.

### The `<audio>` Tag

The `<audio>` element embeds sound content in a page.

```html
<!-- Basic usage -->
<audio src="song.mp3" controls></audio>

<!-- With all common attributes -->
<audio controls autoplay loop muted>
  <source src="song.mp3" type="audio/mpeg">
  <source src="song.ogg" type="audio/ogg">
  Your browser does not support the audio element.
</audio>
```

#### Audio Attributes

| Attribute   | Description                                                  |
|-------------|--------------------------------------------------------------|
| `controls`  | Displays play, pause, volume, and seek controls              |
| `autoplay`  | Audio starts playing as soon as it loads (use sparingly)      |
| `loop`      | Audio replays from the beginning after it ends                |
| `muted`     | Audio is muted by default                                    |
| `preload`   | Hints how much data to preload: `none`, `metadata`, or `auto`|

> **Important:** Most modern browsers block `autoplay` unless the audio is also `muted`. This is a user-experience policy to prevent annoying auto-playing sounds.

#### Supported Audio Formats

| Format | MIME Type    | Browser Support                       |
|--------|-------------|---------------------------------------|
| MP3    | audio/mpeg  | All modern browsers                   |
| WAV    | audio/wav   | All modern browsers                   |
| OGG    | audio/ogg   | Chrome, Firefox, Edge (not Safari)    |

**Real-life example:** A podcast website. Each episode page has an `<audio>` element so visitors can listen directly in the browser without downloading a separate app.

---

### The `<video>` Tag

The `<video>` element embeds video content in a page.

```html
<!-- Basic usage -->
<video src="intro.mp4" controls width="640" height="360"></video>

<!-- With poster image and multiple sources -->
<video controls width="640" height="360"
       poster="thumbnail.jpg" muted>
  <source src="intro.mp4"  type="video/mp4">
  <source src="intro.webm" type="video/webm">
  <source src="intro.ogv"  type="video/ogg">
  Your browser does not support the video element.
</video>
```

#### Video Attributes

| Attribute        | Description                                                |
|------------------|------------------------------------------------------------|
| `controls`       | Displays play, pause, volume, seek, and fullscreen controls|
| `autoplay`       | Video starts playing as soon as it loads                   |
| `loop`           | Video replays from the beginning after it ends             |
| `muted`          | Video audio is muted by default                            |
| `poster`         | URL of an image shown before the video plays               |
| `width`          | Width of the video player in pixels                        |
| `height`         | Height of the video player in pixels                       |
| `preload`        | Hints how much data to preload: `none`, `metadata`, `auto` |

> **Tip:** If you want `autoplay` to work reliably across browsers, also include `muted`. Browsers allow muted autoplay but block unmuted autoplay.

#### Supported Video Formats

| Format | MIME Type  | Browser Support                       |
|--------|-----------|---------------------------------------|
| MP4    | video/mp4 | All modern browsers (best support)    |
| WebM   | video/webm| Chrome, Firefox, Edge, Opera          |
| OGG    | video/ogg | Chrome, Firefox, Edge (not Safari)    |

**Real-life example:** An online learning platform like this very course. Each lesson has a `<video>` element with a poster image (the lesson thumbnail), controls for play/pause, and multiple source formats to ensure compatibility across all browsers.

---

### The `<source>` Tag and Format Support

The `<source>` tag specifies multiple media resources for `<audio>` and `<video>`. The browser picks the first format it supports and ignores the rest.

```html
<video controls width="640" height="360">
  <source src="video.mp4"  type="video/mp4">   <!-- Tried first  -->
  <source src="video.webm" type="video/webm">  <!-- Tried second -->
  <source src="video.ogv"  type="video/ogg">   <!-- Tried third  -->
  <p>Your browser does not support HTML5 video.
     <a href="video.mp4">Download the video</a> instead.</p>
</video>
```

**Why provide multiple formats?** Not every browser supports every format. MP4 has the widest support, so list it first. The fallback text (or link) inside the element is shown only if the browser supports none of the listed formats.

```
  Browser encounters <video>
         |
         v
  Can it play .mp4?
    YES --> Play .mp4, stop
    NO  --> Can it play .webm?
              YES --> Play .webm, stop
              NO  --> Can it play .ogv?
                        YES --> Play .ogv, stop
                        NO  --> Show fallback text
```

---

## 3. Embedding External Content

### The `<iframe>` Tag

The `<iframe>` (inline frame) element embeds another HTML page inside the current page. It is commonly used for embedding YouTube videos, Google Maps, and other third-party widgets.

#### Embedding a YouTube Video

```html
<iframe
  width="560"
  height="315"
  src="https://www.youtube.com/embed/dQw4w9WgXcQ"
  title="YouTube video player"
  frameborder="0"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope"
  allowfullscreen>
</iframe>
```

> **How to get the embed URL:** On YouTube, click "Share" below the video, then click "Embed," and copy the provided `<iframe>` code.

#### Embedding Google Maps

```html
<iframe
  src="https://www.google.com/maps/embed?pb=!1m18!..."
  width="600"
  height="450"
  style="border:0;"
  allowfullscreen=""
  loading="lazy"
  referrerpolicy="no-referrer-when-downgrade">
</iframe>
```

> **How to get the embed URL:** On Google Maps, click "Share," then select "Embed a map," and copy the provided `<iframe>` code.

#### Iframe Attributes

| Attribute         | Description                                              |
|-------------------|----------------------------------------------------------|
| `src`             | URL of the page to embed                                 |
| `width`           | Width of the iframe in pixels                            |
| `height`          | Height of the iframe in pixels                           |
| `frameborder`     | `0` removes the border (deprecated in HTML5, use CSS)    |
| `allowfullscreen` | Allows the iframe content to enter fullscreen mode       |
| `title`           | Describes the iframe content for accessibility           |
| `loading`         | `lazy` defers loading until the iframe is near viewport  |
| `allow`           | Specifies a permissions policy for the iframe            |

**Real-life example:** A restaurant website that shows its location on an embedded Google Map, or a portfolio site that showcases YouTube demo videos directly on the page.

---

### Security Considerations

Iframes can introduce security risks because you are loading someone else's content into your page.

1. **Only embed content from trusted sources.** A malicious iframe could phish your users or run harmful scripts.

2. **Use the `sandbox` attribute** to restrict what the embedded content can do:

   ```html
   <iframe src="https://example.com" sandbox="allow-scripts allow-same-origin"></iframe>
   ```

   Without any values, `sandbox` disables forms, scripts, popups, and more. You selectively re-enable only what is needed.

3. **Never embed sensitive pages in iframes.** Most banks and secure services send an `X-Frame-Options` header that prevents their pages from being embedded -- this is a deliberate security measure.

4. **Use HTTPS sources.** Always embed content over HTTPS to prevent man-in-the-middle attacks.

---

## 4. HTML5 New Input Types

HTML5 introduced many new input types that provide built-in validation, specialized keyboards on mobile devices, and native date/color pickers. These replace the need for custom JavaScript widgets in many cases.

| Input Type       | Code Example                                       | What It Does                                    |
|------------------|----------------------------------------------------|-------------------------------------------------|
| `color`          | `<input type="color" value="#ff0000">`              | Opens a color picker dialog                     |
| `range`          | `<input type="range" min="0" max="100" step="5">`  | Displays a slider control                       |
| `date`           | `<input type="date">`                               | Shows a date picker (YYYY-MM-DD)                |
| `datetime-local` | `<input type="datetime-local">`                     | Date and time picker (no timezone)              |
| `month`          | `<input type="month">`                              | Picker for month and year                       |
| `week`           | `<input type="week">`                               | Picker for week number and year                 |
| `time`           | `<input type="time">`                               | Picker for hours and minutes                    |
| `search`         | `<input type="search" placeholder="Search...">`     | Search field with clear button                  |
| `tel`            | `<input type="tel" placeholder="03XX-XXXXXXX">`     | Telephone number (shows phone keyboard on mobile)|
| `url`            | `<input type="url" placeholder="https://...">`      | URL field with built-in validation              |

#### Complete Form Example with New Input Types

```html
<form action="/submit" method="POST">

  <label for="fav-color">Favorite Color:</label>
  <input type="color" id="fav-color" name="fav-color" value="#3498db">
  <br><br>

  <label for="satisfaction">Satisfaction (1-10):</label>
  <input type="range" id="satisfaction" name="satisfaction"
         min="1" max="10" step="1" value="5">
  <br><br>

  <label for="birthday">Birthday:</label>
  <input type="date" id="birthday" name="birthday">
  <br><br>

  <label for="meeting">Meeting Date & Time:</label>
  <input type="datetime-local" id="meeting" name="meeting">
  <br><br>

  <label for="start-month">Start Month:</label>
  <input type="month" id="start-month" name="start-month">
  <br><br>

  <label for="camp-week">Camp Week:</label>
  <input type="week" id="camp-week" name="camp-week">
  <br><br>

  <label for="alarm">Alarm Time:</label>
  <input type="time" id="alarm" name="alarm">
  <br><br>

  <label for="query">Search:</label>
  <input type="search" id="query" name="query" placeholder="Search articles...">
  <br><br>

  <label for="phone">Phone Number:</label>
  <input type="tel" id="phone" name="phone" placeholder="03XX-XXXXXXX">
  <br><br>

  <label for="website">Website:</label>
  <input type="url" id="website" name="website" placeholder="https://example.com">
  <br><br>

  <button type="submit">Submit</button>

</form>
```

**Real-life example:** An event registration form. You use `date` for the event date, `time` for the session time, `tel` for the attendee's phone number, `url` for their website, and `range` for rating their interest level.

---

## 5. HTML Best Practices

After four weeks of HTML, here are the rules you should follow in every project going forward.

### 1. Proper Indentation

Indent nested elements consistently (2 or 4 spaces -- pick one and stick with it). This makes your code scannable.

```html
<!-- Bad: No indentation -->
<main>
<article>
<h2>Title</h2>
<p>Content</p>
</article>
</main>

<!-- Good: Consistent 2-space indentation -->
<main>
  <article>
    <h2>Title</h2>
    <p>Content</p>
  </article>
</main>
```

### 2. Always Use `alt` on Images

The `alt` attribute describes the image for screen readers and displays when the image fails to load. Every `<img>` must have an `alt` attribute.

```html
<!-- Bad -->
<img src="logo.png">

<!-- Good -->
<img src="logo.png" alt="Company logo - blue circle with white letter A">

<!-- Decorative image (intentionally empty alt) -->
<img src="divider.png" alt="">
```

> **Rule of thumb:** If the image conveys information, describe it. If the image is purely decorative, use an empty `alt=""` so screen readers skip it.

### 3. Always Close Tags

Every opening tag must have a corresponding closing tag (except self-closing/void elements like `<img>`, `<br>`, `<hr>`, `<input>`).

```html
<!-- Bad -->
<p>First paragraph
<p>Second paragraph

<!-- Good -->
<p>First paragraph</p>
<p>Second paragraph</p>
```

### 4. Use Semantic Tags Instead of Divs

Now that you know semantic tags, use them. Reserve `<div>` for situations where no semantic tag fits (pure styling wrappers, for example).

```html
<!-- Bad -->
<div class="header">
  <div class="nav">...</div>
</div>
<div class="content">...</div>
<div class="footer">...</div>

<!-- Good -->
<header>
  <nav>...</nav>
</header>
<main>...</main>
<footer>...</footer>
```

### 5. Validate Your HTML

Use the **W3C Markup Validation Service** at [https://validator.w3.org](https://validator.w3.org) to check your HTML for errors. You can validate by:

- **URL** -- Enter the address of a live page
- **File Upload** -- Upload your `.html` file
- **Direct Input** -- Paste your HTML code

Common errors the validator catches:
- Missing closing tags
- Missing required attributes (e.g., `alt` on images)
- Incorrectly nested elements
- Deprecated tags or attributes
- Invalid attribute values

**Make it a habit:** Validate every page you build. Clean, valid HTML is the foundation of a professional website.

---

## 6. Week 4 Project -- Build a Complete Multi-Page Website

### Project Description

Build a multi-page website for a fictional business (restaurant, school, gym, agency -- your choice). The site must demonstrate everything you have learned in Weeks 1 through 4.

### Requirements

#### Pages (minimum 3)

1. **Home Page (`index.html`)**
   - Site header with logo/title and navigation
   - Hero section introducing the business
   - At least two content sections (e.g., "Our Services" and "Testimonials")
   - An embedded YouTube video or Google Map
   - Footer with copyright and secondary navigation

2. **About Page (`about.html`)**
   - Same header and navigation as the home page
   - An article about the business history
   - A figure with an image and caption
   - A collapsible FAQ section using `<details>` and `<summary>`
   - A table (e.g., team members, business hours, milestones)
   - Footer

3. **Contact Page (`contact.html`)**
   - Same header and navigation
   - A contact form using the new HTML5 input types:
     - `text` for name
     - `email` for email address
     - `tel` for phone number
     - `url` for website (optional field)
     - `date` for preferred contact date
     - `textarea` for message
     - Submit button
   - An embedded Google Maps iframe showing the business location
   - Footer

#### Technical Requirements

- Use semantic HTML throughout (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer>`, `<figure>`, `<figcaption>`)
- Use `<time>` elements for any dates
- Include at least one `<audio>` or `<video>` element
- Include at least one `<iframe>` embed
- All images must have descriptive `alt` attributes
- All pages must link to each other via the navigation
- Code must be properly indented
- Code must pass the W3C validator with no errors

### Suggested File Structure

```
my-website/
  |-- index.html        (Home page)
  |-- about.html         (About page)
  |-- contact.html       (Contact page)
  |-- images/
  |     |-- logo.png
  |     |-- hero.jpg
  |     |-- team.jpg
  |     |-- about-photo.jpg
  |-- media/
  |     |-- intro.mp4    (or background-music.mp3)
```

---

## 7. Summary -- What We Learned in HTML (Weeks 1-4 Recap)

```
  +===========================================================+
  |                   HTML LEARNING PATH                       |
  +===========================================================+
  |                                                            |
  |  WEEK 1: HTML Basics                                       |
  |  ---------------------------------------------------------|
  |  - What is HTML and how the web works                      |
  |  - Document structure (<!DOCTYPE>, <html>, <head>, <body>) |
  |  - Headings (<h1> to <h6>), paragraphs (<p>)              |
  |  - Text formatting (<b>, <i>, <strong>, <em>, <br>, <hr>) |
  |  - Comments (<!-- -->)                                     |
  |                                                            |
  +------------------------------------------------------------+
  |                                                            |
  |  WEEK 2: Links, Images & Lists                             |
  |  ---------------------------------------------------------|
  |  - Hyperlinks (<a>) -- absolute, relative, email, phone   |
  |  - Images (<img>) with alt, width, height                  |
  |  - Unordered lists (<ul>), ordered lists (<ol>)            |
  |  - Nested lists and description lists (<dl>)               |
  |                                                            |
  +------------------------------------------------------------+
  |                                                            |
  |  WEEK 3: Tables & Forms                                    |
  |  ---------------------------------------------------------|
  |  - Tables (<table>, <tr>, <th>, <td>, colspan, rowspan)   |
  |  - Forms (<form>, <input>, <label>, <select>, <textarea>) |
  |  - Form attributes (action, method, required, placeholder) |
  |  - Input types (text, password, email, number, checkbox,   |
  |    radio, file, submit, reset)                             |
  |                                                            |
  +------------------------------------------------------------+
  |                                                            |
  |  WEEK 4: Semantic HTML & HTML5 Features    <-- YOU ARE HERE|
  |  ---------------------------------------------------------|
  |  - Semantic tags (header, nav, main, section, article,     |
  |    aside, footer, figure, figcaption, details, summary,    |
  |    time)                                                   |
  |  - HTML5 multimedia (audio, video, source)                 |
  |  - Embedding external content (iframe)                     |
  |  - New input types (color, range, date, datetime-local,    |
  |    month, week, time, search, tel, url)                    |
  |  - HTML best practices and validation                      |
  |                                                            |
  +===========================================================+
```

### Key Takeaways

1. **Semantic HTML gives your pages meaning.** Use `<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>`, and `<footer>` instead of generic `<div>` elements. This improves accessibility, SEO, and code readability.

2. **HTML5 brings multimedia to the browser natively.** Use `<audio>` and `<video>` with the `<source>` element for cross-browser compatibility. Always provide controls and consider providing multiple formats.

3. **Iframes let you embed third-party content**, but use them responsibly. Only embed from trusted sources and consider using the `sandbox` attribute for security.

4. **New input types reduce your reliance on JavaScript.** Date pickers, color pickers, sliders, and input validation are now built into HTML.

5. **Best practices matter from day one.** Proper indentation, closing tags, alt attributes, semantic structure, and validation are not optional -- they are the mark of a professional developer.

### What Comes Next

With HTML complete, you are ready to move on to **CSS** -- where you will learn how to style, color, position, and animate everything you have built so far. The semantic structure you learned this week will make CSS much easier to write and maintain.

---

> **Congratulations!** You have completed the HTML portion of the MERN stack course. You now have a solid foundation in HTML that will serve you throughout your career as a web developer.
