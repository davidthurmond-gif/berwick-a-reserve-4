# Berwick Saturday PM — Team Site

A simple static site for the Berwick Saturday PM team.

- **Current season (site root):** Summer 26/27 — Open Singles/Doubles **A Reserve 2** (trols section `AP020`, 7 teams + bye). Team: David Thurmond, Shannon Watson, John Keecherer, Tom Maloney, Soe. Season starts 10 Oct 26; finals 13 & 20 Mar 27.
- **Archive:** `winter-2026/` — Winter 2026, A Reserve 4 (`AP012`), final ladder and all results, frozen.

To archive a season: copy `index.html style.css script.js data.json data.js` into a new sub-folder, patch that copy's `saveNotesToGitHub()` paths to the sub-folder, add the archive banner, then rebuild the root `data.json` for the new section.

## What it shows
- **Dashboard** – next match, ladder snapshot, opponent form
- **Ladder** – calculated live from match results (points, sets, games, form)
- **Results** – round-by-round results for the whole section
- **Player Stats** – every player's win/loss record, sets, games, and singles/doubles breakdown, computed from rubber-by-rubber results across all 8 teams. Filter by team.
- **Roster** – Berwick player list with UTR profile links + editable projected UTR
- **Schedule** – full season fixture with venue info and results
- **Venues** – club addresses, Melway refs, contacts, editable court type
- **Opponent Scouting** – editable notes per opponent (age, hand, serve, strengths)

## Files
- `index.html` / `style.css` / `script.js` – the site
- `data.json` – master data (results, roster, schedule, clubs, opponent notes template)
- `data.js` – generated from `data.json` (loaded by the site as `window.SITE_DATA`)

If you ever edit `data.json` by hand, regenerate `data.js` with:
```bash
python3 -c "import json; d=json.load(open('data.json')); f=open('data.js','w'); f.write('window.SITE_DATA = '); json.dump(d,f,indent=2); f.write(';\n')"
```

## Editable notes (Roster UTR, Court Type, Opponent Scouting)
These are saved in your browser's local storage, so they persist between visits on the same browser/device. Use the **Export notes** button on the Opponent Scouting tab to download a backup JSON file, and **Import notes** to load it on another device or browser.

## Hosting on GitHub Pages
1. Create a new repo (e.g. `berwick-a-reserve-4`) and push these files to the `main` branch.
2. In the repo, go to **Settings → Pages**, set Source to `main` branch, root folder.
3. Your site will be live at `https://<your-username>.github.io/berwick-a-reserve-4/`.

## Weekly updates
A scheduled task ("berwick-tennis-results-update") runs every **Wednesday at 8am** and updates `data.json`/`data.js` with the previous weekend's results (scores are posted Tuesday nights). It uses Claude in Chrome to read:
https://www.trols.org.au/wdta/results.php?daytime=AP&section=AP020&style=

For each completed match it also clicks into the match-detail popup to capture per-rubber data (players, set scores, winners) for all teams in the section, which feeds the Player Stats tab.

After it runs, if you're using GitHub Pages, commit and push the updated `data.json`/`data.js` files to keep the live site in sync.

## Data shape: results / rubbers
Each match in `data.json` → `results[].matches[]` has the usual team totals (`homePts/homeR/homeS/homeG`, etc.) plus:
- `homePlayers` / `awayPlayers` – ordered player lists (position 1, 2, 3...) for that match
- `rubbers` – array of 3 entries (2 singles + 1 doubles), each with `homePlayers`/`awayPlayers` (resolved names), `sets` (array of `[homeGames, awayGames]`), `homeSets`/`awaySets`, `homeGames`/`awayGames`, `type`, and `winner` ("home"/"away")

The Player Stats tab aggregates these client-side - no extra data file needed.

## Still to do
- Opponent UTR ratings for opposing players haven't been looked up yet on utrsports.net. Opponent player names are now available via the Player Stats tab (pulled from match-detail data). Ask Claude to look up UTR ratings once Chrome is connected — they could go into the Opponent Scouting tab as a starting point.
x
