# Week 13: Git & GitHub - Practice Questions

**Total Questions: 51 | Practical Exercises: 8**

---

## Section A: Multiple Choice Questions (MCQs)

**15 Questions**

---

**Q1. What is Git?**

- A) A programming language
- B) A distributed version control system
- C) A web hosting platform
- D) A text editor

<details>
<summary>Answer</summary>

**B) A distributed version control system**

Git is a free and open-source distributed version control system designed to track changes in source code during software development.

</details>

---

**Q2. What is the difference between Git and GitHub?**

- A) They are the same tool
- B) Git is a version control system; GitHub is a cloud-based hosting platform for Git repositories
- C) GitHub is a version control system; Git is a cloud-based hosting platform
- D) Git is only available on Linux; GitHub works on all platforms

<details>
<summary>Answer</summary>

**B) Git is a version control system; GitHub is a cloud-based hosting platform for Git repositories**

Git is the version control tool that runs locally on your machine. GitHub is a web-based platform that hosts Git repositories and provides collaboration features like pull requests, issues, and project management.

</details>

---

**Q3. Which command is used to initialize a new Git repository?**

- A) `git start`
- B) `git create`
- C) `git init`
- D) `git new`

<details>
<summary>Answer</summary>

**C) `git init`**

The `git init` command creates a new `.git` subdirectory in your project folder, which initializes a new Git repository.

</details>

---

**Q4. What does the `git add` command do?**

- A) Creates a new file in the repository
- B) Moves files to the staging area (index)
- C) Pushes changes to the remote repository
- D) Deletes files from the repository

<details>
<summary>Answer</summary>

**B) Moves files to the staging area (index)**

The `git add` command adds changes from the working directory to the staging area, preparing them to be included in the next commit.

</details>

---

**Q5. Which command saves the staged changes with a message?**

- A) `git save -m "message"`
- B) `git push -m "message"`
- C) `git commit -m "message"`
- D) `git store -m "message"`

<details>
<summary>Answer</summary>

**C) `git commit -m "message"`**

The `git commit` command records the staged snapshot to the project history. The `-m` flag allows you to include a commit message inline.

</details>

---

**Q6. What does `git push` do?**

- A) Downloads changes from a remote repository
- B) Uploads local repository content to a remote repository
- C) Creates a new branch
- D) Merges two branches together

<details>
<summary>Answer</summary>

**B) Uploads local repository content to a remote repository**

The `git push` command sends your committed changes from your local repository to a remote repository (e.g., on GitHub).

</details>

---

**Q7. Which command is used to download a remote repository to your local machine?**

- A) `git pull`
- B) `git fetch`
- C) `git clone`
- D) `git download`

<details>
<summary>Answer</summary>

**C) `git clone`**

The `git clone` command creates a local copy of a remote repository, including all files, branches, and commit history.

</details>

---

**Q8. What is the staging area in Git?**

- A) The remote server where code is stored
- B) An intermediate area where changes are prepared before committing
- C) The final version of the code
- D) A backup of the repository

<details>
<summary>Answer</summary>

**B) An intermediate area where changes are prepared before committing**

The staging area (also called the index) is a space between the working directory and the repository where you can selectively prepare changes for the next commit.

</details>

---

**Q9. What is a branch in Git?**

- A) A copy of the entire repository on a different computer
- B) A lightweight movable pointer to a specific commit, allowing parallel development
- C) A backup of the main code
- D) A type of merge conflict

<details>
<summary>Answer</summary>

**B) A lightweight movable pointer to a specific commit, allowing parallel development**

A branch represents an independent line of development. It allows you to work on features, fixes, or experiments in isolation without affecting the main codebase.

</details>

---

**Q10. What happens during a `git merge`?**

- A) It deletes one of the branches
- B) It combines changes from one branch into another
- C) It creates a new repository
- D) It reverts all changes to the initial commit

<details>
<summary>Answer</summary>

**B) It combines changes from one branch into another**

The `git merge` command integrates changes from one branch into the current branch, combining the commit histories.

</details>

---

**Q11. What is the purpose of a `.gitignore` file?**

- A) To list all files that should be committed
- B) To specify files and directories that Git should not track
- C) To store Git configuration settings
- D) To log all Git errors

<details>
<summary>Answer</summary>

**B) To specify files and directories that Git should not track**

The `.gitignore` file tells Git which files or folders to ignore and not track. Common entries include `node_modules/`, `.env`, and build output directories.

</details>

---

**Q12. What does the `git status` command display?**

- A) The commit history of the repository
- B) The current state of the working directory and staging area
- C) The list of remote repositories
- D) The contents of the `.gitignore` file

<details>
<summary>Answer</summary>

**B) The current state of the working directory and staging area**

The `git status` command shows which changes have been staged, which have not, and which files are not being tracked by Git.

</details>

---

**Q13. What does `git log` show?**

- A) A list of all branches
- B) The commit history of the repository
- C) The list of staged files
- D) The remote repository URL

<details>
<summary>Answer</summary>

**B) The commit history of the repository**

The `git log` command displays the chronological list of commits made in the repository, including commit hashes, authors, dates, and messages.

</details>

---

**Q14. What is the difference between forking and cloning a repository?**

- A) They are exactly the same operation
- B) Forking creates a copy on your GitHub account; cloning creates a copy on your local machine
- C) Cloning creates a copy on your GitHub account; forking creates a copy on your local machine
- D) Forking deletes the original repository

<details>
<summary>Answer</summary>

**B) Forking creates a copy on your GitHub account; cloning creates a copy on your local machine**

Forking creates a server-side copy of a repository under your own GitHub account, allowing you to freely experiment. Cloning downloads a repository to your local machine for development.

</details>

---

**Q15. What does the `git diff` command do?**

- A) Merges two branches
- B) Shows the differences between files in the working directory, staging area, or between commits
- C) Creates a new branch
- D) Deletes uncommitted changes

<details>
<summary>Answer</summary>

**B) Shows the differences between files in the working directory, staging area, or between commits**

The `git diff` command displays line-by-line differences between file versions, helping you see what has changed before staging or committing.

</details>

---

## Section B: Short Answer Questions

**8 Questions**

---

**Q1. What is version control and why is it important in software development?**

<details>
<summary>Answer</summary>

Version control is a system that records changes to files over time so that you can recall specific versions later. It is important because it:

- **Tracks history:** Maintains a complete record of every change made to the codebase.
- **Enables collaboration:** Allows multiple developers to work on the same project simultaneously without overwriting each other's work.
- **Provides backup and recovery:** Lets you revert to previous versions if something goes wrong.
- **Supports branching and experimentation:** Allows developers to create isolated branches for new features or bug fixes without affecting the main code.
- **Improves accountability:** Every change is attributed to a specific developer with a timestamp and message.

</details>

---

**Q2. Explain the difference between Git and GitHub.**

<details>
<summary>Answer</summary>

**Git** is a distributed version control system that runs locally on your computer. It tracks changes to files, manages commit history, and allows branching and merging. Git works entirely offline and does not require an internet connection.

**GitHub** is a cloud-based hosting platform built on top of Git. It provides a web interface for managing Git repositories and adds collaboration features such as:

- Pull requests for code review
- Issues for bug tracking
- GitHub Actions for CI/CD
- GitHub Pages for hosting static websites
- Social features like starring and forking repositories

In short, Git is the tool; GitHub is a service that hosts Git repositories and facilitates team collaboration.

</details>

---

**Q3. What are the three states (areas) in Git, and what is the role of each?**

<details>
<summary>Answer</summary>

Git has three main states that files can reside in:

1. **Working Directory (Modified):** This is the project folder on your local machine where you actively edit files. Changes here are not yet tracked by Git until you stage them.

2. **Staging Area / Index (Staged):** This is an intermediate area where you prepare changes before committing them. Files are moved here using `git add`. It allows you to selectively choose which changes to include in the next commit.

3. **Repository / .git Directory (Committed):** This is the Git database where committed snapshots are permanently stored. When you run `git commit`, the staged changes are saved to the repository with a unique hash, message, and metadata.

The typical workflow is: modify files in the working directory, stage selected changes with `git add`, and then save them permanently with `git commit`.

</details>

---

**Q4. What is a branch in Git and why is branching useful?**

<details>
<summary>Answer</summary>

A **branch** in Git is a lightweight, movable pointer to a specific commit. It represents an independent line of development that diverges from the main codebase.

Branching is useful because it:

- **Enables parallel development:** Multiple team members can work on different features simultaneously without interfering with each other.
- **Isolates changes:** New features or bug fixes can be developed in isolation, keeping the main branch stable and deployable.
- **Supports experimentation:** Developers can try new ideas on a separate branch and discard them if they do not work out.
- **Facilitates code review:** Feature branches can be reviewed through pull requests before merging into the main branch.
- **Simplifies release management:** Teams can maintain separate branches for development, staging, and production.

Common branching strategies include feature branches, release branches, and hotfix branches.

</details>

---

**Q5. What is a merge conflict and how do you resolve it?**

<details>
<summary>Answer</summary>

A **merge conflict** occurs when Git cannot automatically combine changes from two branches because both branches have modified the same lines of the same file in different ways.

When a conflict occurs, Git marks the conflicting sections in the file with special markers:

```
<<<<<<< HEAD
Your changes on the current branch
=======
Changes from the branch being merged
>>>>>>> feature-branch
```

**Steps to resolve a merge conflict:**

1. Open the conflicted file and locate the conflict markers.
2. Decide which changes to keep (yours, theirs, or a combination of both).
3. Remove the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).
4. Save the file.
5. Stage the resolved file with `git add <filename>`.
6. Complete the merge with `git commit`.

</details>

---

**Q6. What is a pull request and why is it important?**

<details>
<summary>Answer</summary>

A **pull request** (PR) is a feature provided by platforms like GitHub that lets a developer notify team members that they have completed a feature or fix on a branch and would like it to be reviewed and merged into another branch (usually `main`).

Pull requests are important because they:

- **Enable code review:** Team members can review the proposed changes, leave comments, suggest improvements, and catch bugs before the code is merged.
- **Provide discussion space:** PRs serve as a forum for discussing the implementation approach and design decisions.
- **Maintain code quality:** By requiring approvals before merging, PRs help enforce coding standards and best practices.
- **Document changes:** Each PR creates a record of what was changed, why, and who reviewed it.
- **Support CI/CD integration:** Automated tests and checks can run on the PR before merging to ensure nothing is broken.

</details>

---

**Q7. What types of files should typically be listed in a `.gitignore` file?**

<details>
<summary>Answer</summary>

A `.gitignore` file should include files and directories that should not be tracked by Git. Common entries include:

- **Dependencies:** `node_modules/` (installed packages should be reinstalled via `package.json`)
- **Environment variables:** `.env`, `.env.local` (contain sensitive information like API keys and passwords)
- **Build output:** `dist/`, `build/`, `.next/` (generated files that can be recreated)
- **IDE/Editor files:** `.vscode/`, `.idea/`, `*.swp` (personal editor settings)
- **Operating system files:** `.DS_Store` (macOS), `Thumbs.db` (Windows)
- **Log files:** `*.log`, `npm-debug.log*`
- **Coverage reports:** `coverage/`
- **Compiled files:** `*.min.js`, `*.map`

The key principle is to ignore any file that is generated, contains sensitive data, or is specific to an individual developer's environment.

</details>

---

**Q8. What is forking a repository and when would you use it?**

<details>
<summary>Answer</summary>

**Forking** is the process of creating a personal copy of someone else's repository on your own GitHub account. The forked repository is completely independent, so changes made to your fork do not affect the original repository.

You would use forking when:

- **Contributing to open source:** Fork the project, make your changes, and submit a pull request to the original repository.
- **Experimenting with existing code:** You want to try out modifications without affecting the original project.
- **Using a project as a starting point:** You want to build upon someone else's work for your own project.
- **Learning from others' code:** Fork a repository to study, modify, and experiment with the code in your own space.

**Forking workflow:**
1. Fork the repository on GitHub.
2. Clone your fork to your local machine.
3. Create a new branch for your changes.
4. Make and commit your changes.
5. Push the branch to your fork on GitHub.
6. Open a pull request from your fork to the original repository.

</details>

---

## Section C: True or False

**10 Questions**

| No. | Statement | Answer |
|-----|-----------|--------|
| 1 | Git and GitHub are the same thing. | **False.** Git is a version control system; GitHub is a hosting platform for Git repositories. |
| 2 | The `git init` command creates a new `.git` directory in your project folder. | **True.** This hidden directory contains all the metadata and object database for the repository. |
| 3 | You must stage files with `git add` before you can commit them. | **True.** Git requires files to be in the staging area before they can be included in a commit. |
| 4 | The `git pull` command uploads your local changes to the remote repository. | **False.** `git pull` downloads and integrates changes from the remote repository. `git push` uploads local changes. |
| 5 | A `.gitignore` file can only be placed in the root directory of a repository. | **False.** You can place `.gitignore` files in any directory of the repository, and they apply to that directory and its subdirectories. |
| 6 | Once a file is committed, it can never be changed or removed from the Git history. | **False.** Git provides commands like `git revert`, `git reset`, and `git rebase` that can modify commit history, although rewriting shared history is generally discouraged. |
| 7 | The `main` branch is automatically created when you initialize a new Git repository. | **True.** By default, Git creates a `main` (or `master` in older versions) branch when you run `git init`. |
| 8 | Cloning a repository also copies the entire commit history. | **True.** The `git clone` command downloads the complete repository, including all branches and the full commit history. |
| 9 | A merge conflict occurs every time two branches are merged. | **False.** Merge conflicts only occur when both branches have modified the same lines in the same file. If changes are in different files or different parts of the same file, Git merges them automatically. |
| 10 | You need a GitHub account to use Git on your local machine. | **False.** Git is a standalone tool that works entirely on your local machine. A GitHub account is only needed to use GitHub's hosting and collaboration features. |

---

## Section D: Command Matching

**10 Questions**

Match each Git command in **Column A** with its correct description in **Column B**.

| No. | Column A (Command) | Column B (Description) |
|-----|---------------------|------------------------|
| 1 | `git init` | A. Show the commit history |
| 2 | `git clone <url>` | B. Display the current state of the working directory and staging area |
| 3 | `git add .` | C. Upload local commits to the remote repository |
| 4 | `git commit -m "message"` | D. Create a new local copy of a remote repository |
| 5 | `git push` | E. Initialize a new Git repository |
| 6 | `git pull` | F. Show differences between file versions |
| 7 | `git status` | G. Stage all changes in the current directory for the next commit |
| 8 | `git log` | H. Create a new branch |
| 9 | `git branch <name>` | I. Save staged changes to the repository with a message |
| 10 | `git diff` | J. Download and integrate changes from the remote repository |

<details>
<summary>Answers</summary>

| No. | Command | Answer | Description |
|-----|---------|--------|-------------|
| 1 | `git init` | **E** | Initialize a new Git repository |
| 2 | `git clone <url>` | **D** | Create a new local copy of a remote repository |
| 3 | `git add .` | **G** | Stage all changes in the current directory for the next commit |
| 4 | `git commit -m "message"` | **I** | Save staged changes to the repository with a message |
| 5 | `git push` | **C** | Upload local commits to the remote repository |
| 6 | `git pull` | **J** | Download and integrate changes from the remote repository |
| 7 | `git status` | **B** | Display the current state of the working directory and staging area |
| 8 | `git log` | **A** | Show the commit history |
| 9 | `git branch <name>` | **H** | Create a new branch |
| 10 | `git diff` | **F** | Show differences between file versions |

</details>

---

## Section E: Practical Exercises

**8 Tasks**

---

### Task 1: Initialize a New Git Repository and Make Your First Commit

**Objective:** Learn the basic Git workflow from initialization to committing changes.

**Instructions:**

1. Create a new project folder called `my-first-repo`.
2. Open a terminal and navigate to the folder.
3. Initialize a new Git repository using `git init`.
4. Create a file called `index.html` with a basic HTML boilerplate.
5. Check the repository status using `git status`.
6. Stage the file using `git add index.html`.
7. Commit the file with the message `"Initial commit: add index.html"`.
8. Verify the commit using `git log`.

<details>
<summary>Expected Commands</summary>

```bash
mkdir my-first-repo
cd my-first-repo
git init
# Create index.html with your editor
git status
git add index.html
git commit -m "Initial commit: add index.html"
git log
```

</details>

---

### Task 2: Create a `.gitignore` File with Common Entries

**Objective:** Learn how to prevent unnecessary or sensitive files from being tracked by Git.

**Instructions:**

1. In an existing Git repository, create a `.gitignore` file.
2. Add the following entries to the file:
   - `node_modules/`
   - `.env`
   - `dist/`
   - `.DS_Store`
   - `*.log`
   - `.vscode/`
3. Create a `node_modules/` folder and a `.env` file with dummy content.
4. Run `git status` and verify that the ignored files do not appear in the output.
5. Stage and commit the `.gitignore` file.

<details>
<summary>Expected Commands</summary>

```bash
# Create the .gitignore file with the entries listed above
# Create test files/folders
mkdir node_modules
echo "SECRET_KEY=abc123" > .env
git status
# Verify that node_modules/ and .env are NOT listed
git add .gitignore
git commit -m "Add .gitignore file"
```

</details>

---

### Task 3: Create a New Branch, Make Changes, and Merge It Back

**Objective:** Practice the branching and merging workflow.

**Instructions:**

1. Ensure you are on the `main` branch.
2. Create a new branch called `feature-navbar`.
3. Switch to the new branch.
4. Create or modify a file (e.g., add a navigation bar to `index.html`).
5. Stage and commit the changes with an appropriate message.
6. Switch back to the `main` branch.
7. Merge the `feature-navbar` branch into `main`.
8. Verify the merge was successful by checking the file contents and commit log.
9. (Optional) Delete the `feature-navbar` branch after merging.

<details>
<summary>Expected Commands</summary>

```bash
git branch
git checkout -b feature-navbar
# Make changes to index.html
git add index.html
git commit -m "Add navigation bar to index.html"
git checkout main
git merge feature-navbar
git log --oneline
git branch -d feature-navbar
```

</details>

---

### Task 4: Create a GitHub Repository and Push Your Local Code

**Objective:** Learn how to connect a local repository to GitHub and push your code.

**Instructions:**

1. Go to [github.com](https://github.com) and create a new repository (e.g., `my-first-repo`).
2. Do **not** initialize it with a README, `.gitignore`, or license (to avoid conflicts).
3. In your local repository, add the GitHub repository as a remote.
4. Verify the remote was added correctly.
5. Push your local `main` branch to GitHub.
6. Refresh the GitHub page and verify your files appear.

<details>
<summary>Expected Commands</summary>

```bash
git remote add origin https://github.com/YOUR-USERNAME/my-first-repo.git
git remote -v
git branch -M main
git push -u origin main
```

</details>

---

### Task 5: Clone a Public Repository and Explore Its History

**Objective:** Practice cloning repositories and using `git log` to explore commit history.

**Instructions:**

1. Find a public repository on GitHub (e.g., a small open-source project).
2. Clone it to your local machine.
3. Navigate into the cloned repository.
4. Use `git log` to view the commit history.
5. Use `git log --oneline` for a condensed view.
6. Use `git log --oneline --graph` to see the branch structure visually.
7. Use `git diff <commit-hash-1> <commit-hash-2>` to compare two commits.
8. Use `git show <commit-hash>` to view the details of a specific commit.

<details>
<summary>Expected Commands</summary>

```bash
git clone https://github.com/username/repository-name.git
cd repository-name
git log
git log --oneline
git log --oneline --graph
git diff abc1234 def5678
git show abc1234
```

</details>

---

### Task 6: Simulate a Merge Conflict and Resolve It

**Objective:** Understand how merge conflicts occur and practice resolving them.

**Instructions:**

1. Create a new Git repository and add a file called `about.txt` with some initial content.
2. Commit the file on the `main` branch.
3. Create and switch to a new branch called `branch-a`.
4. Modify line 1 of `about.txt` and commit the change.
5. Switch back to `main`.
6. Modify the same line 1 of `about.txt` with different content and commit.
7. Attempt to merge `branch-a` into `main`. A merge conflict should occur.
8. Open `about.txt`, locate the conflict markers, and resolve the conflict.
9. Stage the resolved file and complete the merge commit.

<details>
<summary>Expected Commands</summary>

```bash
mkdir conflict-demo && cd conflict-demo
git init
echo "Hello World" > about.txt
git add about.txt
git commit -m "Initial commit"

git checkout -b branch-a
echo "Hello from Branch A" > about.txt
git add about.txt
git commit -m "Update about.txt from branch-a"

git checkout main
echo "Hello from Main Branch" > about.txt
git add about.txt
git commit -m "Update about.txt from main"

git merge branch-a
# Conflict occurs - open about.txt and resolve manually
# Remove conflict markers and keep desired content
git add about.txt
git commit -m "Resolve merge conflict in about.txt"
```

</details>

---

### Task 7: Create a GitHub Pages Site from a Repository

**Objective:** Deploy a simple static website using GitHub Pages.

**Instructions:**

1. Create a new GitHub repository (e.g., `my-portfolio`).
2. Clone it to your local machine.
3. Create an `index.html` file with a simple portfolio page (include your name, a heading, and a short introduction).
4. Optionally, add a `style.css` file for basic styling.
5. Commit and push your changes to GitHub.
6. Go to the repository on GitHub, navigate to **Settings > Pages**.
7. Under "Source," select the `main` branch and click **Save**.
8. Wait a few minutes and visit your live site at `https://YOUR-USERNAME.github.io/my-portfolio/`.

<details>
<summary>Expected Commands</summary>

```bash
git clone https://github.com/YOUR-USERNAME/my-portfolio.git
cd my-portfolio
# Create index.html and style.css
git add index.html style.css
git commit -m "Add portfolio page with styling"
git push origin main
# Then configure GitHub Pages in the repository Settings
```

</details>

---

### Task 8: Fork a Repository, Make Changes, and Create a Pull Request

**Objective:** Learn the open-source contribution workflow using fork and pull request.

**Instructions:**

1. Find a public repository on GitHub (or use a classmate's repository).
2. Click the **Fork** button to create a copy under your GitHub account.
3. Clone your forked repository to your local machine.
4. Create a new branch called `my-contribution`.
5. Make a meaningful change (e.g., fix a typo, add documentation, or improve code).
6. Stage and commit your changes with a descriptive message.
7. Push the branch to your forked repository on GitHub.
8. Go to the original repository on GitHub and click **"New Pull Request"**.
9. Select your fork and branch as the source, write a clear PR description, and submit.

<details>
<summary>Expected Commands</summary>

```bash
git clone https://github.com/YOUR-USERNAME/forked-repo.git
cd forked-repo
git checkout -b my-contribution
# Make your changes
git add .
git commit -m "Add contribution: improve documentation"
git push origin my-contribution
# Then go to GitHub and create a Pull Request from the browser
```

</details>

---

**End of Practice Questions - Week 13: Git & GitHub**
