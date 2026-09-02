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

Q1 (No Flex vs Flex concept) and Q2 (payout cost of flexing) are IDENTICAL in all four cells —
they are the cross-prototype baseline. Q3 splits by wording with an identical stem, options and
correct answer, so the loss vs ratio cells subtract cleanly:

- Version A (loss framing) -> one-rail, one-rail-lose, two-rails, two-rails-lose
- Version B (ratio framing) -> one-rail-ratio, two-rails-ratio

Page has an answer-key toggle (`body.hide-answers`) for screen-sharing.

### Exact on-screen strings, card fx-2 (FC Salzburg v Pafos FC, 3 picks)

| control  | price | loss framing                          | ratio framing                |
|----------|-------|---------------------------------------|------------------------------|
| No Flex  | 4.68  | (NO sentence shown at all)            | (NO sentence shown at all)   |
| Flex 2/3 | 2.34  | "1 pick can lose and you still win."  | "2 or more picks have to win"|
| Flex 1/3 | 1.35  | "2 picks can lose and you still win." | "1 or more picks have to win"|

**The core insight:** in loss framing the sentence's number is the COMPLEMENT of the pill's
numerator — "2 picks can lose" sits next to `Flex 1/3`. Two different numbers on one card. In
ratio framing they match. Q3's trap answer ("2 of the 3") measures exactly that cost.

### Three corrections made to Jim's draft questions
1. "legs" -> "picks" (`__PICKS=true`; the UI never says legs)
2. "Normal Combo" -> "No Flex" (no such label exists in the UI)
3. Q1 reframed as a concept check — the No Flex state shows no sentence to read

### Caveat recorded on the page
Three questions cannot separate one-rail from two-rails: rail layout changes no wording at all,
so Q3 repeats within each wording pair. Layout is a FINDABILITY variable — measure behaviourally
(time to first Flex interaction, scroll depth, % sessions never touching the control). An
optional 4th findability question is drafted on the page.

## Related

`flex-combos-one-rail` is a lighter source-level rebuild of variant #1 (separate editable files
instead of one 2.6 MB bundle) — https://jimpawa.github.io/flex-combos-one-rail/
