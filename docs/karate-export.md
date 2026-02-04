---
layout: docs
title: Karate Export
---

# Karate Export

> **Beta Feature**: This feature is currently in beta. We welcome feedback and bug reports via [GitHub Issues](https://github.com/karatelabs/xplorer/issues).

Export Postman collections to [Karate](https://karatelabs.io/karate) feature files for API test automation.

## Prerequisites

This feature requires an active Xplorer subscription. Go to **Help > License** to sign in. See [Licensing & Sign-In]({{ '/docs/licensing/' | relative_url }}) for details.

## Quick Start

1. Open a Postman collection file (or drag and drop)
2. Select the **collection root** in the tree
3. Click **Export** in the right toolbar
4. Change export type to **Karate**
5. Click **Save to Folder**

The converter generates Karate feature files with:
- `karate-config.js` with collection variables
- Feature files for each folder
- Converted test scripts (`pm.test` → Karate assertions)
- Auth configuration (`* configure auth`)

## Exporting Selected Requests

You can also export a single request or folder instead of the entire collection:

1. Select any **request** or **folder** in the tree
2. Click **Export** → **Karate**
3. Only the selected item (and its children) will be exported

## What Gets Converted

| Postman | Karate |
|---------|--------|
| Collection variables | `karate-config.js` |
| Folders | Feature files |
| Requests | Scenario steps |
| `pm.test()` assertions | `match` / `assert` statements |
| `pm.environment.set()` | `* def` variables |
| Basic/Bearer/OAuth2 auth | `* configure auth` |
| Query params, headers | `param`, `header` keywords |
| JSON body | `request` keyword |
| Form data | `form field` / `multipart` |

## Next Steps

- [Licensing & Sign-In]({{ '/docs/licensing/' | relative_url }}) - Manage your subscription
- [cURL Export]({{ '/docs/curl-export/' | relative_url }}) - Export as cURL commands
