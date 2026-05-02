---
inclusion: auto
---

# Site Technical Conventions

## Technology
- **Static site generator**: Jekyll
- **Theme**: Minima (with `skin: auto`)
- **Hosting**: GitHub Pages at elenavanengelenmaslova.github.io
- **CSS**: Sass (compressed for production)
- **Markdown**: Kramdown with Rouge syntax highlighting
- **Analytics**: Google Analytics (G-LN4HKRGKZG)

## File Structure
- Pages: `*.markdown` files in root (index, portfolio, speaking, training, credentials)
- Training detail pages: `training/*.md`
- Layouts: `_layouts/` (uses Minima defaults)
- Includes: `_includes/` (header, footer, head, social, google-analytics)
- Assets: `assets/images/` for images, `assets/minima-social-icons.svg` for social icons
- Config: `_config.yml`

## Navigation
Defined in `_config.yml` under `header_pages`:
- Portfolio
- Training
- Speaking
- Credentials
- Blog (external link to Medium, added in header.html)

## Content Guidelines
- All content changes should maintain the professional but approachable tone
- Pages use `layout: page`, homepage uses `layout: home`
- Contact email: elenavanengelen@vintik.nl
- Social links: LinkedIn, GitHub, Mastodon, X (Twitter)
- External links open in new tabs with `target="_blank" rel="noopener"`

## When Modifying the Site
- Keep changes compatible with GitHub Pages supported Jekyll plugins
- Supported plugins: jekyll-sitemap, jekyll-seo-tag
- Custom styling should go in `assets/main.scss` or inline styles (theme constraints)
- Test that responsive/mobile layout still works
- Preserve existing SEO setup (jekyll-seo-tag, sitemap)
- Maintain accessibility: semantic HTML, alt text on images, proper heading hierarchy
- The theme may be changed from Minima to a more modern theme (e.g., Minimal Mistakes or custom CSS overrides) — ensure GitHub Pages compatibility
- User wants to review the site visually at each milestone using `bundle exec jekyll serve`
- All changes must be locally testable before committing
