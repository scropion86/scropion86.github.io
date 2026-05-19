# Kopi Theme - Setup & Development Guide

> **Note:** This is an enhanced version of the original [Kopi theme](https://github.com/bect/kopi) by [bect](https://github.com/bect), updated and enhanced by [scropion86](https://github.com/scropion86).

Complete guide for setting up and developing with the Kopi Hugo theme.

## Prerequisites

### Required
- **Hugo Extended** - Version 0.146.0 or higher
  - Download: [https://gohugo.io/installation/](https://gohugo.io/installation/)
  - **Important:** Must be the Extended version (supports SCSS/SASS compilation)
  - Verify installation: `hugo version`

### Optional but Recommended
- **Git** - For version control
- **VS Code** or your preferred code editor

---

## Local Setup & Testing

### 1. Clone the Repository

```bash
git clone https://github.com/bect/kopi.git
cd kopi
```

### 2. Navigate to Example Site

```bash
cd exampleSite
```

### 3. Run Hugo Locally

```bash
hugo server
```

Expected output:
```
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

### 4. View Your Site

Open your browser and navigate to:
```
http://localhost:1313/
```

The site will **auto-reload** whenever you make changes to files.

### 5. Stop the Server

Press `Ctrl+C` in your terminal to stop the local development server.

---

## Hugo Configuration

### Basic Configuration File (hugo.yaml)

```yaml
baseURL: "https://example.com/"
languageCode: "en-us"
title: "My Site"
theme: kopi

# Output formats
outputFormats:
  JSON:
    mediaType: application/json
    baseName: index
  RADIO:
    mediaType: application/json
    baseName: index

# Menu configuration
menus:
  main:
    - name: Home
      url: /
      weight: 1
    - name: Posts
      url: /infotainment/
      weight: 2
```

---

## Directory Structure

```
exampleSite/
├── assets/
│   ├── css/
│   │   ├── main.scss
│   │   └── _custom.scss
│   └── js/
├── content/
│   ├── _index.md
│   ├── about.md
│   ├── search.md
│   └── infotainment/
│       └── post-1.md
├── data/
│   └── radio.yaml
├── layouts/
├── static/
│   └── images/
├── themes/
│   └── kopi/
└── hugo.yaml
```

---

## Building for Production

When you're ready to test the production build:

```bash
hugo --gc --minify
```

This creates optimized files in the `public/` directory with:
- Minified CSS and JavaScript
- Optimized images
- Generated sitemap and RSS feeds

### Deploying to GitHub Pages

The theme supports automated GitHub Pages deployment via GitHub Actions. See your repository's workflow configuration for details.

---

## Development Tips

### Custom Styles

Add custom CSS in `assets/css/_custom.scss`:

```scss
// Your custom styles here
body {
  font-family: "Your Font", sans-serif;
}

a {
  color: #your-color;
}
```

### Partial Override

To customize a partial, copy it from `themes/kopi/layouts/` to `layouts/` in your site root, preserving the directory structure.

Example:
```
# Original
themes/kopi/layouts/_partials/header.html

# Override
layouts/_partials/header.html
```

### Adding Custom JavaScript

Place custom JS files in `assets/js/` and import them in your template.

---

## Troubleshooting

### "Hugo version too old"
- Update Hugo to the latest Extended version
- Run `hugo version` to verify
- Minimum required: v0.146.0

### SCSS compilation errors
- Ensure you're using Hugo Extended, not Standard
- Check for syntax errors in `assets/css/`
- Clear Hugo cache: `hugo mod clean`

### Theme not loading
- Verify theme directory exists: `themes/kopi/`
- Check `hugo.yaml` has `theme: kopi`
- Run `hugo` in the exampleSite directory (or use `-s exampleSite` flag)

### Changes not showing
- Clear browser cache or do a hard refresh (Ctrl+Shift+R)
- Restart `hugo server`
- Check for errors in terminal output

---

## Next Steps

- [Create content](CONTENT.md) - Learn how to write posts and manage content
- [Setup authors](AUTHORS.md) - Add author profiles with avatars
- [Contributing](../CONTRIBUTING.md) - Help improve the theme
