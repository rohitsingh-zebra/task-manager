---
name: GitHub Sync Helper
description: Use this skill when the user asks to save, commit, push, or upload code to GitHub.
---

# Instructions

When asked to sync code to GitHub, execute the following steps in the terminal:
1.  Check the current git status (`git status`).
2.  If the repo is not initialized, run `git init` and ask the user for the remote repository URL to add it.
3.  Stage all changed files (`git add .`).
4.  Generate a concise, descriptive commit message based on the recent code changes.
5.  Commit the changes (`git commit -m "your message"`).
6.  Push to the main branch (`git push origin main` or `master`).
7.  If any errors occur, analyze the terminal output and fix them before proceeding.
