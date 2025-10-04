---
layout: docs
title: Environments
---

# Environments

Xplorer supports Postman environment files for managing variables across different configurations.

## Loading Environments

**Three ways to load:**

1. **File → Open** and select an environment JSON file
2. **Drag and drop** the environment file into the window
3. Use the **Recent files** menu

When loaded, the environment appears in the **Environment Pane** (right panel).

## Active Environment

**Important**: Only one environment can be active at a time.

- The active environment is available to **all loaded collections**
- Environment name displays at the top of the Environment Pane
- All variables are visible and editable

## Environment Variables

The Environment Pane shows all variables:

**Structure:**
- Variable name (left column)
- Current value (right column)

**During execution:**
- Variables update in real-time
- Changes persist for the session
- Updated values shown after collection runs

## Using Variables in Requests

Reference environment variables using Postman syntax:

**In URLs:**
```
{% raw %}https://{{base_url}}/api/users{% endraw %}
```

**In headers:**
```
{% raw %}Authorization: Bearer {{auth_token}}{% endraw %}
```

**In request bodies:**
```json
{% raw %}{
  "userId": "{{user_id}}",
  "environment": "{{env_name}}"
}{% endraw %}
```

**In scripts:**
```javascript
pm.environment.get("base_url")
pm.environment.set("auth_token", response.token)
```

## Collection Variables

Collection variables are defined at the root collection level.

**To view/edit:**
1. Select the root collection in navigation tree
2. Click the **Variables** tab

Collection variables work the same as environment variables but are specific to that collection.

**Priority:**
- Environment variables override collection variables
- Local variables (in scripts) override both

## Variable Scope

Variable resolution follows this priority (highest to lowest):

1. Local variables (defined in scripts)
2. Environment variables
3. Collection variables
4. Global variables (if supported)

## Creating Environment Files

Environment files are standard Postman JSON format:

```json
{
  "name": "Production",
  "values": [
    {
      "key": "base_url",
      "value": "https://api.example.com",
      "enabled": true
    },
    {
      "key": "api_key",
      "value": "your-api-key",
      "enabled": true
    }
  ]
}
```

## Switching Environments

To switch to a different environment:

1. Open the new environment file (File → Open or drag and drop)
2. The new environment becomes active immediately
3. Previous environment is replaced

**Tip**: Keep multiple environment files for different configurations (dev, staging, production).

## Modifying Variables

Variables can be modified:

**Via Environment Pane:**
- Edit values directly in the pane
- Changes apply immediately

**Via Scripts:**
```javascript
pm.environment.set("auth_token", "new-token-value")
pm.environment.unset("old_variable")
```

## Persistence

**During session:**
- Variable changes persist while the application is running
- Updated values remain until you close the app

**Between sessions:**
- To save changes, you would need to update the environment JSON file
- Consider exporting or manually updating your environment files

## Next Steps

- [Running Requests & Collections]({{ '/docs/running/' | relative_url }})
- [Data-Driven Testing]({{ '/docs/data-driven/' | relative_url }})
- [Interface Overview]({{ '/docs/interface/' | relative_url }})
