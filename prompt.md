# prompt.md — one-shot recreation spec for masakaliwildexperience.com

Give this document to a competent developer (or agent) with an empty
repository; it contains everything needed to rebuild the site from
scratch, in build order, matching the original's architecture and
design decisions.

## Goal

Build the marketing site for **Masakali Wild Experience** — a women-led
backpacking/yoga-retreat travel community founded by Maria and
Verónica. Spanish-language, single page, five sections (hero, trips,
about, blog, contact; a sixth — workshops — shipped but hidden).
Purpose: present four guided group trips with video, tell the founders'
story, publish blog posts, and capture booking inquiries through a
prefilled contact form — all editable by non-technical owners via an
in-browser CMS, hosted free on GitHub Pages at
**https://masakaliwildexperience.com**.

Voice: warm, feminine ("Nosotras"), community-centric; recurring motif
"la TRIBU". Motto: "Viaja. Crece. Conecta."

## Stack (fixed — do not substitute)

- One `index.html` containing all markup, one `<style>` block, two
  inline `<script>` blocks. No framework, no build step, no npm.
- **Mavo** CMS: `<link rel="stylesheet" href="https://get.mavo.io/mavo.css"/>`
  and `<script src="https://get.mavo.io/mavo.js"></script>` in `<head>`.
- **form-wrapper** contact delivery:
  `<script src="https://web.celeritytechconsulting.com/form-wrapper.js" defer></script>`
- **YouTube** iframe embeds for trip videos.
- **GitHub Pages** hosting; `CNAME` file with `masakaliwildexperience.com`.
- Font stack: `"Montserrat", sans-serif` (no webfont link; rely on
  system/installed or add Google Fonts — original omits the link).

## Phased build order

### Phase 1 — Static single-page site

Create `index.html` with `lang="es"`, viewport meta, favicon
(`logo.jpg`), title "Masakali Wild Experience". Sections in order:

1. **Header** — fixed, full width, `rgba(255,255,255,0.95)` background,
   `box-shadow: 0 2px 10px rgba(0,0,0,0.1)`, z-index 1000, 1rem padding.
   Flex nav max-width 1200px: logo block (`transparent_logo.png` at
   height 80px + wordmark "Masakali", 1.8rem bold uppercase,
   letter-spacing 2px, color #2c3e50) and links: Viajes, Nosotras,
   Blog, Talleres, Contacto (0.9rem, uppercase, letter-spacing 1px,
   hover #6e905e). Hamburger (3 bars) hidden ≥768px.
2. **Hero** — 100vh, background `linear-gradient(rgba(0,0,0,0.5),
   rgba(0,0,0,0.5)), url("./flower.JPG")`, cover/center; centered
   white text: `<h1>` 3.5rem uppercase letter-spacing 3px (2.5rem on
   mobile); `<p>` 1.5rem weight 300; CTA pill.
3. **Viajes (trips)** — section id="viajes", title "Nuestros Viajes",
   filter buttons (Todos/India/Vietnam/Bali/Azores; pill style; active
   = green bg white text), and a grid of 4 trip cards.
4. **Nosotras (about)** — id="nosotras", background #ecf0f1, centered;
   `cover.jpg` (max-width 500px, border-radius 15px) + story text.
5. **Blog** — id="blog", card grid of posts.
6. **Talleres (workshops)** — id="talleres", `display: none` on the
   section (parked feature).
7. **Contacto** — id="contacto", form wrapped in
   `<form-wrapper data-form-id="Masa Kali contact-bde060">`; fields
   `name="Nombre"` (text, required), `name="Email"` (email, required),
   `name="Message"` (textarea ≥150px, required); submit button styled
   as CTA pill. Do NOT add any submit handler or preventDefault.
8. **Modals** — `#tripModal` (`.modal` overlay `rgba(0,0,0,0.8)`,
   z-index 2000; `.modal-content` white, border-radius 15px, 80% width
   max 600px, close ×) and `#blogModal` (same pattern, max 800px).

Inline script: mobile menu toggle; smooth scrolling for all `a[href^="#"]`
(closes mobile menu); filter buttons show/hide `.viaje-card` by
`data-destination`; trip modal open/close (×, outside click) driven by a
`tripData` object keyed bali/india/vietnam/azores with title,
description (multi-sentence itinerary), cta; modal CTA click → prefill
contact form Message with `Reserva tu viaje a <title>`, close modal,
smooth-scroll to form; workshop buttons → `alert()` thanks.

### Phase 2 — Deploy

Add `CNAME` (masakaliwildexperience.com), `.gitignore` (`.DS_Store`),
push to GitHub Pages. Do not commit video binaries; trip cards embed
YouTube iframes `width="100%" height="725"` with
`allow="autoplay; encrypted-media"` allowfullscreen:
Bali `8Q1SAStKePE`, India `UYiFv2rwldA`, Vietnam `iKmst1yJvis`,
Azores `t8G7Fdt5vPg`.

### Phase 3 — CMS conversion (Mavo)

- Add the Mavo CSS/JS tags; set `<body>` to:
  `mv-app="masakali" class="mv-autoedit"
   mv-storage="https://github.com/hsingh23/masakaliwildexperiences.com"
   mv-plugins="tinymce" mv-bar="no-login"`.
- Create `masakali.json` (data model below) as the storage file.
- Add `property="..."` to every editable node: heroTitle, heroSubtitle,
  {bali,india,vietnam,azores}{Title,Description}, aboutTitle,
  aboutDescription, workshopTitle/Description/Location.
- Blog posts: container `<div class="blog-posts" mv-list>` with
  `<article class="blog-post" mv-list-item property="blogPosts"
  mv-item-bar>`; inner fields property="postImage" (img),
  postTitle (h3), postExcerpt (p), postContent (p).
- Define a `<blog-post>` custom element (shadow DOM) that renders the
  post card with a "Leer más" button opening a styled reading modal
  (title, full content, styled image max 500px, Cerrar button).
- Remove hardcoded duplicate blog markup so posts render purely from
  data.

### Phase 4 — Real content

Fill `masakali.json` with the 2025 season: hero "Viajes mochileros" /
"Viaja. Crece. Conecta\nAventuras para el Alma\nMochilear con
Propósito"; Bali July 19–31 (Canggu yoga center Serenity + Ubud,
Sidemen, Amed, Gili); India March 20–30 (Rishikesh ashram on the
Ganges); Vietnam August 18–28 (Hanoi, Ha Long Bay, Ninh Binh, Sapa,
Night Market); Azores April 18–26 (São Miguel, whales/dolphins);
about = founders' story; 3 blog posts (mindset change, solo travel,
group travel/"TRIBU") with images at
`https://masakaliwildexperience.com/images/<timestamp>.jpg`.

## Design decisions (all of them)

- **Colors:** text #333 (body) / #2c3e50 (headings, nav); muted card
  text #7f8c8d; page bg #f9f9f9; alt section bg #ecf0f1; filter button
  bg #ecf0f1; **accent green #6e905e** (nav hover, CTA, filters);
  CTA hover **#2980b9** (intentional leftover from the blue theme);
  form input border #bdc3c7.
- **Type:** Montserrat everywhere; section titles 2.5rem uppercase
  letter-spacing 2px; card h3 1.3rem; body line-height 1.6.
- **Buttons:** pill (`border-radius: 50px`), 1rem 2rem padding, bold
  uppercase 0.9rem letter-spacing 1px; hover lifts (`translateY(-3px)`)
  + shadow.
- **Cards:** white, border-radius 15px, shadow
  `0 10px 20px rgba(0,0,0,0.1)`; hover `translateY(-10px)` +
  `0 15px 30px rgba(0,0,0,0.2)`; trip card images/iframe height 250px
  (video iframe 725px), blog images 200px, `object-fit: cover`.
- **Grids:** `repeat(auto-fit, minmax(300px, 1fr))` with 2rem gap.
- **Sections:** 6rem vertical padding, 2rem horizontal.
- **Header:** fixed; content wrapper max-width 1200px.
- **Modal:** overlay rgba(0,0,0,.8), white rounded 15px panel,
  title 2em, description margin 20px 0 30px.
- **Responsive (≤768px):** nav links collapse into absolute dropdown
  under header (toggled by hamburger), hero text shrinks, filter row
  wraps.
- **Motion:** 0.3s ease transitions on colors/lifts; smooth-scroll
  behavior via `scrollIntoView({behavior:"smooth"})`.
- Site is Spanish-only (an ES/EN toggle was built and deleted; do not
  rebuild it).

## Data model (masakali.json)

```json
{
  "heroTitle": "...", "heroSubtitle": "...",
  "baliTitle": "...", "baliDescription": "...",
  "indiaTitle": "...", "indiaDescription": "...",
  "vietnamTitle": "...", "vietnamDescription": "...",
  "azoresTitle": "...", "azoresDescription": "...",
  "aboutTitle": "...", "aboutDescription": "...",
  "blogPosts": [
    { "postImage": "url", "postTitle": "...", "postExcerpt": "...",
      "postContent": "...", "postDate": "..." }
  ],
  "workshopTitle": ["...", "..."],
  "workshopDescription": ["...", "..."],
  "workshopLocation": ["...", "..."]
}
```

Mavo quirk: repeated simple properties serialize as parallel arrays
(workshops); collections of objects use object arrays (blogPosts). If
a single post object ever contains arrays of scalars, that is Mavo's
malformed serialization — split into one object per post.

## External APIs / services (by name)

- **Mavo** (get.mavo.io): `mavo.css`, `mavo.js`, plugins: `tinymce`;
  attributes `mv-app`, `mv-storage` (GitHub URL), `mv-plugins`,
  `mv-bar="no-login"`, `class="mv-autoedit"`, `property`, `mv-list`,
  `mv-list-item`, `mv-item-bar`. Reads/writes `masakali.json` + image
  uploads into `images/` via the GitHub API (requires the editor to be
  logged in to GitHub in-browser).
- **form-wrapper** (web.celeritytechconsulting.com/form-wrapper.js):
  custom element `<form-wrapper data-form-id="Masa Kali contact-bde060">`
  intercepts submit and delivers field data by `name`.
- **YouTube** embeds: the four video IDs listed in Phase 2.
- **GitHub Pages**: static hosting of repo root; `CNAME` claims
  masakaliwildexperience.com.

## Acceptance criteria

1. `python3 -m http.server` + open `index.html`: page renders fully
   offline-of-CMS (Mavo hydrates copy from masakali.json via GitHub;
   without login it still renders the stored data).
2. All copy (hero, four trips, about, blog) matches `masakali.json`
   values; editing the JSON and reloading changes the page.
3. Filter buttons hide/show trip cards by destination.
4. "Más información" opens the modal with the right trip; "Reservar
   ahora" writes `Reserva tu viaje a <title>` into the contact form's
   Message field, closes the modal, and scrolls to the form.
5. Contact form submits through form-wrapper (fields carry name,
   email, message); no custom submit handler exists.
6. ≤768px: hamburger menu opens/closes; nav links scroll smoothly.
7. Talleres section present in markup but not visible.
8. Blog "Leer más" opens the reading modal with image, title, content.
9. No video binaries in the working tree; videos play from YouTube.
10. Push to `main` deploys to https://masakaliwildexperience.com.
11. Logged-in GitHub user can edit any underlined property inline
    (Mavo autoedit) and save commits `masakali.json`.
12. `python3 -m json.tool masakali.json` passes.
