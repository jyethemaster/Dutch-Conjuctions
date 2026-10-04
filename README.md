# Dutch Connectives Trainer

Practise Dutch connectives and linking words (B1–C1): omdat, daarom, doordat, voordat and more.
Installable web app (PWA) hosted on GitHub Pages, works offline once opened.

## Put it online (GitHub Pages)
1. Create a new repository on GitHub (e.g. `dutch-connectives`).
2. Upload all files from this folder to the **root** of the repository (`index.html`, `manifest.json`, `sw.js` and the three `icon-*.png`).
3. Go to **Settings → Pages**, choose **Deploy from a branch**, branch `main`, folder `/ (root)`, and save.
4. After a minute your app is live at `https://<your-username>.github.io/<repository-name>/`.
5. On your phone open that link in Chrome and choose **Add to Home screen** / **Install app**.

## Update the app
Replace `index.html`, then bump `VERSION` in `sw.js` (e.g. `v2`) so phones pick up the change.

## Notes
- Progress, your own example sentences and any edited English meanings (Reference table → ✎ Edit meaning) are stored in the browser (localStorage) on each device.
- If you host several apps under the same `<username>.github.io`, they share browser storage; this app uses its own `dutch-connectives-*` keys, so they don't collide.
