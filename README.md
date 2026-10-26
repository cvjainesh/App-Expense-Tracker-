# Build Ledger — iPhone House Construction Expense Tracker

This package contains a local-first Progressive Web App (PWA) intended for GitHub Pages.

## Files
- `index.html` — tracker UI and app logic
- `manifest.webmanifest` — install metadata
- `sw.js` — caches the app shell for offline loading
- `icon-192.png`, `icon-512.png` — app icons

## Data and PIN
- Expense data is stored in the browser's IndexedDB on the device.
- The records are encrypted with AES-GCM; the key is derived from the 6-digit PIN using PBKDF2.
- The app does not send expense records to GitHub or any backend.
- The PIN is a local vault PIN, not a remote account. If it is forgotten and there is no CSV backup, the encrypted records cannot be recovered.
- The PIN screen is not a guarantee against a determined person with technical access to an unlocked device.
- Safari can remove website data. Export CSV backups regularly and keep them somewhere safe.
- The first-time setup attempts to migrate the original tracker key `houseConstructionExpenses_v1` from `localStorage`, encrypt it into IndexedDB, and removes the old plaintext key only after the encrypted vault has been saved.

## Publish to GitHub Pages
1. Create a GitHub repository, e.g. `house-construction-tracker`.
2. Upload the **contents** of this folder (not the folder itself) to the repository root.
3. Open repository **Settings → Pages**.
4. Under build/deployment, choose **Deploy from a branch**, select `main` and `/(root)`, then save.
5. Wait for GitHub Pages to publish. The URL usually looks like `https://YOUR-USERNAME.github.io/house-construction-tracker/`.
6. Open the published HTTPS URL in Safari on your iPhone. Wait for it to load once while online.
7. In Safari, tap **Share → Add to Home Screen**. If offered, enable **Open as Web App**, then tap Add.
8. Open the Home Screen icon, create your 6-digit PIN, and export a CSV backup after entering records.

## Offline and local-storage notes
- The service worker caches the app shell after the first successful online load. First installation/setup requires internet.
- IndexedDB is scoped to the website origin. Use the same GitHub Pages URL each time; a different URL is a separate database.
- The site files are public, but expense records are not stored in the repository.
- Do not use private details in descriptions. Keep backups protected.
- CSV import appends records and can create duplicates if the same backup is imported twice.

## Testing performed for this package
The package was generated and checked for required files and basic source markers. It has **not** been deployed to GitHub Pages or tested in Safari on a physical iPhone in this session. After publishing, verify setup, lock/unlock, add/delete, CSV export/import, and offline relaunch.
