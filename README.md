# betPawa — Flex Combos prototype variants

The six published builds from Claude Design project `7a99d38c-bfa5-4d85-badf-f16fdabeb1ca`,
hosted as live links.

**Hub:** https://jimpawa.github.io/flex-combos/

| # | Prototype | Rail layout | Wording | URL |
|---|-----------|-------------|---------|-----|
| 1 | One rail · loss framing  | `__COMBO_LAYOUT="one"`   | `__WORD_MODE="lose"`  | [/one-rail/](https://jimpawa.github.io/flex-combos/one-rail/) · alias [/one-rail-lose/](https://jimpawa.github.io/flex-combos/one-rail-lose/) |
| 2 | One rail · win framing | `__COMBO_LAYOUT="one"`   | `__WORD_MODE="ratio"` | [/one-rail-ratio/](https://jimpawa.github.io/flex-combos/one-rail-ratio/) |
| 3 | Two rails · loss framing | `__COMBO_LAYOUT="rails"` | `__WORD_MODE="lose"`  | [/two-rails/](https://jimpawa.github.io/flex-combos/two-rails/) · alias [/two-rails-lose/](https://jimpawa.github.io/flex-combos/two-rails-lose/) |
| 4 | Two rails · win framing| `__COMBO_LAYOUT="rails"` | `__WORD_MODE="ratio"` | [/two-rails-ratio/](https://jimpawa.github.io/flex-combos/two-rails-ratio/) |

## Six folders, four prototypes

`one-rail` and `one-rail-lose` are the same build — identical flags and identical decoded app
code, differing only in `<title>` and a per-publish random resource UUID. Same for `two-rails`
and `two-rails-lose`. All six URLs are published so links stay stable, but there are only four
things to review.

Verified by decoding each bundle's `__bundler/manifest` and hashing the decompressed resources:
all six share resource fingerprint `1c6b4d61b415`.

## Shared across all builds

    __FLEX_V2   = true      3-leg model, flex levels 2/3 and 1/3
    __FLEX_UI   = "pset"    preset control — level reads as a plain fraction
    __FLEX_LOCK = "user"    pinned to the User Flex prototype
    __FLEX_DATA = true      real priced ladder from flex_bet_pricing_5match.xlsx
    __JIM_RAILS = true      Jim's Ideas rail treatment
    __PICKS     = true      combo items are "picks"; multibet items stay "legs"
    __DEVICE    = "ip16"    iPhone 16 Pro
    __APP_MODE  = true      full viewport, no bezel, no SSOT chrome
    __NO_PANELS = true      no guided-demo / open-questions panels

## About the files

Each `index.html` is a self-contained ~2.6 MB page: React 18.3.1, Babel 7.29.0, four Roboto
faces and the 140-symbol pawaIconZ sprite are all inlined as a gzip+base64 resource manifest.
No CDN, so they run offline and inside Maze. First paint takes about a second while Babel
compiles the JSX.

## Related

A lighter, source-level rebuild of the one-rail variant (separate files rather than one 2.6 MB
bundle, useful for editing) lives at
[jimpawa/flex-combos-one-rail](https://github.com/jimpawa/flex-combos-one-rail) —
https://jimpawa.github.io/flex-combos-one-rail/
