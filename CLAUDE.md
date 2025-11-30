# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is an academic personal website for the Duality Lab (Jamie Davis) at Purdue ECE, built using Jekyll and the Minimal Mistakes theme. The site is hosted on GitHub Pages at https://davisjam.github.io.

## Building and Running

### Local Development

To run the site locally:

```bash
bundle install
bundle exec jekyll serve
```

For development with live reload and overrides:
```bash
bundle exec jekyll serve --config _config.yml,_config.dev.yml
```

The site will be served at `http://localhost:4000`.

### Dependencies

- Jekyll 3.9.3
- Ruby with bundler
- Minimal Mistakes Jekyll theme
- Plugins: jekyll-feed, jekyll-sitemap, hawkins

## Content Management

### Publications

Publications are managed through a custom JSON-based workflow:

1. Publications are stored in `markdown_generator/publications.json`
2. To regenerate the publications page after editing the JSON:
   ```bash
   ./regen-pubs.sh
   ```
   This script removes comment lines from the JSON and runs `markdown_generator/publications.py` to generate `auto-publications.md`

3. The JSON schema supports:
   - Publication types: journal, conference, workshop, arxiv, dissertation, patent, poster
   - Fields: title, authors, venue, year, paperBasename, slidesBasename, artifactURL, videoURL, blogURL
   - Awards: bestPaperAward, bestArtifactAward
   - Control: suppress (to hide publications)

### Site Structure

The site uses Jekyll collections:

- `_pages/`: Main pages (about, research, teaching, service, etc.)
- `_publications/`: Individual publication pages (mostly auto-generated)
- `_talks/`: Talk entries
- `_teaching/`: Teaching entries
- `_portfolio/`: Portfolio items
- `_layouts/`: Custom layouts (single, talk, archive, etc.)
- `_includes/`: Reusable components (author-profile, archive-single, etc.)
- `_sass/`: SCSS stylesheets
- `files/`: Static files like PDFs
- `images/`: Image assets

### Configuration

- `_config.yml`: Main site configuration (author info, social links, collections, Jekyll settings)
- `_config.dev.yml`: Development overrides (localhost URL, expanded CSS)
- `_data/navigation.yml`: Site navigation menu structure
- `_data/ui-text.yml`: UI text strings for internationalization

## Architecture Notes

### Custom Publication Generator

The `markdown_generator/` directory contains Python scripts and Jupyter notebooks for converting structured data (JSON/TSV) into markdown files:

- `publications.py`: Generates `auto-publications.md` from `publications.json`
- `pubsFromBib.py`: Alternative BibTeX-based generator
- `talks.py`: Generates talk pages from TSV

The publications generator creates formatted citations with icon links for PDFs, slides, code artifacts, videos, and blog posts. Publications are automatically sorted by year and grouped by type.

### Theme Customization

This is a customized fork of Minimal Mistakes. Key customizations include:

- Custom masthead image logo (`title_mastheadImage` in config)
- Modified author profile layout
- Custom talk layout for presentations
- Publication-specific formatting and icons

### Content Workflow

1. Static pages are in `_pages/` with YAML front matter
2. Publications are managed via JSON → Python script → auto-generated markdown
3. Navigation is controlled via `_data/navigation.yml`
4. Layouts in `_layouts/` define page templates
5. Includes in `_includes/` provide reusable components

## Important Files

- `_config.yml`: Site-wide configuration and metadata
- `regen-pubs.sh`: Regenerate publications page
- `markdown_generator/publications.json`: Source of truth for publications
- `auto-publications.md`: Auto-generated publications page (do not edit directly)
- `Gemfile`: Ruby dependencies
