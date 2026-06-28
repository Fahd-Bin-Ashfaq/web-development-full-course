# Week 0 — Basic Computing

## Table of Contents

1. [What Is a Computer?](#1-what-is-a-computer)
2. [How Does a Computer Work?](#2-how-does-a-computer-work)
3. [Hardware vs Software](#3-hardware-vs-software)
4. [What Is a Network?](#4-what-is-a-network)
5. [What Is the Internet?](#5-what-is-the-internet)
6. [What Is a Website?](#6-what-is-a-website)
7. [Types of Websites](#7-types-of-websites)
8. [History of the Internet](#8-history-of-the-internet)
9. [What Is Programming?](#9-what-is-programming)
10. [Types of Programming Languages](#10-types-of-programming-languages)
11. [Why Not Just Use Drag-and-Drop Website Builders?](#11-why-not-just-use-drag-and-drop-website-builders)
12. [Career Paths in Web Development](#12-career-paths-in-web-development)

---

## 1. What Is a Computer?

A **computer** is an electronic machine that takes input, processes it, and gives output.

**Real-Life Example:** Think of a computer like a chef in a restaurant. You give the chef ingredients (input), the chef follows a recipe to cook food (processing), and you receive a delicious meal (output).

### How a Computer Works — The IPO Model

```
┌─────────┐     ┌─────────────┐     ┌──────────┐
│  INPUT   │ ──▶ │  PROCESSING │ ──▶ │  OUTPUT  │
│          │     │             │     │          │
│ Keyboard │     │    CPU      │     │ Monitor  │
│ Mouse    │     │ (The Brain) │     │ Speaker  │
│ Scanner  │     │             │     │ Printer  │
└─────────┘     └─────────────┘     └──────────┘
                      │
                      ▼
               ┌─────────────┐
               │   STORAGE   │
               │             │
               │ Hard Drive  │
               │ SSD / RAM   │
               └─────────────┘
```

### Key Components of a Computer

| Component | What It Does | Real-Life Analogy |
|-----------|-------------|-------------------|
| **CPU** | Processes all instructions | The brain of the computer |
| **RAM** | Temporary fast memory | Your desk — holds things you're currently working on |
| **Hard Drive / SSD** | Permanent storage | A filing cabinet — stores everything long-term |
| **Monitor** | Displays output visually | A TV screen |
| **Keyboard & Mouse** | Input devices | Your hands — how you communicate with the computer |
| **Motherboard** | Connects all parts together | The nervous system that links everything |

---

## 2. How Does a Computer Work?

Every computer follows a cycle called the **Fetch-Decode-Execute Cycle**:

```
┌──────────────────────────────────────────────┐
│           FETCH-DECODE-EXECUTE CYCLE         │
│                                              │
│   1. FETCH    → CPU gets the instruction     │
│                  from memory (RAM)           │
│                                              │
│   2. DECODE   → CPU understands what the     │
│                  instruction means           │
│                                              │
│   3. EXECUTE  → CPU performs the action      │
│                  (calculate, display, etc.)   │
│                                              │
│   4. STORE    → Result is saved back         │
│                  to memory                   │
│                                              │
│           ↻ This repeats billions            │
│             of times per second              │
└──────────────────────────────────────────────┘
```

**Real-Life Example:** Imagine you are solving a math problem on paper:
1. **Fetch:** You read the problem from the textbook
2. **Decode:** You understand what the problem is asking
3. **Execute:** You calculate the answer
4. **Store:** You write the answer in your notebook

Your computer does this exact process — but **billions of times per second**.

---

## 3. Hardware vs Software

```
┌─────────────────────────────────────────────────────────┐
│                    COMPUTER                             │
│                                                         │
│   ┌─────────────────┐      ┌─────────────────────┐     │
│   │    HARDWARE      │      │     SOFTWARE         │     │
│   │  (Physical Parts)│      │  (Programs & Apps)   │     │
│   │                  │      │                      │     │
│   │  • Monitor       │      │  • Windows / macOS   │     │
│   │  • Keyboard      │      │  • Chrome Browser    │     │
│   │  • CPU           │      │  • VS Code           │     │
│   │  • RAM           │      │  • Microsoft Word    │     │
│   │  • Hard Drive    │      │  • Games             │     │
│   │                  │      │                      │     │
│   │  You can TOUCH   │      │  You can only SEE    │     │
│   │  these parts     │      │  and USE these       │     │
│   └─────────────────┘      └─────────────────────┘     │
└─────────────────────────────────────────────────────────┘
```

### Types of Software

| Type | Description | Examples |
|------|------------|---------|
| **System Software** | Runs the computer itself | Windows, macOS, Linux |
| **Application Software** | Programs you use daily | Chrome, Word, WhatsApp |
| **Programming Software** | Tools to write code | VS Code, IntelliJ, Sublime Text |

**Real-Life Example:** Hardware is like the body of a car (engine, wheels, seats). Software is like the driver's knowledge and skills that make the car actually useful. Without software, hardware is just a pile of expensive parts.

---

## 4. What Is a Network?

A **network** is a group of computers connected to each other so they can share data and resources.

```
┌──────────┐         ┌──────────┐
│ Computer │ ──────▶ │ Computer │
│    A     │ ◀────── │    B     │
└──────────┘         └──────────┘
      │                    │
      │    ┌──────────┐    │
      └──▶ │  Printer  │ ◀─┘
           └──────────┘
     (Shared resource on the network)
```

### Types of Networks

| Type | Full Form | Range | Example |
|------|-----------|-------|---------|
| **PAN** | Personal Area Network | ~10 meters | Bluetooth between phone and earbuds |
| **LAN** | Local Area Network | A building | Office or school network |
| **WAN** | Wide Area Network | Countries/Global | The Internet |

**Real-Life Example:** A network is like a postal system. Just as the post office connects people in different cities so they can send letters to each other, a network connects computers so they can send data to each other.

---

## 5. What Is the Internet?

The **Internet** is the world's largest network — a global system of interconnected computer networks that communicate using a standard set of rules called **protocols**.

```
┌─────────────────────────────────────────────────────────────┐
│                    HOW THE INTERNET WORKS                    │
│                                                             │
│  Your Computer ──▶ Router ──▶ ISP ──▶ Internet Backbone     │
│                                            │                │
│                                            ▼                │
│                                    ┌──────────────┐         │
│                                    │   Server     │         │
│                                    │ (stores the  │         │
│                                    │  website)    │         │
│                                    └──────────────┘         │
│                                                             │
│  ISP = Internet Service Provider (e.g., PTCL, Jazz, Zong)   │
└─────────────────────────────────────────────────────────────┘
```

### Key Internet Concepts

| Term | Meaning |
|------|---------|
| **IP Address** | A unique number for every device on the internet (like a home address) |
| **DNS** | Domain Name System — translates website names to IP addresses |
| **HTTP/HTTPS** | Rules for how data is sent between browser and server |
| **URL** | The address you type in the browser (e.g., www.google.com) |
| **Server** | A powerful computer that stores websites and serves them to users |
| **Client** | Your computer or phone that requests and displays websites |

**Real-Life Example:** When you type `www.google.com` in your browser:
1. Your browser asks DNS: "What is the IP address for google.com?"
2. DNS replies: "It's 142.250.190.46"
3. Your browser sends a request to that IP address
4. Google's server sends back the website
5. Your browser displays it on your screen

This entire process happens in **milliseconds**.

---

## 6. What Is a Website?

A **website** is a collection of web pages stored on a server and accessible through the internet using a browser.

```
┌───────────────────────────────────────────────┐
│               ANATOMY OF A WEBSITE            │
│                                               │
│   ┌──────────────────────────────────────┐    │
│   │         FRONTEND (Client-Side)       │    │
│   │                                      │    │
│   │  HTML  → Structure (skeleton)        │    │
│   │  CSS   → Styling (clothes & makeup)  │    │
│   │  JS    → Behavior (muscles & brain)  │    │
│   └──────────────────────────────────────┘    │
│                     │                         │
│                     ▼                         │
│   ┌──────────────────────────────────────┐    │
│   │         BACKEND (Server-Side)        │    │
│   │                                      │    │
│   │  Server    → Handles requests        │    │
│   │  Database  → Stores data             │    │
│   │  API       → Connects frontend       │    │
│   │              to backend              │    │
│   └──────────────────────────────────────┘    │
└───────────────────────────────────────────────┘
```

**Real-Life Example:** A website is like a restaurant:
- **Frontend** = The dining area (what customers see — menu, decor, tables)
- **Backend** = The kitchen (where food is prepared — customers never see this)
- **Database** = The pantry (where all ingredients are stored)
- **API** = The waiter (takes orders from the dining area to the kitchen and brings food back)

---

## 7. Types of Websites

### Static vs Dynamic Websites

```
┌─────────────────────────┐     ┌─────────────────────────┐
│     STATIC WEBSITE      │     │     DYNAMIC WEBSITE     │
│                         │     │                         │
│  • Same content for     │     │  • Content changes      │
│    every visitor        │     │    based on user         │
│                         │     │                         │
│  • Built with HTML/CSS  │     │  • Uses a database      │
│    only                 │     │    and server logic      │
│                         │     │                         │
│  • Fast and simple      │     │  • Interactive and       │
│                         │     │    personalized         │
│                         │     │                         │
│  Examples:              │     │  Examples:              │
│  • Portfolio sites      │     │  • Facebook             │
│  • Company brochures    │     │  • YouTube              │
│  • Documentation sites  │     │  • Amazon               │
└─────────────────────────┘     └─────────────────────────┘
```

### Other Types of Websites

| Type | Description | Example |
|------|------------|---------|
| **E-Commerce** | Online stores | Amazon, Daraz |
| **Social Media** | User-generated content platforms | Facebook, Instagram |
| **Blog** | Article and content publishing | Medium, WordPress |
| **Web Application** | Complex interactive apps | Gmail, Google Docs |
| **Landing Page** | Single-page marketing sites | Product launch pages |

---

## 8. History of the Internet

### Timeline

```
1960s ──── ARPANET (US Military Project)
   │       └─ First network connecting 4 computers
   │          Scientist: J.C.R. Licklider (vision)
   │                     Vint Cerf & Bob Kahn (TCP/IP)
   ▼
1971 ───── First Email Sent
   │       └─ Ray Tomlinson sent the first email
   │          using the @ symbol
   ▼
1983 ───── TCP/IP Protocol Adopted
   │       └─ The "language" all computers use to
   │          communicate — this is the birth of
   │          the modern Internet
   ▼
1989 ───── World Wide Web Invented
   │       └─ Tim Berners-Lee created HTML, HTTP,
   │          and the first web browser
   │          at CERN (Switzerland)
   ▼
1993 ───── Mosaic Browser Released
   │       └─ First browser with images
   │          Made the web visual and accessible
   ▼
1995 ───── JavaScript Created
   │       └─ Brendan Eich created JavaScript
   │          in just 10 days at Netscape
   ▼
1998 ───── Google Founded
   │       └─ Larry Page & Sergey Brin
   │          revolutionized web search
   ▼
2004 ───── Facebook Launched
   │       └─ Mark Zuckerberg — social media era begins
   ▼
2007 ───── iPhone Released
   │       └─ Mobile internet becomes mainstream
   ▼
2010s ──── Cloud Computing & Modern Web
   │       └─ AWS, React, Node.js, MongoDB
   │          The MERN stack era begins
   ▼
Today ──── AI, Web3, and the Future
           └─ AI-powered apps, blockchain,
              and next-gen web experiences
```

### Key Scientists and Their Contributions

| Scientist | Contribution | Year |
|-----------|-------------|------|
| **J.C.R. Licklider** | Envisioned a global computer network | 1962 |
| **Vint Cerf & Bob Kahn** | Created TCP/IP (Internet protocol) | 1974 |
| **Tim Berners-Lee** | Invented the World Wide Web, HTML, HTTP | 1989 |
| **Brendan Eich** | Created JavaScript | 1995 |
| **Linus Torvalds** | Created Linux and Git | 1991, 2005 |

---

## 9. What Is Programming?

**Programming** is the process of writing instructions that a computer can understand and execute to perform specific tasks.

**Real-Life Example:** Think of programming like writing a recipe. A recipe tells a chef exactly what steps to follow, in what order, and with what ingredients. Similarly, a program tells a computer exactly what to do, step by step.

### Why Do We Learn Programming?

```
┌──────────────────────────────────────────────────────┐
│           WHY LEARN PROGRAMMING?                     │
│                                                      │
│   1. AUTOMATION                                      │
│      → Make computers do repetitive work for you     │
│      → Example: Auto-sorting 10,000 emails           │
│                                                      │
│   2. PROBLEM SOLVING                                 │
│      → Break complex problems into small steps       │
│      → Example: How does Google Maps find the        │
│        shortest route?                               │
│                                                      │
│   3. CAREER OPPORTUNITIES                            │
│      → High demand, high pay, remote work            │
│      → Example: A developer in Pakistan can work     │
│        for a company in the USA                      │
│                                                      │
│   4. BUILD ANYTHING                                  │
│      → Websites, apps, games, AI systems             │
│      → Example: WhatsApp started as a simple idea    │
│        by two developers                             │
│                                                      │
│   5. UNDERSTAND TECHNOLOGY                           │
│      → Know how the tools you use every day work     │
│      → Example: How does YouTube recommend videos?   │
└──────────────────────────────────────────────────────┘
```

### How Programming Works

```
   You write code          Compiler/Interpreter          Computer
   in a language     ──▶   translates it to        ──▶  executes
   (JavaScript)            machine code (0s and 1s)      the task

   let x = 5;             0100110001010...              Stores 5
   console.log(x);        1001010100101...              Shows "5"
```

---

## 10. Types of Programming Languages

### By Level

```
┌─────────────────────────────────────────────────────────┐
│              PROGRAMMING LANGUAGE LEVELS                 │
│                                                         │
│   HIGH-LEVEL LANGUAGES (Human-friendly)                 │
│   ├── JavaScript   → "let name = 'Ali';"               │
│   ├── Python       → "name = 'Ali'"                    │
│   └── Java         → "String name = "Ali";"            │
│                                                         │
│   LOW-LEVEL LANGUAGES (Machine-friendly)                │
│   ├── Assembly     → "MOV AX, 5"                       │
│   └── Machine Code → "01001010 10010101"               │
│                                                         │
│   ↑ Easier for humans          Faster for computers ↑   │
└─────────────────────────────────────────────────────────┘
```

### By Purpose

| Type | Used For | Languages |
|------|----------|-----------|
| **Web Development** | Websites and web apps | JavaScript, HTML, CSS, PHP |
| **Mobile Development** | Phone apps | Swift, Kotlin, React Native |
| **Data Science** | Analyzing data | Python, R |
| **Game Development** | Video games | C++, C#, Unity |
| **System Programming** | Operating systems | C, C++, Rust |

### What We Will Learn in This Course

We will focus on **JavaScript** because:
- It works on both **frontend** (browser) and **backend** (server with Node.js)
- It is the **most popular** programming language in the world
- It is the core of the **MERN stack** (MongoDB, Express, React, Node.js)
- One language for the entire web application — from the button you click to the database that stores your data

---

## 11. Why Not Just Use Drag-and-Drop Website Builders?

Drag-and-drop builders like Wix, WordPress, and Squarespace let you create websites without code. So why learn programming?

```
┌────────────────────────────────────────────────────────────┐
│         DRAG-AND-DROP  vs  CUSTOM CODE                     │
│                                                            │
│  DRAG-AND-DROP (Wix, WordPress)                            │
│  ✓ Quick to start                                          │
│  ✓ No coding knowledge needed                              │
│  ✗ Limited customization — you're stuck with templates     │
│  ✗ Slow performance — bloated code                         │
│  ✗ Monthly fees add up                                     │
│  ✗ You don't OWN the platform                              │
│  ✗ Cannot build complex apps (no login, no database)       │
│  ✗ No career growth — you're a "user", not a "builder"     │
│                                                            │
│  CUSTOM CODE (HTML, CSS, JS, React, Node.js)               │
│  ✓ Unlimited customization — build anything you imagine    │
│  ✓ Fast performance — clean, optimized code                │
│  ✓ Free hosting options available                          │
│  ✓ You OWN everything                                      │
│  ✓ Can build any app — social media, e-commerce, SaaS      │
│  ✓ High-paying career — $50K–$150K+ globally               │
│  ✗ Takes time to learn (but this course makes it easy!)    │
└────────────────────────────────────────────────────────────┘
```

**Real-Life Example:** Using a drag-and-drop builder is like ordering a pre-made suit from a store — it looks okay but never fits perfectly. Learning to code is like becoming a tailor — you can create anything from scratch, exactly the way you want, and you can also alter other people's work. The tailor has a career; the customer just has a suit.

---

## 12. Career Paths in Web Development

```
┌────────────────────────────────────────────────────────┐
│              WEB DEVELOPMENT CAREER PATHS              │
│                                                        │
│   ┌──────────────┐                                     │
│   │  FRONTEND    │  → What users see and interact with │
│   │  DEVELOPER   │  → HTML, CSS, JavaScript, React     │
│   └──────┬───────┘                                     │
│          │                                             │
│   ┌──────▼───────┐                                     │
│   │  BACKEND     │  → Server, database, business logic │
│   │  DEVELOPER   │  → Node.js, Express, MongoDB        │
│   └──────┬───────┘                                     │
│          │                                             │
│   ┌──────▼───────┐                                     │
│   │  FULL-STACK  │  → Both frontend and backend        │
│   │  DEVELOPER   │  → MERN Stack (our goal!)           │
│   └──────┬───────┘                                     │
│          │                                             │
│   ┌──────▼───────────────────────────────────┐         │
│   │  SPECIALIZED ROLES                       │         │
│   │  • DevOps Engineer                       │         │
│   │  • Mobile App Developer (React Native)   │         │
│   │  • UI/UX Designer                        │         │
│   │  • Cloud Architect                       │         │
│   │  • AI/ML Engineer                        │         │
│   └──────────────────────────────────────────┘         │
└────────────────────────────────────────────────────────┘
```

### Salary Expectations (Global Averages)

| Role | Entry Level | Mid Level | Senior Level |
|------|------------|-----------|-------------|
| **Frontend Developer** | $40K–$60K | $60K–$90K | $90K–$130K |
| **Backend Developer** | $45K–$65K | $65K–$100K | $100K–$140K |
| **Full-Stack Developer** | $50K–$70K | $70K–$110K | $110K–$150K |

### Freelancing Opportunities

As a MERN stack developer, you can also work as a freelancer on platforms like:
- **Upwork** — long-term contracts
- **Fiverr** — project-based work
- **Toptal** — premium clients
- **LinkedIn** — direct job opportunities

**Real-Life Example:** A MERN stack developer in Pakistan can earn PKR 80,000–300,000+ per month working remotely for international clients. This course prepares you for exactly that career.

---

## Summary

```
┌─────────────────────────────────────────────────────┐
│              WEEK 0 — KEY TAKEAWAYS                 │
│                                                     │
│  ✓ A computer takes input, processes it, gives      │
│    output (IPO Model)                               │
│                                                     │
│  ✓ Hardware is physical, software is digital         │
│                                                     │
│  ✓ The internet is a global network of networks     │
│                                                     │
│  ✓ A website has a frontend (what you see) and      │
│    a backend (what runs behind the scenes)          │
│                                                     │
│  ✓ Programming means writing instructions for       │
│    computers — we chose JavaScript because it       │
│    works everywhere                                 │
│                                                     │
│  ✓ Custom code beats drag-and-drop builders for     │
│    real careers and real applications               │
│                                                     │
│  ✓ Our goal: become a Full-Stack MERN Developer     │
│    in 10 months                                     │
└─────────────────────────────────────────────────────┘
```

---

**Next Week:** We begin our hands-on journey with **HTML — the skeleton of every website.**
