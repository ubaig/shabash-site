# Shabash Site - Hugo Saasify Theme Setup

This is a website built using the [Hugo Saasify Theme](https://github.com/chaoming/hugo-saasify-theme), a modern and elegant Hugo theme designed for building SaaS marketing websites.

## Setup Guide

### Step 1: Initialize Git Repository
Initialize a new Git repository in your project folder:
```bash
git init
```

### Step 2: Add Theme as Git Submodule
Add the Hugo Saasify theme as a git submodule:
```bash
git submodule add https://github.com/chaoming/hugo-saasify-theme themes/hugo-saasify-theme
```
This clones the theme into the `themes/hugo-saasify-theme` directory.

### Step 3: Copy Example Site Content
Copy the example site content from the theme to your project root:
```bash
cp -r themes/hugo-saasify-theme/exampleSite/* .
```
(On Windows PowerShell: `Copy-Item -Path "themes/hugo-saasify-theme/exampleSite/*" -Destination "." -Recurse -Force`)

This includes:
- Content structure with sample pages (blog, pricing, features, careers)
- Pre-configured `hugo.toml` with the example site settings
- Multilingual support (English and Chinese)

### Step 4: Copy Dependency Configuration Files
Copy the required configuration files for npm and Tailwind CSS:
```bash
cp themes/hugo-saasify-theme/package.json .
cp themes/hugo-saasify-theme/postcss.config.js .
cp themes/hugo-saasify-theme/tailwind.config.copy.js ./tailwind.config.js
```

### Step 5: Install Dependencies
Install npm dependencies:
```bash
npm install
```

### Step 6: Configure hugo.toml
Ensure your `hugo.toml` has the correct theme setting:
```toml
theme = "hugo-saasify-theme"
```

If you encounter Git-related errors, disable Git info:
```toml
enableGitInfo = false
```

## Development

### Start Development Server
Run the development server with live reload:
```bash
npm run start
```
The site will be available at `http://localhost:1313`

### Build for Production
Build the site for production:
```bash
npm run build
```
This generates an optimized site in the `public/` directory.

## Project Structure

```
├── content/              # Page and blog content files
│   ├── _index.md        # Homepage
│   ├── blog/            # Blog posts
│   ├── features/        # Feature pages
│   ├── pricing.md       # Pricing page
│   ├── careers.md       # Careers page
│   └── zh-cn/          # Chinese translations
├── static/              # Static assets (images, fonts, etc.)
├── assets/              # CSS and styling files
├── layouts/             # Theme layout overrides
├── themes/              # Installed themes
│   └── hugo-saasify-theme/
├── archetypes/          # Content templates
├── hugo.toml            # Hugo configuration
├── package.json         # npm dependencies
├── tailwind.config.js   # Tailwind CSS configuration
└── postcss.config.js    # PostCSS configuration
```

## Features

- 🎨 Modern design with TailwindCSS
- 📱 Fully responsive layout
- 🚀 Performance optimized (90+ Lighthouse scores)
- 💅 Clean typography with Inter & Plus Jakarta Sans fonts
- 🎯 Perfect for SaaS and business websites
- 🌍 Full multilingual (i18n) support with automatic language detection
- 21 pre-built shortcodes for rapid page building
- 📚 Documentation layout with automatic sidebar navigation
- 📊 Google Analytics and Google Tag Manager support

## Configuration

Edit `hugo.toml` to customize:
- Site title and description
- Logo path
- Navigation menus
- Header and CTA settings
- Social media links
- Analytics configuration
- Language support

## Content Creation

### Adding Blog Posts
Create a new blog post:
```bash
hugo new blog/my-first-post.md
```

### Adding Pages
Create a new page:
```bash
hugo new mypage.md
```

Edit the markdown files in the `content/` directory to add your own content.

## Troubleshooting

### Shortcode Not Found
Ensure the theme is correctly referenced in `hugo.toml`:
```toml
theme = "hugo-saasify-theme"
```

### Git-related Errors
If you see "failed to load Git data", disable Git info in `hugo.toml`:
```toml
enableGitInfo = false
```

### Missing Styles
Ensure TailwindCSS is properly built by running:
```bash
npm run start
```

## Resources

- 📖 [Complete Documentation](https://github.com/chaoming/hugo-saasify-theme/blob/main/docs/README.md)
- 🎨 [Demo Site](https://saasify-demo.chaoming.li/)
- 🐛 [Report Issues](https://github.com/chaoming/hugo-saasify-theme/issues)
- 💬 [GitHub Discussions](https://github.com/chaoming/hugo-saasify-theme/discussions)

## License

This project uses the Hugo Saasify Theme which is released under the [MIT license](https://github.com/chaoming/hugo-saasify-theme/blob/main/LICENSE).
