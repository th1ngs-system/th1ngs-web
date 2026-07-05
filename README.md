# th1ngs-web

The Th1ngs marketing site — an [Eleventy](https://www.11ty.dev/) (11ty) static site, published to **th1ngs.com**.

## Development

```sh
npm install
npm run start   # eleventy --serve --port=8080
# or
npm run build    # outputs to _site/
```

## Site structure

| Route | Source | Layout | Description |
|---|---|---|---|
| `/` | `src/index.njk` | `base.njk` | Marketing homepage — hero, features, workflows, integrations, CTA, and the site's single contact form (`#contact`). |
| `/features/<name>/` | `src/features/*/index.njk` | `base.njk` | One page per homepage feature: `boxes`, `things`, `relations`, `custom-fields`, `workflows`, `plugins`, `ai-mcp`. Linked from the homepage's feature cards. |
| `/boxes/` | `src/boxes/index.njk` | `base.njk` | Overview grid of every Box Type available in the product (kept in sync with the running app's `/admin/boxtypes` list), plus a "Custom" card. |
| `/boxes/<name>/` | `src/boxes/*/index.njk` | `base.njk` | One page per real Box Type (Agile Software Development, Project Management, Waterfall Software Management, Service Management, Mailbox, Th1ngs-ware, Core, Cards, Places, Photo, Wiki) plus `/boxes/custom/` for building a Box Type from scratch. |
| `/docs/` | `src/docs/index.njk` | `docs-base.njk` | Product documentation (Getting Started, Core Concepts, Boxes, Things, Custom Fields, Workflows, Email, REST API, AI/MCP) — single page with in-page section switching. |
| `/docs/subscribe/` | `src/docs/subscribe/index.njk` | `docs-base.njk` | Newsletter signup (Brevo). |
| `/docs/jira-migration/` | `src/docs/jira-migration/index.njk` | `docs-base.njk` | Jira Cloud → Th1ngs migration gap analysis (unlinked, direct-URL only). |
| `/about/` | `src/about/index.njk` | `base.njk` | About Us — mission, team, placeholder copy. |

All of `src/docs/*` used to live in a separate repo (`th1ngs-doc`, published at `doc.th1ngs.com`) and was migrated into this repo so documentation ships from the same site as the marketing pages. `doc.th1ngs.com`'s auto-deploy has been disabled; that repo is being retired.

Box Types (`/boxes/`) previously lived under `/docs/box-types/` with hand-written per-type detail pages for only 3 types (Mailbox, Stuff, Service Desk). That content was replaced with per-type pages sourced from the actual running app's admin panel (`/admin/boxtypes`) rather than stale docs, covering all real Box Types plus a `/boxes/custom/` page for building one from scratch.

## Contact

There is exactly **one** contact form on the whole site: the `#contact` section at the bottom of the homepage (`src/index.njk`), posting to Formspree. Every "Contact" nav link, floating contact button, and "Get Started"/"Get in touch" CTA across the site — on marketing pages, docs pages, feature pages, and box pages — links to `/#contact` rather than duplicating the form. There used to also be a popup contact modal and a separate `/docs/contact/` page; both were removed in favor of this single form.

## Templates

- **`_includes/base.njk`** — layout for standalone marketing-style pages (home, About Us, Boxes, Features, Box Type pages). Includes the shared nav and the site footer.
- **`_includes/docs-base.njk`** — layout for the `/docs/*` section. Adds the sidebar navigation and doc-specific footer around the shared nav.
- **`_includes/nav.njk`** — the top nav bar, shared by both layouts (Product / Boxes / Documentation / About Us / Contact). "Contact" always links to `/#contact`.

## Stylesheets

- **`css/styles.css`** — marketing site styles (hero, feature grid, integrations, CTA, contact form) and the shared top-nav styles.
- **`css/docs-layout.css`** — `/docs/*` sidebar layout, typography, tables, callouts. Shares the same top-nav class names as `styles.css` (kept visually identical) since only one of the two files loads per page.
- **`css/th1ngs-docs.css`** — remaining `/docs/*`-only bits: doc footer, subscribe form, floating contact button.

Because `docs-layout.css`/`th1ngs-docs.css` and `styles.css` are never loaded on the same page, some class names (e.g. `.feat-grid`, `.hier`) are intentionally reused with different rules across the two stylesheet sets without conflict.

## Analytics

Google Analytics (`gtag.js`, `G-2S96NTD4J5`) is wired into both `base.njk` and `docs-base.njk`, so every page on the site is tracked.

## Links in the page

- `https://th1ngs.com` — the live product/app (Try demo site, Get Started, REST API/MCP base URL).
- `/#contact` — the site's single contact form, used as the nav's Contact link and every "Get Started"/"Get in touch" CTA everywhere on the site.
