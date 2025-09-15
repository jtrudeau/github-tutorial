# Git Basics: Short Tutorial

This tiny repo helps absolute beginners practice the core Git flow: make a change locally and push it to a remote.

## What this is
- Practice project to learn the one workflow most people use every day with Git: change → commit → push.
- You will open a small notebook, run one cell so it produces output, save it, commit, then push to a fresh GitHub repo.
- No prior Git knowledge required. Minimal terminal commands. 

## Who it’s for
- Anyone who has never used Git or GitHub before.
- Works on macOS, Windows, and Linux. A terminal is used a little.
- Light Python/Jupyter usage only to create a visible change (a plot).

## What you’ll learn (concepts)
- “Repository (repo)”: a folder tracked by Git.
- “Commit”: a saved snapshot of your changes with a message.
- “Remote” and “origin”: a copy of your repo hosted on GitHub.
- “Branch” (optional step): a separate line of work you can merge later.

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

### Use SSH with GitHub
SSH preferred for pushing your changes:
- Generate a key: `ssh-keygen -t ed25519 -C "you@example.com"` (use the email you use on Github - the email you used to configure git. Press Enter for defaults)
- Start agent and add key:
  - macOS: `ssh-add --apple-use-keychain ~/.ssh/id_ed25519`
  - Linux/WSL/Windows Git Bash: `eval "$(ssh-agent -s)"; ssh-add ~/.ssh/id_ed25519`
- Copy the public key to clipboard:
  - macOS: `pbcopy < ~/.ssh/id_ed25519.pub`
  - Linux: `xclip -sel clip < ~/.ssh/id_ed25519.pub` (or `cat ~/.ssh/id_ed25519.pub` and copy)
  - Windows: `cat ~/.ssh/id_ed25519.pub` and copy
- Add it in GitHub: Settings → SSH and GPG keys → New SSH key → paste.

More information if needed here at [this link](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

## Clone this repo 

Test whether the ssh protocol works.

`git clone git@github.com:jtrudeau/github-tutorial.git `



## 2) Explore this repo
```
git status
```

## 3) Make a tiny change
Open `exercises/gaussian.ipynb`, run the single cell to generate the plot, then save the notebook.

Tips to open the notebook:
- With Jupyter: run `jupyter notebook` (or `jupyter lab`) and click the file.
- With VS Code: `code exercises/gaussian.ipynb` (requires the Python extension).

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
# EITHER use HTTPS (simple):
git remote add origin https://github.com/<your-username>/git-tutorial-practice.git
# OR use SSH (if you set up keys):
# git remote add origin git@github.com:<your-username>/git-tutorial-practice.git
```

## 6) Push to GitHub
```
git push -u origin main
```

That’s it! You’ve completed the most essential Git workflow.

### Optional next steps
- Option A: Make one more quick edit on `main`
  1) Open `README.md` and add a line at the end: `Completed by: <your name>`
  2) Save the file, then run:
     - `git add README.md`
     - `git commit -m "Add my name to README"`
     - `git push`

- Option B: Practice branch and merge (recommended)
  1) Create and switch to a new branch named `practice`:
     - `git switch -c practice`
  2) Make a small change (e.g., add a line to `README.md`: `Practice change by <your name>`), then save.
  3) Commit your change:
     - `git add README.md`
     - `git commit -m "Practice change on branch"`
  4) Go back to `main` and merge your branch:
     - `git switch main`
     - `git merge practice`
  5) Push the updated `main` to GitHub:
     - `git push`

If anything goes wrong, `git status` usually tells you what to do next.

## Troubleshooting (quick fixes)
- Git not installed / “command not found”
  - macOS: `xcode-select --install` or `brew install git`
  - Ubuntu/Debian: `sudo apt-get install git`
  - Windows: Install “Git for Windows” from the official site, then re-open your terminal.

- Authentication errors when pushing (e.g., publickey/permissions)
  - Use the HTTPS URL when adding `origin` (it starts with `https://`).
  - If you added the wrong URL, reset it:
    - `git remote set-url origin https://github.com/<you>/<repo>.git`

- Push rejected because the GitHub repo isn’t empty
  - Create the GitHub repo with no README/license. If you accidentally added files there, either recreate it empty or run `git pull --rebase` and resolve, then `git push`.

- `main` vs `master`
  - This tutorial uses `main`. If your default branch is `master`, either switch to `main` with `git branch -M main` or adapt commands accordingly.

- Can’t open the notebook
  - Install Jupyter: `pip install notebook` (or use VS Code with the Python extension) and try again.

- Undo an unstaged file change
  - `git restore --source=HEAD -- <file>` (e.g., `git restore --source=HEAD -- README.md`).

You did it if you can see your commit on GitHub under your repo’s “Commits” tab and the README/Notebook changes appear in the file list.
