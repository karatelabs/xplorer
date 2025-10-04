---
layout: docs
title: cURL Import
---

# cURL Import

Convert cURL commands to requests quickly using the Import pane.

## Overview

The cURL import feature allows you to:
- Convert cURL commands to Postman-format requests
- Quickly add requests from API documentation
- Import requests from browser network tools
- Parse headers, methods, and body automatically

## How to Import cURL

1. Click the **Import** button in the right toolbar
2. The Import Pane opens (right panel)
3. Paste your cURL command
4. Click **Import** or press Enter
5. The request is created in your collection

![cURL Import Example]({{ '/assets/images/docs/curl-import-example.png' | relative_url }})

## Supported cURL Features

The import parser supports:

**HTTP Methods:**
- `-X GET`, `-X POST`, `-X PUT`, etc.
- `--request POST`

**Headers:**
- `-H "Content-Type: application/json"`
- `--header "Authorization: Bearer token"`

**Request Body:**
- `-d '{"key": "value"}'`
- `--data '{"key": "value"}'`
- `--data-binary @file.json`

**URL:**
- Full URLs with protocol
- Query parameters

## Example Imports

### Simple GET Request

**cURL command:**
```bash
curl https://api.example.com/users
```

**Result:**
- Method: GET
- URL: `https://api.example.com/users`

### POST with JSON Body

**cURL command:**
```bash
curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d '{"name": "John Doe", "email": "john@example.com"}'
```

**Result:**
- Method: POST
- URL: `https://api.example.com/users`
- Headers: `Content-Type: application/json`
- Body: JSON with name and email

### With Authentication

**cURL command:**
```bash
curl https://api.example.com/protected \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
```

**Result:**
- Method: GET
- URL: `https://api.example.com/protected`
- Headers: `Authorization: Bearer ...`

### Complex Example

**cURL command:**
```bash
curl -X PUT 'https://api.example.com/users/123?verify=true' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer token123' \
  -H 'X-Custom-Header: value' \
  -d '{
    "name": "Jane Doe",
    "email": "jane@example.com",
    "active": true
  }'
```

**Result:**
- Method: PUT
- URL: `https://api.example.com/users/123?verify=true`
- Headers: Multiple headers parsed
- Body: JSON payload

## Getting cURL Commands

### From Browser DevTools

1. Open browser Developer Tools (F12)
2. Go to Network tab
3. Make a request (click a link, submit a form, etc.)
4. Right-click the request in the Network tab
5. Select **Copy → Copy as cURL**
6. Paste into Karate Xplorer Import pane

### From API Documentation

Many API docs provide cURL examples:
- Copy the example command
- Paste into Import pane
- Modify as needed

### From Terminal/Command Line

If you've tested an API via command line:
- Copy your working cURL command
- Import directly into Karate Xplorer
- Save for future use

## After Importing

Once imported, the request appears in your collection:

1. **Review the request**: Check that all fields parsed correctly
2. **Edit as needed**: Modify URL, headers, body
3. **Add tests**: Use the After tab to add test scripts
4. **Save the collection**: File → Save to persist changes

## Tips

- **Line breaks**: Multi-line cURL commands work fine
- **Single vs double quotes**: Both are supported
- **Environment variables**: Replace shell variables (like `$TOKEN`) with Postman variables (like `{{token}}`)
- **File uploads**: Binary data may not import perfectly; review and adjust

## Limitations

**Not currently supported:**
- File uploads (`-F` or `--form`)
- Cookies (`-b` or `--cookie`)
- Some advanced cURL options

For complex requests, import the basic structure and manually add additional settings.

## Troubleshooting

**Import fails or produces unexpected results:**

1. Verify cURL command is valid (test in terminal first)
2. Check for special characters that need escaping
3. Simplify the command and import in steps
4. Report parsing issues at [GitHub Issues](https://github.com/karatelabs/xplorer/issues)

## Next Steps

- [Interface Overview]({{ '/docs/interface/' | relative_url }})
- [Running Requests & Collections]({{ '/docs/running/' | relative_url }})
- [Environments]({{ '/docs/environments/' | relative_url }})
