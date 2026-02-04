---
layout: docs
title: Karate Runner
---

# Karate Runner

> **Beta Feature**: This feature is currently in beta. We welcome feedback and bug reports via [GitHub Issues](https://github.com/karatelabs/xplorer/issues).

Run [Karate](https://karatelabs.io/karate) tests directly from Xplorer with syntax-highlighted editing and real-time output.

## Prerequisites

This feature requires an active Xplorer subscription. Go to **Help > License** to sign in. See [Licensing & Sign-In]({{ '/docs/licensing/' | relative_url }}) for details.

## Opening a Karate Project

1. Click **Karate** in the left navigation bar
2. Use **File > Open Folder** or drag and drop a folder containing:
   - `karate-config.js` (minimal setup), or
   - `karate-pom.json` (full configuration)

The project tree displays your `.feature` and `.js` files.

## Editing Files

Click any `.feature` or `.js` file in the tree to open it in the editor with syntax highlighting:

- **Gherkin keywords** (Feature, Scenario, Given, When, Then) highlighted
- **Tags** (@smoke, @api) in purple
- **Strings and doc strings** in green
- **Embedded JavaScript** supported

Changes are saved with **Cmd+S** (Mac) or **Ctrl+S** (Windows/Linux). A dirty indicator (*) shows unsaved changes.

## Running Tests

Right-click on any item in the tree to run tests:

| Level | Action |
|-------|--------|
| **Project root** | Run all tests |
| **Folder** | Run all tests in folder |
| **Feature file** | Run all scenarios in file |

### During Execution

- Progress shown in status bar
- **Stop** button to cancel
- Real-time output in the **Karate Output** pane (right toolbar)

### Results

- **Green checkmark**: All tests passed
- **Red X**: One or more tests failed
- Folders show aggregated status of all children

Right-click and select **Clear Results** to reset status icons.

## Output Pane

Click **Karate Output** in the right toolbar to see real-time test execution:

- Feature and Scenario grouping
- HTTP request/response details (expandable)
- Assertions with pass/fail status
- Log messages and errors

Filter buttons let you show/hide specific entry types.

## Project Configuration

For advanced configuration, create a `karate-pom.json` in your project root:

```json
{
  "paths": ["src/test/resources"],
  "tags": ["@smoke"],
  "env": "dev",
  "threads": 1
}
```

| Field | Description |
|-------|-------------|
| `paths` | Directories containing test files |
| `tags` | Filter tests by tag |
| `env` | Karate environment (karate.env) |
| `threads` | Parallel execution threads |

## Next Steps

- [Karate Export]({{ '/docs/karate-export/' | relative_url }}) - Convert Postman collections to Karate
- [Licensing & Sign-In]({{ '/docs/licensing/' | relative_url }}) - Manage your subscription