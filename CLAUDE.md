# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the **Th1ngs** marketing/landing page — a static single-page website with no build step, no framework, and no dependencies beyond CDN-loaded Bootstrap 5.3.

## Structure

- `index.html` — the entire site: navbar, hero section, feature columns, footer
- `th1ngs-logo.png` — brand logo used in the navbar

## Development

Open `index.html` directly in a browser, or serve it with any static file server:

```sh
python3 -m http.server 8080
# or
npx serve .
```

## Stack

- **Bootstrap 5.3** (CSS + JS via CDN)
- **Bootstrap Icons 1.11** (via CDN)
- No build pipeline, no package.json, no tests

## Links in the page

- `/login` and `/signup` — linked but not present in this repo (handled elsewhere)
- `https://doc.th1ngs.com` — external documentation site
