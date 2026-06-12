# Hosting on GitHub Pages

This site is plain HTML/CSS/JS (`index.html`, `style.css`, `script.js`, `data.js`), so GitHub Pages can serve it as-is — no build step needed.

## 1. Create the repo

1. On GitHub, create a new repository (e.g. `berwick-tennis`). Public is fine — GitHub Pages is free for public repos (private repos need a paid plan for Pages).
2. Don't initialize with a README (this folder already has one).

## 2. Push this folder

From this project folder:

```bash
cd "Saturday Comp - A Reserve 4"
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/<your-username>/berwick-tennis.git
git push -u origin main
```

## 3. Turn on Pages

1. In the repo, go to **Settings → Pages**.
2. Under "Build and deployment", set **Source** to "Deploy from a branch".
3. Set **Branch** to `main` and folder to `/ (root)`.
4. Save.

After a minute or two, the site will be live at:

```
https://<your-username>.github.io/berwick-tennis/
```

## 4. Keeping it updated

The weekly scheduled task updates `data.json`/`data.js` in this local folder, but GitHub Pages serves whatever is in the GitHub repo — those are separate copies. After each weekly update, you'll need to push the changes:

```bash
cd "Saturday Comp - A Reserve 4"
git add data.json data.js
git commit -m "Update results"
git push
```

If you'd like, the scheduled task can be extended to also commit and push automatically — just let me know and I can set that up (it would need a GitHub personal access token stored securely).

## Notes

- `data.json` is the master file; `data.js` is generated from it (see README/script comments). Make sure both are committed and pushed together so they stay in sync.
- Any in-browser edits (overrides, notes) are stored in each visitor's `localStorage` — they're per-device and won't sync between the site and your local copy.
