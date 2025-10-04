---
layout: docs
title: Data-Driven Testing
---

# Data-Driven Testing

Run collections or folders multiple times with different data sets using CSV or JSON files.

## Overview

Data-driven testing allows you to:
- Execute the same collection/folder with different inputs
- Test multiple scenarios without duplicating requests
- Validate API behavior across various data sets

**Available for:**
- Folders
- Root collections
- (Not available for individual requests)

## Setting Up Data-Driven Tests

1. Select a **folder** or **root collection** in the navigation tree
2. Navigate to the **CSV / JSON** tab
3. Click **Browse** to select your data file
4. Click **Run** to execute

![CSV/JSON Tab for Data-Driven Testing]({{ '/assets/images/docs/data-driven-tab.png' | relative_url }})

## Supported File Formats

### CSV Files

CSV files must have a header row with column names.

**Example:**
```csv
username,password,expected_status
user1,pass123,200
user2,wrongpass,401
admin,admin123,200
```

**Usage in requests:**
```javascript
// Access CSV columns in scripts
let username = pm.iterationData.get("username");
let password = pm.iterationData.get("password");

// Use in URL or body
// URL: https://{{base_url}}/login?user={{username}}
```

### JSON Files

JSON files must contain an array of objects.

**Example:**
```json
[
  {
    "username": "user1",
    "password": "pass123",
    "expected_status": 200
  },
  {
    "username": "user2",
    "password": "wrongpass",
    "expected_status": 401
  },
  {
    "username": "admin",
    "password": "admin123",
    "expected_status": 200
  }
]
```

## Accessing Data in Scripts

Use the `pm.iterationData` object to access current row data:

**Pre-request (Before) script:**
```javascript
// Get data from current iteration
let username = pm.iterationData.get("username");
let password = pm.iterationData.get("password");

// Set as variables for use in request
pm.variables.set("current_user", username);
pm.variables.set("current_pass", password);
```

**Test (After) script:**
```javascript
// Access iteration data for assertions
let expectedStatus = pm.iterationData.get("expected_status");

pm.test("Status code matches expected", function () {
    pm.response.to.have.status(expectedStatus);
});
```

## Using Data in Requests

Reference iteration data using variables set in Before scripts:

**URL:**
```
https://{{base_url}}/users/{{current_user}}
```

**Request body:**
```json
{
  "username": "{{current_user}}",
  "password": "{{current_pass}}"
}
```

## Execution Behavior

When you run a folder/collection with a data file:

1. **First iteration** runs with first data row
2. **Second iteration** runs with second data row
3. Continues until all data rows are processed

**For each iteration:**
- All requests in the folder/collection execute
- Before/After scripts run for each request
- Results aggregate in the Output pane
- Pass/fail indicators update after all iterations complete

## Clearing Data Files

To remove the data file:

1. Go to the **CSV / JSON** tab
2. Click the **Clear** button
3. Next run executes normally (single iteration)

## Example Use Case

**Testing user login with multiple credentials:**

**Data file (users.csv):**
```csv
email,password,should_succeed
valid@example.com,correct123,true
invalid@example.com,wrong456,false
admin@example.com,admin789,true
```

**Before script:**
```javascript
pm.variables.set("email", pm.iterationData.get("email"));
pm.variables.set("password", pm.iterationData.get("password"));
```

**Request URL:**
```
POST https://{{base_url}}/auth/login
```

**Request body:**
```json
{
  "email": "{{email}}",
  "password": "{{password}}"
}
```

**After script:**
```javascript
let shouldSucceed = pm.iterationData.get("should_succeed") === "true";

if (shouldSucceed) {
    pm.test("Login successful", function () {
        pm.response.to.have.status(200);
        pm.expect(pm.response.json()).to.have.property("token");
    });
} else {
    pm.test("Login failed as expected", function () {
        pm.response.to.have.status(401);
    });
}
```

## Tips

- **Keep data files organized**: Store them near your collection files
- **Start small**: Test with 2-3 rows before running large data sets
- **Use meaningful column names**: Makes scripts easier to read
- **Validate data files**: Ensure CSV headers match what scripts expect

## Next Steps

- [Running Requests & Collections](running/)
- [Environments](environments/)
- [Interface Overview](interface/)
