# Portfolio design

This document is the source of truth for how the site looks and how each section is arranged. Implementation copies these rules into `globals.css` and the React components.

The Google Doc changes words, lists, and links. It does not change color, type, spacing, or layout. A new project added in the doc appears in the existing card layout. It does not introduce a new visual style.

## Intent

The site is a dark editorial portfolio mixed with a minimal engineering product page. A visitor should understand who Nandini is, what she builds, and where to read the work, without scrolling through a résumé template.

The page should feel quiet, precise, and spacious. Large type carries the hierarchy. Color is used in small amounts. Surfaces are charcoal, not pure black. Borders are thin. Motion is short and only supports reading.

Avoid these patterns:

- A skill section made of dozens of technology icons.
- Pure black backgrounds and neon glow.
- Heavy gradients, glassmorphism, or animated blobs.
- Identical boxed cards with drop shadows stacked down the page.
- A photo-header résumé, progress bars, or percentage skill meters.
- More than one loud accent color in the same view.

Palette A, Midnight Lavender, is the only theme. It is distinctive without becoming colorful.

## Color

Use the tokens below everywhere. Do not introduce one-off hex values in components.

| Token | Hex | Role |
| --- | --- | --- |
| `--bg` | `#111116` | Page background. Deep charcoal with a slight violet cast. |
| `--surface` | `#1C1C25` | Cards, timeline panels, and the mobile menu. |
| `--text` | `#F4F1FA` | Headings and body copy. Warm off-white, not pure white. |
| `--muted` | `#A39EB2` | Secondary copy, meta labels, durations, and nav links at rest. |
| `--primary` | `#A78BFA` | Links, focus, the active nav item, and small highlights. |
| `--accent` | `#8BE9C1` | Availability, a live-demo hint, and rare secondary highlights. |
| `--border` | `rgba(244, 241, 250, 0.10)` | 1px dividers, card edges, and the navbar hairline. |
| `--primary-soft` | `rgba(167, 139, 250, 0.14)` | Chip backgrounds and the focus ring fill. |
| `--accent-soft` | `rgba(139, 233, 193, 0.12)` | The availability pill background. |

Primary lavender is for interaction and emphasis: text links, the focused control, and a short rule under a section kicker. It is not a fill for large buttons or hero backgrounds.

Mint is rarer than lavender. Use it for the availability status and, when a project has a live demo, a small "Live" label. Do not use it for body links.

Text on the charcoal background stays `--text`. Muted text stays readable; do not drop it below the contrast of `#A39EB2` on `#111116`.

Hover states shift a link or border toward `--primary`. They do not invert the whole card to a bright fill.

## Typography

Two families only.

- **Geist** for interface and body: navigation, buttons, paragraphs, chips, metadata.
- **Instrument Serif** for display: the hero name and the large section titles. Regular weight (400). Italic is reserved for a single short phrase in the hero tagline if the layout needs a pause. Do not set body copy in the serif.

Load both with `next/font` so the page does not wait on a third-party stylesheet.

| Style | Face | Size | Weight | Tracking | Line height | Use |
| --- | --- | --- | --- | --- | --- | --- |
| Hero name | Instrument Serif | `clamp(3.25rem, 8vw, 6.5rem)` | 400 | `-0.03em` | `0.95` | "Nandini Amaravadi" |
| Section title | Instrument Serif | `clamp(2.25rem, 4vw, 3.5rem)` | 400 | `-0.02em` | `1.05` | About, Work, Experience, and the rest |
| Kicker | Geist | `0.75rem` | 500 | `0.16em` | `1` | Uppercase labels such as "Portfolio 2026" |
| Body | Geist | `1.0625rem` | 400 | `0` | `1.7` | Paragraphs. Max width about `65ch`. |
| Card title | Geist | `1.25rem` | 500 | `-0.01em` | `1.3` | Project and job titles |
| Meta | Geist | `0.875rem` | 400 | `0` | `1.5` | Roles, dates, locations, link rows |

Kickers are uppercase and colored `--muted`, except the availability kicker, which uses `--accent`.

Do not center long paragraphs. Hero and section titles are left-aligned. The only centered element allowed is a short footer line.

## Layout

The page is one column of content with a sticky navbar.

- Content max width: `72rem` (1152px).
- Horizontal padding: `1.25rem` on small screens, `2rem` from `768px` up. The max width is in addition to that padding.
- Section padding: `4.5rem` vertical on small screens, `7rem` from `1024px` up.
- Gap between a section title and its content: `2.5rem` on small screens, `3.5rem` from `1024px` up.
- Navbar height: `4rem`. It stays fixed to the top. The page content clears it.

The navbar background is `--bg` at 80% opacity with a backdrop blur, plus a `--border` hairline along the bottom. The wordmark on the left is "Nandini" in Geist, medium weight. Links on the right: About, Work, Experience, Skills, Contact. The current section is `--primary`. Others are `--muted` and turn `--text` on hover.

On viewports below `768px`, the links collapse into a single menu button. The open menu is a `--surface` panel under the navbar, full width, with the same links stacked. No animated overlay beyond a short fade.

Homepage order, top to bottom:

1. Hero
2. About
3. Featured projects
4. Experience
5. Skills
6. Achievements
7. Contact

Section ids match the navbar: `about`, `work`, `experience`, `skills`, `contact`. Achievements sits between Skills and Contact and is reached by scrolling, not by its own nav item, so the bar stays short.

## Breakpoints

| Name | Width | Behavior |
| --- | --- | --- |
| Small | under `768px` | Single column. Hero actions stack. Project cards stack. Timeline is full width. Nav becomes a menu. |
| Medium | `768px` to `1023px` | Project cards in two columns. About stays one column. Timeline stays one column. |
| Large | `1024px` and up | Full editorial layout. Hero can split the headline from the location and availability block. Project grid stays two columns so cards remain wide enough to read. |

Do not introduce a third card column. Wide cards read better than a dense grid.

## Sections

### Hero

The first screen tells a visitor who she is and what she does. It fills at least the viewport below the navbar.

Content, in this order:

- Kicker: `PORTFOLIO 2026`
- Name, display size: Nandini Amaravadi
- Tagline, one sentence, body size or slightly larger: "Building software that solves real problems."
- Roles, meta size, separated by a middle dot: Software Engineer · Full Stack Developer · AI Enthusiast
- Two actions: "Explore my work" (jumps to `#work`) and "Download resume" (uses the resume URL)
- A quiet status row: an availability pill, then the location

The availability pill uses `--accent-soft` background, `--accent` text, and a 6px dot. Example: "Available for opportunities". Location sits beside it in `--muted`, for example "Hyderabad, India". On small screens the status row wraps under the actions.

There is no portrait, no social icon row, and no background illustration in the hero. Social links live in Contact.

### About

A short editorial column, not a two-column biography with a photo.

- Kicker: `About`
- Section title in Instrument Serif
- Two or three paragraphs from the doc, constrained to about `65ch`
- No cards inside this section

If the doc provides a single introduction block, render it as consecutive paragraphs split on blank lines.

### Featured projects

This is the main section of the page.

- Kicker: `Work`
- Section title, for example "Selected projects"
- A short one-line intro in `--muted`, optional
- Cards for projects marked featured. If none are marked, show all projects.

Each card contains:

- Project name
- One-paragraph summary
- Technology chips
- A text link to the detail page
- GitHub and live-demo links when those URLs exist

Cards use `--surface`, a 1px `--border`, and `1rem` corner radius. Padding is `1.5rem` on small screens and `1.75rem` from `768px` up. No drop shadow.

The card title links to `/projects/[slug]`. The whole card is not a single link, so GitHub and the live demo remain separate actions.

Show at most the summary on the homepage. Problem, solution, architecture, and challenges belong on the detail page.

Example cards the layout must fit:

- Verbatim — AI knowledge assistant. Python, LangGraph, RAG, Whisper.
- FlexPay — EMI e-commerce. React, NestJS, MongoDB.
- Diagnostic Booking Service — booking and payments. FastAPI, PostgreSQL, SQLAlchemy.
- ConneX — same card pattern, whatever summary and stack the doc provides.

### Experience

A vertical timeline, one job after another, most recent first.

Each entry:

- Company and title
- Duration and location in `--muted`
- Responsibilities as a short list
- Achievements as a short list, only when the doc has them

The timeline rail is a 1px `--border` line. Each node is an 8px circle, `--primary` for the latest role and `--border` for older roles. Text sits to the right of the rail with `1.5rem` of space. On small screens the rail stays, with slightly tighter padding.

Do not use company logos.

### Skills

Named groups, not an icon wall.

- Kicker: `Skills`
- Section title
- One group per category from the doc: Programming languages, Frontend, Backend, Databases, AI / ML, Tools
- The category name is Geist medium, `--text`
- Skills inside a category are quiet chips or a single wrapping line of meta text separated by middle dots

Prefer a wrapping line of text when a category has many items. Use chips when a category has a short list. Do not mix both styles inside one category. Default to the wrapping line so the section stays calm.

### Achievements

A quiet list, visually lighter than projects.

- Kicker: `Achievements`
- Section title
- Groups from the doc, such as LeetCode, GFG, Certifications, and Awards
- Each group is a label plus its items as plain lines

No trophies, badge images, or progress rings.

### Contact

Links only. No form in this version.

- Kicker: `Contact`
- Section title, for example "Let's talk"
- One sentence of invitation in body text
- A row of text links: Email, LinkedIn, GitHub, Resume
- Each link uses the primary text-link style and a small Lucide icon (mail, linkedin, github, file-down) at 16px, aligned with the cap height

The footer under Contact repeats the name and a short line, "Portfolio 2026", in meta size and `--muted`.

## Project detail page

Route: `/projects/[slug]`, with the slug derived from the project title (`Verbatim` becomes `verbatim`).

The page uses the same navbar, background, type, and content width as the homepage. It is not a modal.

Content, in this order:

- A text link back to `/#work`: "Back to work"
- Kicker with the first few technologies, or "Project" if the stack is empty
- Title in the section-title size (Instrument Serif)
- Summary paragraph
- Technology chips
- GitHub and live-demo links in the same row treatment as the card
- Stacked blocks, only when the field is non-empty: Problem, Solution, Architecture, Challenges
- Challenges render as a list. The other blocks render as paragraphs.

A missing URL hides that link. It does not render an empty button. An unknown slug renders the normal not-found page in the same palette.

## Components

### Text link

Geist, `--text` by default, `--primary` on hover. An arrow (`ArrowUpRight`) follows external links and "Explore my work". Underline appears on hover only, offset by `3px`. Focus uses the focus ring below.

### Actions

Two kinds, both low-chrome:

- **Primary action.** Text link with an arrow. Used for "Explore my work".
- **Secondary action.** Text plus a 1px `--border` pill, transparent background, `--text` label. Hover border becomes `--primary`. Used for "Download resume".

Do not use filled lavender or mint buttons.

### Chips

Inline, `--primary-soft` background, `--text` label, meta size, `999px` radius, `0.25rem 0.6rem` padding. They are not links.

### Cards

`--surface` background, 1px `--border`, `1rem` radius. Hover lifts the border color toward `rgba(167, 139, 250, 0.45)` over `200ms`. The card does not scale or lift on the y-axis.

### Timeline node

8px circle, absolutely centered on the rail. Latest item uses `--primary`. Older items use a hollow circle with a 1px `--border`.

### Focus ring

Every interactive element: `2px` solid `--primary`, `2px` offset, offset color `--bg`. The ring replaces the browser default. It must be visible on `--bg` and on `--surface`.

### Icons

Lucide only, stroke width `1.5`. Use icons for nav menu, external links, GitHub, LinkedIn, mail, and resume. Do not decorate headings with icons.

## Motion

Motion explains hierarchy. It is not decoration.

- On first enter, a section's title and content fade from opacity `0` to `1` and rise `12px`, over `600ms`, with an ease-out curve.
- Cards in a grid stagger by `80ms`, capped so the last card never waits more than `320ms`.
- Hover transitions on links, borders, and the menu are `200ms`.
- Nothing loops. No parallax. No scroll-jacking.
- Animate once, when the block first enters the viewport.

When `prefers-reduced-motion: reduce` is set, skip the rise and the fade. Show content immediately. Keep color and border hovers instant.

## Content and design

| Owned by the Google Doc | Owned by this document and the components |
| --- | --- |
| Name, role, tagline, introduction, location, availability, resume URL | Color, type, spacing, navbar, hero composition |
| About copy | The single reading column |
| Skill groups and skill names | Group layout and chip or text treatment |
| Jobs, dates, responsibilities, achievements | Timeline |
| Project fields and URLs | Card grid and the detail page |
| Contact URLs | Link row and footer |

Empty optional fields are omitted. The layout does not collapse into a different design when a field is missing; the block simply is not rendered.

Images inside the Google Doc are ignored. If a project later needs a visual, it is a normal image URL or a file in `public/images`, displayed inside the existing card radius with no new frame style.
