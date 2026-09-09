# Architectural Diary — Masakali Wild Experience

Narrative history of how this site came to be, reconstructed from the git
history (42 commits, 2024-10-16 → 2024-12-04, plus a 2026-09-08
documentation pass). Commit hashes are post-rewrite; see CHANGELOG.md for
the note on the messages-only history rewrite.

## Phase 1 — Static launch (2024-10-16/17)

The site started as a scaffolded single-page HTML file (d23bd59): hero,
filterable trip grid, about, blog, workshops, contact, ES/EN toggle.
Within a day it gained local trip videos and a full visual redesign
(4dabe0e), a custom domain (6a6be2a), and then a rapid hardening pass:
the contact form moved to the Celerity form-wrapper service and the
half-working language toggle was deleted (6d57f09); a blocking submit
handler was removed (71f80c6); `name` attributes were added so the form
actually captured data (7c3be97); ~49 MB of unused video binaries were
dropped (9290cc1) once trips switched to YouTube embeds (5cb0249,
730ada9). Branding landed the same day: green accent color, corrected
name spelling (9bce3bf), navbar logo, flower hero background (9488994),
real blog photos and the feminine "Nosotras" voice (680099e). The
workshops section was hidden pending content (828c70a).

Key decisions: [001](decisions/001-single-file-static-site.md),
[002](decisions/002-github-pages-custom-domain.md),
[003](decisions/003-youtube-hosting-for-trip-videos.md),
[004](decisions/004-form-wrapper-contact-form.md),
[007](decisions/007-brand-identity-green-palette-feminine-voice.md),
[008](decisions/008-hide-workshops-section.md).

## Phase 2 — CMS conversion (2024-11-26)

A month later the site was converted into a Mavo app so the founders
could edit copy themselves (0161c4c created `masakali.json`,
63130f9 wired `mv-app`/`mv-storage`/`property` bindings and added the
`<blog-post>` custom element). The rest of the day was spent taming the
CMS: fixing Mavo's parallel-array serialization of blog posts (3d20459),
deleting now-redundant hardcoded markup (d5fb7d0), and a series of
add/remove test posts ("Cool", "Hello") that show the owners learning
the editing workflow. The booking flow was finished: the trip modal's
"Reservar ahora" now prefills the contact form and scrolls to it
(e793841), plus modal typography polish (e59457a) and a punctuation
back-and-forth on the hero copy (46a9b76 → cec4f0d).

Key decisions: [005](decisions/005-mavo-cms-with-github-storage.md),
[006](decisions/006-modal-booking-flow-into-contact-form.md).

## Phase 3 — Real content (2024-12-02/04)

Five blog images were uploaded via the CMS, then the big content commit
(77ac05e) replaced all placeholder copy with the real 2025 season:
dated itineraries for Bali (July), India (March), Vietnam (August),
Azores (April), the founders' story, and three blog posts. A final copy
tweak (16d286a) closed the era. The site has been stable since.

## Phase 4 — Documentation (2026-09-08)

Messages-only history rewrite (41 messages, trees untouched) followed by
this documentation suite: README, AGENTS.md, CHANGELOG, diary, and the
one-shot recreation prompt (`prompt.md`).

## Index of decisions

| # | Decision | Date | Commit |
| --- | --- | --- | --- |
| 001 | Single-file static site, no framework | 2024-10-16 | d23bd59 |
| 002 | GitHub Pages + custom domain via CNAME | 2024-10-16 | 6a6be2a |
| 003 | Host trip videos on YouTube, not in-repo | 2024-10-17 | 5cb0249, 9290cc1 |
| 004 | Contact form via Celerity form-wrapper | 2024-10-17 | 6d57f09 |
| 005 | Mavo CMS with GitHub-backed JSON storage | 2024-11-26 | 0161c4c, 63130f9 |
| 006 | Booking = modal CTA prefills contact form | 2024-11-26 | e793841 |
| 007 | Green palette, logo, feminine Spanish voice | 2024-10-17 | 9bce3bf, 680099e |
| 008 | Hide workshops section instead of deleting | 2024-10-17 | 828c70a |
