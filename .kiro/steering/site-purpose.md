---
inclusion: auto
---

# Website Purpose & Business Goals

## Primary Purpose
This is a personal professional website for Elena van Engelen-Maslova, a freelance Senior/Lead Software Engineer based in the Netherlands. The site serves as a **client acquisition and business development tool** — its job is to generate inbound leads for consulting, training, and speaking engagements.

## Business Goals (Priority Order)
1. **Attract freelance engineering clients** — Companies looking for a Kotlin/cloud-native specialist for contract work. This is the primary revenue stream and must remain the most prominent offering on the site.
2. **Generate paid training bookings** — Teams wanting Kotlin training (basics through serverless cloud). Currently generating zero inbound requests.
3. **Get invited to paid speaking engagements** — Conference organizers and corporate event planners. Only one inbound request in ~2 years. Also open to unpaid talks at select conferences.
4. **Showcase open source work** — Demonstrate technical depth and community contribution via MockNest Serverless (AWS 10,000 AIdeas Competition Finalist).

## Target Audiences
- **Engineering managers / CTOs** evaluating freelance senior engineers for Kotlin/cloud projects
- **L&D / team leads** looking for Kotlin training for their development teams
- **Conference organizers** seeking speakers on Kotlin and serverless cloud topics
- **Developer community** — peers who may refer work or collaborate

## Current Challenges (Why the Site Isn't Working)
- The site has generated almost no inbound leads in ~2 years
- Only one talk request came through the site; zero training or consulting requests
- Work is found primarily through agencies, LinkedIn, and self-applying to (unpaid) conferences
- The site reads more like a CV/resume than a sales tool — it describes what Elena does, not what value she delivers to clients
- No clear calls-to-action or value propositions targeted at decision-makers (buyers, not peers)
- Training pages are course catalogs (topics/objectives) rather than sales pages (outcomes/ROI)
- Speaking page lists past talks but doesn't sell Elena as a bookable speaker
- Portfolio reads like a CV with long project descriptions instead of highlighting business impact
- The visual design uses the default Minima Jekyll theme, which looks dated and generic
- No pricing signals on training (even ranges) to filter serious inquiries

## Key Differentiators
- Published author: *Kotlin Crash Course* book
- AWS Community Builder (Serverless)
- AWS + Azure certified (multiple certs)
- Conference speaker at KotlinConf, InfoQ Dev Summit, Voxxed Days
- Featured in Kotlin Weekly, JetBrains Blog, Android Weekly, and other publications
- 20+ years of software engineering experience
- Real enterprise experience at PostNL, Bol.com, KPN, AZL (NN Group)
- Open source: MockNest Serverless — serverless WireMock-compatible mock runtime on AWS with AI-powered mock generation (Amazon Bedrock). AWS 10,000 AIdeas Competition Finalist.
- InfoQ Podcast guest

## Current Availability
- Currently on a project with AZL (NN Group) through ~April 2027
- Available for training and speaking engagements now
- Next availability for project work: April 2027

## MockNest Serverless (Open Source Project)
- **What**: A serverless WireMock-compatible mock runtime for AWS that enables realistic integration testing without live external services, with AI-assisted mock generation using Amazon Bedrock
- **Tech**: Kotlin, AWS Lambda (SnapStart), Amazon S3, Amazon Bedrock (Nova Pro), SQS, API Gateway, AWS SAM, Koog Agent
- **Status**: Winner — Creative Track Award, AWS 10,000 AIdeas Competition
- **Repo**: https://github.com/elenavanengelenmaslova/mocknest-serverless
- **Key features**: WireMock-compatible, AI mock generation from OpenAPI/WSDL/GraphQL specs, one-click SAR deployment, webhook support, persistent mocks across cold starts
- **Articles**: "Goodbye Flaky External APIs — Hello Mocking in the Cloud", "AIdeas Finalist: MockNest Serverless"

## Redesign Direction
- **Visual refresh**: Move away from default Minima to a modern, professional look. Consider switching to a more capable Jekyll theme (e.g., Minimal Mistakes) or heavily customizing Minima with modern CSS. Target: clean sans-serif typography, more whitespace, card-based layouts, visual hierarchy.
- **Content rewrite**: Shift from CV-style to sales-oriented copy. Lead with value propositions and outcomes, not technical descriptions.
- **Immediate focus**: Training and speaking page improvements (these are the underperforming areas). Consultancy remains most prominent but is currently working via other channels.
- **Add MockNest Serverless**: Either as part of portfolio or a new Open Source section.
- **User wants to review visually at each milestone** — changes should be testable locally with `bundle exec jekyll serve`.

## Technical Stack
- Jekyll static site hosted on GitHub Pages
- Minima theme (to be upgraded/replaced)
- Google Analytics enabled (G-LN4HKRGKZG)
- Sessionize integration for speaking schedule
- Must remain compatible with GitHub Pages
