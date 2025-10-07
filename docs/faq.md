---
layout: docs
title: Frequently Asked Questions
---

# Frequently Asked Questions

## General & Philosophy

### What is Xplorer?

Xplorer is a secure, local-first API collection runner designed for developers and enterprises who prioritize data privacy and a streamlined workflow. It's a powerful desktop application for making ad-hoc API calls, exploring responses, and running your existing API collections without cloud-based compromises.

### What makes Xplorer different from Postman, Insomnia, and other API clients?

**The key difference is our local-first philosophy:**

- **No Cloud, No Compromise:** Unlike cloud-based tools, Xplorer runs entirely on your local machine. Your collections, environment variables, and API secrets are never synced to a cloud server, eliminating the risk of cloud-based data leaks.
- **No Accounts Needed:** You don't need to create an account or log in to use Xplorer. Just download it and start working.
- **No Telemetry or Nagware:** We have a strict policy of not collecting any usage data. Your work is your own. We also don't interrupt you with pop-ups or feature-begging.
- **Zero Migration:** Xplorer is designed to work with your existing collections instantly, with no need for modifications.
- **Unlimited Test Runs:** There are no limits on the number of local test runs, unlike Postman's cloud-based runner.

### Who is Xplorer for?

Xplorer is for any developer, QA engineer, or team that needs a fast, reliable, and secure API client. It is especially valuable for those working in enterprise environments or on projects with strict security and data privacy requirements.

## Security & Privacy

### How does Xplorer handle my data and API secrets?

All of your data is stored exclusively on your local machine's filesystem. Nothing is ever transmitted to Karate Labs or any third-party server. This is the core of our local-first promise.

### Do you collect any telemetry or usage data?

No. We do not collect any analytics, telemetry, or usage data.

## Features & Functionality

### What platforms does Xplorer support?

Xplorer is a cross-platform, enterprise-ready application with signed builds for Mac, Windows, and Linux.

### Can I import my collections from Postman?

Yes. Xplorer is designed for a seamless transition. You can instantly import your existing Postman collections and run them with zero modifications.

### Does Xplorer handle Environment Variables and Pre & Post Scripts from Postman?

Yes. Support for environment variables and pre/post-request JavaScript is a core capability of the free version.

### How does Xplorer handle API chaining?

We emulate Postman's behavior, so you can run a collection containing multiple requests where requests depend on each other or use variables updated by previous requests. If a Postman collection does not work as expected in Xplorer, we consider it a bug and will work to fix it quickly.

### Does Xplorer help migrate Postman collections to Karate tests?

The primary purpose of Xplorer is to run Postman collections as-is, not to perform a 1:1 migration. Our recommendation is that teams write all new tests in Karate.

- **Migration is Complex:** Our experience shows that a perfect 1:1 automated migration from Postman to Karate is not feasible due to their fundamental differences; some manual effort will always be needed.
- **Future Migration Tool:** We will provide a free option to migrate a Postman collection to Karate in an upcoming Xplorer release. However, you should budget for manual effort to finalize the migration.
- **CI/CD Runner:** For teams who want to run existing Postman tests alongside Karate tests in the same CI/CD pipeline, we will offer a paid CLI runner for Postman collections.

### Does Xplorer support other formats like OpenAPI/Swagger, cURL, or HAR?

Yes, Xplorer supports importing from all standard formats, allowing you to easily migrate your existing workflows and assets.

## Pricing & Licensing

### How much does Xplorer cost?

Xplorer is **perpetually free** for its core features. This is intended for teams who need an escape hatch from the licensing changes, forced cloud usage, and security risks that come with other tools.

**The free version includes:**

- Running Postman collections as-is
- Support for environment variables
- Support for pre- and post-request JavaScript
- Unlimited local runs

### What is the paid upgrade for?

We will offer an optional paid upgrade (currently estimated at $200/user/year) for advanced, enterprise-focused capabilities, including:

- Saving and sharing HTML reports
- A CI/CD runner to execute collections alongside other tests (like JUnit or Karate)
- Parallel execution for faster runs
- The ability to step-through and debug collections
- Re-using collections as performance tests
- MCP / LLM integration
- Importing OpenAPI/Swagger specs to generate Karate tests

## Getting Started & Support

### Where can I download Xplorer?

You can download the latest version for your operating system from the official Xplorer website: [karatelabs.io/xplorer](https://karatelabs.io/xplorer)

### Where can I find the documentation?

For detailed guides and information on all of Xplorer's features, please visit our [documentation](/xplorer/docs).
