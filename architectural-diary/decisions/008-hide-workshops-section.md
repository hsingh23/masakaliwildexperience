# 008 — Hide the workshops section instead of deleting it

- **Date:** 2024-10-17
- **Commits:** 828c70a
- **Status:** Accepted (parked feature)

## Context

The scaffold included a "Talleres y Cursos" section with two workshop
cards (a Bali mindfulness retreat and an online goal-setting workshop,
both dated 2024). The offering was not ready for publication at launch.

## Decision

Set `style="display: none"` on `#talleres` rather than deleting the
markup. The workshop fields (`workshopTitle[]`,
`workshopDescription[]`, `workshopLocation[]`) were later carried into
`masakali.json` as Mavo-editable parallel arrays, so the section is
CMS-ready.

## Consequences

- Zero-risk parking: markup, styles, and data bindings all survive;
  re-enabling is a one-attribute change.
- The registration buttons use `alert()` placeholders (no real
  enrollment flow), so simply unhiding the section is not enough to
  ship the feature.
- The hidden section still ships in the HTML payload — negligible cost.
