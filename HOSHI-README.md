# Hoshi

Your private anime and manga tracker. No accounts, no servers, nothing sold or shared.

## Files in the repo

Root: `index.html`, `manifest.json`, `sw.js`, `icon-180.png`, `icon-192.png`, `icon-512.png`, `robots.txt`, `.nojekyll`, `README.md`
Folders: `data/news.json`, `scripts/fetch_news.py`, `.github/workflows/update-news.yml`

On a phone you can't upload folders. Use Add file > Create new file, type the full path as the file name (for example `scripts/fetch_news.py`), paste the contents, and commit. GitHub creates the folders for you. Images (the three icons) go in with Add file > Upload files.

## Turn on live data (do this once)

1. Settings > Pages > Deploy from branch > `main` / root.
2. Actions tab > "I understand my workflows, enable them" if asked.
3. Actions > Update news > Run workflow. Wait a minute. A green tick means `data/news.json` now has real headlines. After that it runs by itself every hour.
4. Open the run and read its log. Each source prints a line like `Anime News Network: 25 items`. A line starting FAILED means that one site did not answer; the rest still work. Tell me which one failed and I will swap it.
5. Reload the app. News fills in and the header shows how fresh it is.

What is live:
- News: public feeds, fetched hourly by the Action (a browser cannot read these directly). Cards show headline, source and a short excerpt, then link to the original.
- Add title: searches AniList live, with real covers. Anime and manga both work.
- Calendar: currently airing popular anime with next-episode countdowns, upcoming premieres and films, and your own series marked. Manga chapter dates are not published anywhere reliable, so that tab lists what you are reading instead.
- Voices: type a name and suggestions appear from AniList. Following one loads their roles and birthday, refreshed daily. Heard hours count only episodes you marked sub or dub.

## Data, privacy and security

The code is public, your data is not in it. Your library, ratings, notes and settings live only in your phone's browser storage (keys start `hoshi-`). Anyone who downloads the repo gets a blank app. The app only contacts AniList (for search, covers, calendar and voices) and your own site (for `data/news.json`).

- Turn on two-factor authentication on GitHub. Whoever controls the account controls the site.
- Add the site to your Home Screen from Safari. It becomes a full-screen app and Safari stops clearing its storage after a week unused.
- Padlock button: optional 6-digit passcode, encrypted backups with your own passphrase, and safety snapshots that are taken before every update and before big deletions.
- A new web address starts empty, so if you used the app somewhere else first, back up there and restore here.

## Upgrading with Claude

1. Padlock > Back up (use a passphrase). Save it in Notes.
2. Give Claude `index.html`. Do not send the backup.
3. Replace `index.html` in the repo with the new one. Same address means your data stays. If anything looks off, restore the backup or a snapshot.

Rules for any upgrade: never rename or delete `hoshi-*` storage keys, only add new ones, and bump `HOSHI_VER`.

## Storage keys

Yours: `hoshi-lib3` (library), `hoshi-vas` (voice actors), `hoshi-nc` (new casting), `hoshi-theme`, `hoshi-welcome`, `hoshi-lastbk`.
Never in backups: `hoshi-lock`, `hoshi-snaps`, `hoshi-snapt`, `hoshi-ver`, and caches starting `hx-`.

## If news stops

GitHub pauses scheduled workflows on repos that go quiet. The Action commits every hour, which normally keeps it active. If the header says news is old, open Actions, enable the workflow if it shows as disabled, and press Run workflow.
