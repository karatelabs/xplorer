---
layout: default
title: Importing Postman Collections
---

# Importing Postman Collections

Karate Xplorer supports all Postman collection formats and can import your existing collections without modification.

## Supported Formats

- Postman Collection v1
- Postman Collection v2
- Postman Collection v2.1
- Exported collections from Postman app
- Collections exported from Postman web

## How to Import

### From File

1. Open Karate Xplorer
2. Go to **File → Import Collection**
3. Select your `.json` collection file
4. The collection will appear in the sidebar

### Importing Environments

1. Go to **File → Import Environment**
2. Select your environment `.json` file
3. Switch between environments using the dropdown

## What Gets Imported

- All requests and folder structure
- Pre-request scripts
- Test scripts
- Variables (collection and environment)
- Authentication settings
- Request headers and body

## Compatibility

Karate Xplorer is designed to be a drop-in replacement for Postman:

- ✅ All JavaScript syntax supported
- ✅ Chai assertion library included
- ✅ `pm` object fully supported
- ✅ Dynamic variables work as expected
- ✅ Collection and folder-level scripts

## Troubleshooting

If you encounter issues importing:

1. Ensure the file is a valid JSON file
2. Check that it's exported from Postman (not manually edited)
3. Try re-exporting from Postman
4. Check [GitHub Issues](https://github.com/karatelabs/xplorer/issues) for known issues

## Next Steps

- [Quick Start Guide](quick-start.html)
- [Running Tests](running-tests.html)
