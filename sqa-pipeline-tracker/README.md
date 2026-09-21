# SQA Pipeline Tracker (GitHub-backed)

A shared project tracker: you edit it, your team views a live, read-only
version that refreshes every 5 minutes. One single file serves both roles.

## What's in this folder
```
docs/index.html   -> the whole app (edit mode AND view mode, same file)
docs/data.json    -> the actual shared data (starts empty: [])
```

## One-time setup

### 1. Create a new GitHub repository
Same as before — create a new repo (private is fine).

### 2. Edit 3 lines in `docs/index.html` before uploading
Near the top of the `<script>` section, find:
```js
const REPO_OWNER = 'YOUR_GITHUB_USERNAME';
const REPO_NAME = 'YOUR_REPO_NAME';
const BRANCH = 'main';
```
Replace with your actual GitHub username and the repo name you just created.
Leave `BRANCH` as `'main'` unless your repo uses a different default branch name.

### 3. Upload both files
Upload `docs/index.html` and `docs/data.json` into your new repo, keeping
them inside a `docs` folder (same method as before — Codespaces, or typing
the full path `docs/index.html` when creating a new file on github.com).

### 4. Enable GitHub Pages
Repo → Settings → Pages → Source → select **"Deploy from a branch"** →
Branch: `main`, Folder: `/docs` → Save.

GitHub will give you a URL like:
```
https://your-username.github.io/your-repo-name/
```

### 5. Create your personal access key (one-time)
This is what lets *your* browser save changes. Nobody else needs this.

1. Go to github.com → click your profile picture (top right) → **Settings**
2. Scroll down the left sidebar to **Developer settings**
3. Click **Personal access tokens** → **Fine-grained tokens** → **Generate new token**
4. Give it a name like "SQA Tracker"
5. Under **Repository access**, choose **"Only select repositories"** and pick your new repo
6. Under **Permissions** → **Repository permissions** → find **Contents** → set to **Read and write**
7. Click **Generate token**, then **copy it immediately** (you won't be able to see it again)

## Using it

### To edit (you only)
1. Open `https://your-username.github.io/your-repo-name/`
2. Click **"🔑 Set access key"** in the top right, paste your token, press Enter
3. Add/edit projects as normal — every change saves straight to GitHub automatically
4. Your token is stored only in your own browser (in `localStorage`) — it is never
   uploaded anywhere or visible to anyone else

### To share with your team (view-only)
Give them this link instead:
```
https://your-username.github.io/your-repo-name/?mode=view
```
This version has no edit buttons, no access key prompt, and automatically
refreshes every 5 minutes to show your latest changes.

## Important notes
- **Never share your edit link (without `?mode=view`) publicly** — anyone who opens
  it and knows to click "Set access key" could technically add their own token
  and edit. Only share the `?mode=view` link with your team.
- Your access token is scoped to only this one repo, with only read/write on its
  contents — it cannot access your other repos or account settings.
- If you ever want to revoke access, delete the token from GitHub Settings →
  Developer settings → Personal access tokens.
