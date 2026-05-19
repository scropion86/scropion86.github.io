# Kopi - A Modern Hugo Theme

A high-performance Hugo theme featuring dark mode, fast navigation with Turbo.js, advanced markdown support, and built-in author profiles. Perfect for blogs, technical documentation, and content-rich websites.

## ✨ Features

- **Fast Navigation** - Turbo.js for instant page transitions
- **Dark Mode** - Beautiful dark theme with automatic detection
- **Author Profiles** - Built-in author system with avatars and bios
- **Advanced Markdown** - Support for Mermaid diagrams, code blocks, and custom shortcodes
- **Responsive Design** - Mobile-first design that works on all devices
- **Performance** - Optimized CSS/JS with minification support
- **Radio Widget** - Embedded radio player (optional)
- **Search Integration** - Built-in search functionality
- **SEO Friendly** - Proper meta tags, sitemap, and RSS feeds

## 🚀 Quick Start

### Prerequisites

- **Hugo Extended** v0.146.0 or higher
  - Download: https://gohugo.io/installation/
  - Must use the Extended version (required for SCSS compilation)

### Installation

1. **Clone or download the theme:**
   ```bash
   git clone https://github.com/bect/kopi.git
   cd kopi
   ```

2. **Setup the theme in your site:**
   ```bash
   cd exampleSite
   hugo server
   ```

3. **Visit http://localhost:1313/**

### Using Kopi in Your Project

Copy the `themes/kopi/` directory to your Hugo project:

```bash
cp -r themes/kopi /path/to/your/site/themes/
```

Then in your `hugo.yaml`:
```yaml
theme: kopi
```

## 📚 Documentation

- [Setup Guide](docs/SETUP.md) - Local development, Hugo configuration
- [Content Guide](docs/CONTENT.md) - Creating posts, managing content, front matter
- [Author Setup](docs/AUTHORS.md) - Setting up author profiles and avatars
- [Contributing](CONTRIBUTING.md) - Development workflow and contribution guidelines

## 🎨 Configuration

Basic `hugo.yaml` configuration:

```yaml
baseURL: "https://example.com/"
languageCode: "en-us"
title: "My Site"
theme: kopi
outputFormats:
  JSON:
    mediaType: application/json
    baseName: index
  RADIO:
    mediaType: application/json
    baseName: index
```

## 📄 License

This theme is licensed under the **MIT License**. See the LICENSE file for more details.

## 🙏 Credits & Acknowledgements

- **Turbo.js** - Fast navigation library (https://turbo.hotwired.dev/)
- **Mermaid.js** - Diagram rendering (https://mermaid.js.org/)
- **Hugo** - Static site generator (https://gohugo.io/)

## 🤝 Contributing

Contributions are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## 📞 Support

For issues, questions, or feature requests:
- Open an issue on GitHub
- Check existing documentation in `/docs/`
- Review the example site in `/exampleSite/` for implementation examples

---

**Made with ❤️ for the Hugo community**