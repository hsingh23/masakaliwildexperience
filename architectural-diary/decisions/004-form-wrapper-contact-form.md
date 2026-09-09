# 004 — Contact form via Celerity form-wrapper

- **Date:** 2024-10-17
- **Commits:** 6d57f09 (integrate + drop language toggle), 71f80c6
  (remove blocking handler), 7c3be97 (add name attributes)
- **Status:** Accepted, still in force

## Context

A static site cannot process form submissions. The scaffold's original
handler just showed an alert and reset the form — nothing was delivered.
An ES/EN language toggle was also abandoned mid-implementation.

## Decision

Load `form-wrapper.js` (hosted at
`web.celeritytechconsulting.com/form-wrapper.js`, deferred) and wrap the
contact form in `<form-wrapper data-form-id="Masa Kali contact-bde060">`.
Delete the custom submit handler so the wrapper can intercept submits,
and give each field a `name` attribute (`Nombre`, `Email`, `Message`)
so submissions carry labeled data. Remove the language toggle entirely.

## Consequences

- Working form delivery with no backend and no third-party form SaaS
  account to manage.
- Two follow-up fixes within minutes show the integration's sharp
  edges: a leftover `preventDefault` handler silently blocked the
  wrapper (71f80c6), and placeholder-only fields submitted empty data
  (7c3be97). Both gotchas are now recorded in AGENTS.md.
- The dependency is an external script host; if
  `web.celeritytechconsulting.com` goes away, the form breaks silently.
  There is no fallback or monitoring.
- The `data-form-id` is the only configuration; submissions presumably
  land in an account controlled by whoever provisioned the wrapper.
