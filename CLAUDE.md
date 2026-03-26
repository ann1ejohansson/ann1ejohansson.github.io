# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a static personal academic website for Annie Johansson (PhD Candidate, University of Amsterdam), hosted on GitHub Pages. There is no build system, framework, or package manager — it is plain HTML and CSS.

## Development

Open locally by serving files from the repo root:

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000`. No build step required; changes are visible immediately on reload. Deployment is automatic: pushing to `main` publishes to GitHub Pages.

## Design system

**Fonts:** Fraunces (serif, Google Fonts) for the name and page headings; DM Sans (sans-serif, Google Fonts) for body, nav, and meta text. Loaded via `@import` in `style.css` — no extra `<link>` tags needed in HTML (the font link tags in `<head>` are the preconnect hints only).

**Colors** (defined as CSS variables at the top of `style.css` — edit once, applies everywhere):
- `--purple: #473198` — primary accent, headings, active nav, borders
- `--cream: #F8F6F2` — page background
- `--sidebar-bg: #EFECEA` — left column background
- `--teal: #1D9FB7` — links
- `--text: #2A2A2A` — body text
- `--text-light: #777` — secondary text, meta, captions

**Key CSS classes:** `.project-container` (project/course card with left purple border), `.project-tags` + `.tag` (pill labels), `.collaborate-box` (homepage invite section), `.back-link` (small uppercase back navigation), `.read-more` (animated arrow link), `.sidebar-divider` (hr between bio and nav), `.sidebar-copyright` (pinned to sidebar bottom).

## Architecture

```
ann1ejohansson.github.io/
├── index.html                  # Homepage ("about me")
├── style.css                   # Single global stylesheet
├── images/
│   ├── profile.jpg
│   └── projects/               # One figure per project (PNG/JPEG only)
├── files/                      # PDFs: preprints, posters, slides
└── views/
    ├── projects.html           # Overview: title + abstract + "read more" per project
    ├── projects/
    │   ├── three-strikes.html  # Full project page: abstract, figure, findings, links
    │   └── irtree.html         # Full project page: abstract, figure, findings, links
    ├── publications.html
    ├── conferences.html
    └── readmore.html           # Extended PhD project description
```

## Layout pattern

Every page uses the same two-column layout:
- **Left column** (`.left-column`): sticky sidebar — profile photo, name, affiliation, email, `<nav class="vertical-menu">` navigation
- **Right column** (`.right-column`): scrollable main content

The left column is copy-pasted verbatim in every page. When updating navigation links or profile info, edit **all** HTML files.

## Path convention

- `index.html` uses **relative** paths: `style.css`, `images/profile.jpg`, `views/projects.html`
- All pages inside `views/` use **absolute** paths from root: `/style.css`, `/images/profile.jpg`, `/index.html`
- Pages inside `views/projects/` also use absolute paths from root

## Adding a new project

1. Add a figure (PNG or JPEG) to `images/projects/`
2. Add any PDFs (preprint, poster) to `files/`
3. Copy `views/projects/irtree.html` as a template, rename it, and fill in the `<!-- EDIT: -->` sections
4. Add a new `<div class="project-container">` entry in `views/projects.html` with a link to the new page

## CSS classes for project detail pages

Defined in `style.css` under the `PROJECT DETAIL PAGES` section:
- `.project-detail-title` — large page title
- `.project-detail-meta` — authors and venue line
- `.project-detail-links` — row of links (preprint · GitHub · poster)
- `.project-detail-figure` — centered figure container
- `.figure-caption` — caption text under the figure
- `.project-detail-findings` — key findings bullet list

## Keeping project pages in sync with GitHub research repos

Each research repo (e.g., `github.com/ann1ejohansson/irtree`) contains the source materials for a project. When a project is updated:
1. Update the abstract and key findings text in `views/projects/[name].html`
2. Replace the figure in `images/projects/` if needed
3. Add new PDFs to `files/` and update the links in the project detail page

No automated pipeline — manual copy from the research repo's README when content changes.

## Research repos

- `three-strikes` → project page at `/views/projects/three-strikes.html`
- `irtree` → project page at `/views/projects/irtree.html` (previously linked as `qm-trees` — now corrected)
