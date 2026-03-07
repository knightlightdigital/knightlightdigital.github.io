# AGENTS.md - Project Guide for AI Coding Agents

> This file contains essential information for AI coding agents working on this project.
> Last updated: 2026-03-07

---

## Project Overview

This is **KLD Blog**, a personal blog built with [Jekyll](https://jekyllrb.com/) using the [Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy/) theme (v7.4.1). The blog is authored by David Knighton and covers topics including AI, vibe-coding, Scrum mastering, and general commentary.

- **Site URL**: https://blog.knightlight.digital
- **Repository**: https://github.com/knightlightdigital/knightlightdigital.github.io
- **Language**: English (`lang: en`)
- **License**: MIT

### What is Chirpy Starter?

This project is based on the [chirpy-starter](https://github.com/cotes2020/chirpy-starter) template, which provides a ready-to-use Jekyll site with the Chirpy theme. The theme files themselves are installed as a Ruby gem (`jekyll-theme-chirpy`), while user-customizable files (config, plugins, tabs) are included in this repository.

---

## Technology Stack

| Component | Technology | Version |
|-----------|------------|---------|
| Static Site Generator | Jekyll | 4.4.x |
| Theme | jekyll-theme-chirpy | ~> 7.4 |
| Language | Ruby | 3.3 |
| Package Manager | Bundler | 2.6.x |
| Testing | html-proofer | ~> 5.0 |
| Deployment | GitHub Pages | - |

### Key Gems & Plugins

- `jekyll-archives` - Archive pages for categories and tags
- `jekyll-include-cache` - Performance optimization
- `jekyll-paginate` - Pagination support
- `jekyll-seo-tag` - SEO meta tags
- `jekyll-sitemap` - XML sitemap generation
- `rouge` - Syntax highlighting

---

## Project Structure

```
.
├── _config.yml              # Main Jekyll configuration
├── _data/
│   ├── contact.yml          # Contact/social link configuration
│   └── share.yml            # Social sharing button configuration
├── _plugins/
│   └── posts-lastmod-hook.rb # Custom plugin: Sets last_modified_at from git history
├── _posts/
│   └── .placeholder         # Blog posts directory (Markdown files)
├── _tabs/
│   ├── about.md             # About page
│   ├── archives.md          # Archives page
│   ├── categories.md        # Categories listing
│   └── tags.md              # Tags listing
├── _site/                   # Generated site (build output, gitignored)
├── assets/
│   ├── img/                 # Image assets
│   └── lib/                 # Library assets
├── tools/
│   ├── run.sh               # Local development server script
│   └── test.sh              # Build and test script
├── .github/workflows/
│   └── pages-deploy.yml     # GitHub Actions deployment workflow
├── .devcontainer/           # VSCode DevContainer configuration
├── .vscode/                 # VSCode settings and tasks
├── Gemfile                  # Ruby dependencies
└── index.html               # Homepage (uses 'home' layout)
```

### Directory Details

- **`_posts/`** - Blog posts in Markdown format. Filenames must follow `YYYY-MM-DD-title.md` format. Posts use YAML front matter with `title`, `date`, `categories`, `tags`, etc.
- **`_tabs/`** - Static pages displayed in the sidebar navigation. Each has `icon` and `order` in front matter.
- **`_data/`** - YAML data files accessed via `site.data` in templates.
- **`_plugins/`** - Custom Ruby plugins extending Jekyll functionality.

---

## Build and Development Commands

### Prerequisites

- Ruby 3.3+
- Bundler (`gem install bundler`)
- Node.js (optional, for asset building if needed)

### Install Dependencies

```bash
bundle install
```

### Local Development Server

```bash
# Default: Development mode with live reload
./tools/run.sh

# Bind to specific host
./tools/run.sh -H 0.0.0.0

# Production mode
./tools/run.sh -p
```

The server starts at `http://127.0.0.1:4000` by default with live reload enabled.

### Build for Production

```bash
# Build only
JEKYLL_ENV=production bundle exec jekyll build

# Build and test
./tools/test.sh

# Use custom config
./tools/test.sh -c "_config.yml,_config.local.yml"
```

### Testing

The project uses `html-proofer` to validate the generated HTML:

```bash
bundle exec htmlproofer _site \
  --disable-external \
  --ignore-urls "/^http:\/\/127.0.0.1/,/^http:\/\/0.0.0.0/,/^http:\/\/localhost/"
```

---

## Deployment

### GitHub Pages (Production)

Deployment is automated via GitHub Actions (`.github/workflows/pages-deploy.yml`):

1. **Trigger**: Push to `main` or `master` branch
2. **Build**: Jekyll builds the site with `JEKYLL_ENV=production`
3. **Test**: HTMLProofer validates the output
4. **Deploy**: Uploads to GitHub Pages using `actions/deploy-pages`

Manual deployment can be triggered from the Actions tab.

### Build Output

- Generated site is placed in `_site/` directory
- This directory is gitignored and should never be committed

---

## Configuration Reference

### Key `_config.yml` Settings

| Setting | Value | Description |
|---------|-------|-------------|
| `theme` | `jekyll-theme-chirpy` | Jekyll theme |
| `title` | `KLD Blog` | Site title |
| `tagline` | `Various thoughts and rants` | Subtitle |
| `url` | `https://blog.knightlight.digital` | Site URL |
| `baseurl` | `""` | Subpath (empty for root) |
| `lang` | `en` | Language code |
| `timezone` | - | Timezone (empty = use system) |
| `paginate` | `10` | Posts per page |
| `toc` | `true` | Table of contents (global) |
| `pwa.enabled` | `true` | Progressive Web App support |
| `pwa.cache.enabled` | `true` | Offline caching |

### Social/Author Settings

```yaml
social:
  name: David Knighton
  email: david@knightlight.digital
  links:
    - https://github.com/knightlightdigital
```

### Permalink Structure

- Posts: `/posts/:title/`
- Tabs: `/:title/`
- Categories: `/categories/:name/`
- Tags: `/tags/:name/`

---

## Code Style Guidelines

### Markdown (Posts and Pages)

- Use YAML front matter for metadata
- Categories and tags should be lowercase, hyphen-separated
- Use `<!--more-->` for post excerpts
- Images should use relative paths or be in `assets/img/`

### File Naming Conventions

- **Posts**: `YYYY-MM-DD-title.md` (e.g., `2024-01-15-my-post.md`)
- **Drafts**: Place in `_drafts/` (no date prefix required)
- **Images**: Use descriptive names, lowercase, hyphen-separated

### Front Matter Template (Posts)

```yaml
---
title: "Post Title"
date: YYYY-MM-DD HH:MM:SS +/-TTTT
categories: [category1, category2]
tags: [tag1, tag2, tag3]
# Optional:
image: /path/to/image.png  # Featured image
pin: true                  # Pin to top
math: true                 # Enable math rendering
mermaid: true              # Enable mermaid diagrams
---
```

---

## Development Environment

### VSCode Setup

Recommended extensions (auto-suggested):
- `killalau.vscode-liquid-snippets` - Liquid snippets
- `Shopify.theme-check-vscode` - Liquid formatting
- `yzhang.markdown-all-in-one` - Markdown support
- `esbenp.prettier-vscode` - General formatting

### DevContainer

A development container is configured (`.devcontainer/`):

```bash
# Open in VSCode with DevContainer support
# Or use: Remote-Containers: Reopen in Container
```

Base image: `mcr.microsoft.com/devcontainers/jekyll:2-bullseye`

### Git Workflow

- Main branch: `main` (or `master`)
- All pushes to main trigger deployment
- Use feature branches for changes

---

## Testing Instructions

### Before Committing

1. Build the site locally: `./tools/test.sh`
2. Check for HTML errors (handled by html-proofer)
3. Verify no broken internal links
4. Review changes in browser at `http://127.0.0.1:4000`

### Content Testing Checklist

- [ ] Post renders without errors
- [ ] Images load correctly
- [ ] Links are valid
- [ ] Categories and tags pages update
- [ ] Mobile responsiveness (use browser dev tools)

---

## Security Considerations

- No sensitive data in repository
- GitHub Pages serves static content only
- Comments are disabled (no Disqus/utterances/giscus configured)
- Analytics IDs should be kept private if added

---

## Custom Plugins

### `_plugins/posts-lastmod-hook.rb`

This plugin automatically sets `last_modified_at` for posts based on git commit history:

- Reads git log for each post file
- Sets `last_modified_at` to the last commit date
- Only applies if file has more than 1 commit

---

## External Documentation

- **Chirpy Theme Docs**: https://github.com/cotes2020/jekyll-theme-chirpy/wiki
- **Jekyll Docs**: https://jekyllrb.com/docs/
- **Liquid Syntax**: https://shopify.github.io/liquid/
- **Kramdown Syntax**: https://kramdown.gettalong.org/syntax.html

---

## Troubleshooting

### Common Issues

**Bundle install fails**
- Ensure Ruby 3.3+ is installed
- Run `bundle update` if lockfile is outdated

**Build warnings**
- Check for missing front matter
- Verify image paths are correct

**Changes not reflecting**
- Jekyll has live reload, but some config changes require restart
- Clear `.jekyll-cache/` if issues persist

---

*For questions about this project, refer to the main Chirpy theme repository or Jekyll documentation.*
