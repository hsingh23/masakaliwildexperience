# 007 — Brand identity: green palette, logo, feminine Spanish voice

- **Date:** 2024-10-17
- **Commits:** 9bce3bf (green + title spelling), 9488994 (flower hero +
  short brand), 730ada9 (navbar logo), 680099e ("Nosotras" + real blog
  images)
- **Status:** Accepted, still in force

## Context

The scaffold used a generic blue accent (#3498db), placeholder images,
neuter/masculine Spanish copy ("Nosotros"), and a mistyped brand
("Masa Kali Wild Experience"). The brand is two women addressing a
mostly-female community.

## Decision

- Replace the blue accent with sage green **#6e905e** across nav hover,
  CTA buttons, filter buttons (active + hover), and the language
  toggle; keep dark blue-gray **#2c3e50** for text/headings and
  **#ecf0f1** / **#f9f9f9** for surfaces.
- Correct the page title to "Masakali Wild Experience".
- Use `flower.JPG` as the full-viewport hero background under a 50%
  black overlay; shorten the navbar brand text to "Masakali" beside the
  `transparent_logo.png` mark; `logo.jpg` becomes the favicon;
  `cover.jpg` illustrates the About section.
- Feminine voice throughout: "Nosotras" in the nav link, about id/
  title/alt text, and copy; real photos (flower.JPG, india.JPG) replace
  via.placeholder.com blog images.

## Consequences

- A coherent nature/community identity with essentially zero design
  system effort — colors are hardcoded in the single `<style>` block.
- One deliberate inconsistency remains: CTA buttons hover to blue
  **#2980b9** (a leftover from the original blue theme) rather than a
  darker green.
- Copy is genuinely bilingual-sensitive: content is Spanish only, and
  the ES/EN toggle was removed (decision 004) rather than completed.
