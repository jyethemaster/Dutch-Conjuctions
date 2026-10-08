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

## v37  Reword model answers corrected
- Fixed 27 Reword exercises whose model answer did not match the sentence shown. For example *bovendien* showed a two-sentence prompt but the model answer was a single sentence that dropped the second half; *hierdoor* reversed cause and effect; *zolang*, *anderzijds*, *enerzijds*, *daarnaast* and the second *terwijl* entry had model answers that kept the wrong part or belonged to a different sentence.
- Each model answer now keeps the full meaning of the original sentence and uses the target expression. Prompts still never contain the target expression.
- Only the Reword data changed; nothing else in the app.


## v39  two practice tools (is / was / had, and position verbs)

Both tools live inside `index.html` (no extra files) and share one engine, so they behave the same way. Open them from the two buttons at the bottom of the main screen. Each has its own screens, sentences, progress and "Ik ken dit al" marks (`dutch-aux-*` and `dutch-pos-*` in browser storage), so the connectives game is untouched.

**Is / was / had** (114 sentences, 6 stages): zijn/hebben in the present, perfect, past, pluperfect, unreal conditions and modal perfects, passive.

**Staan / liggen / zitten / hangen / zetten / leggen / stoppen** (187 sentences, 8 stages):
1. Which verb fits the thing (upright, flat, hanging, sitting or attached)
2. Plural subjects and ik / jij / wij
3. Put it there: zetten, leggen, hangen, stoppen
4. State or action: the same noun with staan vs zetten, liggen vs leggen
5. Past tense
6. Perfect tense (gelegen vs gelegd, gezeten vs gezet)
7. Fixed expressions (het staat je goed, het ligt aan jou, het zit me niet mee)

Exercise types in both: choose the word, type the word, build the sentence (short sentences only), find the mistake, mixed.


## v42 navigation fix
- Keeps the auxiliary/position launcher elements hidden on the Conjunctions page so the main topic chooser can still open those tools without showing cross-links.
- Fixes the standalone tool Home buttons to return to the main topic landing page.
- Restores the original v40 tool initialization path; only navigation behavior is changed.


## v45  position verbs: talking about people and yourself

- New stage 8 in the position-verb practice, "People and yourself" (29 sentences). It covers: zijn for where a person is (ik ben in de stad), places lie (Utrecht ligt in het midden), set phrases where the position verb is the normal choice (in de rij staan, in de trein zitten, in bed liggen, in de gevangenis zitten), staan / zitten / liggen / lopen + te + infinitive (ik sta te koken), getting into a position with gaan (ga zitten), and informal zitten (ik zit in de problemen, we zitten zonder koffie).
- The position-verb guide has a new section, "Talking about people and yourself", with an English-to-Dutch table.
- Stage 8 is added at the end, so saved progress for stages 1-7 is unchanged.
