# Week 4: Semantic HTML & HTML5 Features — Practice Questions

---

## Section A: Multiple Choice Questions (MCQs)

**Instructions:** Choose the correct option for each question.

---

**Q1. Which of the following is a semantic HTML tag?**

a) `<div>`  
b) `<span>`  
c) `<article>`  
d) `<b>`

<details>
<summary>Answer</summary>
<strong>c) <code>&lt;article&gt;</code></strong> — The <code>&lt;article&gt;</code> tag is a semantic element that clearly describes the meaning of its content (a self-contained piece of content). Tags like <code>&lt;div&gt;</code> and <code>&lt;span&gt;</code> are non-semantic because they say nothing about their content.
</details>

---

**Q2. What is the primary purpose of the `<nav>` element?**

a) To style a navigation bar with CSS  
b) To define a section of navigation links  
c) To create a clickable button  
d) To embed an external page

<details>
<summary>Answer</summary>
<strong>b) To define a section of navigation links</strong> — The <code>&lt;nav&gt;</code> element represents a section of the page whose purpose is to provide navigation links, either within the current document or to other documents.
</details>

---

**Q3. Which tag is used to define the main content area of a webpage?**

a) `<section>`  
b) `<body>`  
c) `<main>`  
d) `<div id="main">`

<details>
<summary>Answer</summary>
<strong>c) <code>&lt;main&gt;</code></strong> — The <code>&lt;main&gt;</code> element represents the dominant content of the <code>&lt;body&gt;</code>. There should be only one <code>&lt;main&gt;</code> element per page, and it should not be nested inside <code>&lt;article&gt;</code>, <code>&lt;aside&gt;</code>, <code>&lt;footer&gt;</code>, <code>&lt;header&gt;</code>, or <code>&lt;nav&gt;</code>.
</details>

---

**Q4. Which attribute of the `<video>` tag allows the video to start playing automatically?**

a) `loop`  
b) `autoplay`  
c) `preload`  
d) `src`

<details>
<summary>Answer</summary>
<strong>b) <code>autoplay</code></strong> — The <code>autoplay</code> attribute specifies that the video should begin playing as soon as it is ready. Note that most modern browsers require the <code>muted</code> attribute alongside <code>autoplay</code> to allow auto-playing without user interaction.
</details>

---

**Q5. What does the `<aside>` element represent?**

a) The footer of a webpage  
b) Content that is indirectly related to the surrounding content  
c) A block of quoted text  
d) The header area of a webpage

<details>
<summary>Answer</summary>
<strong>b) Content that is indirectly related to the surrounding content</strong> — The <code>&lt;aside&gt;</code> element is used for content that is tangentially related to the main content, such as sidebars, pull quotes, or related links.
</details>

---

**Q6. Which HTML5 input type is specifically designed for email addresses?**

a) `<input type="text">`  
b) `<input type="mail">`  
c) `<input type="email">`  
d) `<input type="address">`

<details>
<summary>Answer</summary>
<strong>c) <code>&lt;input type="email"&gt;</code></strong> — The <code>email</code> input type provides built-in validation to ensure the entered value conforms to a valid email address format. It also triggers an appropriate keyboard layout on mobile devices.
</details>

---

**Q7. What is the correct way to embed a YouTube video in an HTML page?**

a) `<video src="youtube-url"></video>`  
b) `<iframe src="youtube-embed-url"></iframe>`  
c) `<embed src="youtube-url">`  
d) `<link href="youtube-url">`

<details>
<summary>Answer</summary>
<strong>b) <code>&lt;iframe src="youtube-embed-url"&gt;&lt;/iframe&gt;</code></strong> — YouTube videos are embedded using the <code>&lt;iframe&gt;</code> element with the embed URL provided by YouTube (e.g., <code>https://www.youtube.com/embed/VIDEO_ID</code>).
</details>

---

**Q8. Which pair of tags is used to provide a caption for an image or illustration?**

a) `<img>` and `<caption>`  
b) `<figure>` and `<figcaption>`  
c) `<picture>` and `<label>`  
d) `<image>` and `<description>`

<details>
<summary>Answer</summary>
<strong>b) <code>&lt;figure&gt;</code> and <code>&lt;figcaption&gt;</code></strong> — The <code>&lt;figure&gt;</code> element wraps self-contained content like images, diagrams, or code snippets, while <code>&lt;figcaption&gt;</code> provides a caption or description for that content.
</details>

---

**Q9. How does semantic HTML improve SEO (Search Engine Optimization)?**

a) It makes the website load faster  
b) It adds keywords to the page automatically  
c) It helps search engines understand the structure and meaning of the content  
d) It prevents other websites from copying the content

<details>
<summary>Answer</summary>
<strong>c) It helps search engines understand the structure and meaning of the content</strong> — Semantic tags give search engine crawlers meaningful context about the page structure, making it easier to index and rank the content appropriately.
</details>

---

**Q10. Which attribute is used to display playback controls for the `<audio>` element?**

a) `autoplay`  
b) `controls`  
c) `display`  
d) `player`

<details>
<summary>Answer</summary>
<strong>b) <code>controls</code></strong> — The <code>controls</code> attribute adds audio controls such as play, pause, volume, and seek bar to the audio player.
</details>

---

**Q11. What is the difference between `<header>` and `<head>`?**

a) They are the same element  
b) `<head>` contains metadata; `<header>` contains introductory content visible on the page  
c) `<header>` contains metadata; `<head>` contains visible content  
d) `<head>` is used inside `<header>`

<details>
<summary>Answer</summary>
<strong>b) <code>&lt;head&gt;</code> contains metadata; <code>&lt;header&gt;</code> contains introductory content visible on the page</strong> — The <code>&lt;head&gt;</code> element holds metadata like title, links to stylesheets, and scripts. The <code>&lt;header&gt;</code> element is a semantic tag used inside the <code>&lt;body&gt;</code> to represent introductory or navigational content.
</details>

---

**Q12. Which HTML5 input type displays a date picker in supported browsers?**

a) `<input type="calendar">`  
b) `<input type="datetime">`  
c) `<input type="date">`  
d) `<input type="picker">`

<details>
<summary>Answer</summary>
<strong>c) <code>&lt;input type="date"&gt;</code></strong> — The <code>date</code> input type allows the user to select a date from a built-in date picker provided by the browser.
</details>

---

**Q13. Which tag should be used for the bottom section of a webpage containing copyright information?**

a) `<bottom>`  
b) `<section>`  
c) `<footer>`  
d) `<div class="footer">`

<details>
<summary>Answer</summary>
<strong>c) <code>&lt;footer&gt;</code></strong> — The <code>&lt;footer&gt;</code> element represents the footer of a document or section. It typically contains copyright information, contact details, links to privacy policies, or related documents.
</details>

---

**Q14. What does the `sandbox` attribute do in an `<iframe>`?**

a) It adds a border around the iframe  
b) It restricts the capabilities of the embedded content for security  
c) It allows the iframe to resize automatically  
d) It makes the iframe full-screen

<details>
<summary>Answer</summary>
<strong>b) It restricts the capabilities of the embedded content for security</strong> — The <code>sandbox</code> attribute applies extra restrictions to the iframe content, such as blocking scripts, forms, and popups, to prevent malicious content from affecting the parent page.
</details>

---

**Q15. Which of the following is NOT a valid HTML5 semantic element?**

a) `<section>`  
b) `<content>`  
c) `<article>`  
d) `<aside>`

<details>
<summary>Answer</summary>
<strong>b) <code>&lt;content&gt;</code></strong> — There is no standard HTML5 element called <code>&lt;content&gt;</code>. The valid semantic elements include <code>&lt;section&gt;</code>, <code>&lt;article&gt;</code>, <code>&lt;aside&gt;</code>, <code>&lt;header&gt;</code>, <code>&lt;footer&gt;</code>, <code>&lt;nav&gt;</code>, and <code>&lt;main&gt;</code>.
</details>

---

## Section B: Short Answer Questions

**Instructions:** Answer each question in 2-4 sentences.

---

**Q1. What is semantic HTML, and why should developers use it?**

<details>
<summary>Answer</summary>
Semantic HTML refers to the use of HTML elements that clearly describe the meaning and purpose of the content they contain, such as <code>&lt;header&gt;</code>, <code>&lt;nav&gt;</code>, <code>&lt;article&gt;</code>, and <code>&lt;footer&gt;</code>. Developers should use semantic HTML because it improves code readability, enhances accessibility for screen readers and assistive technologies, boosts SEO by helping search engines understand page structure, and makes the codebase easier to maintain and collaborate on.
</details>

---

**Q2. What is the difference between the `<section>` and `<article>` elements?**

<details>
<summary>Answer</summary>
The <code>&lt;section&gt;</code> element represents a generic thematic grouping of content, typically with a heading, and is used to divide a page into logical sections (e.g., "About Us," "Services"). The <code>&lt;article&gt;</code> element represents a self-contained piece of content that could independently make sense outside the context of the page, such as a blog post, news article, or user comment. A key distinction is that an <code>&lt;article&gt;</code> should be independently distributable or reusable, whereas a <code>&lt;section&gt;</code> is a structural division within a document.
</details>

---

**Q3. Why is the `<iframe>` element useful, and what are some common use cases?**

<details>
<summary>Answer</summary>
The <code>&lt;iframe&gt;</code> (inline frame) element is useful because it allows developers to embed external content within a webpage without leaving the current page. Common use cases include embedding YouTube videos, Google Maps, social media feeds, external forms, payment gateways, and third-party widgets. The <code>&lt;iframe&gt;</code> provides attributes like <code>sandbox</code> and <code>allow</code> for controlling the permissions and security of the embedded content.
</details>

---

**Q4. What is the `<figure>` tag used for, and how does `<figcaption>` complement it?**

<details>
<summary>Answer</summary>
The <code>&lt;figure&gt;</code> tag is used to wrap self-contained content such as images, illustrations, diagrams, code snippets, or charts that are referenced from the main flow of the document. The <code>&lt;figcaption&gt;</code> element is placed inside <code>&lt;figure&gt;</code> to provide a visible caption or description for the content. Together, they create a semantic relationship between the media and its caption, which improves accessibility and helps search engines understand the context of the content.
</details>

---

**Q5. How does using semantic HTML improve SEO?**

<details>
<summary>Answer</summary>
Semantic HTML improves SEO by providing search engine crawlers with meaningful structural information about the page content. When elements like <code>&lt;article&gt;</code>, <code>&lt;nav&gt;</code>, <code>&lt;header&gt;</code>, and <code>&lt;main&gt;</code> are used, search engines can better understand which content is primary, which is navigational, and which is supplementary. This structured understanding helps search engines index pages more accurately, potentially leading to better rankings and the generation of rich search results (such as featured snippets).
</details>

---

**Q6. What audio and video formats are commonly supported in HTML5?**

<details>
<summary>Answer</summary>
For audio, the commonly supported HTML5 formats are MP3 (universally supported), WAV (uncompressed, widely supported), and OGG (open format, supported by most modern browsers except Safari). For video, the commonly supported formats are MP4 (with H.264 codec, universally supported), WebM (open format by Google, supported by Chrome, Firefox, and Edge), and OGG/OGV (supported by Firefox and Chrome). To ensure maximum browser compatibility, developers often provide multiple source formats using the <code>&lt;source&gt;</code> element inside the <code>&lt;audio&gt;</code> or <code>&lt;video&gt;</code> tags.
</details>

---

**Q7. What are some HTML5 input types that were not available in earlier versions of HTML?**

<details>
<summary>Answer</summary>
HTML5 introduced several new input types including <code>email</code> (validates email format), <code>url</code> (validates URL format), <code>date</code> (provides a date picker), <code>time</code> (provides a time picker), <code>number</code> (restricts input to numeric values with optional min/max), <code>range</code> (displays a slider control), <code>color</code> (opens a color picker), <code>search</code> (optimized for search queries), <code>tel</code> (optimized for telephone numbers), and <code>datetime-local</code> (selects both date and time). These types provide built-in validation and trigger appropriate keyboards on mobile devices.
</details>

---

**Q8. How does semantic HTML improve web accessibility?**

<details>
<summary>Answer</summary>
Semantic HTML improves web accessibility by providing meaningful structure that assistive technologies like screen readers can interpret. For example, a screen reader can identify a <code>&lt;nav&gt;</code> element and announce it as a navigation region, allowing users to skip directly to it. Similarly, <code>&lt;main&gt;</code> helps users jump to the primary content, and proper use of <code>&lt;header&gt;</code> and <code>&lt;footer&gt;</code> establishes landmarks that make navigating a page much easier for users with visual impairments. Without semantic tags, screen readers treat all content as generic blocks, making navigation slow and frustrating.
</details>

---

## Section C: True or False

**Instructions:** Identify whether each statement is True or False.

| # | Statement | Answer |
|---|-----------|--------|
| 1 | The `<div>` tag is a semantic HTML element. | **False** — `<div>` is a non-semantic, generic container element. |
| 2 | A webpage can contain multiple `<header>` and `<footer>` elements. | **True** — Each `<section>` or `<article>` can have its own `<header>` and `<footer>`. |
| 3 | The `<main>` element can be used multiple times on a single page. | **False** — There should be only one visible `<main>` element per page. |
| 4 | The `<iframe>` element is used to embed external content within a webpage. | **True** — `<iframe>` allows embedding external pages, videos, maps, and other content. |
| 5 | The `autoplay` attribute on a `<video>` tag always works without any other attributes in modern browsers. | **False** — Most modern browsers require the `muted` attribute alongside `autoplay` to allow auto-playing without user interaction. |
| 6 | The `<figcaption>` element can only be used inside a `<figure>` element. | **True** — `<figcaption>` is designed to be a child of `<figure>` and provides a caption for its content. |
| 7 | The `<section>` tag is used for self-contained content that can be independently distributed. | **False** — That describes the `<article>` tag. The `<section>` tag is for thematic grouping of content. |
| 8 | The `controls` attribute on `<audio>` displays a play/pause button, volume slider, and progress bar. | **True** — The `controls` attribute renders the browser's default audio playback controls. |
| 9 | HTML5 introduced new input types such as `email`, `date`, and `range`. | **True** — These are among the many new input types introduced in HTML5. |
| 10 | Semantic HTML has no impact on search engine optimization. | **False** — Semantic HTML significantly improves SEO by helping search engines understand page structure and content meaning. |

---

## Section D: Code Exercises

---

### Task 1: Convert Non-Semantic HTML to Semantic HTML

**Instructions:** The following HTML page is built using only `<div>` tags. Rewrite it using appropriate semantic HTML5 elements. Do not change the visible content — only replace the non-semantic tags with their semantic equivalents.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>My Website</title>
</head>
<body>
    <div class="header">
        <h1>My Website</h1>
        <div class="nav">
            <a href="#home">Home</a>
            <a href="#about">About</a>
            <a href="#contact">Contact</a>
        </div>
    </div>

    <div class="main-content">
        <div class="post">
            <h2>My First Blog Post</h2>
            <p>Published on January 1, 2026</p>
            <p>This is the content of my very first blog post. I am learning semantic HTML.</p>
        </div>

        <div class="post">
            <h2>My Second Blog Post</h2>
            <p>Published on January 15, 2026</p>
            <p>This post covers HTML5 features like audio and video elements.</p>
        </div>
    </div>

    <div class="sidebar">
        <h3>About the Author</h3>
        <p>A passionate web developer learning the MERN stack.</p>
    </div>

    <div class="footer">
        <p>&copy; 2026 My Website. All rights reserved.</p>
    </div>
</body>
</html>
```

<details>
<summary>Expected Output</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>My Website</title>
</head>
<body>
    <header>
        <h1>My Website</h1>
        <nav>
            <a href="#home">Home</a>
            <a href="#about">About</a>
            <a href="#contact">Contact</a>
        </nav>
    </header>

    <main>
        <article>
            <h2>My First Blog Post</h2>
            <p>Published on January 1, 2026</p>
            <p>This is the content of my very first blog post. I am learning semantic HTML.</p>
        </article>

        <article>
            <h2>My Second Blog Post</h2>
            <p>Published on January 15, 2026</p>
            <p>This post covers HTML5 features like audio and video elements.</p>
        </article>
    </main>

    <aside>
        <h3>About the Author</h3>
        <p>A passionate web developer learning the MERN stack.</p>
    </aside>

    <footer>
        <p>&copy; 2026 My Website. All rights reserved.</p>
    </footer>
</body>
</html>
```

</details>

---

### Task 2: Create a Blog Page Using Semantic Elements

**Instructions:** Build a complete blog page that includes the following semantic elements: `<header>`, `<nav>`, `<main>`, `<article>` (at least 2), `<aside>`, and `<footer>`. The page should have:

- A site header with a title and navigation links (Home, Blog, About, Contact).
- A main area containing at least two blog articles, each with its own heading, publication date, and paragraph content.
- A sidebar with a list of recent posts or categories.
- A footer with copyright information.

<details>
<summary>Expected Output</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tech Insights Blog</title>
</head>
<body>
    <header>
        <h1>Tech Insights Blog</h1>
        <nav>
            <ul>
                <li><a href="index.html">Home</a></li>
                <li><a href="blog.html">Blog</a></li>
                <li><a href="about.html">About</a></li>
                <li><a href="contact.html">Contact</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <section>
            <h2>Latest Posts</h2>

            <article>
                <header>
                    <h3>Getting Started with Semantic HTML</h3>
                    <p><time datetime="2026-01-10">January 10, 2026</time> | By Admin</p>
                </header>
                <p>Semantic HTML is one of the most important foundations of modern web development. In this article, we explore what semantic elements are and how they improve the quality of your webpages.</p>
                <footer>
                    <p>Tags: HTML, Semantic, Beginners</p>
                </footer>
            </article>

            <article>
                <header>
                    <h3>HTML5 Multimedia: Audio and Video</h3>
                    <p><time datetime="2026-01-20">January 20, 2026</time> | By Admin</p>
                </header>
                <p>HTML5 made it incredibly easy to embed audio and video content directly into webpages without relying on third-party plugins. Learn how to use the audio and video elements effectively.</p>
                <footer>
                    <p>Tags: HTML5, Multimedia, Audio, Video</p>
                </footer>
            </article>
        </section>
    </main>

    <aside>
        <h3>Categories</h3>
        <ul>
            <li><a href="#">HTML Basics</a></li>
            <li><a href="#">CSS Styling</a></li>
            <li><a href="#">JavaScript</a></li>
            <li><a href="#">MERN Stack</a></li>
        </ul>

        <h3>Recent Posts</h3>
        <ul>
            <li><a href="#">Understanding Iframes</a></li>
            <li><a href="#">HTML5 Input Types</a></li>
            <li><a href="#">Web Accessibility Guide</a></li>
        </ul>
    </aside>

    <footer>
        <p>&copy; 2026 Tech Insights Blog. All rights reserved.</p>
    </footer>
</body>
</html>
```

</details>

---

### Task 3: Embed a YouTube Video and Google Maps

**Instructions:** Create an HTML page that contains:

1. An embedded YouTube video using an `<iframe>` (use any public YouTube video URL).
2. An embedded Google Map showing any location using an `<iframe>`.
3. Proper headings and descriptions for each embedded item.
4. Use semantic HTML elements to structure the page.

<details>
<summary>Expected Output</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Embedded Content Demo</title>
</head>
<body>
    <header>
        <h1>Embedded Content Demo</h1>
        <p>Demonstrating YouTube video and Google Maps embedding using iframes.</p>
    </header>

    <main>
        <section>
            <h2>Featured Video</h2>
            <figure>
                <iframe 
                    width="560" 
                    height="315" 
                    src="https://www.youtube.com/embed/dQw4w9WgXcQ" 
                    title="YouTube Video Player"
                    frameborder="0" 
                    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
                    allowfullscreen>
                </iframe>
                <figcaption>A sample embedded YouTube video.</figcaption>
            </figure>
        </section>

        <section>
            <h2>Our Location</h2>
            <figure>
                <iframe 
                    width="600" 
                    height="450" 
                    src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3619.4674839290766!2d67.0099388!3d24.8607343!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0x0!2zMjTCsDUxJzM4LjYiTiA2N8KwMDAnMzUuOCJF!5e0!3m2!1sen!2s!4v1600000000000"
                    title="Google Maps - Karachi"
                    style="border:0;" 
                    allowfullscreen="" 
                    loading="lazy">
                </iframe>
                <figcaption>Our office location on Google Maps.</figcaption>
            </figure>
        </section>
    </main>

    <footer>
        <p>&copy; 2026 Embedded Content Demo. All rights reserved.</p>
    </footer>
</body>
</html>
```

</details>

---

### Task 4: Create a Multimedia Gallery Page

**Instructions:** Create an HTML page that serves as a multimedia gallery containing:

1. At least 2 audio players with different audio files (use `<audio>` with `controls`).
2. At least 2 video players with different video files (use `<video>` with `controls`).
3. Use `<figure>` and `<figcaption>` to label each media item.
4. Provide multiple `<source>` formats for browser compatibility.
5. Include a fallback message for unsupported browsers.

<details>
<summary>Expected Output</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Multimedia Gallery</title>
</head>
<body>
    <header>
        <h1>Multimedia Gallery</h1>
        <p>A collection of audio tracks and video clips.</p>
    </header>

    <main>
        <section>
            <h2>Audio Collection</h2>

            <figure>
                <audio controls>
                    <source src="audio/track1.mp3" type="audio/mpeg">
                    <source src="audio/track1.ogg" type="audio/ogg">
                    Your browser does not support the audio element.
                </audio>
                <figcaption>Track 1: Relaxing Background Music</figcaption>
            </figure>

            <figure>
                <audio controls>
                    <source src="audio/track2.mp3" type="audio/mpeg">
                    <source src="audio/track2.wav" type="audio/wav">
                    Your browser does not support the audio element.
                </audio>
                <figcaption>Track 2: Upbeat Podcast Intro</figcaption>
            </figure>
        </section>

        <section>
            <h2>Video Collection</h2>

            <figure>
                <video width="640" height="360" controls>
                    <source src="videos/clip1.mp4" type="video/mp4">
                    <source src="videos/clip1.webm" type="video/webm">
                    Your browser does not support the video element.
                </video>
                <figcaption>Clip 1: Introduction to Web Development</figcaption>
            </figure>

            <figure>
                <video width="640" height="360" controls poster="images/clip2-poster.jpg">
                    <source src="videos/clip2.mp4" type="video/mp4">
                    <source src="videos/clip2.ogg" type="video/ogg">
                    Your browser does not support the video element.
                </video>
                <figcaption>Clip 2: Semantic HTML in Action</figcaption>
            </figure>
        </section>
    </main>

    <footer>
        <p>&copy; 2026 Multimedia Gallery. All rights reserved.</p>
    </footer>
</body>
</html>
```

</details>

---

### Task 5: Week 4 Project — Build a Complete Multi-Page Semantic Website

**Instructions:** Build a multi-page website with **three pages**: Home, About, and Contact. This is the capstone project for Week 4. Your website must meet the following requirements:

**General Requirements (All Pages):**
- Use semantic HTML elements throughout (`<header>`, `<nav>`, `<main>`, `<footer>`).
- Each page must have a consistent navigation bar linking to all three pages.
- Each page must have a `<header>` with the site name and a `<footer>` with copyright information.

**Page 1 — Home (`index.html`):**
- A hero section with a welcome heading and a brief introduction paragraph.
- A "Featured Content" section with at least two `<article>` elements.
- An `<aside>` with quick links or announcements.
- At least one embedded YouTube video using `<iframe>`.

**Page 2 — About (`about.html`):**
- An "About Us" section using `<section>`.
- A team members section where each member is displayed using `<figure>` and `<figcaption>` (use placeholder images).
- Use `<article>` for each team member's bio.

**Page 3 — Contact (`contact.html`):**
- A contact form using HTML5 input types: `text`, `email`, `tel`, `date`, and `textarea`.
- An embedded Google Maps `<iframe>` showing a location.
- Include form validation attributes (`required`, `placeholder`, `pattern`).

<details>
<summary>Hints</summary>

- Start by creating the common structure (header and footer) and copy it across all three files.
- Use the `<nav>` element with an unordered list for navigation links.
- For placeholder images, you can use services like `https://via.placeholder.com/300x200`.
- For the contact form, remember to use `<label>` elements associated with each input using the `for` attribute.
- Test each page individually to ensure all links work correctly.
- You may add basic inline styles or a simple CSS file for layout, but the focus should be on correct semantic HTML structure.
</details>

---

## Section E: HTML Weeks 1-4 Comprehensive Review

**Instructions:** This section covers all HTML topics from Weeks 1 through 4. It serves as a comprehensive assessment of the HTML phase before moving on to CSS.

---

**Q1. (MCQ) Which tag is used to define the largest heading in HTML?**

a) `<heading>`  
b) `<h6>`  
c) `<h1>`  
d) `<title>`

<details>
<summary>Answer</summary>
<strong>c) <code>&lt;h1&gt;</code></strong> — HTML provides six levels of headings from <code>&lt;h1&gt;</code> (largest and most important) to <code>&lt;h6&gt;</code> (smallest). The <code>&lt;title&gt;</code> tag defines the page title in the browser tab, not a visible heading on the page.
</details>

---

**Q2. (MCQ) What is the correct HTML for creating a hyperlink that opens in a new tab?**

a) `<a href="url" new>`  
b) `<a href="url" target="_blank">`  
c) `<a href="url" target="new">`  
d) `<a href="url" window="_blank">`

<details>
<summary>Answer</summary>
<strong>b) <code>&lt;a href="url" target="_blank"&gt;</code></strong> — The <code>target="_blank"</code> attribute opens the linked page in a new browser tab or window.
</details>

---

**Q3. (MCQ) Which attribute is required in the `<img>` tag for accessibility?**

a) `title`  
b) `src`  
c) `alt`  
d) `width`

<details>
<summary>Answer</summary>
<strong>c) <code>alt</code></strong> — The <code>alt</code> attribute provides alternative text for the image, which is essential for screen readers and is displayed when the image cannot be loaded. While <code>src</code> is also required for the image to display, <code>alt</code> is specifically important for accessibility.
</details>

---

**Q4. (MCQ) Which HTML element is used to group rows in the header of a table?**

a) `<thead>`  
b) `<header>`  
c) `<th>`  
d) `<head>`

<details>
<summary>Answer</summary>
<strong>a) <code>&lt;thead&gt;</code></strong> — The <code>&lt;thead&gt;</code> element groups the header content in a table. It is used alongside <code>&lt;tbody&gt;</code> and <code>&lt;tfoot&gt;</code> to structure table content semantically.
</details>

---

**Q5. (MCQ) Which input attribute prevents a form from being submitted until the field is filled?**

a) `placeholder`  
b) `required`  
c) `mandatory`  
d) `validate`

<details>
<summary>Answer</summary>
<strong>b) <code>required</code></strong> — The <code>required</code> attribute specifies that an input field must be filled out before the form can be submitted.
</details>

---

**Q6. (Coding) Write the complete HTML structure for a table that displays student records with columns: Roll Number, Name, Email, and Grade. Include at least 3 rows of data. Use `<thead>`, `<tbody>`, and proper table elements.**

<details>
<summary>Expected Output</summary>

```html
<table border="1">
    <thead>
        <tr>
            <th>Roll Number</th>
            <th>Name</th>
            <th>Email</th>
            <th>Grade</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>001</td>
            <td>Ali Ahmed</td>
            <td>ali@example.com</td>
            <td>A</td>
        </tr>
        <tr>
            <td>002</td>
            <td>Sara Khan</td>
            <td>sara@example.com</td>
            <td>B+</td>
        </tr>
        <tr>
            <td>003</td>
            <td>Usman Tariq</td>
            <td>usman@example.com</td>
            <td>A-</td>
        </tr>
    </tbody>
</table>
```

</details>

---

**Q7. (Coding) Create a registration form with the following fields: Full Name (text), Email (email), Password (password), Date of Birth (date), Phone Number (tel), Gender (radio buttons), and a Submit button. Use proper `<label>` tags and form validation attributes.**

<details>
<summary>Expected Output</summary>

```html
<form action="/register" method="POST">
    <div>
        <label for="fullname">Full Name:</label>
        <input type="text" id="fullname" name="fullname" placeholder="Enter your full name" required>
    </div>

    <div>
        <label for="email">Email:</label>
        <input type="email" id="email" name="email" placeholder="Enter your email" required>
    </div>

    <div>
        <label for="password">Password:</label>
        <input type="password" id="password" name="password" placeholder="Enter your password" minlength="8" required>
    </div>

    <div>
        <label for="dob">Date of Birth:</label>
        <input type="date" id="dob" name="dob" required>
    </div>

    <div>
        <label for="phone">Phone Number:</label>
        <input type="tel" id="phone" name="phone" placeholder="03XX-XXXXXXX" pattern="[0-9]{4}-[0-9]{7}">
    </div>

    <div>
        <p>Gender:</p>
        <input type="radio" id="male" name="gender" value="male">
        <label for="male">Male</label>

        <input type="radio" id="female" name="gender" value="female">
        <label for="female">Female</label>
    </div>

    <div>
        <button type="submit">Register</button>
    </div>
</form>
```

</details>

---

**Q8. (Coding) Write the HTML for an ordered list of the top 5 programming languages, where each language contains an unordered nested list of two key features.**

<details>
<summary>Expected Output</summary>

```html
<h2>Top 5 Programming Languages</h2>
<ol>
    <li>JavaScript
        <ul>
            <li>Runs in the browser and on the server (Node.js)</li>
            <li>Essential for web development</li>
        </ul>
    </li>
    <li>Python
        <ul>
            <li>Simple and readable syntax</li>
            <li>Widely used in AI and data science</li>
        </ul>
    </li>
    <li>Java
        <ul>
            <li>Platform-independent (Write Once, Run Anywhere)</li>
            <li>Popular for enterprise applications</li>
        </ul>
    </li>
    <li>C++
        <ul>
            <li>High performance and memory control</li>
            <li>Used in game development and system programming</li>
        </ul>
    </li>
    <li>TypeScript
        <ul>
            <li>Adds static typing to JavaScript</li>
            <li>Improves code reliability and maintainability</li>
        </ul>
    </li>
</ol>
```

</details>

---

**Q9. (Coding) Create a complete HTML5 page that demonstrates proper document structure. Include: DOCTYPE declaration, html tag with lang attribute, head with meta charset, viewport meta tag, title, and a body containing a header, main section with a paragraph and an image, and a footer.**

<details>
<summary>Expected Output</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Complete HTML5 Page</title>
</head>
<body>
    <header>
        <h1>Welcome to My Website</h1>
        <nav>
            <a href="#home">Home</a> |
            <a href="#about">About</a> |
            <a href="#contact">Contact</a>
        </nav>
    </header>

    <main>
        <section>
            <h2>About This Page</h2>
            <p>This page demonstrates the proper structure of an HTML5 document, including semantic elements and essential meta tags for responsive design.</p>
            <figure>
                <img src="https://via.placeholder.com/600x300" alt="A placeholder image demonstrating the img element" width="600" height="300">
                <figcaption>A sample image with proper alt text for accessibility.</figcaption>
            </figure>
        </section>
    </main>

    <footer>
        <p>&copy; 2026 My Website. All rights reserved.</p>
    </footer>
</body>
</html>
```

</details>

---

**Q10. (MCQ) Looking at the following HTML, which combination of corrections would make it fully valid and semantic?**

```html
<div class="header">
    <h1>Blog</h1>
</div>
<div class="main">
    <div class="post">
        <h2>First Post</h2>
        <img src="photo.jpg">
        <p>Content here...</p>
    </div>
</div>
<div class="footer">
    <p>Copyright 2026</p>
</div>
```

a) Replace outer `<div>` tags with `<header>`, `<main>`, and `<footer>`; replace the post `<div>` with `<article>`; add `alt` attribute to `<img>`  
b) Add `id` attributes to all `<div>` tags  
c) Replace `<h1>` with `<title>` and add `<head>` tags  
d) Add CSS classes to make the page semantic

<details>
<summary>Answer</summary>
<strong>a) Replace outer <code>&lt;div&gt;</code> tags with <code>&lt;header&gt;</code>, <code>&lt;main&gt;</code>, and <code>&lt;footer&gt;</code>; replace the post <code>&lt;div&gt;</code> with <code>&lt;article&gt;</code>; add <code>alt</code> attribute to <code>&lt;img&gt;</code></strong> — Semantic HTML requires using meaningful elements instead of generic <code>&lt;div&gt;</code> tags. The <code>alt</code> attribute is required for accessibility. Adding CSS classes or IDs does not make HTML semantic — semantics come from the elements themselves.
</details>

---

## Total Question Count

| Section | Type | Count |
|---------|------|-------|
| Section A | Multiple Choice Questions | 15 |
| Section B | Short Answer Questions | 8 |
| Section C | True or False | 10 |
| Section D | Code Exercises | 5 |
| Section E | Comprehensive Review (Weeks 1-4) | 10 |
| **Total** | | **48 Questions** |
