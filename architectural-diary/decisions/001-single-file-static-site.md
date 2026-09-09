# 001 — Single-file static site, no framework

- **Date:** 2024-10-16
- **Commits:** d23bd59 (scaffold), 4dabe0e (redesign)
- **Status:** Accepted, still in force

## Context

The founders needed a marketing site fast, with zero budget and zero
interest in maintaining tooling. The initial author reached for the
simplest thing that works for a five-section landing page.

## Decision

Build the entire site as one `index.html`: markup, a `<style>` block,
and one inline `<script>` block. No bundler, no framework, no package
manager, no build step. Vanilla DOM APIs for interactivity (menu toggle,
smooth scrolling, card filtering, modals).

## Consequences

- Anyone can open the file and understand/edit it; hosting is trivially
  static.
- Interactivity that a framework would make easy (e.g. the abandoned
  i18n toggle) has to be hand-rolled, which is how the half-working
  language toggle got deleted instead of fixed.
- The file has grown to ~800 lines; further sections would argue for
  splitting CSS/JS out, but at current scope the single file remains
  manageable.
- Mavo (decision 005) layered on top without conflict because Mavo is
  itself a progressive-enhancement, no-build library.
