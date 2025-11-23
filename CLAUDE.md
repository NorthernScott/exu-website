# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a MkDocs-based campaign website for a D&D campaign set in the Exandria setting (Critical Role universe). The site documents world information, player characters, NPCs, and session notes using the Material for MkDocs theme.

## Repository Structure

The repository has two parallel content directories:

- **`docs/`**: Public-facing content published to the website
  - `blog/`: Session recaps published as blog posts (uses MkDocs blog plugin)
  - `the-party/`: Player character profiles and bios
  - `npcs/`: Non-player character profiles
  - `world/`: World-building content including locations, factions, and religion
  - `assets/`: Images, stylesheets (`extra.css`), and scripts (`mathjax.js`)
  - Root-level pages: `index.md`, `ground-rules.md`, `house-rules.md`

- **`dm-docs/`**: Private DM notes NOT published to the website
  - Session planning notes (`session-1.md`, `session-2.md`, etc.)
  - Plot hooks, adventure outlines, and campaign planning materials

- **`templates/`**: Templates for creating new content
  - `npc.md`: Template for NPC profiles
  - `session-notes.md`: Template for session recap blog posts

## Common Commands

### Development Server

```bash
mkdocs serve
```

Starts the development server at `http://127.0.0.1:8000` with live reload.

### Build Site

```bash
mkdocs build
```

Generates static site in `site/` directory.

### Deploy to GitHub Pages

```bash
mkdocs gh-deploy
```

Builds and pushes to the `gh-pages` branch.

### Package Management

This project uses `uv` for Python package management (requires Python 3.13+):

```bash
uv sync          # Install/sync dependencies
uv add <package> # Add a new dependency
```

## Content Conventions

### Frontmatter Structure

All markdown files use YAML frontmatter with consistent fields:

```yaml
---
title: Page Title
date created: Sunday, April 13th 2025, 10:19:29 pm
date modified: Saturday, May 24th 2025, 1:27:00 pm
aliases: [alternative-names]
tags: [relevant, tags]
references:
---
```

### Blog Posts

Blog posts in `docs/blog/posts/` require additional frontmatter:

```yaml
---
title: Session 0
authors: [NorthernScott]
categories: [Sessions]
date: 2025-04-13
draft: true  # Remove when ready to publish
links: [Ground-Rules.md, House-Rules.md]
---
```

Use `<!-- more -->` to mark the excerpt boundary.

### Character/NPC Profiles

Follow the template structure with sections for:
- Summary table (for PCs)
- Role (for NPCs)
- Appearance (with image using `![Name|400](path){ width=400, align=right }`)
- Personality
- Relationships table (for PCs)
- Spoiler sections using `> [!DANGER]- Spoilers` callout

### Internal Linking

- Use relative paths: `[The Party](the-party/index.md)`
- Cross-reference related pages in frontmatter `references:` field
- Link to NPCs, locations, deities using relative paths

## MkDocs Configuration Notes

### Theme Features

The Material theme is configured with:
- Dark/light mode toggle (respects system preference)
- Teal primary color, amber accent
- Navigation path breadcrumbs (`navigation.path`)
- Automatic header hiding on scroll (`header.autohide`)
- Search with suggestions and highlighting
- TOC follows scroll position (`toc.follow`)

### Enabled Plugins

- `blog`: Powers the session recap blog with RSS feed
- `rss`: Generates RSS feed from blog posts
- `callouts`: Obsidian-style callouts (e.g., `> [!DANGER]- Spoilers`)
- `glightbox`: Image lightbox functionality
- `minify`: Minifies HTML output
- `privacy`: Privacy-compliant external resource handling
- `search`: Full-text search

### Markdown Extensions

Notably configured extensions:
- `pymdownx.superfences`: Supports Mermaid diagrams
- `pymdownx.tabbed`: Tabbed content blocks
- `pymdownx.emoji`: Material Design emoji (`:fontawesome-solid-icon:`)
- `pymdownx.arithmatex`: LaTeX math support with MathJax
- `pymdownx.highlight`: Syntax highlighting with line numbers

## Architecture Notes

### DM vs Public Content Separation

**Critical:** The `dm-docs/` directory is NOT included in `mkdocs.yml`'s `docs_dir` setting. Only content in `docs/` is built and published. When working with session notes:
- DM planning notes go in `dm-docs/session-N.md`
- Public session recaps go in `docs/blog/posts/session-N.md`

### Asset Management

Images should be placed in `docs/assets/images/` and referenced using relative paths. Character images use right-aligned formatting with width constraints.

### Validation Settings

MkDocs is configured with validation warnings (not errors) for:
- Omitted files
- Absolute links
- Unrecognized links
- Anchor references

Check build output for validation warnings when adding/modifying content.

## Critical Role / Exandria Context

This campaign is set in the **Exandria** setting (Critical Role universe) in **845 PD** (Post-Divergence), two years after the Apogee Solstice events. The campaign takes place primarily on the **Menagerie Coast**, starting in **Nicodranas**.

When creating content:
- Respect established Critical Role canon for locations, deities, and factions
- The Critical Role wiki is referenced in world documentation: `https://criticalrole.fandom.com/wiki/`
- Campaign uses standard D&D 5e rules with house rules documented in `docs/house-rules.md`
