# AGENTS.md - Bilgisayar Ağları Hugo Site

## Project Overview

Bu proje, Bilgisayar Ağları ders notları için oluşturulmuş bir Hugo statik sitesidir. Türkçe içerik barındırır ve `hugo-theme-relearn` temasını kullanır.

## Build Commands

### Development
```bash
hugo server -D          # Development server with drafts
hugo server --disableFastRender  # Live reload with full render
```

### Production
```bash
hugo                    # Production build
hugo --minify           # Minified output
```

### Testing
```bash
hugo --check            # Check for broken links
hugo -D                 # Draft pages included
```

### Linting
```bash
# No built-in linter - manually verify:
# - Markdown syntax
# - Frontmatter completeness
# - Link validity
```

## Code Style Guidelines

### Frontmatter Format
```yaml
+++
title = "Bölüm Başlığı"
type = "chapter"        # chapter, page
weight = 1
+++

# Markdown İçerik
```

### File Organization
```
content/
├── BilgisayarAglari/          # Main chapter folder
│   ├── _index.md             # Chapter index (required)
│   ├── 01-Konu/index.md      # Each topic as folder with index.md
│   ├── 02-Konu/index.md
│   └── images/               # Chapter-specific images
```

### Naming Conventions
- **Folders**: 2-digit prefix (01-, 02-) for ordering + descriptive name
- **Files**: `index.md` for each section
- **Images**: B00-, B01- prefix pattern (e.g., B03-OSI_Katmanlar.png)

### Markdown Guidelines
- Use Turkish headings
- Prefer `++++` for frontmatter delimiter (not `---`)
- Use Relearn theme shortcodes: `???`, `>`, `![]()`
- Mathematical content: use `$$...$$` for block, `\(...\)` for inline

### Image Paths
```markdown
![Description](./images/filename.png){ width=300 }
```
Place images in chapter's `images/` folder or `content/BilgisayarAglari/images/`

### Content Types
- `type = "chapter"` - Main section container
- `type = "page"` - Regular content page (default)

### Link Syntax
- Internal: `[Link Text](path/to/page/)`
- External: `[Link Text](https://example.com)`
- Anchors: `[Link Text](#anchor-id)`

## Project Configuration

### hugo.toml Key Settings
```toml
baseURL = 'https://example.org/'
locale = 'tr-TR'
title = 'Ders Notları'
theme = 'hugo-theme-relearn'
[markup.goldmark.extensions.passthrough]
  enable = true  # For math rendering
```

### Math Support
- Enabled via Goldmark passthrough
- Use `$$...$$` for display math
- Use `\(...\)` for inline math
- KaTeX/MathJax handled by theme

## Development Workflow

### Adding New Content
1. Create folder under `content/BilgisayarAglari/XX-Konu/`
2. Add `index.md` with frontmatter
3. Add images to `images/` subfolder
4. Verify with `hugo server -D`

### Frontmatter Checklist
- [ ] title (required)
- [ ] type (chapter/page)
- [ ] weight (for ordering)

### Common Issues
- **Missing _index.md**: Each chapter folder needs `_index.md`
- **Image not found**: Check relative path from content file
- **Math not rendering**: Ensure `passthrough` enabled in config

## Important Notes

- This is a static documentation site - no JavaScript/Python tests
- Content is Turkish - maintain language consistency
- Images are heavy - optimize before adding
- Use semantic HTML in custom templates if needed

## Relearn Theme Shortcodes

```markdown
??? note "Başlık"     # note, tip, warning, danger, abstract, info
    İçerik buraya
{{</* icon name="github" */>}}
{{</* button href="/link" */>}}Metin{{</* /button */>}}
```

## Git Workflow

- Commit messages: Turkish for content, English for config changes
- Branch strategy: `main` for production, `draft/*` for work in progress

## Troubleshooting

- Theme not found: `hugo mod get -u`
- Port in use: `hugo server --port 1314`
- Missing navigation: Ensure `_index.md` exists in each folder

## Image Guidelines

### Formats
- PNG for diagrams/screenshots
- SVG for vector graphics
- JPG for photos

### Naming
- Prefix: B## (B01, B02, ...)
- Descriptive: B03-OSI_Katmanlar.png

### Optimization
- PNG: Use optipng or similar
- Photos: Compress to <200KB
- Max dimension: 1920px width