# Week 13: Version Control with Git & GitHub

> **MERN Stack Full Course**
> You have completed the HTML, CSS, and JavaScript phases. Now it is time to learn how developers
> manage, track, and collaborate on code using Git and GitHub.

---

## Table of Contents

1. [What is Version Control?](#1-what-is-version-control)
2. [What is Git?](#2-what-is-git)
3. [Installing Git](#3-installing-git)
4. [Git Basics — The Three States](#4-git-basics--the-three-states)
5. [Essential Git Commands](#5-essential-git-commands)
6. [Branching](#6-branching)
7. [What is GitHub?](#7-what-is-github)
8. [Connecting Git to GitHub](#8-connecting-git-to-github)
9. [Collaboration on GitHub](#9-collaboration-on-github)
10. [Git Best Practices](#10-git-best-practices)
11. [Common Git Workflow](#11-common-git-workflow)
12. [Summary & Command Cheat Sheet](#12-summary--command-cheat-sheet)

---

## 1. What is Version Control?

### The Problem

Imagine you are writing an essay. You save it as `essay.doc`. Then you make changes and save it as `essay_v2.doc`. More changes become `essay_final.doc`, then `essay_final_REALLY_FINAL.doc`. Sound familiar?

```
Documents/
  essay.doc
  essay_v2.doc
  essay_final.doc
  essay_final_REALLY_FINAL.doc
  essay_final_REALLY_FINAL_v2.doc       <-- This is chaos
```

Now imagine this with thousands of code files and a team of 10 developers. It would be a disaster.

### The Solution: Version Control

**Version control** is a system that records changes to files over time so you can recall specific versions later.

**Real-Life Example: Google Docs Version History**

If you have ever used Google Docs, you know you can click **File > Version History** and see every change ever made to the document. You can see who made each change, when they made it, and you can restore any previous version with a single click. Version control for code works the same way, but it is far more powerful.

### Why Version Control Matters

| Benefit | Explanation |
|---------|-------------|
| **Save Progress** | Every change is recorded. You can always go back to a working version. |
| **Collaboration** | Multiple developers can work on the same project simultaneously without overwriting each other's work. |
| **Backup** | Your entire project history is stored. Even if your laptop breaks, the code is safe. |
| **Accountability** | You can see who changed what and when. This is critical for debugging. |
| **Experimentation** | You can try new ideas without fear. If they fail, just revert. |

### Types of Version Control

#### Centralized (e.g., SVN)

```
                    +------------------+
                    |  Central Server  |
                    |   (single copy)  |
                    +--------+---------+
                             |
              +--------------+--------------+
              |              |              |
         +----+----+   +----+----+   +----+----+
         |  Dev A  |   |  Dev B  |   |  Dev C  |
         | (partial|   | (partial|   | (partial|
         |  copy)  |   |  copy)  |   |  copy)  |
         +---------+   +---------+   +---------+

    * One central server holds the full history
    * Developers check out only the files they need
    * If the server goes down, nobody can work
```

#### Distributed (e.g., Git)

```
         +---------+   +---------+   +---------+
         |  Dev A  |   |  Dev B  |   |  Dev C  |
         |  (FULL  |   |  (FULL  |   |  (FULL  |
         |  copy)  |   |  copy)  |   |  copy)  |
         +----+----+   +----+----+   +----+----+
              |              |              |
              +--------------+--------------+
                             |
                    +--------+---------+
                    |  Remote Server   |
                    | (GitHub/GitLab)  |
                    +------------------+

    * Every developer has a FULL copy of the repository
    * You can work offline — commits, branches, history are all local
    * If the server goes down, any developer's copy can restore it
```

#### Why Git Won

- **Speed**: Git operations are almost instant because everything is local.
- **Branching**: Git makes branching cheap and easy (SVN branching was painful).
- **Distributed**: No single point of failure.
- **Adoption**: GitHub made Git the industry standard. Today, over 90% of developers use Git.

---

## 2. What is Git?

### A Brief History

Git was created by **Linus Torvalds** in **2005** — the same person who created the Linux operating system. When the existing version control tool for Linux development (BitKeeper) revoked its free license, Linus decided to build his own. He designed Git to be fast, distributed, and capable of handling massive projects like the Linux kernel (which has over 30 million lines of code).

### Git vs GitHub

This is one of the most common points of confusion for beginners. They are **not** the same thing.

```
  +---------------------------------------------+
  |                                             |
  |   Git                  GitHub               |
  |   ===                  ======               |
  |                                             |
  |   - A software tool    - A website/platform |
  |   - Runs on your       - Runs on the cloud  |
  |     computer           - Hosts Git repos    |
  |   - Tracks changes     - Adds collaboration |
  |     locally              features           |
  |   - Free & open        - Pull requests,     |
  |     source               issues, actions    |
  |   - Works offline      - Requires internet  |
  |                                             |
  +---------------------------------------------+

  Think of it this way:

  Git    = The engine         (the tool)
  GitHub = The highway system (the platform)

  You can use Git without GitHub.
  You cannot use GitHub without Git.
```

**Other platforms similar to GitHub**: GitLab, Bitbucket, Azure DevOps. They all use Git under the hood.

---

## 3. Installing Git

### Windows

1. Download Git from [https://git-scm.com/download/win](https://git-scm.com/download/win)
2. Run the installer. Accept the default settings (they are fine for beginners).
3. Git Bash will be installed alongside Git — this gives you a Unix-like terminal on Windows.

### Mac

```bash
# Option 1: Install via Homebrew (recommended)
brew install git

# Option 2: Install Xcode Command Line Tools (includes Git)
xcode-select --install
```

### Linux (Ubuntu/Debian)

```bash
sudo apt update
sudo apt install git
```

### Verify Installation

After installation, open your terminal (or Git Bash on Windows) and run:

```bash
git --version
```

You should see something like:

```
git version 2.43.0
```

If you see a version number, Git is installed and ready.

### Initial Configuration

Before you start using Git, you need to tell it who you are. This information is attached to every commit you make.

```bash
# Set your name
git config --global user.name "Your Name"

# Set your email (use the same email you will use for GitHub)
git config --global user.email "your.email@example.com"

# Verify your configuration
git config --list
```

| Command | Purpose |
|---------|---------|
| `git config --global user.name "Name"` | Set your name for all repos |
| `git config --global user.email "email"` | Set your email for all repos |
| `git config --global init.defaultBranch main` | Set default branch name to `main` |
| `git config --list` | View all configuration settings |

> **Note**: The `--global` flag means these settings apply to all Git repositories on your computer. Without it, the setting applies only to the current repository.

---

## 4. Git Basics — The Three States

This is the most important concept in Git. Every file in a Git repository exists in one of three states.

### The Three States Diagram

```
  +-------------------+     git add     +-------------------+   git commit   +-------------------+
  |                   | --------------> |                   | ------------> |                   |
  |  WORKING          |                 |  STAGING AREA     |               |  REPOSITORY       |
  |  DIRECTORY        |                 |  (Index)          |               |  (.git directory) |
  |                   |                 |                   |               |                   |
  |  Where you edit   |                 |  Where you        |               |  Where Git        |
  |  your files       |                 |  prepare your     |               |  permanently      |
  |                   |                 |  next commit      |               |  stores snapshots |
  +-------------------+                 +-------------------+               +-------------------+

        You write code here           You choose what to               Git saves a snapshot
                                      include in the next              of your staged changes
                                      snapshot                         with a message
```

### Real-Life Analogy: Mailing a Letter

| Step | Git Equivalent | What Happens |
|------|---------------|--------------|
| **Writing the letter** | Working Directory | You are actively editing your files. Nothing is saved yet. |
| **Putting the letter in an envelope** | Staging Area (`git add`) | You have decided which changes you want to include. The letter is sealed and ready. |
| **Dropping it in the mailbox** | Repository (`git commit`) | The letter is sent. It is now permanently recorded in the post office's system. |

### Why a Staging Area?

You might wonder: why not just save directly? The staging area gives you **control**. Imagine you changed 5 files, but only 3 of those changes are related to the feature you are working on. The staging area lets you commit only those 3 files now and deal with the other 2 later.

```
  Changed Files:           Staging Area:           Commit:
  +-- login.js             +-- login.js            "Add login feature"
  +-- signup.js            +-- signup.js              includes: login.js
  +-- header.css           +-- (not staged)                    signup.js
  +-- README.md            +-- (not staged)
  +-- bug-fix.js           +-- (not staged)

  You choose what goes into each commit. This keeps your history clean.
```

---

## 5. Essential Git Commands

### 5.1 git init — Initialize a New Repository

```bash
# Create a new project folder and initialize Git
mkdir my-project
cd my-project
git init
```

Output:

```
Initialized empty Git repository in /home/user/my-project/.git/
```

This creates a hidden `.git` folder inside your project. That folder is where Git stores all the version history. **Never delete or modify the `.git` folder manually.**

### 5.2 git status — Check Current State

This is the command you will use the most. It tells you what is going on.

```bash
git status
```

Example output:

```
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)

        modified:   index.html

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        style.css

no changes added to commit (use "git add" to track)
```

**Translation**: `index.html` was modified but not staged. `style.css` is a new file Git has never seen before.

### 5.3 git add — Stage Changes

```bash
# Stage a specific file
git add index.html

# Stage multiple specific files
git add index.html style.css

# Stage all changed and new files in the current directory
git add .

# Stage all changes across the entire repository
git add -A
```

> **Tip**: Prefer `git add <filename>` over `git add .` so you know exactly what you are committing.

### 5.4 git commit — Save a Snapshot

```bash
# Commit with a message
git commit -m "Add navigation bar to homepage"
```

Output:

```
[main a1b2c3d] Add navigation bar to homepage
 2 files changed, 45 insertions(+), 3 deletions(-)
```

A commit is like a **save point** in a video game. You can always come back to it.

### Writing Good Commit Messages

Bad commit messages:

```
git commit -m "fixed stuff"
git commit -m "update"
git commit -m "asdfgh"
```

Good commit messages follow the **Conventional Commits** format:

```
<type>: <short description>

Types:
  feat:     A new feature
  fix:      A bug fix
  docs:     Documentation changes
  style:    Code formatting (not CSS styling)
  refactor: Code restructuring without behavior change
  test:     Adding or fixing tests
  chore:    Maintenance tasks (dependencies, configs)
```

Examples of good commit messages:

```bash
git commit -m "feat: add user login page"
git commit -m "fix: resolve crash on empty cart checkout"
git commit -m "docs: update API endpoint documentation"
git commit -m "style: format code with Prettier"
git commit -m "refactor: extract validation logic into helper"
```

### 5.5 git log — View History

```bash
# Full log
git log

# Compact one-line format (most useful)
git log --oneline

# Show last 5 commits
git log --oneline -5

# Show a visual graph of branches
git log --oneline --graph --all
```

Example output of `git log --oneline`:

```
a1b2c3d (HEAD -> main) feat: add navigation bar
e4f5g6h fix: correct footer alignment
i7j8k9l feat: create homepage layout
m0n1o2p Initial commit
```

### 5.6 git diff — See Changes

```bash
# See unstaged changes (working directory vs staging area)
git diff

# See staged changes (staging area vs last commit)
git diff --staged

# See changes between two commits
git diff a1b2c3d e4f5g6h
```

Example output:

```diff
--- a/index.html
+++ b/index.html
@@ -10,6 +10,8 @@
   <body>
     <h1>Welcome</h1>
+    <nav>
+      <a href="/">Home</a>
+      <a href="/about">About</a>
+    </nav>
   </body>
```

Lines starting with `+` are additions. Lines starting with `-` are deletions.

### 5.7 .gitignore — What Files to Ignore

Some files should **never** be committed: dependencies, environment secrets, build outputs, OS files. You list them in a file called `.gitignore` at the root of your project.

```bash
# Create a .gitignore file
touch .gitignore
```

A typical `.gitignore` for a MERN stack project:

```gitignore
# Dependencies
node_modules/

# Environment variables (SECRETS - never commit these)
.env
.env.local
.env.production

# Build output
dist/
build/

# OS files
.DS_Store
Thumbs.db

# IDE settings
.vscode/
.idea/

# Logs
*.log
npm-debug.log*

# Coverage reports
coverage/
```

> **Critical Rule**: If you accidentally commit `node_modules` or `.env`, they stay in Git history forever (even after deleting them). Always set up `.gitignore` before your first commit.

### Essential Commands Reference Table

| Command | What It Does |
|---------|-------------|
| `git init` | Initialize a new Git repository |
| `git status` | Show the current state of your files |
| `git add <file>` | Stage a specific file |
| `git add .` | Stage all changes in current directory |
| `git commit -m "msg"` | Create a commit with a message |
| `git log --oneline` | View commit history (compact) |
| `git diff` | Show unstaged changes |
| `git diff --staged` | Show staged changes |

---

## 6. Branching

### What is a Branch?

A branch is an **independent line of development**. When you create a branch, you are creating a parallel copy of your code where you can make changes without affecting the main codebase.

**Real-Life Example: Parallel Universes**

Think of the movie "Everything Everywhere All at Once." Each branch is like a parallel universe. In one universe, you are adding a login page. In another universe, someone else is fixing a bug. These universes are completely independent. When the work is done, you merge the universes back together.

### ASCII Diagram of Branching

```
                              feature/login
                             /
  main:  o---o---o---o---o---o
                          \
                           o---o---o
                              fix/navbar

  Legend:
    o     = a commit
    ---   = the timeline
    /  \  = branch point

  "main" continues forward.
  "feature/login" branches off to work on login.
  "fix/navbar" branches off to fix the navbar.
  Each branch is independent until merged back.
```

### Branch Commands

```bash
# List all local branches (* marks the current branch)
git branch

# Create a new branch
git branch feature/login

# Switch to a branch (older syntax)
git checkout feature/login

# Switch to a branch (newer, preferred syntax)
git switch feature/login

# Create AND switch to a new branch in one command
git checkout -b feature/login
# or
git switch -c feature/login

# Delete a branch (after merging)
git branch -d feature/login
```

### Merging Branches

When your feature is complete, you merge it back into `main`.

```bash
# Step 1: Switch to the branch you want to merge INTO
git switch main

# Step 2: Merge the feature branch into main
git merge feature/login
```

```
  BEFORE MERGE:

  main:           o---o---o---o
                               \
  feature/login:                o---o---o

  AFTER MERGE:

  main:           o---o---o---o-----------M
                               \         /
  feature/login:                o---o---o

  M = merge commit (combines both histories)
```

### Merge Conflicts

A merge conflict happens when two branches modify the **same line** in the **same file**. Git does not know which version to keep, so it asks you to decide.

**When you encounter a conflict**, Git marks the file like this:

```
<<<<<<< HEAD
<h1>Welcome to Our Store</h1>
=======
<h1>Welcome to the Shop</h1>
>>>>>>> feature/login
```

**How to resolve**:

1. Open the file in your editor.
2. Decide which version to keep (or combine both).
3. Remove the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).
4. Stage and commit the resolved file.

```bash
# After manually resolving the conflict in your editor:
git add index.html
git commit -m "fix: resolve merge conflict in homepage heading"
```

### Common Branching Strategies

```
  main (production-ready code)
    |
    +-- develop (integration branch)
          |
          +-- feature/login
          +-- feature/cart
          +-- fix/payment-bug

  Flow:
  1. Create a feature branch from "develop"
  2. Work on your feature
  3. Merge back into "develop"
  4. When "develop" is stable, merge into "main"
  5. "main" always contains working, deployable code
```

| Branch Name | Purpose |
|------------|---------|
| `main` | Production-ready code. Always stable. |
| `develop` | Integration branch where features come together. |
| `feature/*` | New features (e.g., `feature/user-auth`). |
| `fix/*` or `bugfix/*` | Bug fixes (e.g., `fix/login-crash`). |
| `hotfix/*` | Urgent production fixes. |

---

## 7. What is GitHub?

GitHub is a **cloud-based platform** that hosts Git repositories. It adds a web interface and collaboration tools on top of Git.

Think of it this way:
- **Git** is like writing in a notebook (local, private).
- **GitHub** is like publishing that notebook on a shared bookshelf where others can read it, suggest edits, and contribute.

### What GitHub Adds Beyond Git

| Feature | Description |
|---------|-------------|
| **Remote hosting** | Your code is stored in the cloud. Accessible from anywhere. |
| **Pull Requests** | A formal way to propose and review code changes. |
| **Issues** | Track bugs, features, and tasks. |
| **Actions** | Automate testing, deployment, and other workflows. |
| **Pages** | Free hosting for static websites. |
| **Profile** | Your public developer portfolio. |

### Creating a GitHub Account

1. Go to [https://github.com](https://github.com)
2. Click **Sign Up**
3. Choose a professional username (this will be on your resume)
4. Verify your email address

> **Tip**: Your GitHub profile is your developer resume. Employers will look at it. Choose a clean username and start contributing.

### Creating a Repository on GitHub

1. Click the **+** icon in the top right corner and select **New repository**.
2. Give it a name (e.g., `my-first-project`).
3. Add a description.
4. Choose **Public** (visible to everyone) or **Private** (only you can see it).
5. Optionally check **Add a README file**.
6. Click **Create repository**.

### README.md — Your Project's Front Page

The `README.md` file is the first thing people see when they visit your repository. It is written in Markdown (the same format as this document).

A good README includes:

```markdown
# Project Name

Short description of what this project does.

## Features
- Feature 1
- Feature 2

## Installation
1. Clone the repo: `git clone <url>`
2. Install dependencies: `npm install`
3. Start the app: `npm start`

## Technologies Used
- HTML, CSS, JavaScript
- Node.js, Express
- MongoDB, React

## Screenshots
(Add screenshots here)

## License
MIT
```

---

## 8. Connecting Git to GitHub

### The Connection Flow

```
  LOCAL (your computer)                    REMOTE (GitHub)
  +-------------------+                   +-------------------+
  |                   |    git push       |                   |
  |   Local Repo      | ----------------> |   Remote Repo     |
  |   (.git folder)   |                   |   (GitHub.com)    |
  |                   | <---------------- |                   |
  |                   |    git pull       |                   |
  +-------------------+                   +-------------------+
```

### Step-by-Step: Push a Local Project to GitHub

```bash
# Step 1: Create a repo on GitHub (do this on the website first)

# Step 2: In your local project, add the remote connection
git remote add origin https://github.com/yourusername/your-repo.git

# Step 3: Push your code to GitHub
git push -u origin main
```

**Breakdown**:
- `remote add origin` — tells Git where your remote repository lives. `origin` is just a nickname for the URL.
- `push` — uploads your commits to the remote.
- `-u origin main` — sets `origin/main` as the default upstream, so next time you can just type `git push`.

### git pull — Get Latest Changes

```bash
# Download and merge the latest changes from GitHub
git pull origin main

# If you set upstream (-u), just:
git pull
```

`git pull` is actually two commands combined:
1. `git fetch` — downloads changes from the remote.
2. `git merge` — merges those changes into your current branch.

### git clone — Download a Repository

```bash
# Clone a repository from GitHub to your computer
git clone https://github.com/username/repository.git

# Clone into a specific folder name
git clone https://github.com/username/repository.git my-folder
```

This downloads the entire repository, including all history and branches.

### SSH vs HTTPS

| | HTTPS | SSH |
|--|-------|-----|
| **URL format** | `https://github.com/user/repo.git` | `git@github.com:user/repo.git` |
| **Authentication** | Username + personal access token | SSH key pair |
| **Setup** | Easier (no key generation) | Requires one-time SSH key setup |
| **Security** | Secure | Secure |
| **Convenience** | May ask for credentials repeatedly | No password prompts after setup |
| **Recommendation** | Good for beginners | Preferred for daily use |

To set up SSH (optional, for later):

```bash
# Generate an SSH key
ssh-keygen -t ed25519 -C "your.email@example.com"

# Copy the public key and add it to GitHub Settings > SSH Keys
cat ~/.ssh/id_ed25519.pub
```

### Remote Commands Reference

| Command | What It Does |
|---------|-------------|
| `git remote add origin <url>` | Connect local repo to GitHub |
| `git remote -v` | View remote connections |
| `git push -u origin main` | Push to GitHub (first time) |
| `git push` | Push to GitHub (after first time) |
| `git pull` | Download and merge latest changes |
| `git clone <url>` | Download a repository |
| `git fetch` | Download changes without merging |

---

## 9. Collaboration on GitHub

### Forking a Repository

A **fork** is your personal copy of someone else's repository on GitHub. You can make changes to your fork without affecting the original project.

```
  Original Repo (owned by someone else)
  github.com/original-author/cool-project
           |
           |  [Fork button on GitHub]
           v
  Your Fork (your copy on GitHub)
  github.com/your-username/cool-project
           |
           |  git clone
           v
  Your Local Copy (on your computer)
  ~/projects/cool-project
```

**When to fork**: When you want to contribute to an open-source project you do not own.

### Pull Requests (PRs)

A **Pull Request** is a formal way to propose changes to a repository. It says: "I made these changes in my branch. Please review them and, if they look good, merge them into the main branch."

**How to create a Pull Request**:

1. Create a branch and make your changes.
2. Push the branch to GitHub.
3. On GitHub, click **Compare & pull request**.
4. Write a title and description explaining your changes.
5. Request reviewers.
6. Click **Create pull request**.

```
  Developer's Workflow:

  1. git switch -c feature/dark-mode
  2. (make changes)
  3. git add .
  4. git commit -m "feat: add dark mode toggle"
  5. git push -u origin feature/dark-mode
  6. Go to GitHub --> "Compare & pull request"
  7. Team reviews the code
  8. If approved --> Merge
  9. Delete the feature branch
```

### Code Review Process

When someone opens a pull request, team members review the code before it is merged.

Reviewers can:
- **Approve** — "This looks good, merge it."
- **Request changes** — "Please fix these issues first."
- **Comment** — "I have a question about this approach."

Code review catches bugs, enforces coding standards, and spreads knowledge across the team. In professional environments, code is **never** merged without at least one review.

### Issues — Tracking Bugs and Features

GitHub Issues are like a to-do list for your project. They help you track:

- **Bugs**: "Login button does not work on mobile."
- **Features**: "Add dark mode support."
- **Tasks**: "Set up CI/CD pipeline."

Each issue has:
- A title and description
- Labels (bug, enhancement, documentation)
- An assignee (who is responsible)
- A milestone (which release it belongs to)

### GitHub Pages — Free Hosting for Static Sites

GitHub Pages lets you host static websites (HTML, CSS, JavaScript) for free directly from a repository.

**How to enable GitHub Pages**:

1. Go to your repository on GitHub.
2. Click **Settings** > **Pages**.
3. Under **Source**, select the branch (usually `main`) and folder (`/root` or `/docs`).
4. Click **Save**.
5. Your site will be live at `https://yourusername.github.io/repository-name/`.

This is perfect for portfolio sites, project documentation, and course assignments.

---

## 10. Git Best Practices

### The Rules Every Developer Should Follow

#### 1. Commit Often with Clear Messages

```bash
# Bad: One giant commit after a full day of work
git commit -m "did stuff"

# Good: Small, focused commits throughout the day
git commit -m "feat: add email validation to signup form"
git commit -m "style: align form fields on mobile"
git commit -m "fix: prevent duplicate form submissions"
```

Small commits make it easy to find bugs. If something breaks, you only need to revert a small change, not an entire day of work.

#### 2. Never Commit node_modules or .env

```gitignore
# These MUST be in .gitignore before your first commit
node_modules/
.env
```

- `node_modules/` can contain hundreds of thousands of files. Anyone who clones your repo will run `npm install` to get them.
- `.env` contains secrets (API keys, database passwords). Committing them is a **security breach**.

#### 3. Use Branches for Features

Never work directly on `main`. Always create a branch.

```bash
# Good workflow
git switch -c feature/shopping-cart
# (work on the feature)
git commit -m "feat: add shopping cart component"
git push -u origin feature/shopping-cart
# (create a pull request on GitHub)
```

#### 4. Pull Before Push

Always pull the latest changes before pushing to avoid conflicts.

```bash
git pull origin main
# (resolve any conflicts if they arise)
git push origin main
```

#### 5. Review Before Merging

Never merge your own pull request without a review. A second pair of eyes catches mistakes you will not see yourself.

---

## 11. Common Git Workflow

### The Standard Development Workflow

```
  +-------+     +--------+     +------+     +-------+     +--------+
  | Clone | --> | Branch | --> | Code | --> | Stage | --> | Commit |
  +-------+     +--------+     +------+     +-------+     +--------+
                                                              |
                                                              v
  +-------+     +---------+     +------+                 +--------+
  | Merge | <-- | Pull    | <-- | Push | <-------------- |  Push  |
  +-------+     | Request |     +------+                 +--------+
                +---------+
```

### Step-by-Step Walkthrough

```bash
# 1. CLONE — Get the project
git clone https://github.com/team/project.git
cd project

# 2. BRANCH — Create a feature branch
git switch -c feature/user-profile

# 3. CODE — Make your changes
#    (edit files in your code editor)

# 4. STAGE — Prepare your changes
git add src/components/UserProfile.jsx
git add src/styles/profile.css

# 5. COMMIT — Save a snapshot
git commit -m "feat: add user profile page with avatar upload"

# 6. PUSH — Upload to GitHub
git push -u origin feature/user-profile

# 7. PULL REQUEST — Open a PR on GitHub
#    (done on the GitHub website)

# 8. MERGE — After review, merge into main
#    (done on the GitHub website or via command line)
```

### After Merging

```bash
# Switch back to main
git switch main

# Pull the merged changes
git pull origin main

# Delete the feature branch (cleanup)
git branch -d feature/user-profile

# Start working on the next feature
git switch -c feature/settings-page
```

---

## 12. Summary & Command Cheat Sheet

### What We Learned

In this week, we covered the entire Git and GitHub workflow:

- **Version control** saves your progress and enables collaboration.
- **Git** is the tool that tracks changes locally.
- **GitHub** is the platform that hosts your code in the cloud.
- The **three states** (Working Directory, Staging Area, Repository) are the foundation of Git.
- **Branches** let you work on features without affecting the main codebase.
- **Pull requests** are how teams review and merge code.
- **Best practices** keep your project clean and your team productive.

### Complete Command Cheat Sheet

#### Setup & Configuration

| Command | Description |
|---------|-------------|
| `git --version` | Check Git version |
| `git config --global user.name "Name"` | Set your name |
| `git config --global user.email "email"` | Set your email |
| `git config --list` | View configuration |

#### Creating & Cloning Repositories

| Command | Description |
|---------|-------------|
| `git init` | Initialize a new repository |
| `git clone <url>` | Clone a remote repository |

#### Basic Workflow

| Command | Description |
|---------|-------------|
| `git status` | Check file states |
| `git add <file>` | Stage a specific file |
| `git add .` | Stage all changes |
| `git commit -m "message"` | Commit staged changes |
| `git log --oneline` | View commit history |
| `git diff` | View unstaged changes |
| `git diff --staged` | View staged changes |

#### Branching & Merging

| Command | Description |
|---------|-------------|
| `git branch` | List all branches |
| `git branch <name>` | Create a new branch |
| `git switch <name>` | Switch to a branch |
| `git switch -c <name>` | Create and switch to a branch |
| `git merge <branch>` | Merge a branch into current branch |
| `git branch -d <name>` | Delete a branch |

#### Remote Repositories

| Command | Description |
|---------|-------------|
| `git remote add origin <url>` | Add a remote connection |
| `git remote -v` | View remote URLs |
| `git push -u origin main` | Push (first time) |
| `git push` | Push (subsequent) |
| `git pull` | Pull latest changes |
| `git fetch` | Fetch without merging |

#### Undoing Changes

| Command | Description |
|---------|-------------|
| `git restore <file>` | Discard changes in working directory |
| `git restore --staged <file>` | Unstage a file |
| `git revert <commit>` | Create a new commit that undoes a previous commit |
| `git log --oneline` | Find commit hashes to reference |

---

### Next Week Preview

In the coming weeks, we will move into the **backend** phase of the MERN stack. We will start with **Node.js** and **Express.js**, where you will build your first server and API. The Git and GitHub skills you learned this week will be used in every project from here on.

---

> **Practice Assignment**: Create a new GitHub repository, add an `index.html` file with a basic webpage,
> make at least 5 commits with proper commit messages, create a branch, make changes on the branch,
> merge it back into main, and push everything to GitHub. Then enable GitHub Pages to host your site.

---

*Week 13 of the MERN Stack Full Course — Version Control with Git & GitHub*
