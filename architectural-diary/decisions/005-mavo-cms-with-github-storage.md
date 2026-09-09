# 005 — Mavo CMS with GitHub-backed JSON storage

- **Date:** 2024-11-26
- **Commits:** 0161c4c (masakali.json), 63130f9 (convert to Mavo app),
  3d20459 (fix blogPosts shape), d5fb7d0 (drop hardcoded duplicate),
  e793841 (autoedit/tinymce/no-login/mv-list)
- **Status:** Accepted — the defining architectural decision of the site

## Context

After launch, every copy change required the developer. The owners
(Maria and Verónica) are non-technical and needed to edit trip
descriptions, the about story, and blog posts themselves. Options: a
headless CMS (needs a service + rebuild), a hosted site builder
(migration cost), or Mavo — a declarative CMS that annotates plain HTML
and stores data in the repo itself.

## Decision

Convert the page into a Mavo app:

- `<body mv-app="masakali" class="mv-autoedit"
  mv-storage="https://github.com/hsingh23/masakaliwildexperiences.com"
  mv-plugins="tinymce" mv-bar="no-login">`
- Load `mavo.css`/`mavo.js` from get.mavo.io.
- Annotate every editable node with `property="..."`; repeated content
  (blog posts) uses `mv-list`/`mv-list-item`.
- Data lives in `masakali.json` at the repo root; Mavo commits saves
  (including uploaded images under `images/`) back to GitHub.
- TinyMCE plugin gives rich-text editing for long fields; `no-login`
  hides the Mavo bar for anonymous visitors (GitHub login in-browser
  is still required to save); `mv-autoedit` puts logged-in editors
  straight into inline editing mode.
- A `<blog-post>` custom element with shadow DOM renders each post and
  a reading modal.

## Consequences

- Owners edit the live site in place; content commits appear in history
  authored by "Masakaliwildexperience" (the saving GitHub account).
- The learning curve is visible in history: throwaway "Cool"/"Hello"
  test posts, punctuation experiments, an empty no-op save commit.
- Mavo's serialization quirks caused one data-shape bug: repeated
  properties serialized as parallel arrays inside a single object
  (fixed by hand in 3d20459). Workshop fields still use parallel
  arrays by design.
- `mv-storage` names `masakaliwildexperiences.com` while the repo is
  `masakaliwildexperience` — it works only via GitHub's rename
  redirect. Fragile if repos are renamed again.
- Data model in masakali.json: heroTitle/heroSubtitle;
  {bali,india,vietnam,azores}{Title,Description}; aboutTitle/
  aboutDescription; blogPosts[]{postImage, postTitle, postExcerpt,
  postContent, postDate}; workshopTitle[]/workshopDescription[]/
  workshopLocation[].
