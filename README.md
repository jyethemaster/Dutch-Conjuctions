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


## v35  bug fixes

- Editing sentences for the second *terwijl* (stage 3) saved them into the first *terwijl* (stage 1). The editor now remembers which entry it opened.
- Progress for the two *terwijl* entries is now tracked separately.
- The sentence scrambler now shows English translations you typed in the sentence editor (it only used the bundled ones before).
- The sentence editor no longer copies the bundled English into browser storage, so future translation fixes show up. A one-time clean-up removes copies of the old word-by-word translations that earlier saves left behind; translations you typed yourself are kept.
- Typed answers ignore case, extra spaces, trailing punctuation and how the gap in two-part expressions is typed (`zowel ... als`, `zowel...als`, `zowel als`).
- Multiple choice always shows four options, also when only 1-3 expressions are selected.
- Progress and sentence saves no longer break the answer flow if browser storage is unavailable.
- Removed `app.js`: it was an older, out-of-date copy of the script that `index.html` already contains inline, and was never loaded. The service worker no longer caches it.


## v36  lesson explanations in feedback, complete Reword set

- The explanation shown after each answer is now the word's lesson explanation (the text from its stage lesson), including any edits you saved in the app. The old generic text is only a fallback.
- Reword now has data for all 114 expressions (36 new rewrite pairs, mainly stages 6-10). Reword mode no longer falls back to fill-in-the-blank.
- Two Reword prompts no longer contain the target word: *of* and *tot*.
