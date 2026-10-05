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
- Stages run from the most to the least common connectors (a rough everyday-frequency estimate), spreading competing words over different stages; the two C1 stages come last.
- Translation questions show a cue under the prompt (word class, what it points to, tone, nuance). Fill-in-the-blank hides the English meaning until you request the hint. In Mixed mode, sentence examples are varied within a game and across successive games. Twin words (e.g. als gevolg van / ten gevolge van) are both accepted.
- Progress, your own example sentences and any edited English meanings (Reference table → ✎ Edit meaning) are stored in the browser (localStorage) on each device.
- If you host several apps under the same `<username>.github.io`, they share browser storage; this app uses its own `dutch-connectives-*` keys, so they don't collide.

## Sentence scrambler

The trainer includes a **Sentence scrambler** mode. A saved Dutch example sentence is split into clickable word tiles and shuffled. Tap the words in the correct order, then check your answer. Clicking a word in the assembled sentence returns it to the word bank. The English meaning remains available as an optional hint.

Mixed mode **always includes at least one Sentence scrambler question** in every Mixed game; the remaining questions use the other exercise types for variety.


## v31 — bundled sentence translations and refresh stability

Sentence-scrambler translations are read from built-in app data (`sentenceTranslations`)
when present; the practice screen does not call an online translation service. The
translation layer is no longer stored separately in `localStorage`.

The service worker uses a versioned, cache-first app shell and caches `app.js` together
with `index.html`. This prevents refreshes from mixing files from different releases.
Bump `VERSION` in `sw.js` for each deployment.


- v31 bundles an English translation for every built-in Dutch example sentence directly in `EXPRESSIONS[].sentenceTranslations` (570 translations total).
- The Sentence Scrambler does not use an online translator or a separate translation `localStorage` database.
- The service worker cache is versioned as `v31-bundled-sentence-translations`; after deployment, refresh once to install the new cache.


## v34  rewritten sentence translations

All 570 bundled English sentence translations (`EXPRESSIONS[].sentenceTranslations`) were rewritten as natural English. The previous ones were word-by-word glosses that left Dutch words in the English text. The data is identical in `index.html` and `app.js`.
