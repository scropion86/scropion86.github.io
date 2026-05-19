# Kopi Theme - Author Profiles Setup Guide

Complete guide for setting up author profiles with avatars in the Kopi theme.

## Table of Contents

- [Overview](#overview)
- [Creating Author Profiles](#creating-author-profiles)
- [Avatar Setup](#avatar-setup)
- [Using Authors in Posts](#using-authors-in-posts)
- [Customization](#customization)

---

## Overview

Authors are defined as individual content pages in the `content/authors/` directory. Each author profile includes:
- Display name and bio
- Avatar image (optional)
- Role/title
- Detailed biography
- Automatic listing of all articles they've written

---

## Creating Author Profiles

### File Location

Create author profiles in: `content/authors/`

Filename format: `content/authors/first-last.md` (lowercase with hyphens)

### File Structure

Create a file like `content/authors/jane-smith.md`:

```markdown
---
title: "Jane Smith"
date: 2026-05-18T00:00:00Z
role: "Senior Engineer"
avatar_local: "/images/authors/jane-smith.png"
avatar: "https://example.com/avatars/jane-smith.png"
bio: "Jane specializes in cloud infrastructure and DevOps automation."
exclude_recent: false
---

## About Jane

Jane has over 10 years of experience in cloud infrastructure and DevOps. She's passionate about automation, scalability, and building reliable systems.

### Expertise

- Kubernetes and container orchestration
- Infrastructure as Code (Terraform, CloudFormation)
- CI/CD pipelines
- Monitoring and observability

### Interests

When not working on infrastructure, Jane enjoys rock climbing and photography.
```

### Required Front Matter Fields

| Field | Type | Description |
|-------|------|-------------|
| `title` | string | Author's display name (must match author references in posts exactly) |
| `date` | datetime | Creation date (ISO 8601 format) |
| `role` | string | Job title/role (e.g., "Contributor", "Senior Engineer", "Lead Developer") |
| `bio` | string | Short biography (1-2 sentences, appears on profile and posts) |

### Optional Front Matter Fields

| Field | Type | Description |
|-------|------|-------------|
| `avatar_local` | string | Path to local avatar: `/images/authors/{filename}.png` |
| `avatar` | string | URL to external avatar (fallback if local doesn't exist) |
| `exclude_recent` | boolean | Set to `true` to hide from "Recent Authors" sections |

---

## Avatar Setup

### Avatar Specifications

- **Format:** PNG or JPG
- **Size:** 256×256px (square)
- **Location:** `static/images/authors/`
- **Filename:** Lowercase with hyphens (e.g., `jane-smith.png`)
- **File size:** < 100KB recommended

### Avatar Fallback Priority

The system automatically displays avatars in this order:

1. **Local avatar** (`avatar_local` in frontmatter)
   - Path: `/images/authors/{filename}.png`
   - Recommended for production (fast, self-hosted)

2. **External avatar** (`avatar` in frontmatter)
   - Full URL to external image (e.g., CDN, Gravatar)
   - Used as fallback if local avatar not found

3. **No avatar**
   - If neither local nor external avatar provided
   - Theme displays a CSS gradient placeholder

### Step-by-Step: Adding an Avatar

1. **Prepare your image:**
   ```bash
   # Resize to 256x256 using ImageMagick
   convert original.jpg -resize 256x256 -quality 85 jane-smith.png
   ```

2. **Save to static folder:**
   ```
   exampleSite/static/images/authors/jane-smith.png
   ```

3. **Update author frontmatter:**
   ```yaml
   avatar_local: "/images/authors/jane-smith.png"
   avatar: "https://fallback-url-here.png"
   ```

4. **Verify:**
   - Run `hugo server`
   - Visit author profile page
   - Avatar should display with circular border

---

## Using Authors in Posts

### Linking Authors in Post Front Matter

In your post's front matter, reference authors by their exact `title`:

#### Single Author

```yaml
---
title: "My Blog Post"
date: 2026-05-15T10:00:00Z
author: "Jane Smith"
---
```

#### Multiple Authors

```yaml
---
title: "Collaborative Article"
date: 2026-05-15T10:00:00Z
authors:
  - "Jane Smith"
  - "John Doe"
---
```

### Important: Exact Name Matching

- Author `title` field must match **exactly** (case-sensitive)
- Example: If author file has `title: "Jane Smith"`, post must use `author: "Jane Smith"`
- URL slug is auto-generated: `Jane Smith` → `/authors/jane-smith/`

---

## Author Profile Page

### What Appears on Author Pages

When someone visits `/authors/jane-smith/`, they see:

1. **Author Header**
   - Avatar (circular, with border)
   - Name
   - Role/Title
   - Short bio

2. **Full Biography**
   - All content from the markdown file body
   - Formatted sections (headings, lists, links, etc.)

3. **Articles Grid**
   - All posts authored by this person
   - Card-based layout
   - Hover effects for better UX

### Customizing Author Page Layout

The author profile template is at: `layouts/authors/single.html`

To customize:
1. Copy to `layouts/authors/single.html` in your site root
2. Edit the template as needed
3. Theme will use your custom version instead

---

## Best Practices

1. **Use consistent author names** - Exactly match post and author file titles
2. **Provide local avatars** - Faster than external URLs, works offline
3. **Keep external URL as fallback** - Useful for migration or recovery
4. **Use descriptive bios** - 50-100 characters recommended
5. **Add detailed content** - Author markdown body can include expertise, interests, etc.
6. **Test before publishing** - Run `hugo server` and check author pages
7. **Optimize images** - Compress avatars to reduce file size
8. **Follow naming conventions** - Use lowercase filenames with hyphens

---

## Troubleshooting

### Avatar not displaying

**Check:**
1. File exists: `static/images/authors/jane-smith.png`
2. Filename matches frontmatter path (case-sensitive on Linux)
3. `avatar_local` path is correct: `/images/authors/jane-smith.png`
4. Image dimensions are 256×256px

**Solution:**
```bash
# Verify file exists
ls -la exampleSite/static/images/authors/

# Clear Hugo cache
hugo mod clean

# Restart server
hugo server
```

### Author page not found

**Check:**
1. Author file location: `content/authors/first-last.md`
2. Frontmatter `title` matches exactly in posts
3. Hugo generated the page: check terminal output during `hugo server`

**Solution:**
```bash
# Check for errors
hugo server -D

# Verify author file
cat content/authors/jane-smith.md
```

### Author name not matching in posts

**Check:**
1. Post `author` field matches frontmatter `title` exactly
2. Case-sensitive: `"Jane Smith"` ≠ `"jane smith"`
3. No extra spaces or special characters

**Solution:**
```yaml
# Author file
title: "Jane Smith"

# Post file - must match exactly
author: "Jane Smith"  # ✓ Correct
author: "jane smith"  # ✗ Won't match
```

### Multiple authors not showing

**Check:**
```yaml
# Use array syntax for multiple authors
authors:
  - "Jane Smith"    # ✓ Correct
  - "John Doe"

author:
  - "Jane Smith"    # ✗ Wrong (this is `author`, not `authors`)
```

---

## Example: Complete Setup

### 1. Create Author File

**File:** `content/authors/jane-smith.md`

```markdown
---
title: "Jane Smith"
date: 2026-05-18T00:00:00Z
role: "Senior DevOps Engineer"
avatar_local: "/images/authors/jane-smith.png"
avatar: "https://example.com/jane.png"
bio: "Cloud infrastructure specialist with 10+ years of experience."
---

## Background

Jane started her career as a systems administrator and has evolved into a cloud architect.

## Expertise

- Kubernetes
- Terraform
- AWS and GCP
- CI/CD pipelines
```

### 2. Add Avatar Image

```bash
# Place image at
exampleSite/static/images/authors/jane-smith.png
```

### 3. Reference in Post

**File:** `content/blog/k8s-guide.md`

```markdown
---
title: "Kubernetes Best Practices"
date: 2026-05-15T10:00:00Z
author: "Jane Smith"
---

Great Kubernetes guide content...
```

### 4. Test Locally

```bash
hugo server
# Visit: http://localhost:1313/authors/jane-smith/
```

---

## Next Steps

- [Content Creation Guide](CONTENT.md) - Learn how to write posts
- [Setup & Development](SETUP.md) - Configure the theme
- [Contributing](../CONTRIBUTING.md) - Help improve the theme
