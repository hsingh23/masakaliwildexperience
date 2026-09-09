# AGENTS.md — guide for AI agents working in this repo

## What this is

A single-page, Spanish-language marketing site (no build system) for a
women-led backpacking/yoga-retreat travel project. Content is edited via
Mavo and stored in `masakali.json`. Hosted on GitHub Pages at
https://masakaliwildexperience.com. Read `README.md` first for product
context.

## Commands

There is no build, test, or lint tooling. Everything is a static file.

```bash
# Serve locally (any static server works)
python3 -m http.server 8000

# Validate the content file after editing
python3 -m json.tool masakali.json > /dev/null && echo OK

# Inspect history (messages were rewritten 2026-09-08; see CHANGELOG note)
git log --oneline
```

Deploy = push to `main` (GitHub Pages). Never force-push `main` unless
explicitly asked; a pre-rewrite backup exists at
`backup/pre-docs-20260908` (local only).

## Architecture map

```
index.html ── the whole app
  ├── <style>            all CSS (design tokens inline: see prompt.md)
  ├── Mavo <script>/<link> from get.mavo.io
  ├── form-wrapper.js    from web.celeritytechconsulting.com (defer)
  ├── <body mv-app="masakali" class="mv-autoedit"
  │        mv-storage="https://github.com/hsingh23/masakaliwildexperiences.com"
  │        mv-plugins="tinymce" mv-bar="no-login">
  │     every editable node carries property="..." → bound to masakali.json
  ├── <blog-post> custom element (shadow DOM, reading modal)
  └── inline <script>    menu, smooth scroll, filters, trip modal, CTA flow

masakali.json ── Mavo storage (data model)
  heroTitle, heroSubtitle
  {bali,india,vietnam,azores}{Title,Description}
  aboutTitle, aboutDescription
  blogPosts[] { postImage, postTitle, postExcerpt, postContent, postDate }
  workshopTitle[], workshopDescription[], workshopLocation[]   (parallel arrays)

images/      CMS-uploaded binaries (timestamped names)
CNAME        custom domain for GitHub Pages
```

Rendering flow: Mavo loads `masakali.json` from GitHub, matches each
`property` attribute in `index.html` to a JSON key, and fills the DOM.
Saves write the JSON (and new images) back as commits authored by the
GitHub account that saved (history shows author "Masakaliwildexperience").

## Conventions

- **Language:** all user-facing copy is Spanish, feminine voice
  ("Nosotras"), warm/community tone ("la TRIBU").
- **Commits:** conventional-commit style (`feat:`, `fix:`, `chore:`,
  `style:`, `docs:`, `test:` with optional scope). Subject imperative,
  ≤72 chars, body explaining why. (History before 2024-12-04 predates
  this and was rewritten in place on 2026-09-08 — messages only.)
- **Content changes** go in `masakali.json` (or via the live Mavo UI),
  not hardcoded in `index.html`.
- **Structural/styling changes** go in `index.html`.
- No frameworks, no build step — keep it that way unless the owner asks.

## Gotchas

1. **`mv-storage` points at `masakaliwildexperiences.com`**, not this
   repo's name (`masakaliwildexperience`). GitHub's rename redirect makes
   Mavo saves still land here. If the redirect ever breaks, Mavo saves
   will silently target a nonexistent repo — check the Mavo UI's save
   status after any repo rename.
2. **Mavo needs a GitHub login in-browser.** `mv-bar="no-login"` hides
   the login bar; anonymous visitors cannot edit, but a logged-in
   maintainer can (autoedit mode is always on via `class="mv-autoedit"`).
3. **Contact form fields must keep their `name` attributes**
   (`Nombre`, `Email`, `Message`) or form-wrapper submits empty data.
   Do not add your own submit/preventDefault handler — it will break
   form-wrapper delivery (this happened once; see 71f80c6).
4. **Form delivery is third-party:** `form-wrapper.js` is loaded from
   `web.celeritytechconsulting.com`. If that host dies, the form stops
   delivering silently.
5. **Large binaries are in git history** (`bali.mp4` 54 MB, `vietnam.mp4`
   48 MB, `azores.mp4` 24 MB at HEAD). GitHub warns about `bali.mp4`.
   Videos actually displayed are YouTube embeds now — do not add more
   big media to the repo.
6. **`#talleres` is hidden, not deleted** (`display: none`). Don't
   "clean it up" without asking; it is intentionally parked.
7. **Empty commits happen:** Mavo sometimes saves with zero changes
   (e.g. 59d26c7). Not an error.
8. **`blogPosts` shape:** proper array of objects. Mavo's
   parallel-array serialization produced a malformed shape once
   (fixed in 3d20459); if posts render wrong, check for arrays of
   scalars inside a single post object.
9. **Workshop fields are parallel arrays** (`workshopTitle[i]` pairs with
   `workshopDescription[i]` and `workshopLocation[i]`) — Mavo's
   serialization for repeated simple properties. Keep indexes aligned.
10. **Blog-post custom element vs Mavo:** the `<blog-post>` shadow-DOM
    element defined in `index.html` coexists with the Mavo-rendered
    article list; the Mavo path is the live one.

## Verifying changes

1. `python3 -m json.tool masakali.json > /dev/null` — JSON valid.
2. Serve locally and load the page:
   - hero/trips/about/blog text matches `masakali.json`;
   - filter buttons show/hide trip cards;
   - "Más información" → modal → "Reservar ahora" prefills the contact
     form and scrolls to it;
   - mobile width (≤768px): hamburger menu opens and closes.
3. If you touched `index.html` structure, confirm every `property=`
   attribute still has a matching key in `masakali.json`, or Mavo will
   show it as new/empty data.

## Pointers

- Decision records: `architectural-diary/decisions/`
- Full history with bullets per commit: `CHANGELOG.md`
- Recreation spec (design tokens, data model, APIs): `prompt.md`
- Mavo docs: https://mavo.io/docs
