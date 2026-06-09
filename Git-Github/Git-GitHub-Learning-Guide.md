# Git and GitHub Learning Guide

A beginner-friendly guide by Naresh Sajwani.  
This document explains Git and GitHub concepts step by step, following a logical flow.

---

## 1. What is Git?

**Git** is a **Version Control System** (VCS).  
It tracks changes in your code/files over time. You can go back to any previous version, see who changed what, and work with others without overwriting each other's work.

Think of it as a **smart save button** with history.

---

## 2. What is GitHub?

**GitHub** is a website (hosting service) that stores your Git repositories on the internet.  
It allows you to:
- Share your code with others
- Collaborate with teammates
- Showcase your projects

Git ≠ GitHub. Git is the tool, GitHub is the online platform.

---

## 3. Difference between Git and GitHub

| Feature           | Git                                      | GitHub                                      |
|-------------------|------------------------------------------|---------------------------------------------|
| Type              | Tool / Software                          | Website / Hosting Service                   |
| Where it runs     | On your laptop                           | On the internet (cloud)                     |
| Purpose           | Track changes locally                    | Store, share, and collaborate remotely      |
| Needs internet?   | No                                       | Yes (to push/pull)                          |

---

## 4. What is HEAD?

**HEAD** is a pointer that tells you **which branch and commit** you are currently on.  
It usually points to the latest commit of your current branch.

---

## 5. What is Branch and Commit?

- **Commit**: A snapshot of your changes. Every time you do `git commit`, you save a version of your project.
- **Branch**: A separate line of development. You can work on new features without affecting the main code.

Default branch is usually `master` or `main`.

---

## 6. Uses of Git / GitHub

- Track code changes
- Work on features safely using branches
- Collaborate with others
- Review code (Pull Requests)
- Backup your project
- Build portfolio / open source contributions

---

## 7. What is Merge?

**Merge** combines changes from one branch into another.  
It brings the work done in a feature branch back to the main branch.

---

## 8. Fast Forward Merge vs Merge Commit

- **Fast Forward Merge**: Happens when there are no new commits on the target branch. Git simply moves the pointer forward. (Clean history)
- **Merge Commit**: Happens when both branches have new commits. Git creates a new commit that combines both histories.

---

## 9. What is Rebase?

**Rebase** moves your branch commits on top of the latest commits from another branch.  
It makes the history look linear and clean.

---

## 10. Difference between Merge and Rebase

| Feature           | Merge                                   | Rebase                                      |
|-------------------|-----------------------------------------|---------------------------------------------|
| History           | Creates merge commit                    | Keeps linear history                        |
| Use Case          | Safe for public branches                | Good for cleaning feature branches          |
| Risk              | Safer                                   | Can be dangerous if not used carefully      |

---

## 11. What is Squash Commit?

Squash combines multiple small commits into **one clean commit**.  
Useful before merging a feature branch.

---

## 12. git clone vs git fork

- **`git clone`**: Downloads a copy of the repository to your laptop.
- **`git fork`**: Creates your own copy of someone else's repository on GitHub (under your account).

---

## 13. How to check history of a file?

```bash
git log --oneline filename.txt
git log -p filename.txt        # Shows changes

Your Practiced Commands with Explanation
Prepare Folder
Bash
mkdir Naresh
cd Naresh
touch first.txt second.txt
echo "first" > first.txt
echo "second" > second.txt
Initialize Git
Bashgit init
git status
Add Files
Bashgit add first.txt
git add second.txt
git status
Set User Info (Important before commit)
Bashgit config --global user.email "naresh.sajwani1612@gmail.com"
git config --global user.name "Naresh Sajwani"
git config --list
First Commit
Bashgit commit -m "Commit-1"
git status
git log --oneline --graph --all
Create & Work on Branches
Bashgit branch
echo `date` >> first.txt
git add first.txt
git commit -m "Commit-2"
git log --oneline --graph --all

# Create new branch
git checkout -b NewBranch
echo "third" > third.txt
git add third.txt
git commit -m "Commit-3"
Merging
Bashgit checkout master
git merge feature/tablespace-monitoring
git log --oneline --graph --all

git merge feature/ansible-automation
git log --oneline --graph --all

Understanding Clone, Fetch & Origin (Very Important)
git clone

Downloads the entire repository.
Creates only one local branch (master/main).
All other branches exist on the server.

origin

origin is just a nickname for the GitHub repository URL.
Every cloned folder has its own origin.
Check it using: git remote -v

git fetch vs git fetch --all

git fetch → Updates information of all branches from origin (the GitHub repo you cloned).
git fetch --all → Updates information from all remotes (useful only if you have multiple remotes like origin + upstream).

In your case (single remote), both commands do the same thing.
Useful Commands
Bashgit branch -a          # See all branches (local + remote)
git checkout <branch>  # Switch to any branch
git fetch              # Get latest updates from GitHub
