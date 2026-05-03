# 💳 My Wallet + 🔐 Family Vault

Two personal PWA apps for storing cards, documents and important numbers — fully offline, no account required, installable on Android and desktop Chrome.

---

## Apps

### 💳 My Wallet (`index.html`)

A digital wallet for all your loyalty cards, membership cards, shopping cards and coupons.

**Features**
- Upload any card as a photo or screenshot with a pan/zoom crop editor
- Swipe left/right to flip through cards
- Home screen carousel with card thumbnails for quick navigation
- Optional logo per card — shown in the header when viewing
- Edit card name, replace card image or logo at any time
- Offline-first — everything stored locally in the browser

---

### 🔐 Family Vault (`vault.html`)

A secure document and number vault for the whole family. Stores passports, IDs, driving licences, vehicle registrations, and important numbers like IBANs and registration plates.

**Features**
- PIN lock screen on every open — 4-digit PIN, set on first launch
- Up to 6 family members, each with their own documents
- Swipe left/right between people on the home screen
- Per-person photo avatar with circle crop editor
- Documents shown fully expanded — scan at full size, all fields with one-tap copy
- National number displayed and auto-formatted per person
- Front + back scan support — swipe the scan to flip sides
- Belgian registration plate rendered as a real plate visual
- IBAN displayed with spacing, copied without spaces
- Numbers: swipe left to delete, tap left to edit, tap right panel to copy
- Expiry tracking — amber warning on home screen when any document expires within 90 days
- Synology WebDAV sync — reads and writes a shared file on your NAS automatically
- Export / import as `.json` backup (export requires PIN confirmation)
- Android back gesture navigates up one level instead of exiting
- Fully offline after first load

---

## Installation

Both apps are single HTML files — no build step, no dependencies, no server.

### Host on GitHub Pages

1. Create a new GitHub repository
2. Upload `index.html` and/or `vault.html` to the root
3. Go to **Settings → Pages → Deploy from branch → main → / (root)**
4. Your apps are live at:
   - `https://yourusername.github.io/yourrepo/` — Wallet
   - `https://yourusername.github.io/yourrepo/vault.html` — Vault

### Install as PWA on Android (Chrome)

1. Open the URL in Chrome
2. Tap the **⋮ menu → Add to Home Screen** or **Install App**
3. The app opens full-screen with no browser chrome

### Install as PWA on Mac (Chrome)

1. Open the URL in Chrome
2. Click the **install icon** in the address bar (or Chrome menu → Install)
3. The app appears in your Dock and runs as a standalone window

### Open locally (no hosting needed)

Simply open either HTML file directly in Chrome. Both apps work fully offline from a local file.

---

## Synology WebDAV Sync (Vault only)

The Vault app can sync data automatically between Android and Mac via a file on your Synology NAS.

**Requirements**
- Synology NAS with WebDAV enabled
- QuickConnect or direct URL access

**Setup**
1. On your Synology: go to **Control Panel → File Services → WebDAV** and enable it
2. Open Vault → **⚙️ Settings → WebDAV sync**
3. Enter your NAS URL (e.g. `https://yourname.quickconnect.to:5006`), username and password
4. Tap **Test & Connect** — the app creates a `FamilyVault/` folder on your NAS automatically
5. Every save now pushes to the NAS; every app open pulls the latest version

**How sync works**
- `localStorage` is always the primary storage — the app works instantly, offline, without network
- WebDAV is a sync layer on top — if the NAS is unreachable, the app continues normally
- On app open, if the NAS has a newer version it is pulled automatically
- The PIN is stored only in `localStorage` on each device — never synced

---

## Privacy & Security

- **No data leaves your device** except via the optional WebDAV sync you configure
- **No account, no cloud service, no analytics**
- All document scans, numbers and personal data are stored in browser `localStorage`
- Export files are unencrypted plain JSON — store them securely (e.g. in an encrypted folder)
- The Vault PIN is a practical access barrier, not encryption — do not store the export file on a shared device

---

## File structure

```
index.html    — My Wallet PWA
vault.html    — Family Vault PWA
README.md     — This file
```

No other files needed.

---

## Browser support

| Browser | Wallet | Vault | PWA install | WebDAV sync |
|---|---|---|---|---|
| Android Chrome | ✅ | ✅ | ✅ | ✅ |
| Mac Chrome | ✅ | ✅ | ✅ | ✅ |
| Mac Safari | ✅ | ✅ | ✅ (Add to Dock) | ✅ |
| iPhone Safari | ✅ | ✅ | ✅ (Add to Home) | ⚠️ Limited |

> WebDAV sync on iPhone Safari has limited support due to iOS restrictions on background fetch.

---

## Built with

- Vanilla HTML, CSS, JavaScript — zero frameworks, zero dependencies
- [Plus Jakarta Sans](https://fonts.google.com/specimen/Plus+Jakarta+Sans) (Google Fonts)
- Canvas API for pan/zoom image cropping
- File System / Clipboard API for copy and export
- Service Worker for offline caching
- History API for Android back gesture navigation
