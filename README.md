# Property Fact Sheet Generator (PWA)

A single-page, installable web app for generating A4 property fact sheets
(Fact Sheet, Location, Site Photos) as print-ready PDFs. No backend, no
build step — everything runs in the browser.

## Files

```
index.html        The app itself (open this, or deploy it)
manifest.json      PWA manifest (name, icons, theme color)
sw.js               Service worker (offline caching)
icons/icon-192.png  App icon
icons/icon-512.png  App icon
```

## Deploy on GitHub Pages

1. Create a new GitHub repository.
2. Add these files to the repository root (keep the `icons/` folder
   structure intact):
   ```
   git init
   git add .
   git commit -m "Property fact sheet generator PWA"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git push -u origin main
   ```
3. In the repo, go to **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**.
5. Set **Branch** to `main` and folder to `/ (root)`, then **Save**.
6. After a minute, your app will be live at:
   ```
   https://<your-username>.github.io/<repo-name>/
   ```
7. On mobile Chrome/Safari you'll see an "Add to Home Screen" / "Install"
   option, turning it into an app icon that opens full-screen.

## Updating the app later

Push changes to `main` and GitHub Pages redeploys automatically. The
service worker now uses a **network-first** strategy for the app shell,
so returning visitors always get your latest deployed version when
they're online — it only falls back to the cached copy when offline.
(An earlier build of this service worker used cache-first, which could
show a stale version until the cache was manually cleared; that's fixed
as of `fact-sheet-generator-v2`.)

## What's included in this build

Narrower sidebar, colour-coded collapsible sections (all collapsed by
default), listing code under Branding, flexible key-specification rows
(text/land area/built-up area with sub-notes/tenure/ceiling height),
auto psf calculation shown to one decimal place, For Sale/For Rent
pricing display ("RM {figure} /month" for rentals), an optional Special
Features & Highlights section (fully hidden when empty), location map
upload with legend + description banner, landscape/portrait-aware site
photo pagination with enlarged checkmarks, a page-selection dialog for
printing only chosen pages, and "Save as (json)" / "Load it" using the
File System Access API on Chrome/Edge — pick a file once and future
saves write straight back to it, with a download/upload fallback on
other browsers.

## Notes

- All data lives only in the browser tab's memory while you work —
  nothing is uploaded anywhere. Use **Save as (json)** to keep a record
  you can reload later via **Load it**.
- Requires `https://` (e.g. the GitHub Pages URL) for the linked-file
  save/load and offline caching to work — opening the file directly via
  `file://` will fall back to plain download/upload instead.
