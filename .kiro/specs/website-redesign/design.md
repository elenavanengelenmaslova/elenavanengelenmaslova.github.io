# Design Document: Website Redesign

## Overview

This design describes the comprehensive redesign of Elena van Engelen-Maslova's freelance professional website from a CV-style Jekyll site using the default Minima theme into a modern, client-acquisition-focused site using the Minimal Mistakes theme. The redesign touches every page, restructures navigation, adds a new Open Source page, and rewrites content with sales-oriented copy — all while preserving existing SEO, analytics, third-party integrations, and GitHub Pages compatibility.

This revision repositions the site's service offering. Training is removed entirely (page, five detail pages, and `/training/` permalinks). In its place, the site presents a single **Consulting** offering built around a "deployed forward engineer" short-term model alongside long-term engagements. The site now presents two service pillars — **Consulting** (most prominent) and **Speaking** — and adds a dedicated Consulting page. The theme-migration strategy, Minimal Mistakes configuration approach, and all third-party integrations established in the prior iteration are preserved.

### Key Design Decisions

1. **Theme: Minimal Mistakes via remote_theme** — Rather than heavily customizing Minima or building from scratch, we adopt Minimal Mistakes. It is 100% compatible with GitHub Pages as a remote theme, provides built-in responsive layouts (splash, single, archive), feature rows, header overlays, author profiles, and card-based styling out of the box. This eliminates the need to write custom CSS for layout primitives. The `remote_theme` approach avoids Gemfile whitelisting issues on GitHub Pages.

2. **Homepage as splash layout** — The Minimal Mistakes `splash` layout provides full-width header overlays with CTA buttons and `feature_row` blocks, which map directly to the hero section and two service pillar requirements (Consulting and Speaking). No custom layout needed.

3. **Custom CSS layer for brand refinements** — A custom `assets/css/main.scss` file will import the theme's Sass and add overrides for the Inter font stack, social proof strip styling, and minor spacing adjustments. This keeps customizations minimal and maintainable.

4. **Preserve all remaining permalinks** — Every existing page that remains keeps its current `permalink` front matter value. The new Consulting page gets `/consulting/`. The Open Source page keeps `/open-source/`. The `/training/` permalinks are intentionally removed and will return the site's standard 404.

5. **Content-first approach** — Each page's Markdown content is rewritten in place. The theme handles visual presentation through layouts and front matter configuration, so the migration is primarily a theme swap + content rewrite rather than a structural rebuild.

6. **Single Consulting offering, two delivery modes** — Short-term deployed-forward projects and long-term engagements are consolidated under one Consulting_Offering. The homepage presents this as a single Consulting pillar; the dedicated Consulting page distinguishes the two delivery modes visually and textually.

## Architecture

### High-Level Site Architecture

```mermaid
graph TD
    subgraph "Jekyll Build Pipeline"
        CONFIG["_config.yml<br/>(Minimal Mistakes remote theme)"]
        GEMFILE["Gemfile<br/>(github-pages gem)"]
        LAYOUTS["Layouts<br/>(splash, single, page)"]
        INCLUDES["_includes/<br/>(custom head, analytics, Credly, Sessionize)"]
        DATA["_data/<br/>(navigation.yml)"]
        SASS["assets/css/main.scss<br/>(theme + custom overrides)"]
    end

    subgraph "Content Pages"
        HOME["index.html<br/>layout: splash"]
        CONSULTING["consulting.markdown<br/>layout: single, wide"]
        PORTFOLIO["portfolio.markdown<br/>layout: single, wide"]
        SPEAKING["speaking.markdown<br/>layout: single, wide"]
        OPENSOURCE["open-source.markdown<br/>layout: single, wide"]
        CREDENTIALS["credentials.markdown<br/>layout: single, wide"]
    end

    subgraph "Third-Party Integrations"
        GA["Google Analytics<br/>G-LN4HKRGKZG"]
        CREDLY["Credly Badges<br/>(credentials page)"]
        SESSIONIZE["Sessionize Widget<br/>(speaking page)"]
        SEO["jekyll-seo-tag<br/>jekyll-sitemap"]
    end

    CONFIG --> LAYOUTS
    CONFIG --> DATA
    GEMFILE --> CONFIG
    LAYOUTS --> HOME
    LAYOUTS --> CONSULTING
    LAYOUTS --> PORTFOLIO
    LAYOUTS --> SPEAKING
    LAYOUTS --> OPENSOURCE
    LAYOUTS --> CREDENTIALS
    INCLUDES --> GA
    INCLUDES --> CREDLY
    INCLUDES --> SESSIONIZE
    SEO --> CONFIG
```

### Theme Migration Strategy

The migration from Minima to Minimal Mistakes follows this approach:

1. **Gemfile**: Replace `gem "minima"` and `gem "jekyll"` with `gem "github-pages"` and add `gem "jekyll-include-cache"`.
2. **_config.yml**: Replace `theme: minima` with `remote_theme: "mmistakes/minimal-mistakes@4.28.0"`. Add `jekyll-include-cache` to plugins. Configure Minimal Mistakes-specific settings (skin, author profile, footer links, defaults).
3. **Navigation**: Replace `header_pages` with `_data/navigation.yml` using Minimal Mistakes' masthead navigation system.
4. **Layouts**: Remove custom `_layouts/home.html`. Use theme-provided layouts: `splash` for homepage, `single` with `classes: wide` for content pages.
5. **Includes**: Remove Minima-specific includes (`_includes/header.html`, `_includes/footer.html`, `_includes/social.html`, `_includes/head.html`). Keep `_includes/google-analytics.html` and move it into Minimal Mistakes' `_includes/head/custom.html` hook. Credly and Sessionize scripts remain inline in their respective page Markdown.
6. **Styling**: Create `assets/css/main.scss` that imports the theme and adds custom overrides.

### Deployment Compatibility

- **GitHub Pages**: The `remote_theme` directive is natively supported by GitHub Pages. The `github-pages` gem bundles all whitelisted plugins.
- **Local development**: `bundle exec jekyll serve` works with the `github-pages` gem. The `jekyll-remote-theme` plugin (bundled in `github-pages`) fetches the theme at build time.
- **Plugins used**: `jekyll-seo-tag`, `jekyll-sitemap`, `jekyll-feed`, `jekyll-include-cache` — all GitHub Pages whitelisted or bundled.

## Components and Interfaces

### 1. Configuration (`_config.yml`)

The central configuration file is restructured for Minimal Mistakes. Subtitle, description, and bio reflect the Consulting · Speaking positioning (no training references):

```yaml
# Site settings
title: Elena van Engelen-Maslova
subtitle: "Kotlin & Cloud-Native Consultant · Speaker"
name: Elena van Engelen-Maslova
email: elenavanengelen@vintik.nl
description: >-
  Freelance Kotlin and cloud-native consultant helping teams build scalable
  systems on AWS and Azure. Short-term deployed-forward projects, long-term
  engagements, and conference speaking.
url: "https://elenavanengelenmaslova.github.io"
repository: "elenavanengelenmaslova/elenavanengelenmaslova.github.io"

# Theme
remote_theme: "mmistakes/minimal-mistakes@4.28.0"
minimal_mistakes_skin: "default"  # clean, professional look

# Author profile (shown in sidebar)
author:
  name: "Elena van Engelen-Maslova"
  avatar: "/assets/images/profile.jpeg"
  bio: "Freelance Kotlin & Cloud-Native Consultant. Author of *Kotlin Crash Course*. AWS Community Builder."
  location: "Netherlands"
  links:
    - label: "Email"
      icon: "fas fa-fw fa-envelope"
      url: "mailto:elenavanengelen@vintik.nl"
    - label: "LinkedIn"
      icon: "fab fa-fw fa-linkedin"
      url: "https://www.linkedin.com/in/elena-van-engelen-maslova/"
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: "https://github.com/elenavanengelenmaslova"
    - label: "Mastodon"
      icon: "fab fa-fw fa-mastodon"
      url: "https://hachyderm.io/@elenavanengelen"

# Analytics
analytics:
  provider: "google-gtag"
  google:
    tracking_id: "G-LN4HKRGKZG"

# SEO
plugins:
  - jekyll-sitemap
  - jekyll-seo-tag
  - jekyll-feed
  - jekyll-include-cache

# Front matter defaults
defaults:
  - scope:
      path: ""
    values:
      layout: "single"
      author_profile: true
  - scope:
      path: ""
      type: "posts"
    values:
      layout: "single"
      author_profile: true

# Footer
footer:
  links:
    - label: "LinkedIn"
      icon: "fab fa-fw fa-linkedin"
      url: "https://www.linkedin.com/in/elena-van-engelen-maslova/"
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: "https://github.com/elenavanengelenmaslova"
    - label: "Mastodon"
      icon: "fab fa-fw fa-mastodon"
      url: "https://hachyderm.io/@elenavanengelen"
```

### 2. Navigation (`_data/navigation.yml`)

Minimal Mistakes uses a data file for masthead navigation instead of `header_pages`. Consulting replaces Training and leads the list:

```yaml
main:
  - title: "Consulting"
    url: /consulting/
  - title: "Portfolio"
    url: /portfolio/
  - title: "Speaking"
    url: /speaking/
  - title: "Open Source"
    url: /open-source/
  - title: "Credentials"
    url: /credentials/
  - title: "Blog"
    url: "https://medium.com/@elenavanengelen"
    target: "_blank"
    rel: "noopener"
```

### 3. Homepage (`index.html`)

Converted from Markdown to HTML front matter to leverage the `splash` layout with `feature_row`. The hero value proposition names Kotlin and cloud-native and references both consulting and speaking. The `feature_row` has exactly two entries — Consulting (first, most prominent) and Speaking:

```yaml
---
layout: splash
permalink: /
header:
  overlay_color: "#1a1a2e"
  overlay_filter: "0.6"
  overlay_image: /assets/images/profile.jpeg
  actions:
    - label: "Get in Touch"
      url: "mailto:elenavanengelen@vintik.nl"
excerpt: >
  Helping teams build scalable Kotlin and cloud-native systems on AWS and Azure.
  Consulting · Speaking
feature_row:
  - title: "Consulting"
    excerpt: "Deployed-forward engineering for your team. I join, deliver a focused short-term project, then roll off — or take on a longer engagement. Short-term projects available now; long-term engagements from April 2027."
    url: "/consulting/"
    btn_label: "Explore Consulting"
    btn_class: "btn--primary btn--large"
  - title: "Speaking"
    excerpt: "Engaging conference talks with live coding on Kotlin and serverless cloud. Featured at KotlinConf, Voxxed Days, InfoQ Dev Summit, and more."
    url: "/speaking/"
    btn_label: "Book a Talk"
    btn_class: "btn--primary"
---
```

The Consulting pillar is rendered first in source order and uses `btn--primary btn--large` for greater visual prominence than the Speaking pillar (satisfying the prominence requirement through both higher position and distinct emphasis styling).

The homepage body content (below front matter) includes:
- Social proof strip with client logos/names (PostNL, Bol.com, KPN, AZL/NN Group), with text fallback if a logo image fails to load
- Credibility indicators (published author of "Kotlin Crash Course", AWS Community Builder, conference speaker referencing KotlinConf, AWS and Azure certifications)
- Availability note with three distinct statements: short-term deployed-forward projects available now, long-term consulting engagements available from April 2027, speaking engagements available now
- At least two secondary CTA elements linking to the contact mechanism or a service page
- Profile image referenced from `assets/images/profile.jpeg`

### 4. Consulting Page (`consulting.markdown`) — NEW

Uses `layout: single` with `classes: wide` and `permalink: /consulting/`. It presents the single Consulting_Offering with two clearly distinguished delivery modes:

```yaml
---
layout: single
title: "Consulting"
permalink: /consulting/
classes: wide
author_profile: true
---
```

Content structure:
- **Outcome-oriented opening copy** describing business value and delivery, placed *before* any technology listing (no tech list appears above this copy)
- **Deployed-forward model section** — describes the short-term consultancy approach stating all three phases: Elena joins a team, delivers a focused short-term project, and then rolls off
- **Long-term engagements section** — presented as a separate, clearly labeled option within the same Consulting_Offering, visually and textually distinct from the deployed-forward model
- **Pricing statement** — short-term projects are priced either per hour or per finished fixed-price project; directs visitors to contact Elena for pricing; displays no specific rate, price amount, or numeric cost figure
- **Availability statement** — short-term deployed-forward projects available now; long-term engagements available starting April 2027
- **Relevant client work reference** with a link to the Portfolio page
- **CTA element** with action-oriented visible text (e.g., "Get in Touch" or "Book a Call") linking to a contact method (`mailto:`), with an alternative contact method presented if the primary link target cannot be resolved

### 5. Speaking Page (`speaking.markdown`)

Uses `layout: single` with `classes: wide`. Restructured for conference organizers:

- Speaker bio section (concise, copy-paste ready for organizers)
- Available talk topics with formats (keynote, session, workshop, live coding demo)
- "What you get" section (audience experience, live coding, practical content)
- Speaking metrics (Voxxed Days Amsterdam 2025 top 4 most-viewed)
- Availability statement (paid and unpaid at select conferences)
- Sessionize widget preserved (inline script)
- Past recorded talks with video links
- CTA for organizers ("Invite Me to Speak" → mailto)

### 6. Open Source Page (`open-source.markdown`)

Uses `layout: single` with `classes: wide` and `permalink: /open-source/`. The page is built from a repeatable **heading + description entry-block** pattern: each project is a discrete block (a project heading followed by description, key features, tech stack, optional award line, and a GitHub CTA). Because every project reuses the same block structure, the page scales to multiple projects without changing the page layout. The page now documents **two projects**, and both entries render on the same page in source order.

- Page intro explaining open source involvement
- **Project 1 — MockNest Serverless** (first entry block, with logo image):
  - Description: serverless WireMock-compatible mock runtime for AWS with AI-powered mock generation using Amazon Bedrock
  - GitHub link: https://github.com/elenavanengelenmaslova/mocknest-serverless
  - Key features list (WireMock-compatible, AI mock generation from OpenAPI/WSDL/GraphQL specs, one-click SAR deployment)
  - Tech stack (Kotlin, AWS Lambda with SnapStart, Amazon S3, Amazon Bedrock, SQS, API Gateway, AWS SAM, Koog Agent)
  - Award: Creative Track Award, AWS 10,000 AIdeas Competition (text only, no badge)
  - CTA: "Explore on GitHub" → MockNest GitHub repository
- **Project 2 — AWS Lambda Response Streaming for JVM** (second entry block, same structure as Project 1; text heading only, **no logo image** for this entry — unlike MockNest, which has a logo):
  - Description: a JVM library implementing the AWS Lambda / Amazon API Gateway HTTP response streaming protocol for Kotlin and Java, filling the gap where AWS only ships Node.js helpers for the wire format. Primary use case: streaming Server-Sent Events (SSE), including token-by-token LLM output from Amazon Bedrock.
  - GitHub link: https://github.com/elenavanengelenmaslova/aws-lambda-response-streaming-jvm
  - Published dependency coordinate: `nl.vintik:aws-lambda-streaming-core`
  - Key features list:
    - Implements the API Gateway response-streaming wire protocol (metadata JSON + 8-byte delimiter + body) so JVM developers do not hand-roll it
    - Memory-bounded streaming via a fixed 1 MB buffer — flat memory usage regardless of payload size
    - SSE streaming, including Bedrock token-by-token LLM output
    - Minimal dependencies (only `kotlinx-serialization-json`; no AWS artifacts)
    - Compiled for Java 21; runs on the `java21`/`java25` runtimes
    - Kotlin and Java example modules
  - Tech stack: Kotlin, Java, AWS Lambda, Amazon API Gateway, kotlinx-serialization, Amazon Bedrock (SSE/LLM example)
  - No award for this entry
  - CTA: "Explore on GitHub" → AWS Lambda Response Streaming for JVM GitHub repository

The entry-block/heading pattern is the extension point for open source growth: adding a project means adding another block, not restructuring the page.

### 7. Portfolio Page (`portfolio.markdown`)

Uses `layout: single` with `classes: wide`. Descriptions tightened to impact-first format. The Portfolio page is now also linked from the Consulting page:

- Each project: Client name, Role, Key business outcome (1-2 sentences), Technologies
- Removes lengthy problem/solution/impact narratives
- Adds MockNest Serverless cross-reference linking to Open Source page
- Retains all four clients: AZL/NN Group, PostNL, Bol.com, KPN

### 8. Credentials Page (`credentials.markdown`)

Uses `layout: single` with `classes: wide`. Minimal changes:
- Credly badge scripts preserved inline
- Azure certification images preserved
- Academic achievements preserved
- Styling adjusted to work with Minimal Mistakes (flex layouts remain as inline styles)

### 9. Custom Styling (`assets/css/main.scss`)

```scss
---
# Only the main Sass file needs front matter dashes
---

@import "minimal-mistakes/skins/{{ site.minimal_mistakes_skin | default: 'default' }}";
@import "minimal-mistakes";

// Custom font stack
html {
  font-family: "Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    "Helvetica Neue", Arial, sans-serif;
}

// Social proof strip
.social-proof-strip {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  gap: 2rem;
  padding: 2rem 0;
  border-top: 1px solid #eee;
  border-bottom: 1px solid #eee;
  margin: 2rem 0;

  span {
    font-size: 1.1rem;
    font-weight: 600;
    color: #555;
  }
}

// CTA button enhancements
.btn--cta {
  font-size: 1.1rem;
  padding: 0.75rem 1.5rem;
}
```

### 10. Google Analytics Integration

Minimal Mistakes has built-in Google Analytics support via `_config.yml`:

```yaml
analytics:
  provider: "google-gtag"
  google:
    tracking_id: "G-LN4HKRGKZG"
```

This replaces the custom `_includes/google-analytics.html` include. The theme handles the gtag.js injection automatically. The custom include file can be removed.

### 11. Include Files Cleanup

**Remove** (replaced by theme):
- `_includes/header.html` — Minimal Mistakes provides its own masthead
- `_includes/footer.html` — Minimal Mistakes provides its own footer
- `_includes/social.html` — Minimal Mistakes handles social links via `_config.yml`
- `_includes/head.html` — Minimal Mistakes provides its own head with SEO

**Remove** (functionality moved to theme config):
- `_includes/google-analytics.html` — handled by `analytics` config

**Remove** (replaced by theme):
- `_layouts/home.html` — replaced by `splash` layout
- `assets/minima-social-icons.svg` — Minimal Mistakes uses Font Awesome

**Keep/Create**:
- `_includes/head/custom.html` — for any additional head tags (favicon)

### 12. Favicon Preservation

Create `_includes/head/custom.html`:

```html
<link rel="icon" href="{{ '/assets/images/logo.png' | relative_url }}" type="image/png">
```

## Data Models

This is a static Jekyll site with no database or dynamic data store. The "data models" are the front matter structures and data files that Jekyll processes at build time.

### Page Front Matter Schema

**Homepage (splash layout)**:
```yaml
layout: splash
permalink: /
header:
  overlay_color: string     # hex color for overlay
  overlay_filter: string    # opacity value
  overlay_image: string     # path to background image
  actions:                  # CTA buttons in header
    - label: string
      url: string
excerpt: string             # tagline text displayed in overlay
feature_row:                # service pillar cards (exactly two: Consulting, Speaking)
  - title: string
    excerpt: string
    url: string
    btn_label: string
    btn_class: string
```

**Content pages (single layout)**:
```yaml
layout: single
title: string
permalink: string           # must match existing permalink (or /consulting/ for the new page)
classes: wide               # optional, for full-width content
author_profile: true|false  # show/hide sidebar author profile
```

### Navigation Data (`_data/navigation.yml`)

```yaml
main:                       # masthead navigation
  - title: string           # display text
    url: string             # relative or absolute URL
    target: string          # optional, "_blank" for external
    rel: string             # optional, "noopener" for external
```

### Author Data (in `_config.yml`)

```yaml
author:
  name: string
  avatar: string            # path to profile image
  bio: string               # short bio (Markdown supported)
  location: string
  links:                    # social/contact links
    - label: string
      icon: string          # Font Awesome class
      url: string
```

### File Structure After Migration

```
.
├── _config.yml                    # Updated for Minimal Mistakes
├── _data/
│   └── navigation.yml             # NEW: masthead navigation (Consulting replaces Training)
├── _includes/
│   └── head/
│       └── custom.html            # NEW: favicon + any custom head tags
├── assets/
│   ├── css/
│   │   └── main.scss              # NEW: theme import + custom overrides
│   └── images/                    # UNCHANGED: all existing images
│       ├── profile.jpeg
│       ├── logo.png
│       └── ...
├── Gemfile                        # Updated: github-pages gem
├── index.html                     # CHANGED: splash layout, two feature_row entries
├── consulting.markdown            # NEW: Consulting offering (deployed-forward + long-term)
├── portfolio.markdown             # UPDATED: impact-first content, linked from Consulting
├── speaking.markdown              # UPDATED: organizer-focused content
├── open-source.markdown           # Open source showcase (MockNest Serverless)
├── credentials.markdown           # MINOR UPDATES: styling compatibility
├── 404.html                       # Uses default layout from theme
└── README.md                      # UNCHANGED
```

**Removed files** (replaced by theme):
- `_includes/header.html`
- `_includes/footer.html`
- `_includes/social.html`
- `_includes/head.html`
- `_includes/google-analytics.html`
- `_layouts/home.html`
- `assets/minima-social-icons.svg`

**Removed files** (intentional deletions for the training removal):
- `training.markdown` — training landing page removed
- `training/kotlin-basics.md` — course detail page removed
- `training/kotlin-crash-course.md` — course detail page removed
- `training/kotlin-aws-lambda.md` — course detail page removed
- `training/kotlin-azure-functions.md` — course detail page removed
- `training/bite-size-kotlin.md` — course detail page removed

The entire `training/` directory is removed. All `/training/` permalinks (the landing page and the five course detail pages) are intentionally removed; requests to those paths return the site's standard 404 response.

## Error Handling

### Build Errors

Since this is a static site built by Jekyll, errors manifest at build time rather than runtime.

| Error Scenario | Detection | Resolution |
|---|---|---|
| **Remote theme fetch failure** | `bundle exec jekyll serve` fails with theme download error | Verify internet connectivity; pin theme version in `remote_theme` directive; fall back to gem-based install if persistent |
| **Missing include file** | Jekyll build error: "Could not locate the included file" | Ensure all referenced includes exist; Minimal Mistakes provides its own includes, so remove Minima-specific references |
| **Invalid front matter** | Jekyll build error with YAML parse failure | Validate YAML syntax in front matter; use quotes around strings with special characters |
| **Plugin not found** | Bundler/Jekyll error for missing gem | Ensure all plugins are listed in Gemfile and `_config.yml` plugins array; use only GitHub Pages whitelisted plugins |
| **Broken permalink** | 404 on previously working URL | Verify `permalink` front matter matches original value on every remaining page; test all remaining URLs after migration |
| **Stale /training/ reference** | A retained link points to a removed `/training/` path | Remove or repoint any internal links that targeted training; `/training/` paths are expected to 404 by design |
| **Credly/Sessionize script failure** | Third-party widget doesn't render | Scripts are loaded client-side; ensure inline `<script>` tags are preserved exactly in page Markdown; no Jekyll processing needed |
| **Google Analytics not firing** | No data in GA dashboard | Verify `analytics.google.tracking_id` in `_config.yml`; check that `JEKYLL_ENV=production` is set for production builds (GA is typically gated on environment) |
| **Image not found** | Broken image on page | Verify image paths use `{{ '/assets/images/...' | relative_url }}` or correct relative paths; ensure all images are committed |

### Graceful Degradation

- **Font loading**: The Inter font is loaded via the CSS font stack. If it fails to load (no CDN dependency — it's a system font fallback chain), the browser falls back to `-apple-system`, `BlinkMacSystemFont`, `Segoe UI`, etc.
- **Feature rows**: If `feature_row` front matter is malformed, the splash layout renders without the feature blocks but doesn't break the page.
- **Social proof logos**: If a logo image fails to load, the corresponding organization name is shown as text so all four organizations (PostNL, Bol.com, KPN, AZL/NN Group) remain identifiable.
- **Consulting CTA**: If the primary contact link target cannot be resolved, the Consulting page presents an alternative contact method or a message indicating the contact option is temporarily unavailable.
- **External links**: The Blog link to Medium opens in a new tab. If Medium is down, the link still works — it's just a standard `<a>` tag.
- **Sessionize widget**: If Sessionize's API is unavailable, the widget area is simply empty. The rest of the page renders normally.
- **Credly badges**: Same as Sessionize — client-side JavaScript that degrades to empty space if the CDN is unreachable.

## Testing Strategy

### Why Property-Based Testing Does Not Apply

This feature is a static website redesign involving theme configuration, content rewriting, HTML/CSS layout, and third-party widget integration. There are no pure functions, parsers, serializers, data transformations, or algorithms with meaningful input variation. The acceptance criteria describe:

- **Visual presentation** — theme, fonts, responsive layouts (best tested with visual inspection and snapshot tests)
- **Content presence** — specific text, sections, and links on pages (best tested with example-based HTML assertions)
- **Configuration correctness** — Jekyll builds, plugin compatibility (best tested with smoke tests)
- **Integration preservation** — Google Analytics, Credly, Sessionize scripts present in output (best tested with example-based HTML assertions)

None of these criteria can be meaningfully expressed as "for all inputs X, property P(X) holds." Property-based testing is not appropriate for this feature.

### Testing Approach

#### 1. Build Smoke Tests

Verify the site builds without errors at each milestone:

```bash
# Must exit 0 with no errors
JEKYLL_ENV=production bundle exec jekyll build
```

**What this validates**: Requirements 9.1, 9.2, 9.5, 9.6

#### 2. HTML Output Assertions

After building the site, inspect the generated HTML in `_site/` to verify content and structure. These are example-based tests that check specific elements exist in the rendered output.

**Homepage (`_site/index.html`)**:
- Contains hero section text (value proposition naming "Kotlin", "cloud-native", referencing consulting and speaking)
- Contains a primary CTA link with `mailto:` or contact URL
- Contains exactly two service pillar sections (Consulting, Speaking), with Consulting before Speaking in source order
- Consulting pillar mentions both short-term deployed-forward projects and long-term engagements and links to `/consulting/`
- Contains social proof names: PostNL, Bol.com, KPN, AZL
- Contains availability note text (short-term now, long-term April 2027, speaking now)
- Contains credibility indicators (Kotlin Crash Course, AWS Community Builder, KotlinConf, AWS and Azure certifications)
- Contains at least two CTA elements
- Contains profile image reference (`profile.jpeg`)
- Validates: Requirements 3.1–3.10, 8.1, 8.2

**Navigation (all pages)**:
- Masthead contains links in order: Consulting, Portfolio, Speaking, Open Source, Credentials, Blog
- No item labeled Training is present
- Consulting link points to `/consulting/`
- Blog link has `target="_blank"` and `rel="noopener"`
- Validates: Requirements 2.1–2.5

**Consulting page (`_site/consulting/index.html`)**:
- Contains deployed-forward model text stating all three phases (joins a team, delivers a focused short-term project, rolls off)
- Contains a separate, clearly labeled long-term engagements option
- Outcome-oriented copy appears before any technology listing (no tech list above the opening copy)
- Contains per-hour or per-finished-fixed-price pricing language
- Contains no specific rate, price amount, or numeric cost figure
- Contains availability statements (short-term now, long-term April 2027)
- Contains a link to `/portfolio/` and at least one client work reference
- Contains an action-oriented CTA linking to a contact method
- Validates: Requirements 4.1–4.11

**Speaking page (`_site/speaking/index.html`)**:
- Contains speaker bio section
- Contains talk topics with format descriptions (keynote, session, workshop, live coding demo)
- Contains Sessionize script tag (`sessionize.com`)
- Contains CTA mailto link
- Contains "top 4 most-viewed" or equivalent Voxxed Days Amsterdam 2025 metric text
- Contains video links for past talks
- Validates: Requirements 5.1–5.8

**Open Source page (`_site/open-source/index.html`)**:
- MockNest Serverless entry:
  - Contains "MockNest Serverless" text
  - Contains MockNest GitHub repository link (`mocknest-serverless`)
  - Contains key features (WireMock-compatible, AI mock generation, SAR deployment)
  - Contains tech stack (Kotlin, AWS Lambda, Bedrock, etc.)
  - Contains "Creative Track Award" text (no badge image)
  - Contains CTA link to the MockNest GitHub repository
- AWS Lambda Response Streaming for JVM entry:
  - Contains the heading text "AWS Lambda Response Streaming for JVM"
  - Contains its GitHub repository link (`aws-lambda-response-streaming-jvm`)
  - Contains the published dependency coordinate `nl.vintik:aws-lambda-streaming-core`
  - Contains the SSE/Bedrock mention (Server-Sent Events / Amazon Bedrock token-by-token LLM output)
  - Contains a CTA link to its GitHub repository
- Both project entries render on the same page using the same entry-block structure
- Validates: Requirements 6.1–6.12

**Portfolio page (`_site/portfolio/index.html`)**:
- Contains all four client names: AZL, PostNL, Bol.com, KPN
- Contains MockNest Serverless cross-reference with link to `/open-source/`
- Project descriptions are concise (impact-first format)
- Validates: Requirements 7.1–7.4

**Credentials page (`_site/credentials/index.html`)**:
- Contains Credly script tag (`credly.com`)
- Contains Azure certification images
- Contains academic degree information
- Validates: Requirement 1.8

#### 3. Permalink Preservation Tests

After building, verify that all remaining existing URLs produce output files, the new Consulting page is produced, and `/training/` paths are gone:

```
_site/index.html             → /
_site/consulting/index.html  → /consulting/ (new)
_site/portfolio/index.html   → /portfolio/
_site/speaking/index.html    → /speaking/
_site/open-source/index.html → /open-source/
_site/credentials/index.html → /credentials/
_site/404.html               → /404.html

# Must NOT exist (intentionally removed — requests return 404):
_site/training/index.html
_site/training/kotlin-basics/index.html
_site/training/kotlin-crash-course/index.html
_site/training/kotlin-aws-lambda/index.html
_site/training/kotlin-azure-functions/index.html
_site/training/bite-size-kotlin/index.html
```

**What this validates**: Requirements 9.3, 9.4

#### 4. SEO and Analytics Verification

- Built HTML contains `<meta>` tags from jekyll-seo-tag (title, description, og:tags)
- `_site/sitemap.xml` exists and contains all remaining page URLs (and no `/training/` URLs)
- Built HTML contains Google Analytics tracking script with ID `G-LN4HKRGKZG`
- Favicon link tag references `assets/images/logo.png`

**What this validates**: Requirements 1.6, 1.7, 9.7

#### 5. Accessibility Checks

- All content `<img>` tags have non-empty `alt` attributes; decorative images use `alt=""`
- Heading hierarchy is sequential (no skipped levels)
- Semantic HTML elements used (`<nav>`, `<main>`, `<header>`, `<footer>`) with exactly one `<main>` per page

**What this validates**: Requirement 9.8, 9.9

#### 6. Responsive Layout Verification

Manual testing at three breakpoints using browser dev tools:
- Desktop (1200px+)
- Tablet (768px)
- Mobile (375px)

Verify that navigation collapses to a toggle control below 768px and displays inline at or above 768px, feature rows stack vertically, and content remains readable.

**What this validates**: Requirements 1.4, 2.5

#### 7. Visual Review Milestones

The user wants to review the site visually at each milestone using `bundle exec jekyll serve`. The implementation should be structured so that each major change (theme swap, homepage, consulting page, etc.) produces a locally testable state.

**Milestone sequence**:
1. Theme swap + config + navigation (site builds with new theme, Consulting nav item present, all remaining pages render, `/training/` removed)
2. Homepage redesign (splash layout with hero, two service pillars with Consulting most prominent, social proof, availability note)
3. Consulting page (deployed-forward model, long-term engagements, pricing language, availability, portfolio link, CTA)
4. Speaking page (organizer-focused, bio section, Sessionize preserved)
5. Open Source page (MockNest Serverless + AWS Lambda Response Streaming for JVM)
6. Portfolio page (impact-first descriptions, cross-reference, linked from Consulting)
7. Final polish (credentials, 404, cleanup of old includes/layouts, removal of training files)
