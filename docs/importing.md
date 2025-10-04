---
layout: docs
title: Importing Collections
---

# Importing Collections

Karate Xplorer supports Postman collection formats and can open your existing collections without modification.

## Supported Formats

- Postman Collection v2.0
- Postman Collection v2.1
- Environment JSON files
- All standard JavaScript assertion syntax

## Opening Collections

**Three ways to open:**

1. **File → Open** - Browse to select your collection JSON file
2. **Drag and drop** - Drop collection or environment files into the window
3. **Recent files** - Access from File menu for quick access

## Opening Environments

1. Use **File → Open** or drag and drop your environment JSON file
2. The active environment appears in the **Environment Pane** (right panel)
3. Variables are displayed and can be modified
4. Only one environment can be active at a time

## What Works Out of the Box

- All requests and folder structure
- Pre-request scripts (Before tab)
- Test scripts (After tab)
- Collection and environment variables
- Authentication settings (Basic, Bearer, OAuth2)
- Request headers, params, and body
- Query parameters

## Compatibility

Karate Xplorer is designed for zero migration effort:

- ✅ All JavaScript syntax supported
- ✅ `pm` object fully supported
- ✅ Dynamic variables work as expected
- ✅ Collection and folder-level scripts
- ✅ Request-level configuration

## Beta Notice

**Note**: This is beta software. We recommend backing up your Postman collections before making edits. When saving over existing files, you'll see a confirmation dialog.

## Troubleshooting

If you encounter issues:

1. Ensure the file is a valid Postman collection JSON
2. Check that it's exported from Postman (not manually edited)
3. Try re-exporting from Postman
4. Report issues at [GitHub Issues](https://github.com/karatelabs/xplorer/issues)

## Next Steps

- [Quick Start Guide]({{ '/docs/quick-start/' | relative_url }})
- [Interface Overview]({{ '/docs/interface/' | relative_url }})
- [Running Collections]({{ '/docs/running/' | relative_url }})
