# flex-combos — project memory

Hub of the six published Flex Combos builds from Claude Design project
`7a99d38c-bfa5-4d85-badf-f16fdabeb1ca`, taken from Jim's local
`~/Downloads/publish` export (NOT via DesignSync — see below).

- Hub:  https://jimpawa.github.io/flex-combos/
- Repo: `jimpawa/flex-combos`, branch `main`, Pages from `/` on main
- Folder: `/Users/jimtsipoutas/Claude_Projects/flex-combos/`

## Six folders = four prototypes

Two independent variables:
- rail layout — `__COMBO_LAYOUT` `"one"` (single carousel) vs `"rails"` (Popular + Flex split)
- wording     — `__WORD_MODE` `"lose"` ("2 picks can lose and you still win") vs
                `"ratio"` ("1 or more picks have to win")

**NAMING (Jim, 2026-09-02):** the second wording option is called **"Win framing"** in all
display text — never "Ratio framing". But the published folder names stay `one-rail-ratio` /
`two-rails-ratio` and the flag stays `__WORD_MODE="ratio"`: those URLs are already shared and the
flag is baked into the 2.6 MB bundles. Display name != folder name, deliberately.

| # | URL | layout | wording |
|---|-----|--------|---------|
| 1 | /one-rail/  (≡ /one-rail-lose/)   | one   | lose  |
| 2 | /one-rail-ratio/                  | one   | ratio |
| 3 | /two-rails/ (≡ /two-rails-lose/)  | rails | lose  |
| 4 | /two-rails-ratio/                 | rails | ratio |

`one-rail` ≡ `one-rail-lose` and `two-rails` ≡ `two-rails-lose` are true duplicates: identical
flags, identical decoded app code (all six share resource fingerprint `1c6b4d61b415`), differing
only in `<title>` and a per-publish random resource UUID. All six URLs published for link
stability.

Rendered proof: one-rail shows 1 combo rail / 5 cards; two-rails shows 2 rails / 10 cards.

## THE IMPORTANT GOTCHA — publish bundles are incomplete

Each 2.59 MB bundle inlines only **16 resources: JS + the 4 Roboto fonts**. It does NOT inline
`app/sprite.svg` or `uploads/*.jpg`, yet the page still fetches them at runtime on relative
paths. Hosted anywhere outside the Claude Design runtime that means:

- `app/sprite.svg` 404s → all **106** `<use href="#pIcon-…">` refs resolve to nothing →
  **zero icons**, and GitHub's 404 HTML gets injected into `#sprite-host`
- `uploads/*.jpg` 404s → every casino game tile falls back to a placeholder

Fix applied: the 140-symbol sprite and the six thumbnails are committed into **each** variant
folder at `<variant>/app/sprite.svg` and `<variant>/uploads/`. Repo is ~41 MB as a result.
**Any future publish export needs the same treatment** — check for these 404s first.

## Verified 2026-09-02 (live URLs, Chromium 402x874)

All six: 140 sprite symbols, icons painting, 6/6 game images HTTP 200 (`naturalWidth` 400,
inside the image-slot shadow root — a `.gtile img` selector cannot see them), 0 unexpected 404s.
The `.image-slots.state.json` 404 is expected and harmless.

## Test script — /test-questions/

https://jimpawa.github.io/flex-combos/test-questions/ (linked from the hub)

**Structure = 2x2.** Primary tabs = wording (`"2 picks can lose"` / `"1 of 3 must win"`).
Sub-tabs = rail layout (`One Rail` / `Two Rails`). Four cells, three questions each.
Deep-link any cell with `#<wording>-<layout>`, e.g. `#win-two`. Variant blocks are shown/hidden
by body classes `w-lose|w-win` and `l-one|l-two`; answer key toggles with `hide-answers`.
`#ratio-*` is still accepted as an alias for `#win-*` so links shared before the rename resolve.

Each cell carries a `.proto` strip above Q1 — **the whole strip is one `<a>`**, since Jim asked
(2026-09-02) that it be obvious this is the link to the build. It shows a teal
"Prototype to test — tap to open" kicker, the folder name + alias, the printed URL, the
per-cell explanation, and an "Open prototype ↗" button (a `<span>`, not a nested `<a>`).
Opens in a new tab. Keep it to this strip — not the verbose grey box that was removed earlier.

**Two CSS traps in that strip, both already hit once:**
1. Do NOT put `display` on `a.proto`. `a.proto` is (0,1,1) and outranks `.v { display:none }`
   at (0,1,0), which made all four cells' strips render at once. `display:flex` must come only
   from the `body.l-*.w-*` combo rules at (0,3,1).
2. Its parts are `<span>`s (they live inside an anchor, so they cannot be `<div>`s) and each
   structural one needs `display:block`, or name / alias / URL / description collapse into a
   single inline wrapped line.

- **Q1 = the LAYOUT question** (Regular vs Flex). Stem changes per layout, options identical in
  all four cells so the layouts stay comparable.
- **Q2 = payout.** Constant everywhere. Real ladder on screen: No Flex 4.68 / Flex 2/3 2.34 /
  Flex 1/3 1.35. Trap = "it is higher, Flex is an extra feature".
- **Q3 = the WORDING question.** Identical stem/options/answer in both wording tabs; only the
  quoted sentence changes, which is what makes the cells subtractable. Trap = "2 of the 3".

Jim wants this page **questions-only**. Removed on his instruction: strings table, draft-wording
corrections, mapping table, rationale blocks, and (2026-09-02) the per-layout grey context box
including the "Prototype: one-rail · alias ..." links that lived inside it. Page is now
header -> wording tabs -> layout sub-tabs -> Q1/Q2/Q3. Do not reintroduce explanatory blocks.
The per-layout screen facts are recorded below for question-writing, NOT for display on the page.

### What each layout actually puts on screen (verified live)

**one-rail** — ONE "Popular Combos" row, 5 cards ALTERNATING:
positions 1/3/5 are flexed (`Flex 1/3` 1.35, `Flex 2/3` 1.48, `Flex 2/3` 1.76, each with an
explainer line); positions 2/4 are regular, price only (1.78, 2.51). **Nothing labels the two
kinds** — the participant must spot the difference. That is the whole point of this cell.

**two-rails** — TWO rows: "Popular Combos" (CirlceInfo icon) = 5 regular cards, price only;
"Flex Combos" (ShieldCheck icon) = 5 flexed cards. Same fixtures in both rows at different
prices, e.g. FC Salzburg 1.95 regular vs 1.35 at `Flex 1/3`.

### Exact on-screen strings, card fx-2 (FC Salzburg v Pafos FC, 3 picks)

| control  | price | loss framing                          | win framing                  |
|----------|-------|---------------------------------------|------------------------------|
| No Flex  | 4.68  | (NO sentence shown at all)            | (NO sentence shown at all)   |
| Flex 2/3 | 2.34  | "1 pick can lose and you still win."  | "2 or more picks have to win"|
| Flex 1/3 | 1.35  | "2 picks can lose and you still win." | "1 or more picks have to win"|

**Core insight behind Q3:** in loss framing the sentence's number is the COMPLEMENT of the pill's
numerator — "2 picks can lose" sits next to `Flex 1/3`, two different numbers on one card. In
win framing they match.

### Question-accuracy audit (2026-09-02) — verified with DOM geometry, not by eye

Card anatomy, measured: the **explainer sentence sits ABOVE the Flex button** (top 861 vs 899px),
and the **Flex button sits LEFT of the price on the same row** (both top 899; left 26 vs 127).
Cards **arrive already flexed** at `Flex 1/3` / **1.35** — they never start on No Flex, and
4.68 / 2.34 only appear once the button is tapped. The first flexed card is `fx-2`
FC Salzburg v Pafos FC in BOTH layouts, so Q2 and Q3 can be identical across all four cells and
still be true to the default screen.

Five errors fixed: "underneath" -> above; "above the price" -> next to the price; dropped the
"Flex 2/3" reference from Q1 (first card reads 1/3); Q2 rewritten to the arrival state and
answered in prices only (1.35 correct, 4.68 the trap); Q3 option D was "the two numbers don't
agree" which is only true in the loss cell — now a neutral "Not sure." everywhere, and a high B
in the loss cell is the mismatch signal.

### Preloader (2026-09-02)

All six builds shipped a white `#faf9f5` full-screen placeholder with a crude "2/3" card sketch
and an "Unpacking..." pill. Replaced with the **betPawa wordmark on `#16191B`, pulsing**
(`#__pawa_preload`, opacity 1 -> 0.28, 1.15s infinite, disabled under prefers-reduced-motion);
status pill hidden. **Only the pre-boot shell was edited — the resource manifest and loader
script are untouched.** A future re-publish from Claude Design will overwrite this; re-apply.
To see it, load with JS disabled — locally it boots too fast to observe.

### ANCHOR CARD for Q2 and Q3: `fx-8` (PSV v Fortuna Sittard)

Verified identical in all four builds — arrives at `Flex 2/3` @ **1.48**, picks PSV / Over 3.5 /
Perisic 2+, and its **only other dropdown option is `No Flex` @ 4.82**. `Flex 1/3` is NOT offered
on this card: it would price under the 1.20 floor (`levels` filter in ui.jsx). Only the sentence
differs by wording ("1 pick can lose and you still win." vs "2 or more picks have to win").

**`Flex 2/3` is the dominant default** — 2 of 3 flexed cards in one rail, 4 of 5 in two rails.
`fx-2` (FC Salzburg, `Flex 1/3` @ 1.35, three-level ladder 4.68 / 2.34 / 1.35) is the EXCEPTION.
Do not write a stem promising three options unless it is specifically about fx-2.

### Alignment with Jim's original draft questions

Q3 uses **2/3 Flex** with his original option order (A all 3 / B at least 2 / C only 1),
correct = B, trap = C. Q2 uses his **lower / higher / same** options, correct = A, trap = B —
asking for a specific price instead had lost the "stays the same" mental model.

Two deliberate deviations from his draft, both still open for him to overrule:
1. **"Normal Combo" -> "No Flex"** / "a card without the Flex button". The UI has no "Normal
   Combo" label anywhere; the control says No Flex and the rails say Popular / Flex Combos.
   If a moderator introduces the term "Normal Combo" in the brief, his wording becomes fine.
2. **Q1 option B is inverted** from his draft. He had Normal = can change picks; the page has
   Flex = can change picks, because "Flex" sounding like "editable" is the more tempting
   misconception. It is a distractor either way.

Also shortened every D to a plain "Not sure." per his "simple and straight" instruction; his
fuller "Not sure / I don't know the difference between X and Y" is available if preferred.

### Vocabulary rules for any future question writing
- Say **picks**, never "legs" (`__PICKS=true`; the UI never says legs).
- Say **No Flex**, never "Normal Combo" (no such label exists in the UI).
- The No Flex state shows NO explainer sentence, so a "what is Flex" question is a concept check,
  not a reading check.

## Related

`flex-combos-one-rail` is a lighter source-level rebuild of variant #1 (separate editable files
instead of one 2.6 MB bundle) — https://jimpawa.github.io/flex-combos-one-rail/
