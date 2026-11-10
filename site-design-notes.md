# Ely José Couto's website: design notes and handoff

A record of how the site is built, why it looks the way it does, and what's still open. Written so it can be handed to another chat or designer as context.

---

## The site in one paragraph

A small, hand-written static site (HTML + one `style.css`, no framework) for Ely José Couto, a Portuguese writer of horror, weird fiction and occasional SFF. The main audience is **literary agents and editors**: the site exists to present the novels, especially *It Crawls Under Your Skin*, which is seeking representation. It should feel **amateur-ish but polished**: made by a person, not a template or an AI, with some of Ely's personality showing through at a modest professional level. It should also hint at the writing itself: **philosophical, terrifying, a little macabre, with dry humor**.

## Pages

| File | What it is |
|---|---|
| `index.html` | Home: handwritten name + portrait, genre tagline, short bio, novels shelf, latest short stories, about link, socials |
| `novels.html` | Both novels with covers, genre lines and status |
| `it-crawls-under-your-skin.html` | Book page: cover beside title, query-style blurb, comps, details, excerpt panel |
| `short-stories.html` | Compact list of stories, genres hanging in the left margin on wide screens, poems section |
| `about.html` | Biography with large round portrait, current projects, contact, socials with Ely's rant |
| `style.css` | Everything visual |
| `assets/img/hand/name.svg` | Ely's handwritten name with skulls and a little hanged figure |

Covers live in `assets/img/covers/`, the photo at `assets/img/photo.jpeg`.

---

## Design decisions (and why)

### Layout
- **One centered column on every page** (46rem wide). Header, content and footer share the same edges. An earlier version hung section labels in the left margin, which made the whole page look pushed to one side. Removing that fixed the "not centered on widescreen" problem for good.
- **The one exception:** on the short stories page, genres hang in the left margin on wide screens (64rem and up), baseline-aligned with each title using a grid. The text column itself stays centered. Ely specifically liked this.
- **Section headings sit above their sections**, not in the margin.
- **Home page has no divider lines**, only space, to reduce clutter. Other pages keep thin rules between sections. The line under the header was removed sitewide. The footer keeps its line because it closes the page.

### Typography
- **Font:** Spectral (Google Fonts), with Palatino/Georgia fallbacks.
- **Body:** 17px on laptops and up. It was 18px and felt too large on a laptop.
- **Small text** (meta lines, genres, footer, shelf) uses weight 400 instead of 300 so it doesn't go faint.
- **Section headings:** italic, 1.35rem, in a dark oxblood (`--rust`). Ely liked the italics and darker colors of the original site.
- **Header nav links:** 16px, solid ink, current page in the red accent and underlined.

### Color palette
Moved away from the warm cream + terracotta look, which reads as a stock "tasteful literary" template. Now colder, with a sparing dried-blood accent.

| Variable | Light | Dark | Used for |
|---|---|---|---|
| `--paper` | `#E4E2DA` bone grey | `#131414` charcoal | background |
| `--ink` | `#16191A` | `#E2E0D9` | text |
| `--muted` | `#5B5F5C` | `#999B95` | meta, genres, captions |
| `--rule` | `#C8C6BC` | `#2D2F2E` | lines |
| `--bruise` | `#7A1C17` dried blood | `#C8685C` | accent: status, link underlines, hovers |
| `--bruise-soft` | `#D8D6CC` | `#1E2020` | tinted panels |
| `--rust` | `#4E1714` oxblood | `#D08A7E` | section headings |

**Rule: keep the red rare.** It marks status ("Seeking representation") and interaction, nothing decorative.

The site follows the visitor's device setting (light/dark). Ely's devices are in dark mode, so he mainly sees the dark version. Making the site dark-only was discussed but not decided.

### Home page
- Handwritten name large beside the round portrait, then the tagline: *Horror, Weird Fiction, & Occasional Detours into SFF*.
- One bio paragraph only. The "Be welcome, Agents and Editors!" line lives at the top of the Novels section, where it's actionable.
- **Novels shelf:** two compact tinted panels side by side (stacked on phones), small cover + title + genre line + status. Chosen over big bordered cards, which took too much space.
- Short stories and About are compact single blocks. Socials are just three links in a row; the rant paragraph lives only on the about page.

### Book page
- Cover (10rem) beside the title, genre line and status, vertically centered. An earlier version had a huge cover with the title stuck at the bottom, which looked broken on laptops.
- **Excerpt** sits in a tinted panel, with "From *It Crawls Under Your Skin*" right-aligned at the bottom, like an epigraph attribution.

### Short stories page
- Compact, scannable list: small genre, smaller title, short summary, tiny publication line and link.
- Links read "you may find it here" (Ely's wording, kept on purpose). Behind the scenes they carry an `aria-label` with the story title, and dates are wrapped in `<time>` tags.

---

## The handwritten name

### What's there
Ely drew his name on a Samsung Tab S6 with the S Pen and exported it as SVG. It includes three small skulls and a hanged figure, which suit the tone perfectly.

### How it was prepared
- The app exported a **white background rectangle** behind the drawing. It was removed, along with ~60 empty groups.
- The canvas was **cropped** to the drawing (viewBox `37 220 1828 793`, ratio about 2.3 : 1).

### How it's used
- **Home page:** large, beside the portrait, as the `<h1>`.
- **Header on every page:** small, as the logo (7.5rem wide, 6.5rem on phones, left-aligned above the nav on mobile).
- It's a plain `<img>` with `alt="Ely José Couto"`, so screen readers and search engines still get the name.

### Colors
The drawing is black. CSS filters tint it:

- **Dark mode:** cream, via `invert(0.88) sepia(0.5) brightness(0.9)`.
- **Light mode:** stays near-black.
- **Hover (header only):** red in both modes. Light: `invert(0.22) sepia(1) saturate(6) hue-rotate(-38deg) brightness(0.72)`. Dark: `invert(0.5) sepia(1) saturate(2.6) hue-rotate(-38deg) brightness(0.82)`.

### Why not a CSS mask?
The first version used the SVG as a CSS mask so it could take any color directly. It **showed nothing** when the pages were opened from a local folder (browsers block masks on `file://`), and some hosts can block it too. The plain image plus filters works everywhere. Don't switch back to the mask approach.

### Known limitation
At header size, the thin strokes (hat, skulls) get delicate. A possible improvement is a **second drawing just for the header**: only the name, no skulls, thicker stroke.

---

## Making more handwriting

**Apps on the Tab S6:**
- **Infinite Design:** vector, exports SVG directly. Probably the best fit.
- **Concepts:** vector, pen-friendly. SVG export may be a paid feature on Android.
- **Any drawing app + Inkscape:** export a high-res PNG, then in Inkscape on a computer use *Path → Trace Bitmap*.

Free tiers and features change, so check current versions.

**Drawing tips:**
- Write big, one pen at one size, black on transparent.
- Write each piece several times and keep the most natural one.
- Make sure the app doesn't export a background rectangle (or remove it).

**Where handwriting should and shouldn't go:**
- **Yes:** the name (done), a signature at the end of the bio, maybe the favicon or one tiny margin note.
- **No:** nav links and novel titles. Nav needs to be instantly readable and work with screen readers, zoom and translation. Agents copy and search titles, and the covers already carry their designed look.
- Rule of thumb: three or four handwritten touches across the whole site, maximum.

**Adding a new piece:** save it in `assets/img/hand/`, use a plain `<img>` with alt text, and copy the filter rules from `.hand-name` for the cream/red colors.

**A full handwriting font** (via Calligraphr, then converted to WOFF2) is possible but only worth it for many changing notes. Never use it for body text.

---

## Ely's preferences (learned along the way)

- Wants it **not to look AI-generated or templated**. Amateur-ish, hand-made, but polished.
- Likes **italics**, **darker colors**, and **the genre hanging in the margin** on the short stories page.
- Dislikes **clutter** and **too much space**; asked for spacing to stay moderate when removing lines.
- Wants **links clearly visible**: dark and underlined.
- Keeps his own voice in the copy ("snoop Ely's full bio", "genre slash genre", "playlists curated by Apollo himself"). **Don't polish the wording away.**
- Uses a laptop and a phone, both in dark mode, plus a Samsung Tab S6 for drawing.

---

## Open ideas and to-dos

**Content to fill in**
- *Synthesis of Flesh*: add a one-line hook on the home shelf (there's an HTML comment marking the spot). When it gets its own page, point its links there.
- Covers and portrait: confirm the image files are in place.

**Ideas suggested but not yet done**
- **An epigraph on the home page:** one short, disquieting line from Ely's own fiction (the beetle's-eye line from the excerpt is a candidate). Tells an agent what reading him feels like in five seconds.
- **The eye motif** from the *It Crawls Under Your Skin* cover as favicon and the single ornament on the site.
- **Link the playlists** mentioned on the novels page ("curated by Apollo himself").
- **Handwritten signature** at the end of the bio.
- **A footer line in Ely's voice** (currently reading/writing).
- **Margin notes** in his voice on the short stories page, using the same hanging device as the genres.
- **One small, deliberate wrongness:** e.g. story titles turning blood-red on hover. Easy to miss, never in the way of reading. Avoid glitch effects and blood fonts.
- **Dark-only site:** suits the tone; undecided.
- **Open Graph tags** so shared links show a cover and description.
- On the book page, the details list repeats genre and status; could become a single contact line.
- Short stories metadata wording is inconsistent ("SF Horror" vs "Science fiction | Philosophy", different date formats). Ely chose to keep the visible text as is.

**Rejected on purpose**
- A full-screen intro on mobile with an arrow to scroll to the novels. It hides the most important content behind a tap and looks like a template.
- A hamburger menu on mobile. The three links fit on one line.
- Handwritten nav links or novel titles (see above).
