# Masakali Wild Experience — masakaliwildexperience.com

Spanish-language marketing site for **Masakali Wild Experience**, a women-led
backpacking and yoga-retreat travel project founded by Maria and Verónica.
The site presents four guided group trips (Bali, India, Vietnam, Azores),
a blog, and a contact/booking form — all editable by non-technical owners
through the Mavo CMS.

**Live site:** https://masakaliwildexperience.com (GitHub Pages + CNAME)

## Why this exists

The founders needed a simple, cheap, maintainable web presence for their
travel community ("la TRIBU"). Instead of a framework or a hosted CMS
subscription, the site is a single static HTML file whose copy is stored in
`masakali.json` and edited in-place in the browser via
[Mavo](https://mavo.io), which commits changes straight back to this GitHub
repository. GitHub Pages serves it on the custom domain. There is no build
step, no server-side code, and no cost beyond the domain.

## Features

- **Hero** — full-viewport section over a flower photo with the motto
  "Viaja. Crece. Conecta." and a CTA scrolling to the trips grid.
- **Trips (Viajes)** — four cards with YouTube video embeds and filter
  buttons (Todos / India / Vietnam / Bali / Azores); "Más información"
  opens a details modal whose "Reservar ahora" CTA prefills the contact
  form and scrolls to it.
- **About (Nosotras)** — the founders' story and photo.
- **Blog** — posts rendered from `masakali.json` (Mavo `mv-list`), with a
  custom `<blog-post>` element and a reading modal.
- **Contact (Contacto)** — form wrapped in the Celerity `form-wrapper`
  service (`data-form-id="Masa Kali contact-bde060"`) that delivers
  submissions without a backend.
- **Workshops (Talleres)** — section kept in the markup but hidden with
  `display: none` until content is ready.
- Fully responsive: fixed header, hamburger menu under 768px, smooth
  scrolling, card hover animations.

## Stack

| Concern | Choice |
| --- | --- |
| Markup / styles / logic | Single `index.html` (vanilla HTML + CSS + JS) |
| CMS | [Mavo](https://get.mavo.io) (`mavo.css`/`mavo.js`, tinymce plugin, GitHub storage) |
| Content storage | `masakali.json` in this repo (Mavo reads/writes it) |
| Hosting | GitHub Pages, custom domain via `CNAME` |
| Form delivery | `form-wrapper.js` from `web.celeritytechconsulting.com` |
| Trip videos | YouTube iframe embeds |
| Typography | Montserrat (Google font stack, sans-serif fallback) |

## Quickstart

```bash
git clone git@github.com:hsingh23/masakaliwildexperience.git
cd masakaliwildexperience
python3 -m http.server 8000   # any static file server works
open http://localhost:8000
```

Editing content:

- **In the browser (preferred for non-technical editors):** open the live
  site; Mavo's `mv-autoedit` mode makes every underlined text/property
  editable inline. Saving commits `masakali.json` (and any uploaded
  images) back to GitHub. Because `mv-bar="no-login"` is set, you must
  already be logged in to GitHub in the same browser.
- **By hand:** edit `masakali.json` (or `index.html` for structure) and
  commit to `main`. GitHub Pages redeploys automatically.

There are no environment variables, no build step, and no dependencies to
install.

## Repository structure

```
.
├── index.html        # the entire site: markup, CSS, JS, Mavo bindings
├── masakali.json     # Mavo storage: all editable copy and blog posts
├── CNAME             # masakaliwildexperience.com (GitHub Pages)
├── images/           # CMS-uploaded blog images (timestamped names)
├── cover.jpg         # About section photo
├── flower.JPG        # hero background
├── india.JPG         # blog image
├── logo.jpg          # favicon
├── transparent_logo.png  # navbar logo
├── azores.mp4, bali.mp4, india.mp4, vietnam.mp4  # legacy local videos
└── .gitignore        # .DS_Store
```

The `.mp4` files at the root are legacy: trips now embed YouTube videos,
but the binaries remain in history (see AGENTS.md gotchas).

## Deployment

Push to `main` — GitHub Pages serves the repo root at
https://masakaliwildexperience.com. The `CNAME` file claims the custom
domain; the DNS records are managed outside this repo.

## Further reading

- `AGENTS.md` — working conventions, architecture map, gotchas
- `CHANGELOG.md` — every commit, newest first
- `architectural-diary/` — decision records
- `prompt.md` — one-shot spec to recreate this site from scratch
