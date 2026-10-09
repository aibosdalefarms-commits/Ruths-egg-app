# Egg App

Daily egg collection and weekly sales for our backyard flock. It's a PWA on Firebase, used by Nate and Ruth on their Android phones. Version 1.2.

**Live app:** https://ruths-egg-app.web.app (Firebase project `ruths-egg-app`, owned by Ruth)

## What it does

- **Who's this?**: pick Nate or Ruth once per phone. It's remembered until you tap **Switch user**, and every entry is stamped with that name.
- **Record tab**: today's egg total with a Nate/Ruth breakout and the lay rate (eggs ÷ hens). Use the **+1 / +6 / +12 / +42** buttons (42 = a full tray) and **Undo last**.
  - Tap the total (✏️) to set it directly. Lowering it takes eggs off whoever logged more that day; raising it adds them for whoever is using the phone. Both are saved as corrections.
  - **Last 7 days** chart with this week's total. The day shown is gold, and tapping a bar jumps to that day.
  - The **‹ ›** arrows beside the date step back to past days, so missed collections can be added with the same buttons.
  - A past day shows in egg-brown, with a **Today** pill beside the date to jump back.
  - The app always returns to today when it's reopened or comes back from the background.
- **Sales tab**: last week and this week, in dozens and dollars. Weeks run Sunday to Saturday.
  - **Customers**: one row per price with **+6** (half dozen) and **+12** (dozen). Tap a row's count to correct this week's total for that price.
  - **Farm**: free eggs sent to the family farm, with **+6 / +12 / +42**. Tap the total to correct it. Farm eggs aren't counted in dollars.
- **Menu** (tap your name at the top right):
  - **History**: one card per day (today and yesterday first, then **Load more** for 7 more days) showing eggs collected, dozens sold with dollars, and dozens to the farm. Tap a day to set its totals; the differences are saved as corrections. Empty days are listed too, so a missed day can be filled in.
  - **Export**: CSV for a date range.
  - **Flock**: total eggs since the flock start date, the start date itself, and the current number of hens with − / + buttons. Each size change is saved with its date, so past days keep the right lay rate.
  - **Prices**: the price list shown on the Customers tab.
  - **Switch user**

## How the data works

Every tap saves one small entry instead of overwriting a total, so both phones can tap at the same time without losing anything. Totals are added up from the entries.

| Collection | Contents |
|---|---|
| `entries` | `type` (`collected` / `sold` / `farm`), `eggs` (whole eggs: +6 = half dozen), `price` (per dozen, sales only), `user`, `date` (YYYY-MM-DD), `createdAt`, optional `adjust: true` for corrections |
| `settings/main` | `prices`: the price list. `flockStart`: YYYY-MM-DD. `flockLog`: `[{ date, size }]`, the flock size from each date on. |

A correction (setting a new total anywhere in the app) saves the difference as an entry marked `adjust`, so the data shows exactly what changed. The individual entries can be seen in the CSV export.

## Tech stack

- **Frontend:** single-file vanilla HTML/CSS/JS ([index.html](index.html)) with no build step, the same approach as Bosdale Receipts
- **Auth:** Firebase anonymous sign-in, done silently in the background. There are no passwords. The database only answers requests from the app.
- **Database:** Cloud Firestore (region `northamerica-northeast2`, Toronto)
- **Hosting:** Firebase Hosting
- **Offline:** service worker ([sw.js](sw.js)). Network-first for the app, cache-first for icons, fonts and libraries. Firestore's offline cache keeps recent data on the phone, so the app opens to the last numbers before the server answers.

## Deploying changes

```bash
firebase deploy
```

Bump `CACHE_NAME` in [sw.js](sw.js) and the version label in [index.html](index.html) with each release so installed apps pick up the update.

## Key files

| File | Purpose |
|---|---|
| `index.html` | The entire app (UI + logic) |
| `sw.js` | Service worker |
| `manifest.json` | PWA install manifest |
| `icon-*.png`, `apple-touch-icon.png`, `favicon-48.png` | App icons (original artwork in `branding/`) |
| `firestore.rules` | Database security rules |
| `firebase.json` | Hosting, rules and emulator config |
| `SETUP-GUIDE.md` | First-time Firebase setup and installing on the phones |
| `docs/testing.md` | Testing on this computer with the private test copy |
| `tools/serve.js` | Tiny local web server for testing |

Notes (`*.md`), `docs/`, `branding/` and `tools/` are not published to the website.

## Changing the people

The names are in two places and must match: `USERS` near the top of the script in `index.html`, and `d.user in [...]` in `firestore.rules`.
