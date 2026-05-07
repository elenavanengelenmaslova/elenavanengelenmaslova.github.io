---
layout: single
title: Open Source
permalink: /open-source/
classes: wide
---

I believe in building in the open. Open source is where I experiment with new ideas, contribute back to the developer community, and push the boundaries of what is possible with Kotlin and cloud-native technologies. Below are projects I have created and actively maintain.

---

## <img src="/assets/images/logos/MockNestServerless-logo.png" alt="MockNest Serverless logo" style="height: 40px; width: auto; vertical-align: middle; margin-right: 8px;">MockNest Serverless

A serverless, WireMock-compatible mock runtime for AWS with AI-powered mock generation using Amazon Bedrock. MockNest Serverless lets your team spin up realistic API mocks in minutes — no infrastructure to manage, no complex setup.

🏆 **Creative Track Award** — <a href="https://builder.aws.com/content/3D5gTWIjP2zvKncBZBCs849xRqn/aws-10000-aideas-competition-meet-the-winners" target="_blank" rel="noopener">AWS 10,000 AIdeas Competition (2025)</a>

**Key Features:**

- **WireMock-compatible** — Drop-in replacement for existing WireMock stub mappings, so your team can migrate without rewriting mocks
- **AI-powered mock generation** — Automatically generate mock definitions from OpenAPI, WSDL, and GraphQL specs using Amazon Bedrock
- **One-click SAR deployment** — Deploy to your AWS account in minutes via the AWS Serverless Application Repository
- **Webhook support** — Simulate asynchronous callback flows for realistic integration testing
- **Persistent mocks across cold starts** — Mocks survive Lambda cold starts, ensuring consistent behavior in serverless environments

**Tech Stack:** Kotlin · AWS Lambda (SnapStart) · Amazon S3 · Amazon Bedrock (Nova Pro) · SQS · API Gateway · AWS SAM · Koog Agent

[Explore on GitHub](https://github.com/elenavanengelenmaslova/mocknest-serverless){:target="_blank" rel="noopener" .btn .btn--primary .btn--large}
