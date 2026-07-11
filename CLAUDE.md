# Spelling Quest

A spelling practice game for Ava (age 8), SpongeBob themed, built as a single-file PWA. Inspired by Times Tables Quest. UK National Curriculum word lists (DfE English Appendix 1), three year-group tiers: Y1-2 common exception words, Y3-4 and Y5-6 statutory lists.

## Architecture — hard constraints

- **Everything lives in `index.html`.** No build step, no bundler, no separate JS/CSS files. Keep it that way.
- Word data is inlined as JS constants (sections marked `── YEARS 1–2 ──` etc. around lines 680–1000).
- Profiles and progress persist in `localStorage` under the key `spellingQuest.v1` (multiple profiles supported; each profile carries a `yearGroup` of `y12`/`y34`/`y56`).
- Audio is the Web Speech API (`speechSynthesis`), deliberately pitched high and fast. No audio files.
- A `<script type="module">` block at the bottom of the file connects to the **shared Firebase project `ava-rewards`** (same Firestore profile doc `profiles/ava` as Ava's Emerald Quest rewards app). Finishing a round with at least one correct answer calls `markSpellingPractice()`, which merges today's date into `spellingDays` so the rewards app grants an emerald and both apps show the practice streak. Reported once per day per device (`spq_lastReport` in localStorage). **Never overwrite that doc; always `setDoc(..., { merge: true })`.**

## Screens and features

Home (profile picker) → Hub (year tabs, focus words, streak) → game modes (Look/Cover/Write/Check, Hear & Spell, Lightning), Learning Aids (crossword, spelling rules), Word Sets grouped in 4 difficulty tiers of 25, printable word list, Progress Report with per-word status ticks.

## Testing and deploying

- Test by opening `index.html` directly or via any static server; it's fully client-side.
- Deployed via GitHub Pages from this repo. Pushing to `main` publishes.
- Verify on a phone-sized viewport too — Ava uses it on an iPad and iPhone.

## Wider context

This is one of James's family apps. Project memory lives in Notion: **Spelling App** page `37e350b8-f5ee-818f-ad05-d49ab56a17e5` (under Claude → Projects). Central cross-project memory: **memory.md** page `381350b8-f5ee-81da-8281-f7e85d31ace5`. If the Notion connector is available, read the project page at the start of substantive sessions and log significant decisions back to it.

Writing style for any user-facing text or docs: direct, concise, no filler (see writing-rules.md page `381350b8-f5ee-8170-aa66-e5e6d699e49f` in Notion).
