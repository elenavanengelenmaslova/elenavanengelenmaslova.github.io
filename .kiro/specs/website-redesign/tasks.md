# Implementation Plan: Website Redesign — Consulting Repositioning (Delta)

## Overview

The Minimal Mistakes theme migration and the sales-oriented rewrite of the homepage, portfolio, speaking, open-source, and credentials pages are **already implemented**. This plan covers **only the delta** required to reposition the site away from the Training offering and toward the new single **Consulting** offering (short-term deployed-forward projects + long-term engagements).

Scope of the delta:
- Remove all training content (page, five course detail pages, `/training/` links)
- Update navigation to replace Training with Consulting
- Update `_config.yml` positioning copy (drop trainer/training references)
- Create the new Consulting page
- Update the homepage (two pillars instead of three, revised hero and availability note)
- Clean up any dangling `/training/` references on the portfolio page
- Add a second open source project to the Open Source page
- Verify the build, permalinks, navigation, and integrations

Each task builds on the current implemented state and produces a locally testable site via `bundle exec jekyll serve`. A mandatory human-in-the-loop checkpoint follows **every** milestone: the agent runs the site locally, the user reviews the milestone's changes, and the agent halts until the user explicitly approves before the next milestone begins.

## Tasks

- [x] 1. Remove training content and dangling links (Milestone 1 — training fully removed)
  - [x] 1.1 Delete the training landing page and course detail pages
    - Delete `training.markdown` from the project root
    - Delete the entire `training/` directory and all five course detail pages: `training/kotlin-basics.md`, `training/kotlin-crash-course.md`, `training/kotlin-aws-lambda.md`, `training/kotlin-azure-functions.md`, `training/bite-size-kotlin.md`
    - _Requirements: 9.4_

  - [x] 1.2 Remove internal links pointing to `/training/` across remaining pages
    - Search all remaining content files (`index.html`, `portfolio.markdown`, `speaking.markdown`, `open-source.markdown`, `credentials.markdown`, and any includes) for references to `/training/` or training detail slugs
    - Remove or repoint each such link so no retained page links to a removed `/training/` path
    - _Requirements: 9.3, 9.4_

  - [x] 1.3 Verify Milestone 1 — training output is gone
    - Run `bundle exec jekyll build` and confirm zero errors
    - Confirm `_site/training/index.html` and all five `_site/training/{slug}/index.html` output files no longer exist
    - Confirm no remaining built page contains an `href` to a `/training/` path
    - _Requirements: 9.1, 9.3, 9.4_

- [x] 2. Checkpoint — Approval gate after Milestone 1 (training removal)
  - Run `bundle exec jekyll serve` and open the site locally
  - Review the changes from Milestone 1: confirm the training landing page and all five course detail pages are gone and no retained page links to a `/training/` path
  - STOP and wait for the user to confirm they approve the changes, or to request adjustments
  - Do NOT proceed to the next milestone until the user explicitly approves
  - If the user requests changes, make them and re-run this checkpoint before continuing

- [x] 3. Navigation and configuration repositioning (Milestone 2 — nav + config reflect Consulting)
  - [x] 3.1 Update `_data/navigation.yml`
    - Remove the Training item
    - Add a Consulting item linking to `/consulting/` as the first entry
    - Final `main:` order: Consulting, Portfolio, Speaking, Open Source, Credentials, Blog (Blog keeps `target: "_blank"` and `rel: "noopener"`)
    - _Requirements: 2.1, 2.2, 2.3_

  - [x] 3.2 Update `_config.yml` positioning copy
    - Update `subtitle` to "Kotlin & Cloud-Native Consultant · Speaker" (remove any Trainer/training reference)
    - Rewrite `description` to the consulting-and-speaking positioning per design (short-term deployed-forward projects, long-term engagements, conference speaking; no training)
    - Update the `author.bio` to drop any trainer/training reference and reflect "Freelance Kotlin & Cloud-Native Consultant"
    - Leave theme, analytics, plugins, defaults, and footer settings unchanged
    - _Requirements: 10.1, 10.3_

  - [x] 3.3 Verify Milestone 2 — navigation and config
    - Run `bundle exec jekyll build` and confirm zero errors
    - Verify the masthead in built HTML shows items in order: Consulting, Portfolio, Speaking, Open Source, Credentials, Blog, with no Training item, and the Consulting link points to `/consulting/`
    - Verify no built page's `<head>`/metadata references training
    - _Requirements: 2.1, 2.2, 2.3, 10.1, 10.3_

- [x] 4. Checkpoint — Approval gate after Milestone 2 (navigation + config)
  - Run `bundle exec jekyll serve` and open the site locally
  - Review the changes from Milestone 2: confirm navigation shows Consulting (not Training) in the correct order and the site description/positioning copy reflects consulting and speaking
  - STOP and wait for the user to confirm they approve the changes, or to request adjustments
  - Do NOT proceed to the next milestone until the user explicitly approves
  - If the user requests changes, make them and re-run this checkpoint before continuing

- [x] 5. Create the Consulting page (Milestone 3 — new /consulting/ page)
  - [x] 5.1 Create `consulting.markdown`
    - Create `consulting.markdown` in the project root with front matter: `layout: single`, `title: "Consulting"`, `permalink: /consulting/`, `classes: wide`, `author_profile: true`
    - Write outcome-oriented opening copy describing business value and delivery, placed before any technology listing (no tech list above this copy)
    - Add a deployed-forward model section stating all three phases: Elena joins a team, delivers a focused short-term project, then rolls off
    - Add a separate, clearly labeled long-term engagements section, visually and textually distinct from the deployed-forward model, within the same Consulting offering
    - Add a pricing statement: short-term projects are priced either per hour or per finished fixed-price project; direct visitors to contact Elena for pricing; include no specific rate, price amount, or numeric cost figure
    - Add an availability statement: short-term deployed-forward projects available now; long-term engagements available starting April 2027
    - Add at least one relevant client work reference with a link to `/portfolio/`
    - Add an action-oriented CTA (e.g., "Get in Touch" / "Book a Call") linking to a `mailto:` contact method, with an alternative contact method presented as a fallback
    - Use second-person, sales-oriented copy addressing engineering managers and CTOs
    - _Requirements: 4.1, 4.2, 4.3, 4.4, 4.5, 4.6, 4.7, 4.8, 4.9, 4.10, 4.11, 10.1, 10.2, 10.3, 10.4_

  - [x] 5.2 Verify Milestone 3 — consulting page renders correctly
    - Run `bundle exec jekyll build` and confirm zero errors
    - Verify `_site/consulting/index.html` exists and contains: deployed-forward three-phase text (joins, delivers short-term project, rolls off); a separate long-term engagements option; outcome-oriented copy appearing before any technology listing; per-hour or per-finished-fixed-price pricing language with no numeric cost figure; availability statements (short-term now, long-term April 2027); a link to `/portfolio/` and a client work reference; an action-oriented CTA linking to a contact method
    - _Requirements: 4.1–4.11, 10.1–10.4_

- [~] 6. Checkpoint — Approval gate after Milestone 3 (Consulting page)
  - Run `bundle exec jekyll serve` and open the site locally
  - Review the Consulting page: opening copy before tech, deployed-forward model, long-term engagements, pricing language (no numbers), availability, portfolio link, and CTA with fallback
  - STOP and wait for the user to confirm they approve the changes, or to request adjustments
  - Do NOT proceed to the next milestone until the user explicitly approves
  - If the user requests changes, make them and re-run this checkpoint before continuing

- [x] 7. Update homepage for two-pillar positioning (Milestone 4 — homepage reflects Consulting + Speaking)
  - [x] 7.1 Update `index.html` feature_row and hero
    - Change `feature_row` from three entries to exactly two: Consulting (first) and Speaking
    - Consulting entry: `btn--primary btn--large` for prominence, excerpt mentions both short-term deployed-forward projects and long-term engagements, `url: "/consulting/"`
    - Speaking entry retained with its existing content
    - Remove the Training pillar entirely
    - Update the hero `excerpt`/value proposition to name "Kotlin" and "cloud-native" and reference consulting and speaking (drop training)
    - _Requirements: 3.1, 3.2, 3.3, 3.4, 3.5_

  - [x] 7.2 Update homepage body availability note and remove training references
    - Update the availability note to three distinct statements: short-term deployed-forward projects available now, long-term consulting engagements available from April 2027, speaking engagements available now
    - Remove any training availability text or links from the homepage body
    - Preserve the social proof strip (PostNL, Bol.com, KPN, AZL/NN Group with text fallback), credibility indicators (Kotlin Crash Course author, AWS Community Builder, KotlinConf, AWS and Azure certifications), secondary CTAs, and the profile image reference (`profile.jpeg`)
    - _Requirements: 3.6, 3.7, 3.8, 3.9, 3.10, 8.1, 8.2_

  - [x] 7.3 Verify Milestone 4 — homepage renders correctly
    - Run `bundle exec jekyll build` and confirm zero errors
    - Verify `_site/index.html` contains exactly two service pillars with Consulting before Speaking in source order; the Consulting pillar mentions short-term deployed-forward and long-term engagements and links to `/consulting/`; the hero value proposition references consulting and speaking (no training); the updated availability note (short-term now, long-term April 2027, speaking now); social proof names; credibility indicators; and the profile image reference
    - _Requirements: 3.1–3.10, 8.1, 8.2_

- [~] 8. Checkpoint — Approval gate after Milestone 4 (homepage)
  - Run `bundle exec jekyll serve` and open the site locally
  - Review the homepage: two pillars (Consulting most prominent, before Speaking), the revised hero, and the revised availability note with no training references
  - STOP and wait for the user to confirm they approve the changes, or to request adjustments
  - Do NOT proceed to the next milestone until the user explicitly approves
  - If the user requests changes, make them and re-run this checkpoint before continuing

- [x] 9. Portfolio cleanup (Milestone 5 — no dangling training references)
  - [x] 9.1 Clean up `portfolio.markdown` training references
    - Verify the portfolio page retains all four clients (AZL/NN Group, PostNL, Bol.com, KPN) in impact-first format and the MockNest Serverless cross-reference linking to `/open-source/`
    - Remove or repoint any `/training/` link; tighten copy only if a training reference needs removing (otherwise leave existing impact-first content unchanged)
    - _Requirements: 7.1, 7.2, 7.3, 7.4_

  - [x] 9.2 Verify Milestone 5 — portfolio page renders correctly
    - Run `bundle exec jekyll build` and confirm zero errors
    - Verify `_site/portfolio/index.html` contains all four client names and the MockNest Serverless cross-reference to `/open-source/`, with no `/training/` links
    - _Requirements: 7.1–7.4_

- [~] 10. Checkpoint — Approval gate after Milestone 5 (portfolio cleanup)
  - Run `bundle exec jekyll serve` and open the site locally
  - Review the portfolio page: all four clients (AZL/NN Group, PostNL, Bol.com, KPN) in impact-first format, the MockNest Serverless cross-reference to `/open-source/`, and no dangling `/training/` links
  - STOP and wait for the user to confirm they approve the changes, or to request adjustments
  - Do NOT proceed to the next milestone until the user explicitly approves
  - If the user requests changes, make them and re-run this checkpoint before continuing

- [x] 11. Add second open source project (Milestone 6 — Open Source page lists two projects)
  - [x] 11.1 Add "AWS Lambda Response Streaming for JVM" entry to `open-source.markdown`
    - Add a second project entry alongside the existing MockNest Serverless entry, using the same repeatable heading + description entry-block pattern as MockNest
    - Add a text heading "AWS Lambda Response Streaming for JVM" (no logo image for this entry)
    - Add a description: a JVM library implementing the AWS Lambda / Amazon API Gateway HTTP response streaming protocol for Kotlin and Java, filling the gap where AWS only ships Node.js helpers for the wire format; key use case is streaming Server-Sent Events (SSE) including token-by-token LLM output from Amazon Bedrock
    - Add the GitHub repo link: `https://github.com/elenavanengelenmaslova/aws-lambda-response-streaming-jvm`
    - State the published dependency coordinate: `nl.vintik:aws-lambda-streaming-core`
    - List key features: implements the API Gateway response-streaming wire protocol (metadata JSON + 8-byte delimiter + body); memory-bounded streaming via a fixed 1 MB buffer (flat memory regardless of payload size); SSE streaming including Bedrock token-by-token LLM output; minimal dependencies (only kotlinx-serialization-json, no AWS artifacts); compiled for Java 21, runs on java21/java25 runtimes; Kotlin and Java example modules
    - List the tech stack: Kotlin, Java, AWS Lambda, Amazon API Gateway, kotlinx-serialization, Amazon Bedrock (SSE/LLM example)
    - Add an "Explore on GitHub" CTA linking to the repo
    - _Requirements: 6.6, 6.7, 6.8, 6.9, 6.10, 6.11, 6.12_

  - [x] 11.2 Verify Milestone 6 — open source page renders both projects
    - Run `bundle exec jekyll build` and confirm zero errors
    - Verify `_site/open-source/index.html` contains both the MockNest Serverless entry AND the new "AWS Lambda Response Streaming for JVM" heading, its GitHub repo link, the dependency coordinate `nl.vintik:aws-lambda-streaming-core`, the SSE/Bedrock mention, and its "Explore on GitHub" CTA
    - _Requirements: 6.1, 6.2, 6.6–6.12_

- [~] 12. Checkpoint — Approval gate after Milestone 6 (Open Source second project)
  - Run `bundle exec jekyll serve` and open the site locally
  - Review the Open Source page with both projects: the existing MockNest Serverless entry and the new "AWS Lambda Response Streaming for JVM" entry (heading, description, GitHub repo link, dependency coordinate, SSE/Bedrock mention, and GitHub CTA)
  - STOP and wait for the user to confirm they approve the changes, or to request adjustments
  - Do NOT proceed to the next milestone until the user explicitly approves
  - If the user requests changes, make them and re-run this checkpoint before continuing

- [x] 13. Final verification (Milestone 7 — full integrity check)
  - [x] 13.1 Production build and permalink/removal verification
    - Run `JEKYLL_ENV=production bundle exec jekyll build` and confirm zero errors
    - Verify remaining permalinks produce output files: `/`, `/consulting/` (new), `/portfolio/`, `/speaking/`, `/open-source/`, `/credentials/`, `/404.html` — each preserved byte-for-byte except the new Consulting page and the updated Open Source page
    - Verify all `_site/training/*` output files are gone (training landing page and all five course detail pages return 404 by absence)
    - _Requirements: 9.1, 9.2, 9.3, 9.4, 9.6_

  - [x] 13.2 Verify SEO, analytics, favicon, sitemap, and accessibility
    - Verify `_site/sitemap.xml` exists, includes `/consulting/`, and contains no `/training/` URLs
    - Verify built HTML contains the Google Analytics tracking script with ID `G-LN4HKRGKZG` and jekyll-seo-tag metadata
    - Verify the favicon link tag references `assets/images/logo.png`
    - Verify every content `<img>` has a non-empty `alt` attribute (decorative images use `alt=""`) and each page uses semantic sectioning with exactly one `<main>`
    - _Requirements: 1.6, 1.7, 9.7, 9.8, 9.9_

- [~] 14. Final checkpoint — Full visual walkthrough and approval gate
  - Run `JEKYLL_ENV=production bundle exec jekyll build` and confirm zero errors, then run `bundle exec jekyll serve` and open the site locally
  - Do a full visual walkthrough: homepage (two pillars), consulting, portfolio, speaking, open source (both projects), credentials, and 404. Confirm training is gone everywhere, navigation shows Consulting, CTAs work, third-party widgets (Credly, Sessionize) and analytics load, and layout is responsive
  - STOP and wait for the user to confirm they approve the finished site, or to request adjustments
  - Do NOT consider the plan complete until the user explicitly approves
  - If the user requests changes, make them and re-run this checkpoint before continuing

## Notes

- **This is a delta plan.** The theme migration to Minimal Mistakes and the sales-oriented rewrites of the homepage, portfolio, speaking, open-source, and credentials pages are already implemented. These tasks only cover the repositioning away from Training toward the new Consulting offering plus the addition of a second open source project.
- Each milestone (tasks 1, 3, 5, 7, 9, 11, 13) produces a locally testable state via `bundle exec jekyll serve`.
- Checkpoints (tasks 2, 4, 6, 8, 10, 12, 14) are mandatory human-in-the-loop approval gates. At every checkpoint the agent runs the site locally, the user reviews the milestone's changes, and the agent halts and waits for explicit user sign-off before the next milestone begins. If the user requests changes, the agent makes them and re-runs the checkpoint.
- All existing permalinks are preserved; the only URL additions/removals are the new `/consulting/` page and the intentional removal of all `/training/` paths.
- **Property-based testing does not apply** to this static site redesign. The acceptance criteria describe visual presentation, content presence, configuration correctness, and integration preservation — none can be meaningfully expressed as "for all inputs X, property P(X) holds." Verification uses build smoke tests, HTML output assertions, and permalink/removal checks.
- Each task references specific requirements for traceability.

## Task Dependency Graph

```json
{
  "waves": [
    { "id": 0, "tasks": ["1.1", "1.2", "3.1", "3.2", "5.1", "11.1"] },
    { "id": 1, "tasks": ["1.3", "3.3", "5.2", "7.1", "11.2"] },
    { "id": 2, "tasks": ["7.2", "9.1"] },
    { "id": 3, "tasks": ["7.3", "9.2"] },
    { "id": 4, "tasks": ["13.1"] },
    { "id": 5, "tasks": ["13.2"] }
  ]
}
```
