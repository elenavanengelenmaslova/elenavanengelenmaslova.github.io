# Requirements Document

## Introduction

This document specifies the requirements for a comprehensive redesign of Elena van Engelen-Maslova's freelance professional website (elenavanengelenmaslova.github.io). The site runs on Jekyll with the Minimal Mistakes theme and GitHub Pages hosting. The redesign transforms the site from a CV-style presentation into a client acquisition tool that generates inbound leads for consulting and speaking engagements.

This revision changes the service positioning. Training is removed entirely. In its place, the site now offers a short-term consultancy model based on a "deployed forward engineer" approach: Elena joins a team, delivers a focused short-term project, then rolls off. Short-term projects sit alongside long-term engagements, and both are consolidated under a single Consulting offering. The site therefore presents two service pillars — Consulting and Speaking — with Consulting as the most prominent. The site must remain on Jekyll + GitHub Pages throughout.

## Glossary

- **Site**: The Jekyll-based website hosted at elenavanengelenmaslova.github.io
- **Theme_Engine**: The Jekyll theme system (Minimal Mistakes) that controls visual presentation, layouts, and styling
- **Homepage**: The landing page at the root URL of the Site
- **Hero_Section**: A prominent banner area at the top of the Homepage containing the value proposition and primary call-to-action
- **Service_Pillar**: One of two primary service offerings displayed on the Homepage (Consulting, Speaking)
- **Consulting_Offering**: The combined consulting service encompassing both short-term deployed-forward projects and long-term engagements
- **Deployed_Forward_Model**: The short-term consultancy model in which Elena joins a team, delivers a focused short-term project, then rolls off
- **Consulting_Page**: A dedicated page describing the Consulting_Offering, including the short-term deployed-forward model and long-term engagements
- **Social_Proof_Strip**: A horizontal section displaying client company logos to establish credibility
- **CTA**: A call-to-action element (button or link) that directs visitors toward a conversion action such as booking a call or sending an email
- **Speaking_Page**: The page showcasing speaking experience and availability for event organizers
- **Speaker_Bio_Section**: A dedicated area on the Speaking_Page containing a concise biography formatted for conference organizers
- **Open_Source_Page**: A page showcasing open source projects, starting with MockNest Serverless
- **Portfolio_Page**: The page displaying selected professional project highlights
- **Credentials_Page**: The page displaying certifications and academic achievements
- **Navigation_Bar**: The site-wide header navigation component
- **Card_Layout**: A visual pattern using bordered/shadowed containers to group related content
- **GitHub_Pages**: The hosting platform constraining plugin and build compatibility
- **Sessionize_Widget**: The embedded JavaScript widget from Sessionize displaying upcoming speaking engagements
- **Credly_Badges**: The embedded JavaScript widgets from Credly displaying verified AWS certifications
- **Google_Analytics**: The analytics tracking service (ID: G-LN4HKRGKZG) integrated into the Site
- **SEO_Plugins**: The jekyll-seo-tag and jekyll-sitemap plugins that support search engine optimization

## Requirements

### Requirement 1: Theme and Visual Modernization

**User Story:** As a site visitor, I want to see a modern, professional website design, so that I perceive Elena as a credible, high-quality freelance engineer.

#### Acceptance Criteria

1. THE Theme_Engine SHALL use the Minimal Mistakes Jekyll theme or equivalent custom styling that replaces the default Minima theme
2. THE Theme_Engine SHALL render all pages using a sans-serif font stack that includes Inter and system fonts as fallbacks
3. THE Theme_Engine SHALL apply consistent whitespace, visual hierarchy, and Card_Layout patterns across all pages
4. THE Theme_Engine SHALL support responsive layouts that render correctly on desktop, tablet, and mobile screen widths
5. THE Theme_Engine SHALL remain compatible with GitHub_Pages supported build processes and plugins
6. THE Theme_Engine SHALL preserve the existing Google_Analytics integration (tracking ID: G-LN4HKRGKZG)
7. THE Theme_Engine SHALL preserve the existing SEO_Plugins (jekyll-seo-tag and jekyll-sitemap) functionality
8. THE Theme_Engine SHALL preserve the existing Credly_Badges integration on the Credentials_Page
9. THE Theme_Engine SHALL preserve the existing Sessionize_Widget integration on the Speaking_Page
10. WHEN a visitor loads any page, THE Site SHALL render the page with clear typographic hierarchy and consistent spacing

### Requirement 2: Navigation Restructuring

**User Story:** As a site visitor, I want clear navigation that helps me find relevant information quickly, so that I can evaluate Elena's services without confusion.

#### Acceptance Criteria

1. THE Navigation_Bar SHALL display exactly the following items in order: Consulting, Portfolio, Speaking, Open Source, Credentials, Blog, with no additional items
2. THE Navigation_Bar SHALL link Consulting to the Consulting_Page
3. THE Navigation_Bar SHALL NOT display any item labeled Training, and WHEN a visitor requests a former /training/ path, THE Site SHALL return its standard 404 response
4. WHEN a visitor clicks the Blog link in the Navigation_Bar, THE Site SHALL open the external Medium blog in a new browsing context while keeping the current page open
5. WHILE the viewport width is at or above 768px, THE Navigation_Bar SHALL display its items inline; WHILE the viewport width is below 768px, THE Navigation_Bar SHALL collapse its items behind a toggle control

### Requirement 3: Homepage Redesign

**User Story:** As a potential client visiting the site for the first time, I want to immediately understand what Elena offers and why she is credible, so that I can decide whether to explore further or get in touch.

#### Acceptance Criteria

1. THE Homepage SHALL display a Hero_Section as the first visible section above the fold, containing a value proposition text that names both "Kotlin" and "cloud-native" and references both consulting and speaking
2. THE Hero_Section SHALL include exactly one primary CTA element that links to the contact page or contact mechanism and uses action-oriented label text (such as "Book a Call" or "Get in Touch")
3. THE Homepage SHALL display exactly two Service_Pillar sections, one labeled Consulting and one labeled Speaking, with the Consulting Service_Pillar positioned before the Speaking Service_Pillar in the page source order
4. WHEN a visitor views the Consulting Service_Pillar, THE Homepage SHALL present the Consulting_Offering within a single pillar and SHALL include text describing both short-term deployed-forward projects and long-term engagements
5. WHEN a visitor views the Service_Pillar sections, THE Homepage SHALL render the Consulting Service_Pillar with greater visual prominence than the Speaking Service_Pillar through at least one of: larger allocated area, higher vertical position, or distinct emphasis styling
6. THE Homepage SHALL display a Social_Proof_Strip containing a logo image or text name for each of the following four organizations: PostNL, Bol.com, KPN, and AZL (NN Group)
7. THE Homepage SHALL display an availability note containing three distinct statements: short-term deployed-forward projects are available now, long-term consulting engagements are available from April 2027, and speaking engagements are available now
8. THE Homepage SHALL include at least two CTA elements, each linking to the contact page, a service page, or the contact mechanism
9. THE Homepage SHALL display credibility indicators that include all of the following: published author of "Kotlin Crash Course", AWS Community Builder, conference speaker referencing KotlinConf, and AWS and Azure certifications
10. IF the Social_Proof_Strip cannot load one or more logo images, THEN THE Homepage SHALL display the corresponding organization name as text so that all four organizations remain identifiable

### Requirement 4: Consulting Page

**User Story:** As an engineering manager or CTO, I want to understand how Elena can help my team through either a focused short-term project or a longer engagement, so that I can decide to get in touch.

#### Acceptance Criteria

1. THE Consulting_Page SHALL be reachable through a Navigation_Bar link that is present on every rendered site page
2. WHEN a visitor selects the Consulting_Page link in the Navigation_Bar, THE Consulting_Page SHALL load and render its content
3. THE Consulting_Page SHALL describe the Deployed_Forward_Model as a short-term consultancy approach that states all three phases: Elena joins a team, delivers a focused short-term project, and then rolls off
4. THE Consulting_Page SHALL present long-term consulting engagements as a separate, clearly labeled option within the same Consulting_Offering, visually and textually distinct from the Deployed_Forward_Model
5. THE Consulting_Page SHALL place outcome-oriented copy that describes business value and delivery before any technology listing, and SHALL NOT include a list of technologies above that copy
6. THE Consulting_Page SHALL state that short-term projects are priced either per hour or per finished fixed-price project
7. THE Consulting_Page SHALL direct visitors to contact Elena for pricing and SHALL NOT display any specific rate, price amount, or numeric cost figure
8. THE Consulting_Page SHALL state that short-term deployed-forward projects are available now and that long-term engagements are available starting April 2027
9. THE Consulting_Page SHALL display at least one CTA element whose visible text is action-oriented (such as "Get in Touch" or "Book a Call") and that links to a contact method
10. IF the linked contact method is unavailable or the CTA link target cannot be resolved, THEN THE Consulting_Page SHALL present an alternative contact method or an error message indicating the contact option is temporarily unavailable
11. THE Consulting_Page SHALL reference at least one relevant client work item and SHALL include a link to the Portfolio_Page

### Requirement 5: Speaking Page Redesign

**User Story:** As a conference organizer, I want to quickly evaluate Elena as a potential speaker and find the information I need to extend an invitation, so that I can book her for my event.

#### Acceptance Criteria

1. THE Speaking_Page SHALL display a Speaker_Bio_Section containing a concise biography suitable for conference organizer use
2. THE Speaking_Page SHALL list available talk topics with their supported formats (keynote, session, workshop, live coding demo)
3. THE Speaking_Page SHALL describe what organizers receive when booking Elena, including audience size experience, live coding demonstrations, and practical content
4. THE Speaking_Page SHALL state that Elena is open to both paid and unpaid speaking engagements at select conferences
5. THE Speaking_Page SHALL highlight notable speaking metrics, including that the Voxxed Days Amsterdam 2025 talk was among the top 4 most-viewed
6. THE Speaking_Page SHALL preserve the existing Sessionize_Widget integration for displaying upcoming talks
7. THE Speaking_Page SHALL include a CTA element directing organizers to initiate a speaking invitation via email
8. THE Speaking_Page SHALL list past recorded talks with links to video recordings

### Requirement 6: Open Source Page

**User Story:** As a developer or potential client, I want to see Elena's open source contributions, so that I can assess her technical depth and community involvement.

#### Acceptance Criteria

1. WHEN a visitor selects the Open Source link in the Navigation_Bar, THE Open_Source_Page SHALL be displayed
2. THE Open_Source_Page SHALL render each open source project as a discrete, repeatable entry block so that additional projects can be added without altering the page structure
3. THE Open_Source_Page SHALL display MockNest Serverless as the first project entry with all of the following: a project description identifying it as a serverless WireMock-compatible mock runtime for AWS with AI-powered mock generation using Amazon Bedrock, a link to the GitHub repository (https://github.com/elenavanengelenmaslova/mocknest-serverless), the key features list (WireMock-compatible, AI mock generation from OpenAPI/WSDL/GraphQL specs, one-click SAR deployment), and the technology stack list (Kotlin, AWS Lambda with SnapStart, Amazon S3, Amazon Bedrock, SQS, API Gateway, AWS SAM, Koog Agent)
4. THE Open_Source_Page SHALL display, as text and without a badge image, a statement that MockNest Serverless won the Creative Track Award in the AWS 10,000 AIdeas Competition
5. THE Open_Source_Page SHALL display, within the MockNest Serverless entry, a call-to-action element that links to the MockNest Serverless GitHub repository (https://github.com/elenavanengelenmaslova/mocknest-serverless)
6. THE Open_Source_Page SHALL display a second project entry, headed "AWS Lambda Response Streaming for JVM", rendered using the same entry block structure as the MockNest Serverless entry, with both entries visible on the page
7. THE Open_Source_Page SHALL display, within the "AWS Lambda Response Streaming for JVM" entry, a project description identifying it as a JVM library that implements the AWS Lambda and Amazon API Gateway HTTP response streaming protocol for Kotlin and Java, stating that it fills the gap left by AWS providing only Node.js helpers for the wire format, and naming streaming Server-Sent Events including token-by-token LLM output from Amazon Bedrock as a key use case
8. THE Open_Source_Page SHALL display, within the "AWS Lambda Response Streaming for JVM" entry, a link to the GitHub repository (https://github.com/elenavanengelenmaslova/aws-lambda-response-streaming-jvm)
9. THE Open_Source_Page SHALL display, within the "AWS Lambda Response Streaming for JVM" entry, the published dependency coordinate nl.vintik:aws-lambda-streaming-core
10. THE Open_Source_Page SHALL display, within the "AWS Lambda Response Streaming for JVM" entry, a key features list containing all of the following items: implementation of the API Gateway response-streaming wire protocol (metadata JSON, an 8-byte delimiter, and body) so JVM developers do not hand-roll it; memory-bounded streaming through a fixed 1 MB buffer that keeps memory usage flat regardless of payload size; Server-Sent Events streaming including token-by-token LLM output from Amazon Bedrock; minimal dependencies (only kotlinx-serialization-json and no AWS artifacts); compilation for Java 21 with support for the java21 and java25 Lambda runtimes; and inclusion of Kotlin and Java example modules
11. THE Open_Source_Page SHALL display, within the "AWS Lambda Response Streaming for JVM" entry, a technology stack list containing Kotlin, Java, AWS Lambda, Amazon API Gateway, kotlinx-serialization, and Amazon Bedrock (for the SSE and LLM example)
12. THE Open_Source_Page SHALL display, within the "AWS Lambda Response Streaming for JVM" entry, a call-to-action element that links to the GitHub repository (https://github.com/elenavanengelenmaslova/aws-lambda-response-streaming-jvm)

### Requirement 7: Portfolio Page Refinement

**User Story:** As a potential consulting client, I want to see concise, results-oriented project descriptions, so that I can quickly assess Elena's ability to deliver business value.

#### Acceptance Criteria

1. THE Portfolio_Page SHALL present project descriptions that lead with business impact and measurable results rather than detailed technical implementation narratives
2. THE Portfolio_Page SHALL use a concise format for each project that includes: client name, role, key business outcome, and technologies used
3. THE Portfolio_Page SHALL include a cross-reference entry for MockNest Serverless linking to the Open_Source_Page
4. THE Portfolio_Page SHALL retain all four current client projects (AZL/NN Group, PostNL, Bol.com, KPN) with tightened descriptions

### Requirement 8: Profile Picture Accommodation

**User Story:** As the site owner, I want the site layout to accommodate an updated profile picture, so that I can replace the current image with a new one featuring an AI-generated background.

#### Acceptance Criteria

1. THE Homepage SHALL display the profile picture in a prominent position within or near the Hero_Section
2. THE Site SHALL reference the profile image from the existing file path (assets/images/profile.jpeg) so that a manual image replacement takes effect without code changes

### Requirement 9: Technical Integrity and Compatibility

**User Story:** As the site owner, I want all technical integrations and SEO setup preserved after the redesign, so that I do not lose search engine rankings, analytics data, or third-party functionality.

#### Acceptance Criteria

1. WHEN `bundle exec jekyll serve` is executed, THE Site SHALL complete the build with zero build errors and serve all remaining pages over the local Jekyll server
2. WHEN the site is deployed to GitHub_Pages, THE Site SHALL complete the GitHub_Pages build with zero build errors and publish all remaining pages
3. THE Site SHALL preserve, byte-for-byte, the existing permalink of every page that remains after the redesign, excluding the intentionally removed /training/ permalinks defined in criterion 4
4. THE Site SHALL remove the training landing page and all five Kotlin course detail pages, and THE Site SHALL remove every /training/ permalink so that requests to those paths return the site's standard 404 (Not Found) response
5. IF a build error occurs during `bundle exec jekyll serve` or GitHub_Pages deployment, THEN THE Site SHALL halt the build and emit an error message through Jekyll's standard error output identifying the file and cause of the failure
6. THE Site SHALL use only Jekyll plugins that are on the GitHub_Pages supported-plugins list or are declared as gems in the Gemfile
7. THE Site SHALL preserve the existing favicon referenced at assets/images/logo.png without changing its path or file
8. THE Site SHALL render every page using semantic HTML sectioning elements (header, nav, main, footer) with exactly one main element per page
9. THE Site SHALL include a non-empty alt attribute on every content image, and THE Site SHALL use an empty alt attribute (alt="") on every decorative image

### Requirement 10: Content Tone and Messaging

**User Story:** As a potential client, I want the site copy to speak to my needs and challenges, so that I feel confident Elena understands my business context and can deliver value.

#### Acceptance Criteria

1. THE Site SHALL use sales-oriented copy across all pages that leads with client value and outcomes rather than self-descriptive CV-style language
2. THE Site SHALL address the target audience directly using second-person language ("your team", "your project") where appropriate
3. THE Site SHALL maintain a professional yet approachable tone consistent with a senior freelance engineer's personal brand
4. THE Site SHALL frame services in terms that resonate with decision-makers (engineering managers, CTOs, conference organizers) rather than jargon-heavy descriptions aimed only at technical peers
