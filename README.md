# Portfolio Website (Framer)

A single-author portfolio / creative-agency website built in [Framer](https://framer.com).
Design-driven and component-based, with CMS-backed projects, insights, and legal pages.

> Working on this project with an AI agent (Framer AI or an MCP client)? Read
> [`AGENTS.md`](./AGENTS.md) — it documents the conventions and guardrails the agent
> should follow.

---

## Overview

The site is composed almost entirely from reusable components layered on top of a shared
design-token system (color styles + text styles). Pages are assembled from section-level
components rather than one-off layouts, which keeps spacing, typography, and color
consistent across the whole site.

- **Type system:** Clash Display (Medium) for display headings, Inter Display for body/UI.
- **Color:** a neutral dark/light scale plus a single brand accent, orange `rgb(255, 85, 51)`.
- **Content:** projects, insights/blog, and legal pages are CMS-driven via `:slug` templates.

## Pages

| Path | Description |
|------|-------------|
| `/` | Home |
| `/about` | About the author |
| `/services` | Services offered |
| `/projects` | Project index |
| `/projects/:slug` | Project detail (CMS) |
| `/insights` | Insights / blog index |
| `/insights/:slug` | Article detail (CMS) |
| `/testimonials` | Client testimonials |
| `/faq` | Frequently asked questions |
| `/contact` | Contact / inquiry |
| `/legal/:slug` | Legal pages (CMS) |
| `/404` | Not-found page |

A non-published `Design` page holds design explorations and prototypes.

## Structure

**Sections** — the main page building blocks:
Hero · Services · Process · Pricing · FAQ Section · Testimonials · Featured Projects ·
Insights · CTA Section · Footer

**Cards** — repeated inside sections:
Project Card · Service Card · Blog Card · Client Card · Testimonial · Award Card ·
Education Card · Price Card · Process Card

**Primitives & utilities:**
Button · Link · Logo · Span · Number · Counter · Ticker · Cursor · Dotted Lines ·
Plus-Minus · Graphic Element · Menu / Nav · Newsletter Form · Inquiry Form

**Code components** (`Workshop/`):
`NumberCounter.tsx`, `JackpotText.tsx`, `FitTextEffect.tsx`

## Design tokens

**Color styles:** `/Dark 2`, `/Dark 10`, `/Dark 30`, `/Dark 50`, `/Light 80`, `/Light 90`,
`/Light 98`, `/White 100`, `/Orange 60`.

**Text styles:** `/Heading 1`–`/Heading 4` (plus Small variants), `/Body`, `/Subheadline`,
`/Name`, `/Role`, `/Button`, `/Span`, `/Span Italic`, `/Quotes`, `/Logo`, and pricing styles
(`/Price Desktop`, `/Price Mobile`, `/$ Sign Desktop`, `/$ Sign Mobile`).

When editing, always reference these styles rather than hardcoding values, so changes stay
consistent and update site-wide.

## Editing

This project can be edited directly in the Framer app, or programmatically through the
Framer MCP server (used by Framer AI and compatible AI clients). The MCP connection lets an
agent read the project structure and make changes to pages and components.

> **Security note:** the MCP connection URL includes a secret token. Never commit it, paste
> it into files, or share it. If it has been exposed, regenerate it from Framer's MCP
> settings.

## License / usage

Add your license and usage terms here.
