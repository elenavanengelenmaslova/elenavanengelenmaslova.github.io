# Requirements Document

## Introduction

This document specifies the requirements for a comprehensive redesign of Elena van Engelen-Maslova's freelance professional website (elenavanengelenmaslova.github.io). The site currently runs on Jekyll with the default Minima theme and has generated almost zero inbound leads in approximately two years. The redesign transforms the site from a CV-style presentation into a client acquisition tool that generates inbound leads for consulting, training, and speaking engagements. The site must remain on Jekyll + GitHub Pages throughout.

## Glossary

- **Site**: The Jekyll-based website hosted at elenavanengelenmaslova.github.io
- **Theme_Engine**: The Jekyll theme system that controls visual presentation, layouts, and styling
- **Homepage**: The landing page at the root URL of the Site
- **Hero_Section**: A prominent banner area at the top of the Homepage containing the value proposition and primary call-to-action
- **Service_Pillar**: One of three primary service offerings displayed on the Homepage (Consulting, Training, Speaking)
- **Social_Proof_Strip**: A horizontal section displaying client company logos to establish credibility
- **CTA**: A call-to-action element (button or link) that directs visitors toward a conversion action such as booking a call or sending an email
- **Training_Page**: The main page listing all available Kotlin training offerings
- **Training_Detail_Page**: An individual page describing a specific training course
- **Speaking_Page**: The page showcasing speaking experience and availability for event organizers
- **Speaker_Bio_Section**: A dedicated area on the Speaking_Page containing a concise biography formatted for conference organizers
- **Open_Source_Page**: A new page showcasing open source projects, starting with MockNest Serverless
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

**User Story:** As a site visitor, I want to see a modern, professional website design, so that I perceive Elena as a credible, high-quality freelance engineer and trainer.

#### Acceptance Criteria

1. THE Theme_Engine SHALL use a modern Jekyll theme (such as Minimal Mistakes) or equivalent custom styling that replaces the default Minima theme
2. THE Theme_Engine SHALL render all pages using a sans-serif font stack that includes Inter and system fonts as fallbacks
3. THE Theme_Engine SHALL apply consistent whitespace, visual hierarchy, and Card_Layout patterns across all pages
4. THE Theme_Engine SHALL support responsive layouts that render correctly on desktop, tablet, and mobile screen widths
5. THE Theme_Engine SHALL remain compatible with GitHub_Pages supported build processes and plugins
6. THE Theme_Engine SHALL preserve the existing Google_Analytics integration (tracking ID: G-LN4HKRGKZG)
7. THE Theme_Engine SHALL preserve the existing SEO_Plugins (jekyll-seo-tag and jekyll-sitemap) functionality
8. THE Theme_Engine SHALL preserve the existing Credly_Badges integration on the Credentials_Page
9. THE Theme_Engine SHALL preserve the existing Sessionize_Widget integration on the Speaking_Page
10. WHEN a visitor loads any page, THE Site SHALL render the page with a clean, professional appearance that uses adequate whitespace and clear typographic hierarchy

### Requirement 2: Navigation Restructuring

**User Story:** As a site visitor, I want clear navigation that helps me find relevant information quickly, so that I can evaluate Elena's services without confusion.

#### Acceptance Criteria

1. THE Navigation_Bar SHALL display links to: Portfolio, Training, Speaking, Open Source, Credentials, and Blog (external link to Medium)
2. THE Navigation_Bar SHALL include the Open_Source_Page as a new navigation item
3. WHEN a visitor clicks the Blog link in the Navigation_Bar, THE Site SHALL open the external Medium blog in a new browser tab
4. THE Navigation_Bar SHALL render correctly on both desktop and mobile screen widths with a responsive menu pattern

### Requirement 3: Homepage Redesign

**User Story:** As a potential client visiting the site for the first time, I want to immediately understand what Elena offers and why she is credible, so that I can decide whether to explore further or get in touch.

#### Acceptance Criteria

1. THE Homepage SHALL display a Hero_Section at the top of the page containing a clear value proposition focused on Kotlin and cloud-native consulting, training, and speaking
2. THE Hero_Section SHALL include a primary CTA that directs visitors to initiate contact (such as "Book a Call" or "Get in Touch")
3. THE Homepage SHALL display three Service_Pillar sections for Consulting, Training, and Speaking, with Consulting presented as the most prominent offering
4. WHEN a visitor views the Service_Pillar sections, THE Homepage SHALL present Consulting with greater visual prominence than Training and Speaking (through size, position, or styling)
5. THE Homepage SHALL display a Social_Proof_Strip containing company logos or names for PostNL, Bol.com, KPN, and AZL (NN Group)
6. THE Homepage SHALL display a current availability note stating that project work is available from April 2027 and that training and speaking engagements are available now
7. THE Homepage SHALL include at least two CTA elements directing visitors toward contact or service pages
8. THE Homepage SHALL display key credibility indicators including: published author of Kotlin Crash Course, AWS Community Builder, conference speaker at KotlinConf and other major events, and AWS/Azure certifications

### Requirement 4: Training Page Redesign

**User Story:** As a team lead or L&D manager, I want to understand the business outcomes and logistics of Kotlin training, so that I can evaluate whether to book training for my team.

#### Acceptance Criteria

1. THE Training_Page SHALL lead with outcome-oriented copy that emphasizes business value and team productivity gains rather than course syllabi
2. THE Training_Page SHALL display pricing information starting from €2,000 per day for corporate training
3. THE Training_Page SHALL state that travel and accommodation costs apply for on-site training outside the Netherlands
4. THE Training_Page SHALL state that remote training is available worldwide and on-site training is available in Europe
5. THE Training_Page SHALL display student testimonials in a prominent position near the top of the page, above or alongside the course listings
6. THE Training_Page SHALL include CTA elements with action-oriented text such as "Book a Call" that link to a contact method
7. WHEN a visitor views a training course listing, THE Training_Page SHALL provide a link to the corresponding Training_Detail_Page
8. THE Training_Page SHALL list the organizations that have received training (AZL/NN Group, Version 1, EDSN) as social proof

### Requirement 5: Training Detail Page Improvements

**User Story:** As a team lead evaluating a specific course, I want to understand what my team will gain and how to book, so that I can make a purchasing decision.

#### Acceptance Criteria

1. WHEN a visitor views a Training_Detail_Page, THE Training_Detail_Page SHALL present course content with outcome-oriented descriptions that emphasize what participants will be able to do after the training
2. THE Training_Detail_Page SHALL include at least one CTA element with action-oriented text such as "Book This Training" that links to a contact method
3. THE Training_Detail_Page SHALL retain the existing course structure and content details while improving the sales-oriented framing

### Requirement 6: Speaking Page Redesign

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

### Requirement 7: Open Source Page Creation

**User Story:** As a developer or potential client, I want to see Elena's open source contributions, so that I can assess her technical depth and community involvement.

#### Acceptance Criteria

1. THE Open_Source_Page SHALL be a new page accessible from the Navigation_Bar
2. THE Open_Source_Page SHALL use a structure that supports listing multiple open source projects over time
3. THE Open_Source_Page SHALL display MockNest Serverless as the first project entry with the following details: project description as a serverless WireMock-compatible mock runtime for AWS with AI-powered mock generation using Amazon Bedrock, a link to the GitHub repository (https://github.com/elenavanengelenmaslova/mocknest-serverless), key features (WireMock-compatible, AI mock generation from OpenAPI/WSDL/GraphQL specs, one-click SAR deployment), and the technology stack (Kotlin, AWS Lambda with SnapStart, Amazon S3, Amazon Bedrock, SQS, API Gateway, AWS SAM, Koog Agent)
4. THE Open_Source_Page SHALL mention that MockNest Serverless won the Creative Track Award in the AWS 10,000 AIdeas Competition as text without a badge image
5. THE Open_Source_Page SHALL include a CTA element encouraging visitors to explore the project on GitHub

### Requirement 8: Portfolio Page Refinement

**User Story:** As a potential consulting client, I want to see concise, results-oriented project descriptions, so that I can quickly assess Elena's ability to deliver business value.

#### Acceptance Criteria

1. THE Portfolio_Page SHALL present project descriptions that lead with business impact and measurable results rather than detailed technical implementation narratives
2. THE Portfolio_Page SHALL use a concise format for each project that includes: client name, role, key business outcome, and technologies used
3. THE Portfolio_Page SHALL include a cross-reference entry for MockNest Serverless linking to the Open_Source_Page
4. THE Portfolio_Page SHALL retain all four current client projects (AZL/NN Group, PostNL, Bol.com, KPN) with tightened descriptions

### Requirement 9: Profile Picture Accommodation

**User Story:** As the site owner, I want the site layout to accommodate an updated profile picture, so that I can replace the current image with a new one featuring an AI-generated background.

#### Acceptance Criteria

1. THE Homepage SHALL display the profile picture in a prominent position within or near the Hero_Section
2. THE Site SHALL reference the profile image from the existing file path (assets/images/profile.jpeg) so that a manual image replacement takes effect without code changes

### Requirement 10: Technical Integrity and Compatibility

**User Story:** As the site owner, I want all technical integrations and SEO setup preserved after the redesign, so that I do not lose search engine rankings, analytics data, or third-party functionality.

#### Acceptance Criteria

1. THE Site SHALL build and serve correctly using `bundle exec jekyll serve` for local testing
2. THE Site SHALL deploy successfully to GitHub_Pages without build errors
3. THE Site SHALL preserve all existing page permalinks to avoid breaking external links and search engine indexing
4. IF a build error occurs during local testing, THEN THE Site SHALL provide a clear error message through Jekyll's standard error output
5. THE Site SHALL use only Jekyll plugins that are supported by GitHub_Pages or are included as gems in the Gemfile
6. THE Site SHALL preserve the existing favicon (assets/images/logo.png)
7. THE Site SHALL maintain semantic HTML structure and include alt text on all images for accessibility compliance

### Requirement 11: Content Tone and Messaging

**User Story:** As a potential client, I want the site copy to speak to my needs and challenges, so that I feel confident Elena understands my business context and can deliver value.

#### Acceptance Criteria

1. THE Site SHALL use sales-oriented copy across all pages that leads with client value and outcomes rather than self-descriptive CV-style language
2. THE Site SHALL address the target audience directly using second-person language ("your team", "your project") where appropriate
3. THE Site SHALL maintain a professional yet approachable tone consistent with a senior freelance engineer's personal brand
4. THE Site SHALL avoid jargon-heavy descriptions that only appeal to technical peers and instead frame services in terms that resonate with decision-makers (engineering managers, CTOs, L&D leads, conference organizers)
