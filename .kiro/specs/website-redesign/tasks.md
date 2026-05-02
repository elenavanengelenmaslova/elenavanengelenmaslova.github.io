# Implementation Plan: Website Redesign

## Overview

This plan migrates Elena van Engelen-Maslova's freelance professional website from the default Minima Jekyll theme to Minimal Mistakes (remote_theme), rewrites all page content from CV-style to sales-oriented copy, adds a new Open Source page, and restructures navigation. Each top-level task produces a locally testable state via `bundle exec jekyll serve`, matching the milestone sequence defined in the design document.

## Tasks

- [x] 1. Theme swap, configuration, and navigation (Milestone 1 — site builds with new theme)
  - [x] 1.1 Update Gemfile for github-pages and jekyll-include-cache
    - Replace `gem "jekyll", "~> 4.3.2"` and `gem "minima", "~> 2.5"` with `gem "github-pages", group: :jekyll_plugins`
    - Add `gem "jekyll-include-cache"` to the `:jekyll_plugins` group
    - Keep existing platform gems and `jekyll-feed`, `jekyll-sitemap`
    - Run `bundle install` to update Gemfile.lock
    - _Requirements: 1.1, 1.5, 10.1, 10.2, 10.5_

  - [x] 1.2 Rewrite _config.yml for Minimal Mistakes
    - Replace `theme: minima` with `remote_theme: "mmistakes/minimal-mistakes@4.28.0"`
    - Remove `minima:` skin config and `header_pages` array
    - Add `minimal_mistakes_skin: "default"`
    - Add `subtitle`, `name`, `repository` fields
    - Rewrite `description` to sales-oriented copy per design
    - Add `author:` block with name, avatar, bio, location, and social links (Email, LinkedIn, GitHub, Mastodon)
    - Add `analytics:` block with `provider: "google-gtag"` and `tracking_id: "G-LN4HKRGKZG"`
    - Update `plugins:` list to include `jekyll-feed`, `jekyll-sitemap`, `jekyll-seo-tag`, `jekyll-include-cache`
    - Update `defaults:` to use `layout: "single"` and `author_profile: true`
    - Add `footer:` links block (LinkedIn, GitHub, Mastodon)
    - Preserve `google_analytics` key removal (handled by `analytics:` block now)
    - Preserve `sass:`, `markdown:`, `highlighter:`, and `exclude:` settings
    - _Requirements: 1.1, 1.5, 1.6, 1.7, 10.2, 10.5_

  - [x] 1.3 Create _data/navigation.yml
    - Create `_data/` directory and `navigation.yml` file
    - Define `main:` array with entries: Portfolio (`/portfolio/`), Training (`/training/`), Speaking (`/speaking/`), Open Source (`/open-source/`), Credentials (`/credentials/`), Blog (external Medium link with `target: "_blank"` and `rel: "noopener"`)
    - _Requirements: 2.1, 2.2, 2.3, 2.4_

  - [x] 1.4 Create custom head include for favicon
    - Create `_includes/head/custom.html` with `<link rel="icon" href="{{ '/assets/images/logo.png' | relative_url }}" type="image/png">`
    - _Requirements: 10.6_

  - [x] 1.5 Create custom CSS file with theme import and overrides
    - Create `assets/css/main.scss` with front matter dashes, Minimal Mistakes skin import, and theme import
    - Add Inter font stack override on `html` element
    - Add `.social-proof-strip` styles (flex, wrap, centered, gap, borders)
    - Add `.btn--cta` enhancement styles
    - _Requirements: 1.2, 1.3, 1.10_

  - [x] 1.6 Update existing page layouts for Minimal Mistakes compatibility
    - Change `layout: page` to `layout: single` on portfolio.markdown, training.markdown, speaking.markdown, credentials.markdown
    - Add `classes: wide` to portfolio.markdown, training.markdown, speaking.markdown, credentials.markdown
    - Change `layout: page` to `layout: single` on all training detail pages (training/*.md)
    - Ensure all existing `permalink:` values are preserved exactly
    - _Requirements: 1.1, 1.3, 10.3_

  - [x] 1.7 Remove Minima-specific includes, layouts, and assets
    - Delete `_includes/header.html` (replaced by Minimal Mistakes masthead)
    - Delete `_includes/footer.html` (replaced by Minimal Mistakes footer)
    - Delete `_includes/social.html` (replaced by config-driven social links)
    - Delete `_includes/head.html` (replaced by Minimal Mistakes head + custom.html hook)
    - Delete `_includes/google-analytics.html` (replaced by `analytics:` config)
    - Delete `_layouts/home.html` (replaced by `splash` layout)
    - Delete `assets/minima-social-icons.svg` (Minimal Mistakes uses Font Awesome)
    - _Requirements: 1.1_

  - [x] 1.8 Verify Milestone 1 — site builds and all pages render with new theme
    - Run `bundle exec jekyll build` and confirm zero errors
    - Verify `_site/index.html`, `_site/portfolio/index.html`, `_site/training/index.html`, `_site/speaking/index.html`, `_site/credentials/index.html` all exist
    - Verify all training detail page permalinks produce output files in `_site/`
    - Verify navigation contains Portfolio, Training, Speaking, Open Source, Credentials, Blog links
    - _Requirements: 10.1, 10.2, 10.3, 10.4_

- [x] 2. Checkpoint — Verify theme migration
  - Ensure the site builds without errors. Run `bundle exec jekyll serve` and visually confirm all pages render with the Minimal Mistakes theme, navigation works, and no broken layouts. Ask the user if questions arise.

- [x] 3. Homepage redesign (Milestone 2 — splash layout with hero, service pillars, social proof)
  - [x] 3.1 Convert index.markdown to index.html with splash layout
    - Rename `index.markdown` to `index.html`
    - Set `layout: splash` with `permalink: /`
    - Add `header:` block with `overlay_color`, `overlay_filter`, `overlay_image` (profile.jpeg), and `actions:` array with primary CTA ("Get in Touch" → mailto)
    - Add `excerpt:` with value proposition tagline
    - Add `feature_row:` array with three Service Pillar entries (Consulting, Training, Speaking) per design — Consulting first with `btn--primary btn--large` for visual prominence
    - _Requirements: 3.1, 3.2, 3.3, 3.4, 9.1, 9.2_

  - [x] 3.2 Write homepage body content below front matter
    - Add social proof strip with `<div class="social-proof-strip">` containing client names: PostNL, Bol.com, KPN, AZL (NN Group)
    - Add credibility indicators section: published author (Kotlin Crash Course), AWS Community Builder, conference speaker (KotlinConf, Voxxed Days, InfoQ Dev Summit), AWS/Azure certifications
    - Add availability note: project work from April 2027, training and speaking available now
    - Add secondary CTA section with contact link
    - Use second-person language ("your team", "your project") per requirements
    - _Requirements: 3.5, 3.6, 3.7, 3.8, 11.1, 11.2, 11.3, 11.4_

  - [x] 3.3 Verify Milestone 2 — homepage renders correctly
    - Run `bundle exec jekyll build` and confirm zero errors
    - Verify `_site/index.html` contains hero section text, CTA link, three service pillars, social proof names, availability note, credibility indicators, and profile image reference
    - _Requirements: 3.1–3.8, 9.1, 9.2, 10.1_

- [x] 4. Checkpoint — Verify homepage
  - Ensure the site builds without errors. Run `bundle exec jekyll serve` and visually confirm the homepage splash layout, hero section, feature row pillars, social proof strip, and CTAs. Ask the user if questions arise.

- [x] 5. Training page and detail pages (Milestone 3)
  - [x] 5.1 Rewrite training.markdown with outcome-oriented content
    - Lead with outcome-oriented headline and value proposition emphasizing business value and team productivity
    - Move student testimonials to a prominent position near the top (above course listings)
    - Add pricing: "Starting from €2,000 per day for corporate training"
    - Add logistics: remote worldwide, on-site in Europe, travel costs for outside NL
    - Add training client list as social proof (AZL/NN Group, Version 1, EDSN)
    - Restructure course listings with links to detail pages
    - Add CTA buttons ("Book a Call" → mailto) at top and bottom
    - Use second-person language addressing team leads and L&D managers
    - _Requirements: 4.1, 4.2, 4.3, 4.4, 4.5, 4.6, 4.7, 4.8, 11.1, 11.2, 11.3, 11.4_

  - [x] 5.2 Rewrite all training detail pages with outcome framing and CTAs
    - Update all five training detail pages (kotlin-basics.md, kotlin-crash-course.md, kotlin-aws-lambda.md, kotlin-azure-functions.md, bite-size-kotlin.md)
    - Reframe "Learning Objectives" as "What your team will be able to do" with outcome-oriented descriptions
    - Add CTA button at top and bottom of each page ("Book This Training" → mailto)
    - Retain course structure and content details
    - Ensure `layout: single` and existing `permalink:` values are preserved
    - _Requirements: 5.1, 5.2, 5.3, 10.3_

  - [x] 5.3 Verify Milestone 3 — training pages render correctly
    - Run `bundle exec jekyll build` and confirm zero errors
    - Verify `_site/training/index.html` contains pricing text "€2,000", testimonials, CTA links, training client names, and links to detail pages
    - Verify all five training detail pages exist at their original permalinks in `_site/`
    - _Requirements: 4.1–4.8, 5.1–5.3, 10.1, 10.3_

- [x] 6. Checkpoint — Verify training pages
  - Ensure the site builds without errors. Run `bundle exec jekyll serve` and visually confirm the training page layout, testimonials placement, pricing, CTAs, and training detail pages. Ask the user if questions arise.

- [x] 7. Speaking page redesign (Milestone 4)
  - [x] 7.1 Rewrite speaking.markdown for conference organizers
    - Add Speaker Bio Section with concise, copy-paste-ready biography for organizers
    - Add available talk topics with formats (keynote, session, workshop, live coding demo)
    - Add "What you get" section (audience experience, live coding, practical content)
    - Add speaking metrics (Voxxed Days top 4 most-viewed)
    - Add availability statement (paid and unpaid at select conferences)
    - Preserve Sessionize widget inline script tag exactly
    - Preserve past recorded talks with video links
    - Add podcasts section
    - Add CTA for organizers ("Invite Me to Speak" → mailto)
    - Use `layout: single` with `classes: wide`
    - _Requirements: 6.1, 6.2, 6.3, 6.4, 6.5, 6.6, 6.7, 6.8, 11.1, 11.3_

  - [x] 7.2 Verify Milestone 4 — speaking page renders correctly
    - Run `bundle exec jekyll build` and confirm zero errors
    - Verify `_site/speaking/index.html` contains speaker bio, talk topics, Sessionize script tag, CTA mailto link, speaking metrics text, and video links
    - _Requirements: 6.1–6.8, 10.1_

- [x] 8. Checkpoint — Verify speaking page
  - Ensure the site builds without errors. Run `bundle exec jekyll serve` and visually confirm the speaking page layout, speaker bio, talk topics, Sessionize widget, and CTAs. Ask the user if questions arise.

- [x] 9. Open Source page creation (Milestone 5 — new page)
  - [x] 9.1 Create open-source.markdown
    - Create new file `open-source.markdown` in project root
    - Set `layout: single`, `title: Open Source`, `permalink: /open-source/`, `classes: wide`
    - Write page intro explaining open source involvement
    - Add MockNest Serverless as first project entry with:
      - Description: serverless WireMock-compatible mock runtime for AWS with AI-powered mock generation using Amazon Bedrock
      - GitHub link: https://github.com/elenavanengelenmaslova/mocknest-serverless
      - Key features: WireMock-compatible, AI mock generation from OpenAPI/WSDL/GraphQL specs, one-click SAR deployment, webhook support, persistent mocks across cold starts
      - Tech stack: Kotlin, AWS Lambda (SnapStart), Amazon S3, Amazon Bedrock (Nova Pro), SQS, API Gateway, AWS SAM, Koog Agent
      - Award: Creative Track Award, AWS 10,000 AIdeas Competition (text only, no badge)
    - Add CTA: "Explore on GitHub" linking to the repository
    - Use heading + description pattern that scales to additional projects
    - _Requirements: 7.1, 7.2, 7.3, 7.4, 7.5_

  - [x] 9.2 Verify Milestone 5 — open source page renders correctly
    - Run `bundle exec jekyll build` and confirm zero errors
    - Verify `_site/open-source/index.html` exists and contains "MockNest Serverless", GitHub link, key features, tech stack, "Creative Track Award" text, and CTA link
    - _Requirements: 7.1–7.5, 10.1, 10.3_

- [x] 10. Portfolio page refinement (Milestone 6)
  - [x] 10.1 Rewrite portfolio.markdown with impact-first descriptions
    - Tighten each project to concise format: Client name, Role, Key business outcome (1-2 sentences), Technologies
    - Remove lengthy problem/solution/impact narratives
    - Retain all four clients: AZL/NN Group, PostNL, Bol.com, KPN
    - Add MockNest Serverless cross-reference entry linking to `/open-source/`
    - Retain Earlier Experience summary and LinkedIn Recommendations link
    - Use `layout: single` with `classes: wide`
    - _Requirements: 8.1, 8.2, 8.3, 8.4, 11.1_

  - [x] 10.2 Verify Milestone 6 — portfolio page renders correctly
    - Run `bundle exec jekyll build` and confirm zero errors
    - Verify `_site/portfolio/index.html` contains all four client names, MockNest Serverless cross-reference with link to `/open-source/`, and concise project descriptions
    - _Requirements: 8.1–8.4, 10.1_

- [x] 11. Checkpoint — Verify open source and portfolio pages
  - Ensure the site builds without errors. Run `bundle exec jekyll serve` and visually confirm the new Open Source page and the refined Portfolio page. Ask the user if questions arise.

- [x] 12. Final polish (Milestone 7 — credentials, 404, cleanup)
  - [x] 12.1 Update credentials.markdown for Minimal Mistakes compatibility
    - Ensure `layout: single` with `classes: wide`
    - Preserve Credly badge scripts inline exactly
    - Preserve Azure certification images with links
    - Preserve academic achievements section
    - Verify inline flex styles work with Minimal Mistakes (adjust if needed)
    - Ensure all `<img>` tags have `alt` attributes
    - _Requirements: 1.8, 10.3, 10.7_

  - [x] 12.2 Update 404.html for Minimal Mistakes
    - Change `layout: default` to `layout: single` (or appropriate Minimal Mistakes layout)
    - Preserve `permalink: /404.html`
    - Keep user-friendly 404 message
    - Remove custom inline CSS that conflicts with theme styling (or keep if compatible)
    - _Requirements: 10.3_

  - [x] 12.3 Final build verification and permalink check
    - Run `JEKYLL_ENV=production bundle exec jekyll build` and confirm zero errors
    - Verify all existing permalinks produce output files: `/`, `/portfolio/`, `/training/`, `/speaking/`, `/credentials/`, `/open-source/` (new), `/404.html`, and all five `/training/{slug}/` pages
    - Verify `_site/sitemap.xml` exists and contains all page URLs
    - Verify built HTML contains Google Analytics tracking script with ID `G-LN4HKRGKZG`
    - Verify all `<img>` tags in output have `alt` attributes
    - Verify favicon link tag references `assets/images/logo.png`
    - _Requirements: 10.1, 10.2, 10.3, 10.5, 10.6, 10.7, 1.6, 1.7_

- [x] 13. Final checkpoint — Ensure all pages pass
  - Ensure the site builds without errors with `JEKYLL_ENV=production bundle exec jekyll build`. Run `bundle exec jekyll serve` and do a full visual walkthrough of every page: homepage, portfolio, training (main + all 5 detail pages), speaking, open source, credentials, and 404. Verify navigation, CTAs, third-party widgets (Credly, Sessionize), analytics, and responsive layout. Ask the user if questions arise.

## Notes

- Each milestone (tasks 1, 3, 5, 7, 9, 10, 12) produces a locally testable state via `bundle exec jekyll serve`
- Checkpoints (tasks 2, 4, 6, 8, 11, 13) are visual review points where the user can inspect the site
- All existing permalinks are preserved — no URLs change except the new `/open-source/` addition
- The design explicitly states property-based testing does not apply to this static site redesign
- Third-party integrations (Credly, Sessionize, Google Analytics) are preserved through configuration and inline scripts
- Each task references specific requirements for traceability
