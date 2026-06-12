# Hosting on GitHub Pages

**Live site:** https://davidthurmond-gif.github.io/berwick-a-reserve-4/

**Repo:** https://github.com/davidthurmond-gif/berwick-a-reserve-4 (public)

This site is plain HTML/CSS/JS (`index.html`, `style.css`, `script.js`, `data.js`), served as-is by GitHub Pages from the `main` branch root.

## Keeping it updated

The weekly scheduled task (`berwick-tennis-results-update`, Wednesdays 8am) now automatically commits and pushes updated `data.json`/`data.js` to GitHub after each run, so the live site stays current without any manual steps.

If you ever need to push a manual edit yourself:

```bash
cd "Saturday Comp - A Reserve 4"
git clone https://github.com/davidthurmond-gif/berwick-a-reserve-4.git /tmp/berwick-push
cp data.json data.js /tmp/berwick-push/
cd /tmp/berwick-push
git add data.json data.js
git commit -m "Update results"
git push https://davidthurmond-gif:<PAT>@github.com/davidthurmond-gif/berwick-a-reserve-4.git main
```

The PAT used for auto-push is stored in `.github-pat` in this project folder (gitignored, never pushed to the repo). It's a fine-grained token scoped only to this repo with Contents read/write.

## Notes

- `data.json` is the master file; `data.js` is generated from it (see README/script comments). Both are committed and pushed together so they stay in sync.
- Any in-browser edits (overrides, notes) are stored in each visitor's `localStorage` — they're per-device and won't sync between the site and the GitHub copy.
