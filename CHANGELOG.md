# Changelog

All notable changes to the Masakali Wild Experience site are documented here,
newest first. Dates reflect author commit dates.

> **History rewrite note (2026-09-08):** Commit *messages only* were rewritten
> on 2026-09-08 to follow conventional-commit style. Every tree, file, author,
> and date is byte-for-byte identical to the original history; only the
> messages changed (41 of 42 commits; `52534b7` "Create CNAME" was kept).
> A pre-rewrite backup of `main` exists locally as
> `backup/pre-docs-20260908`. Short hashes below are post-rewrite.

## 2024-12-04

- **16d286a — docs: update India retreat description and post title**
  - Expanded `indiaDescription` to mention Rishikesh surroundings and a closing line about disconnecting while connecting with Indian culture.
  - Dropped the trailing period from the group-travel blog post title.

- **77ac05e — feat(content): add real 2025 trip and blog content to masakali.json**
  - Replaced placeholder hero, trip, and about copy with dated 2025 itineraries (Bali July, India March, Vietnam August, Azores April) and the founders' story (Maria and Verónica).
  - Pointed blog images at hosted URLs, added the group-travel post, and left three empty placeholder post objects for future entries.

- **d792a59 — chore(assets): add image 1733312425683.jpg** — 216 KB blog image for the solo-travel post.
- **172c056 — chore(assets): add image 1733312464962.jpg** — 1.1 MB CMS-uploaded image asset.
- **7ed1cd6 — chore(assets): add image 1733312173388.jpg** — 357 KB CMS-uploaded image asset.
- **cb07924 — chore(assets): add image 1733312234009.jpg** — 277 KB blog image for the group-travel post.
- **ff451bd — chore(assets): add image 1733312196085.jpg** — 1.9 MB blog image for the mindset post.

## 2024-12-02

- **36253bd — fix(content): add missing trailing period to heroTitle** — restored the final period in "Viaja. Crece. Conecta." to match heroSubtitle punctuation.
- **cafdf17 — chore(content): remove test blog post entry** — dropped the junk "Hey"/"asdfadf" post added minutes earlier.
- **9967e32 — test(content): add throwaway blog post entry** — appended a dummy post ("Hey"/"asdfadf" with screenshot image) to exercise the Mavo editing flow.
- **db526c4 — test(assets): add screenshot image for CMS publish test** — 2.9 MB screenshot referenced by the throwaway test post.
- **d838ccf — chore(content): drop trailing period from heroTitle** — punctuation experiment, reverted in 36253bd.

## 2024-11-26

- **4010ec1 — chore(content): remove "Hello" test blog post entry** — deleted the placeholder "Hello" post, leaving only real posts.
- **9668b42 — test(content): drop postContent from "Hello" test post** — removed a placeholder field while exercising the CMS editor.
- **81c7194 — chore(data): add placeholder "Hello" test post to masakali.json** — appended dummy title/excerpt/content ("Hello") plus a screenshot URL to test the content pipeline.
- **9fb812c — chore(assets): add screenshot image for new blog post** — 658 KB screenshot used by the "Hello" test post.
- **cec4f0d — style(copy): add trailing periods to hero title and subtitle** — settled the punctuation experiment from 46a9b76.
- **46a9b76 — style(copy): remove trailing periods from hero title and subtitle** — punctuation experiment, reverted moments later in cec4f0d.
- **e59457a — style(modal): enlarge title and add vertical spacing to description** — added `.modal-title` (2em) and `.modal-description` (20px/30px margins) applied inside the trip modal.
- **e793841 — feat(booking): prefill contact form from trip modal CTA**
  - Trip modal "Reservar ahora" CTA now prefills the contact form Message field with "Reserva tu viaje a <trip>", closes the modal, and smooth-scrolls to the form.
  - Enabled Mavo auto-edit mode with the tinymce plugin and no-login bar; restructured the blog list to `mv-list`/`mv-list-item` syntax.
- **59d26c7 — chore: record no-op Mavo CMS save (empty commit)** — tree identical to parent; an automated Mavo save that wrote nothing.
- **9110cb2 — chore(data): remove "Cool" test post from masakali.json** — cleaned up the "Cool"/"Beans"/"Nice" test entry.
- **97fd34b — chore(data): add "Cool" test post to masakali.json** — placeholder post ("Cool") added while trying the Mavo workflow.
- **5f8b9ab — chore(assets): add tree-Photoroom.jpg image for blog post** — 589 KB image referenced by the "Cool" test post.
- **d5fb7d0 — refactor(blog): drop hardcoded post now served by Mavo data** — deleted the second hardcoded blog article; posts now come exclusively from masakali.json.
- **3d20459 — fix(data): split parallel-array blogPosts into one object per post** — fixed Mavo's parallel-array serialization so each blog post is a well-formed object with scalar fields.
- **63130f9 — feat(cms): convert site to Mavo app with GitHub-backed editing**
  - Loaded Mavo from get.mavo.io, set `mv-app="masakali"` with GitHub `mv-storage`, and annotated hero, trips, about, blog, and workshops with `property` attributes so all copy is data-driven.
  - Added a `BlogPost` custom element (shadow DOM) that renders a card and opens a styled modal.
- **0161c4c — feat(data): create masakali.json with initial Mavo content** — 50-line storage file seeding hero/trip/about/workshop strings and a blogPosts collection.

## 2024-10-17

- **680099e — fix(content): use real blog images and feminine "Nosotras" copy** — swapped placeholder.com images for flower.JPG/india.JPG and changed gendered copy to "Nosotras" (nav, about, Bali description).
- **9bce3bf — fix(ui): switch accent color to green and fix title spelling** — replaced #3498db blue with #6e905e green across hovers/CTAs/filters and corrected the page title to "Masakali Wild Experience".
- **9488994 — feat(assets): add flower/india photos and set flower as hero backdrop** — flower.JPG became the hero background (replacing cover.jpg); nav brand shortened to "Masakali".
- **730ada9 — feat(ui): add logo, real video IDs, about image, and blog modal** — navbar logo image, real YouTube IDs in all four trip embeds, cover.jpg in About, and blogModal scaffold with data-post tags.
- **5cb0249 — feat(ui): embed trip videos via YouTube instead of local files** — replaced local `<video>` cards with YouTube iframes (placeholder IDs at first), added logo.jpg favicon and blog-modal CSS.
- **828c70a — chore(ui): hide the Talleres (workshops) section** — `display:none` on #talleres until content is ready.
- **7c3be97 — fix(contact): add name attributes so form fields submit values** — added name="Nombre"/"Email"/"Message" so form-wrapper captures labeled data.
- **9290cc1 — chore: add .gitignore for .DS_Store and drop local video files** — removed azore.mp4 (~43 MB) and india.MOV (~6 MB) now that videos live on YouTube.
- **71f80c6 — fix(contact): remove submit handler that blocked form-wrapper** — deleted the preventDefault handler so the form-wrapper service can deliver submissions.
- **6d57f09 — feat(contact): integrate form-wrapper service and drop language toggle**
  - Loaded Celerity form-wrapper.js and wrapped the contact form in `<form-wrapper data-form-id="Masa Kali contact-bde060">`.
  - Removed the EN/ES toggle and its partially-working translation script.

## 2024-10-16

- **6a6be2a — Create CNAME** — custom domain masakaliwildexperience.com for GitHub Pages.
- **52534b7 — fix(copy): rename Bali trip title to "Retiro de Yoga"** — heading changed from "Retiro de Mindfulness" to "Retiro de Yoga".
- **4dabe0e — feat(site): add trip videos, details modal, and visual redesign**
  - Local `<video>` trip cards with new media assets, cover.jpg hero, trip details modal (tripData + "Más información"), workshop alerts, contact submit handler.
  - Montserrat typography, refreshed palette, pill buttons, hover animations, responsive tweaks.
- **d23bd59 — feat: scaffold Masakali Wild Experience single-page site** — initial Spanish-language landing page: hero, filterable trip grid (Bali, India, Vietnam, Azores), About, Blog, Workshops, contact form, mobile menu, smooth scrolling, ES/EN toggle.

## 2026-09-08 (documentation)

- **docs: add README, AGENTS.md, CHANGELOG, architectural diary, and one-shot recreation prompt** — this documentation suite, plus the messages-only history rewrite described in the note above.
