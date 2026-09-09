# 003 — Host trip videos on YouTube, not in-repo

- **Date:** 2024-10-17
- **Commits:** 5cb0249 (switch to embeds), 9290cc1 (drop unused binaries)
- **Status:** Accepted, still in force

## Context

The first redesign (4dabe0e) shipped trip videos as local `<video>`
elements with binaries committed to git (~176 MB total across
bali/vietnam/azores/india clips). This bloated clones and brushed
against GitHub's 100 MB hard limit; playback also burned site bandwidth.

## Decision

Upload the videos to YouTube and embed them as iframes (one per trip
card: Bali `8Q1SAStKePE`, India `UYiFv2rwldA`, Vietnam `iKmst1yJvis`,
Azores `t8G7Fdt5vPg`). Delete the now-unused `azore.mp4` (~43 MB) and
`india.MOV` (~6 MB) from the working tree and add a `.gitignore` for
`.DS_Store`.

## Consequences

- Cheap, fast, adaptive-bitrate video; YouTube bears the bandwidth.
- Four iframes per page view is heavy (each ~725 px tall), trading page
  weight for simplicity — acceptable for a marketing page.
- The old `<video>` markup was kept commented out for a while, then
  removed.
- Large binaries remain in git *history* (`bali.mp4` 54 MB still at
  HEAD triggers GitHub's "large file" warning on push). Removing them
  would require a history rewrite the owners have not asked for.
- Embed IDs are hardcoded in `index.html`, not in `masakali.json`, so
  swapping a video is a code change.
