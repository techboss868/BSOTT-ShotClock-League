# Billiards Shot Clock & Scorecard — PWA

This folder is a ready-to-deploy Progressive Web App. Once it's hosted on an
HTTPS URL, anyone can open the link on a phone and "Add to Home Screen" to get
a fullscreen, offline-capable app — no app store required.

## What's in here

- `index.html` — the app (shot clock, scorecard, settings) with PWA wiring added
- `manifest.json` — app name, icons, colors, standalone display
- `sw.js` — service worker that caches the app so it runs offline
- `icons/` — app icons (192, 512, 512 maskable, 180 Apple touch icon)

## Important: PWAs need HTTPS

Service workers (offline + installability) only work over `https://` or on
`localhost`. Opening `index.html` by double-clicking it (a `file://` path) will
show the app but **not** the install prompt or offline mode. Use one of the
options below.

## Deploy options (easiest first)

### 1. Netlify Drop — no account math, ~1 minute
1. Go to https://app.netlify.com/drop
2. Drag this entire `Billiards PWA` folder onto the page.
3. You get a public `https://...netlify.app` link. Open it on your phone.

### 2. GitHub Pages — free, permanent URL
1. Create a repo and upload the contents of this folder.
2. Settings → Pages → deploy from the `main` branch, root folder.
3. Your app is served at `https://<username>.github.io/<repo>/`.
   (Paths are relative, so it works fine in a subfolder like this.)

### 3. Test locally first
From inside this folder run a local server, then open the URL it prints:

```
python3 -m http.server 8080
```

Then visit `http://localhost:8080` (localhost counts as secure, so install and
offline work here too).

## Installing on a phone

- **Android (Chrome):** open the link → menu (⋮) → "Install app" / "Add to Home screen".
- **iPhone (Safari):** open the link → Share button → "Add to Home Screen".

After installing, launch it once while online so the service worker caches
everything; from then on it works with no connection.

## Updating the app later

Edit `index.html`, then bump `CACHE_VERSION` in `sw.js` (e.g. `billiards-v1`
→ `billiards-v2`) and re-deploy. The version bump tells installed devices to
fetch the new files instead of serving the old cached ones.

## Notes for your app specifically

- Your saved match (teams, players, scores, settings, theme) is stored on the
  device and persists across launches.
- Voice announcements use the browser's speech engine; some phones require one
  tap/interaction before they'll play audio.
- The CSV export downloads a file — this works in the browser. If you later wrap
  this in a native shell (e.g. Capacitor), switch it to a share/save plugin.
