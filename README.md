# Git Basics: The Simplest Tutorial

Welcome! This tiny repo helps absolute beginners practice the core Git flow: make a change locally and push it to a remote.

## What you’ll do
- Configure Git with your name and email.
- Make a small local change (run and save a notebook).
- Commit your change.
- Create a new GitHub repository and push to it.

## Prerequisites
- Git installed (macOS: `xcode-select --install` or `brew install git`; Ubuntu: `sudo apt-get install git`).
- A GitHub account.
- Python with Jupyter (e.g., `pip install notebook matplotlib numpy`), or use VS Code with the Python extension.

## 1) Configure Git (once per machine)
```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

## 2) Explore this repo
```
git status
git log --oneline --decorate --graph --all
```

## 3) Make a tiny change
Open `exercises/gaussian.ipynb` in Jupyter or VS Code, run the single cell to generate the plot, then save the notebook. Saving will record the output inside the file.

## 4) Commit your change
```
git add exercises/gaussian.ipynb
git commit -m "Run Gaussian notebook and save output"
```

## 5) Create a GitHub repo and set `origin`
- In GitHub, click “New repository”. Name it something like `git-tutorial-practice` and keep it empty (no README, no license).
- Copy the repo URL (HTTPS is simplest).
- Back in your terminal, run:
```
git branch -M main
git remote add origin https://github.com/<your-username>/git-tutorial-practice.git
```

## 6) Push to GitHub
```
git push -u origin main
```

That’s it! You’ve completed the most essential Git workflow.

### Optional next steps
- Make another tiny edit to `README.md` (add your name), commit, and `git push` again.
- Create a new branch, make a change, merge it:
```
git switch -c practice
# make a small change
git add -A && git commit -m "Practice change"
git switch main
git merge practice
git push
```

If anything goes wrong, `git status` usually tells you what to do next.
