# Ledger — PWA setup

This folder is a complete installable Progressive Web App.

## Why this beats a WebView APK right now
A WebView APK needs Android Studio, the Android SDK/build tools, and a signing
key to produce an installable `.apk` — none of which are available in this
environment, and getting them working reliably usually means installing
~1–2 GB of tooling on your own machine. A PWA gets you the same result —
an offline, home-screen app with its own icon — using only the files below,
installable on Android, iOS, and desktop, with no build step at all.

## Important: PWAs must be served over HTTPS (or localhost) to install
Browsers only allow "Install app" and offline service workers on secure
origins. Opening `index.html` directly via `file://` (like before) still
works as a webpage, but Chrome/Android will **not** show the install prompt
or cache it for offline use from a `file://` path.

**Easiest free hosting options (pick one):**
- **GitHub Pages** — push this folder to a repo, enable Pages, done.
- **Netlify Drop** — go to app.netlify.com/drop and drag this folder in; get a live HTTPS URL in seconds.
- **Vercel** — `vercel deploy` from this folder.

Once it's live at an HTTPS URL:

1. Open that URL in Chrome on Android.
2. Tap **⤓ Install app** (top right) or the browser's own "Add to Home
   screen" / "Install app" menu option.
3. Launch it from the home screen icon from then on — it runs fully
   offline, with your data saved on-device via local storage.

## Files
- `index.html` — the app itself
- `manifest.json` — name, icons, colors, standalone display mode
- `sw.js` — service worker; caches all app files on first load so it works with no connection afterward
- `icons/` — 192px, 512px, and a maskable 512px icon

## Later: a real Android APK
If you do want a true `.apk` (for the Play Store, or install without a
browser at all), the standard path is Android Studio's WebView template:
create a project with a single `WebView` pointed at `file:///android_asset/index.html`,
copy this folder into `app/src/main/assets/`, and build. I can generate the
full Android Studio project source for you to build on your own machine if
you'd like — just ask.
