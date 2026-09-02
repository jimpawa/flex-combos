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

## Related

`flex-combos-one-rail` is a lighter source-level rebuild of variant #1 (separate editable files
instead of one 2.6 MB bundle) — https://jimpawa.github.io/flex-combos-one-rail/
