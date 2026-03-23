# Shabash Site — Claude Context

## What This Is

A Hugo-based marketing/landing site for **Shabash**, a family chore tracker app. "Shabash" means "Well Done" in Urdu. The site is deployed at `https://info.shabashkids.online/` via GitHub Pages.

---

## Development Commands

```bash
# Development (runs TailwindCSS watcher + Hugo server concurrently)
npm start
# → Hugo dev server at http://localhost:1313

# Production build (minifies CSS + Hugo output into /public/)
npm run build
```

> CSS is **not** processed by Hugo pipelines — TailwindCSS runs as a separate CLI step and outputs to `static/css/style.css`. Do not try to move CSS processing into Hugo assets.

---

## Tech Stack

| Layer | Tool |
|---|---|
| Static site generator | Hugo (Extended, v0.80+) |
| Theme | `hugo-saasify-theme` (git submodule) |
| CSS framework | TailwindCSS 3.x + PostCSS + Autoprefixer |
| Plugins | @tailwindcss/forms, @tailwindcss/typography |
| Task runner | npm scripts + `concurrently` |
| Deployment | GitHub Actions → GitHub Pages (`gh-pages` branch) |

---

## Project Structure

```
shabash-site/
├── hugo.toml                    # Hugo config (base URL, menus, params)
├── tailwind.config.js           # TailwindCSS config (extends theme preset)
├── postcss.config.js            # PostCSS (tailwindcss + autoprefixer)
├── package.json                 # npm scripts and deps
│
├── content/                     # All site pages (Markdown + YAML frontmatter)
│   ├── _index.md                # Homepage — uses shortcodes heavily
│   ├── company.md               # "Why We Built Shabash" story
│   ├── features/
│   │   ├── chores.md
│   │   ├── rewards.md
│   │   └── safety.md            # layout: simple (no sidebar/newsletter)
│   ├── docs/
│   │   ├── _index.md            # Docs landing
│   │   ├── getting-started.md
│   │   └── faq.md
│   └── [signin, signup, privacy, terms, license].md
│
├── assets/css/main.css          # CSS source — TailwindCSS directives + custom components
├── static/css/style.css         # Compiled CSS output (do not hand-edit)
├── static/images/               # Logos, favicons, feature graphics, screenshots
│
├── layouts/
│   └── partials/footer.html    # Custom footer override (replaces theme default)
│
└── themes/hugo-saasify-theme/  # Git submodule — do not edit directly
    └── layouts/
        ├── _default/            # baseof, single, list, simple, company, feature
        ├── shortcodes/          # 21 pre-built shortcodes
        ├── partials/            # header, footer, CTA, sidebar, analytics
        └── docs/                # Docs layout with auto sidebar
```

---

## Content & Layouts

### Available Layouts (set via `layout:` in frontmatter)

| Layout | Use Case |
|---|---|
| `single` (default) | Standard content page |
| `simple` | Stripped-down — no sidebar, no newsletter (used for safety.md) |
| `company` | Company story page with special formatting |
| `feature` | Feature description pages |
| `docs` | Documentation with auto-generated sidebar |
| `pricing` | Pricing page |

### Homepage Shortcodes Pattern

The homepage (`content/_index.md`) is built entirely from shortcodes:
```
{{< hero ... >}}
{{< section-container >}}
  {{< benefits-grid ... >}}
  {{< features-section >}}
    {{< feature ... >}}
  {{< /features-section >}}
  {{< testimonials ... >}}
  {{< cta >}}
{{< /section-container >}}
```

All 21 shortcodes live in `themes/hugo-saasify-theme/layouts/shortcodes/`.

---

## CSS Architecture

- **Source:** `assets/css/main.css` — edit this for custom styles
- **Output:** `static/css/style.css` — auto-generated, do not edit manually
- **Fonts:** Inter (body), Plus Jakarta Sans (headings) — loaded via theme
- **Colors:** Indigo-to-purple gradient for CTAs; standard Tailwind grays elsewhere
- **Custom classes defined in main.css:** `.btn`, `.btn-primary`, `.btn-secondary`, `.btn-outline`, `.cta-section`, `.cta-gradient`, `.card`, `.section`, `.container`, `.nav-link`, `.feature-grid`

After editing `assets/css/main.css`, run `npm start` (or the build command) to recompile `static/css/style.css`.

---

## Hugo Configuration Highlights

Key `hugo.toml` settings to be aware of:

- **baseURL:** `https://info.shabashkids.online/`
- **Blog:** disabled (`blog.enabled = false`)
- **Markup:** Unsafe HTML enabled in Goldmark (allows raw HTML in Markdown)
- **Build stats:** `hugo_stats.json` is generated for TailwindCSS JIT — this file is in `.gitignore` and regenerated on each build
- **Menu items:** Defined in `[menus]` section — Features, Docs, Safety, Support, Sign In, Get Started
- **Footer menus:** Three columns configured in params

---

## Theme Submodule

The theme is a git submodule at `themes/hugo-saasify-theme`.

- **Do not edit theme files directly** — changes will be lost on submodule updates.
- Override layouts by creating matching files under `layouts/` in the project root.
- The custom footer at `layouts/partials/footer.html` overrides the theme's footer.

To update the theme:
```bash
git submodule update --remote themes/hugo-saasify-theme
```

---

## Deployment

GitHub Actions workflow (`.github/workflows/deploy.yml`):
1. Triggered on push to `main`
2. Runs `npm ci` → `npm run build`
3. Ensures `CNAME` file exists in `public/`
4. Deploys `public/` to `gh-pages` branch → served at `info.shabashkids.online`

The `public/` directory is gitignored and should never be committed manually.

---

## Site Content Overview

| Page | URL | Purpose |
|---|---|---|
| Homepage | / | Hero + features + testimonials + CTA |
| Company | /company/ | Founder story and mission |
| Chores | /features/chores/ | Feature: chore tracking |
| Rewards | /features/rewards/ | Feature: reward system |
| Safety | /features/safety/ | Safety & privacy details |
| Getting Started | /docs/getting-started/ | User onboarding guide |
| FAQ | /docs/faq/ | Common questions |
| Sign In | /signin/ | Auth page |
| Sign Up | /signup/ | Registration page |
| Privacy | /privacy/ | Privacy policy |
| Terms | /terms/ | Terms of service |

---

## Key Files to Know

| File | Role |
|---|---|
| [hugo.toml](hugo.toml) | All Hugo configuration, menus, site params |
| [assets/css/main.css](assets/css/main.css) | CSS source — edit for style changes |
| [static/css/style.css](static/css/style.css) | Compiled CSS — do not hand-edit |
| [content/_index.md](content/_index.md) | Homepage content (shortcode-driven) |
| [layouts/partials/footer.html](layouts/partials/footer.html) | Custom footer override |
| [tailwind.config.js](tailwind.config.js) | TailwindCSS setup |
| [package.json](package.json) | Build scripts |
| [.github/workflows/deploy.yml](.github/workflows/deploy.yml) | CI/CD pipeline |
