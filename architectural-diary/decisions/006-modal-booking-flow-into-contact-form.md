# 006 — Booking = modal CTA prefills the contact form

- **Date:** 2024-11-26
- **Commits:** e793841 (CTA wiring), e59457a (modal typography)
- **Status:** Accepted, still in force

## Context

Each trip card's "Más información" opens a details modal
(title/description from a `tripData` object in the inline script). The
modal's "Reservar ahora" button originally pointed at an anchor with no
destination — there is no booking engine, checkout, or even a
dedicated booking page.

## Decision

Make the modal CTA a bridge into the contact form: clicking it writes
`Reserva tu viaje a <trip title>` into the contact form's `Message`
field, closes the modal, and smooth-scrolls to the form. The traveler
then only adds name/email and submits via form-wrapper (decision 004).
Also enlarge the modal title (2em) and add vertical spacing to the
description for hierarchy.

## Consequences

- A complete-enough funnel — video → details → prefilled inquiry —
  with zero backend logic.
- The prefill overwrites whatever the user may have already typed in
  the Message field; acceptable at this scale.
- `tripData` (durations, itineraries, CTA labels) lives in the inline
  script, not in masakali.json, so the richer descriptions owners edit
  in the CMS do not automatically appear in the modal — the modal copy
  and card copy can drift.
