# Pro — mobile landing page

A scroll-driven mobile landing page. One HTML file, no build step, no
dependencies.

## Sections

**Hero** — a 3.4×-height track with a sticky stage, so scroll distance acts as
the timeline. "Pro" fades and lifts, the black-and-white portrait dissolves to
reveal the hand beneath it, then the copy arrives. Every step is a CSS
`clamp()` reading one `--p` custom property that JS writes once per frame.

**Dot grid** — a canvas lattice on the acid tile. Each dot fades between 20%
and 100% opacity on its own clock, with phase and speed derived from a hash of
its grid position, so the field shimmers without any crest travelling across
it. Rows are derived from the column pitch, keeping the lattice square at any
tile height. It only animates while on screen.

**Watch / Practice / Prove** — a second sticky track split in thirds. Each
third opens one row, which grows into all the slack the collapsed rows leave
and pins its text to the foot of that span, while the matching asset
cross-fades in behind. The clip plays only while its own row is open.

## Running it

Any static server from this directory:

```bash
python3 -m http.server 4178
```

## Typography

Set in **Söhne** (Klim Type Foundry). The font files are licensed and are
**not** in this repo — `assets/fonts/` is gitignored, including the
`fonts.css` that declares the `@font-face` rules. The published site 404s on
that stylesheet and falls back to Helvetica Neue.

To restore Söhne locally, drop these into `assets/fonts/` and recreate
`fonts.css` with `@font-face` rules for each:

| File | Weight |
| --- | --- |
| `Sohne-Buch.otf` | 400 |
| `Sohne-Kraeftig.otf` | 500 |
| `Sohne-Halbfett.otf` | 600 |
| `Sohne-Dreiviertelfett.otf` | 700 |

The hero word is sized to fill the card width exactly. CSS does this from
Söhne's own advance ratio, then JS re-measures whatever font actually rendered
and corrects — so it stays flush to both insets with or without the licensed
font.

## Notes

- Layout is capped at a 440px column: a phone page, centred on wider screens.
- Sticky stages top out at 720px, the dot tile at 600px, both centred in the
  viewport and letterboxed by the page behind them.
- Honours `prefers-reduced-motion`: the dot field renders as a still lattice
  and the clip stays paused.
