# Overload — Workout Tracker

A minimal, personal workout tracker. Build your own programs with multiple
training days (e.g. a Push/Pull/Legs split), assign them to a weekly
schedule, log sets during a workout, and get automatic weight/rep
progression suggestions and PR alerts. Everything is stored locally in your
browser — no account, no server, no data leaves your device.

## Files

- `index.html` — the entire app (HTML/CSS/JS, self-contained)
- `manifest.json` — PWA manifest so it can be installed as a standalone app
- `service-worker.js` — enables offline use and controls update caching
- `icons/` — app icons used for the home screen

## Run it locally

Just open `index.html` in a browser — no build step, no dependencies.
For the service worker to register (needed for the "Add to Home Screen"
install prompt and offline support), it needs to be served over `http(s)`
rather than opened as a bare `file://` path. Any static file server works,
e.g. from this folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploy with GitHub Pages (free, gives you a real installable app)

1. Push this repo to GitHub (see commands below).
2. On GitHub, go to **Settings → Pages**.
3. Under **Source**, choose the `main` branch and `/ (root)` folder, then
   save.
4. GitHub will give you a URL like
   `https://<your-username>.github.io/<repo-name>/`. It can take a minute
   to go live.

### Push this folder to a new GitHub repo

```bash
cd overload-repo
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

(Create the empty repo on GitHub first — github.com → New repository —
then use its URL in the `git remote add` command above.)

## Install it on your iPhone as a real app

Once it's live on GitHub Pages:

1. Open the GitHub Pages URL in **Safari** (must be Safari, not another
   browser or an in-app browser).
2. Tap the **Share** button → **Add to Home Screen**.
3. Because this is a proper PWA (manifest + icons + service worker), Safari
   will use the app's own icon automatically, open full-screen with no
   browser bar, and keep working offline — no Shortcuts workaround needed.

## Updating

Whenever you push a change and it's live on GitHub Pages, the service
worker fetches the latest version the next time you have a connection and
open the app. If you ever want to force every device to drop old cached
files, bump the `CACHE_NAME` version string at the top of
`service-worker.js` (e.g. `overload-cache-v1` → `v2`) and push again.

## About a "real" App Store app

Turning this into a native iOS app you'd download from the App Store is a
different path — it needs Xcode on a Mac, an Apple Developer account
($99/year), and a tool like Capacitor to wrap this same HTML/CSS/JS as a
native shell. That's outside what can be built and shipped from here, but
the PWA setup above gets you the same practical result on your iPhone: a
home-screen icon, full-screen standalone window, offline support, and all
data kept locally — without any of that cost or tooling.
