# AGENTS.md

Operating instructions for AI agents (Framer AI, MCP clients) working in this project.
Read this file before making changes. It describes the conventions, structure, and
guardrails specific to **this** project. For a human-oriented overview, see `README.md`.

---

## Project type

A single-author portfolio / creative-agency website built in Framer. It is content-light
and design-heavy: most pages are composed from reusable components, CMS collections, and
a shared design-token system. Treat visual consistency as the top priority — this is a
template-quality site where spacing, type, and color discipline matter more than raw output.

## Golden rules

1. **Always call `getProjectXml` first** at the start of a session to load current
   structure, available attributes, and pre-built section components. Structure below may
   drift over time; the live project is the source of truth.
2. **Reuse before you create.** This project already has ~60 components. Before building
   anything new, check the component list and prefer inserting/configuring an existing one.
3. **Never hardcode colors or fonts on text or frames.** Use the project's color styles
   (e.g. `/Dark 10`, `/Orange 60`) and text styles (e.g. `/Heading 1`, `/Body`). To change
   text color you MUST go through a text style — inline color on text nodes is not allowed.
4. **Insert sections under the root Desktop breakpoint** of a page, never inside another
   component, so responsive breakpoints are preserved.
5. **Make changes incrementally.** Call `updateXmlForNode` with small XML fragments, one
   logical change per call, so edits stream into the canvas and stay reviewable. Do not
   batch the whole tree into one giant update.
6. **Don't touch credentials.** The MCP connection secret must never be written into a file,
   component, or committed anywhere. If you encounter one, flag it for rotation.

## Design tokens (use these — do not invent values)

**Color styles**
- Neutrals: `/Dark 2`, `/Dark 10`, `/Dark 30`, `/Dark 50`, `/Light 80`, `/Light 90`,
  `/Light 98`, `/White 100`
- Accent: `/Orange 60` — `rgb(255, 85, 51)`. This is the single brand accent; use sparingly
  for emphasis (CTAs, highlights), not for body surfaces.

**Text styles**
- Display headings use **Clash Display Medium**: `/Heading 1` (48), `/Heading 2` (48),
  `/Heading 2 Small` (32), `/Heading 3` (32), `/Heading 3 Small` (24).
- Body / UI use **Inter Display**: `/Heading 4`, `/Body`, `/Subheadline`, `/Name`, `/Role`,
  `/Button`, `/Span`, `/Span Italic`, `/Quotes`.
- Pricing has dedicated styles: `/Price Desktop` (96), `/Price Mobile` (60),
  `/$ Sign Desktop`, `/$ Sign Mobile`.
- A text node uses EITHER a text style (`inlineTextStyle`) OR a raw `font` — never both.

## Page map

Published web pages:

| Path | Purpose |
|------|---------|
| `/` | Home |
| `/about` | About |
| `/services` | Services |
| `/projects` + `/projects/:slug` | Project index + CMS detail |
| `/insights` + `/insights/:slug` | Blog index + CMS detail |
| `/testimonials` | Testimonials |
| `/faq` | FAQ |
| `/contact` | Contact |
| `/legal/:slug` | CMS legal pages |
| `/404` | Not-found |

`:slug` pages are CMS-driven detail templates — edits there affect every collection item.
Design explorations live on the `Design` design page and are not published.

## Component conventions

- Section-level components (`Hero`, `Services`, `Pricing`, `FAQ Section`, `Testimonials`,
  `Process`, `Insights`, `CTA Section`, `Footer`, `Featured Projects`) are the building
  blocks of pages. Compose pages from these rather than from primitives.
- Card components (`Project Card`, `Service Card`, `Blog Card`, `Client Card`,
  `Testimonial Crad`, `Award Card`, `Education Card`, `Price Card`, `Process Card`) are
  meant to be repeated inside their parent sections.
- Primitives / utilities: `Button`, `Link`, `Span`, `Logo`, `Number`, `Counter`, `Ticker`,
  `Cursor`, `Dotted Line(s)`, `Plus-Minus`, `Graphic Element`.
- **Linked vs detached:** insert components linked by default so they track the source. Only
  add `?detached=true` when you genuinely need to edit a component's internal structure;
  after detaching, re-read the parent with `getNodeXml` to see the generated layers.
- Known typos in component names (`Testimonial Crad`, `Blog Crad`-style) exist in the live
  project — match them exactly when referencing by name; do not "fix" them unless asked, as
  renaming can break instances.

## Code files

React/TypeScript code components live under `Workshop/`:
`NumberCounter.tsx`, `JackpotText.tsx`, `FitTextEffect.tsx`.
Before creating or editing any Framer code file, read the MCP resource
`mcp://mcp.unframer.co/prompts/how-to-write-framer-code-files.md` first — Framer code files
have specific constraints (property controls, exports) that differ from plain React.

## Working with images

To use an external/local image as a `backgroundImage`, upload it first and use the returned
URL. Do not paste large base64 blobs into XML.

## What to confirm with the human first

- Deleting pages, components, or CMS collections.
- Renaming components (breaks existing instances).
- Changing global color or text styles (cascades site-wide).
- Anything that alters a `:slug` detail template (affects all items).

## Definition of done

A change is complete when: it reuses existing tokens and components, renders correctly on
the Desktop breakpoint, respects the type/color system, and has been verified by re-reading
the affected node with `getNodeXml`.
