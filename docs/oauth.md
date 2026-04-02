---
layout: docs
title: OAuth 2.0
---

# OAuth 2.0 Authentication

Xplorer provides comprehensive OAuth 2.0 support, allowing you to test APIs that require user authentication and authorization. The implementation follows industry standards and works seamlessly with popular OAuth providers like GitHub, Google, Microsoft, Auth0, and more.

![OAuth 2.0 Configuration]({{ '/assets/images/docs/oauth.png' | relative_url }})

## Overview

OAuth 2.0 is an authorization framework that enables applications to obtain limited access to user accounts on an HTTP service. Xplorer handles the complex OAuth flow automatically, so you can focus on testing your APIs.

### Key Features

- **System Browser Integration**: Uses your system's default browser for authentication - secure and familiar
- **Existing Sessions Work**: If you're already logged into the OAuth provider, authentication is instant
- **Secure by Design**: Your credentials never pass through Xplorer - authentication happens directly with the provider
- **Automatic Token Management**: Tokens are cached and automatically refreshed when expired
- **PKCE Support**: Built-in Proof Key for Code Exchange for enhanced security
- **Multiple Grant Types**: Client Credentials, Authorization Code, and Authorization Code with PKCE

## Supported Grant Types

### Client Credentials
Best for **server-to-server** authentication where no user interaction is required.

**Use cases:**
- Backend services calling APIs
- Automated scripts and batch jobs
- Service accounts

### Authorization Code
Best for **web applications** where user authentication is required.

**Use cases:**
- Web applications with a backend server
- Apps that need user-specific data
- When client secret can be kept confidential

### Authorization Code with PKCE
Best for **public clients** like mobile apps, SPAs, and desktop applications.

**Use cases:**
- Native mobile applications
- Single-page applications (SPAs)
- Desktop applications (like Xplorer itself!)
- Any scenario where client secret cannot be securely stored

## Setting Up OAuth 2.0

### Step 1: Register Your Application

Before using OAuth with Xplorer, you need to register an application with your OAuth provider. This typically involves:

1. Going to your OAuth provider's developer console
2. Creating a new OAuth application
3. Configuring the redirect/callback URL (see below)
4. Obtaining the Client ID (and Client Secret, if applicable)

### Step 2: Configure Callback URL

This is the **most important step** for OAuth to work with Xplorer.

Xplorer uses a local callback server that listens on one of the following ports (tried in order):

```
http://127.0.0.1:8080/callback
http://127.0.0.1:8888/callback
http://127.0.0.1:9090/callback
http://127.0.0.1:3000/callback
```

**When registering your OAuth application, configure the callback URL(s) based on your OAuth provider:**

- **If you know a port is available** (e.g., port 8080 is free): Register just that one URL: `http://127.0.0.1:8080/callback`
- **If your provider supports multiple callback URLs** (like Google, Auth0): Add all four URLs for maximum flexibility
- **If your provider allows only one URL** (like some GitHub configurations): Use `http://127.0.0.1:8080/callback` (the first port Xplorer tries)

> **Note**: This is the same approach used by Postman, so if you've already configured Postman callback URLs, Xplorer will work without any changes!

#### Examples by Provider

**GitHub:**
1. Go to Settings → Developer settings → OAuth Apps
2. Create a new OAuth App
3. Set Authorization callback URL to `http://127.0.0.1:8080/callback`
4. Copy the Client ID and generate a Client Secret

**Google:**
1. Go to Google Cloud Console → APIs & Services → Credentials
2. Create OAuth 2.0 Client ID
3. Add the callback URLs to "Authorized redirect URIs" (Google supports multiple URLs)
4. Copy the Client ID and Client Secret

**Auth0:**
1. Go to Applications → Create Application
2. Add the callback URLs to "Allowed Callback URLs" (comma-separated or multiple entries)
3. Copy the Client ID and Client Secret

### Step 3: Configure OAuth in Xplorer

1. **Open a request** that requires OAuth authentication
2. **Navigate to the Auth tab**
3. **Select OAuth 2.0** from the Auth Type dropdown
4. **Choose a Grant Type** (Client Credentials, Authorization Code, or Authorization Code with PKCE)
5. **Fill in the OAuth configuration fields:**

#### For Authorization Code or Authorization Code with PKCE:

| Field | Description | Example |
|-------|-------------|---------|
| **Authorization URL** | Where users log in | `https://github.com/login/oauth/authorize` |
| **Access Token URL** | Where tokens are exchanged | `https://github.com/login/oauth/access_token` |
| **Client ID** | Your application's client ID | `your-client-id` |
| **Client Secret** | Your application's secret (optional for PKCE) | `your-client-secret` |
| **Scope** | Permissions requested | `user repo` |

#### For Client Credentials:

| Field | Description | Example |
|-------|-------------|---------|
| **Access Token URL** | Token endpoint | `https://oauth.example.com/token` |
| **Client ID** | Your application's client ID | `your-client-id` |
| **Client Secret** | Your application's secret | `your-secret` |
| **Scope** | Permissions requested (optional) | `api:read api:write` |

## Using OAuth 2.0

### First Request - Authentication Flow

1. **Click the Run button** on your request
2. **Browser dialog opens** with the OAuth provider's login page
3. **Log in** with your credentials (or skip if already logged in)
4. **Authorize the application** - grant the requested permissions
5. **Dialog closes automatically** after successful authorization
6. **Request executes** with your access token
7. **View the response** in the Output pane

### Subsequent Requests - Token Reuse

For subsequent requests using the same OAuth configuration:

1. **Click Run** on any request with the same OAuth config
2. **No browser dialog** - cached token is used automatically
3. **Request executes immediately**

Xplorer automatically handles token refresh when the token expires, so you only need to authenticate once per session.

## Example: GitHub OAuth with Environment Variables

This complete example demonstrates OAuth 2.0 with GitHub, using environment variables for all credentials. Download the sample files and try it yourself:

- [github-oauth.postman_collection.json]({{ '/assets/samples/github-oauth.postman_collection.json' | relative_url }}) — the collection (no secrets, just {% raw %}`{{variables}}`{% endraw %})
- [github-dev.postman_environment.json]({{ '/assets/samples/github-dev.postman_environment.json' | relative_url }}) — sample dev environment
- [github-prod.postman_environment.json]({{ '/assets/samples/github-prod.postman_environment.json' | relative_url }}) — sample prod environment

![OAuth 2.0 with Environment Variables]({{ '/assets/images/docs/oauth-env-variables.png' | relative_url }})

### How to Use

1. **Register a GitHub OAuth App** at GitHub → Settings → Developer settings → OAuth Apps
   - Set the callback URL to `http://127.0.0.1:8080/callback`
   - Copy the Client ID and generate a Client Secret
2. **Edit the environment file** — replace `your-dev-client-id` and `your-dev-client-secret` with your actual credentials
3. **Open the collection** in Xplorer (File → Open or drag and drop)
4. **Load the environment file** (File → Open or drag and drop)
5. **Click Send** on any request — the browser opens for GitHub login
6. **Authorize the app** — the token is cached for subsequent requests

### Collection Auth Configuration

The collection uses {% raw %}`{{variables}}`{% endraw %} for all OAuth fields. Auth is set at the **collection level**, so all requests inherit it automatically:

```json
{
  "auth": {
    "type": "oauth2",
    "oauth2": [
      { "key": "grant_type", "value": "authorization_code", "type": "string" },
      { "key": "authorizationUrl", "value": "{% raw %}{{githubAuthUrl}}{% endraw %}", "type": "string" },
      { "key": "url", "value": "{% raw %}{{githubTokenUrl}}{% endraw %}", "type": "string" },
      { "key": "client_id", "value": "{% raw %}{{githubClientId}}{% endraw %}", "type": "string" },
      { "key": "client_secret", "value": "{% raw %}{{githubClientSecret}}{% endraw %}", "type": "string" },
      { "key": "scope", "value": "{% raw %}{{githubScope}}{% endraw %}", "type": "string" }
    ]
  }
}
```

### Environment File

Each environment file provides the actual values. Edit the Client ID and Secret for your OAuth app:

```json
{
  "name": "GitHub - Dev",
  "values": [
    { "key": "githubApiUrl", "value": "https://api.github.com", "enabled": true },
    { "key": "githubAuthUrl", "value": "https://github.com/login/oauth/authorize", "enabled": true },
    { "key": "githubTokenUrl", "value": "https://github.com/login/oauth/access_token", "enabled": true },
    { "key": "githubClientId", "value": "your-dev-client-id", "enabled": true },
    { "key": "githubClientSecret", "value": "your-dev-client-secret", "enabled": true },
    { "key": "githubScope", "value": "user repo", "enabled": true }
  ]
}
```

### Switching Environments

To switch from dev to production, simply open a different environment file — the collection stays the same. The prod environment might have a different Client ID, Client Secret, or more restricted scopes.

The Bearer token is automatically added to your requests by Xplorer after successful OAuth authentication.

## Security Considerations

### Why System Browser?

Xplorer uses your system's default browser for OAuth authentication because:

- **Secure**: Your credentials go directly to the OAuth provider, never through Xplorer
- **Familiar**: You see the real OAuth provider's page with proper SSL certificates
- **Session Reuse**: If you're already logged in, authentication is instant
- **Transparency**: You can verify the URL and certificate in your browser

### HTTPS Requirement

For security, OAuth providers typically require HTTPS for their authorization endpoints. Xplorer works best with HTTPS OAuth providers.

**Recommended providers:** GitHub, Google, Microsoft, Auth0, Okta, and other major OAuth providers that use HTTPS.

## Troubleshooting

### Browser Dialog Doesn't Open

**Issue:** Clicking Run doesn't show the browser dialog.

**Solutions:**
- Check that you've selected the correct Grant Type (should be "Authorization Code" or "Authorization Code with PKCE")
- Verify your Authorization URL is correct and uses HTTPS
- Make sure all required fields are filled in

### "Invalid Redirect URI" Error

**Issue:** OAuth provider shows an error about the redirect URI.

**Solution:** Make sure you've added the callback URLs to your OAuth provider's configuration:
```
http://127.0.0.1:8080/callback
http://127.0.0.1:8888/callback
http://127.0.0.1:9090/callback
http://127.0.0.1:3000/callback
```

### Token Expired Errors

**Issue:** Getting 401 Unauthorized errors on subsequent requests.

**Solution:** Xplorer automatically refreshes tokens, but if you're still seeing errors:
- Some OAuth providers don't support token refresh
- You may need to re-authenticate manually
- Check your OAuth provider's token lifetime settings

### Port Already in Use

**Issue:** All callback ports are in use.

**Solution:** Xplorer tries ports 8080, 8888, 9090, and 3000 in sequence. If all are in use:
- Stop other applications using these ports
- Or restart Xplorer to try again

## Using Environment Variables with OAuth

OAuth configuration fields fully support {% raw %}`{{variable}}`{% endraw %} syntax. This lets you keep sensitive values like Client ID, Client Secret, and token URLs out of your collection and manage them per environment instead.

### Step 1: Use Variables in the Auth Tab

In the Auth tab, use {% raw %}`{{variable}}`{% endraw %} placeholders instead of hardcoded values:

| Field | Value |
|-------|-------|
| **Access Token URL** | {% raw %}`{{tokenUrl}}`{% endraw %} |
| **Client ID** | {% raw %}`{{clientId}}`{% endraw %} |
| **Client Secret** | {% raw %}`{{clientSecret}}`{% endraw %} |
| **Scope** | {% raw %}`{{scope}}`{% endraw %} |

The same approach works for Authorization Code flows — use variables for the Authorization URL as well.

### Step 2: Create Environment Files

Create a separate environment JSON file for each environment. These follow the standard Postman environment format.

**dev.postman_environment.json:**
```json
{
  "name": "Dev",
  "values": [
    {
      "key": "baseUrl",
      "value": "https://dev-api.example.com",
      "enabled": true
    },
    {
      "key": "tokenUrl",
      "value": "https://dev-auth.example.com/oauth2/token",
      "enabled": true
    },
    {
      "key": "clientId",
      "value": "dev-client-id",
      "enabled": true
    },
    {
      "key": "clientSecret",
      "value": "dev-client-secret",
      "enabled": true
    },
    {
      "key": "scope",
      "value": "read write",
      "enabled": true
    }
  ]
}
```

**staging.postman_environment.json:**
```json
{
  "name": "Staging",
  "values": [
    {
      "key": "baseUrl",
      "value": "https://staging-api.example.com",
      "enabled": true
    },
    {
      "key": "tokenUrl",
      "value": "https://staging-auth.example.com/oauth2/token",
      "enabled": true
    },
    {
      "key": "clientId",
      "value": "staging-client-id",
      "enabled": true
    },
    {
      "key": "clientSecret",
      "value": "staging-client-secret",
      "enabled": true
    },
    {
      "key": "scope",
      "value": "read write",
      "enabled": true
    }
  ]
}
```

Create similar files for production or any other environment.

### Step 3: Switch Environments

1. Open your collection in Xplorer
2. Load the desired environment file via **File → Open** or drag and drop
3. The environment name appears in the Environment Pane (right panel)
4. Run your requests — OAuth fields automatically resolve to the active environment's values
5. To switch, simply open a different environment file

This way your collection file stays unchanged — only the environment determines which OAuth provider, credentials, and API endpoints are used.

> **Tip**: For Okta-style setups, the Access Token URL typically looks like: {% raw %}`https://{{oktaDomain}}/oauth2/default/v1/token`{% endraw %}. You can make even the domain part a variable for maximum flexibility.

### Example: Okta Client Credentials per Environment

A common enterprise pattern is Okta with Client Credentials grant type, where each environment has its own Okta tenant.

**Collection Auth tab configuration:**

| Field | Value |
|-------|-------|
| Auth Type | OAuth 2.0 |
| Grant Type | Client Credentials |
| Access Token URL | {% raw %}`{{oktaTokenUrl}}`{% endraw %} |
| Client ID | {% raw %}`{{oktaClientId}}`{% endraw %} |
| Client Secret | {% raw %}`{{oktaClientSecret}}`{% endraw %} |
| Scope | {% raw %}`{{oktaScope}}`{% endraw %} |

**qa.postman_environment.json:**
```json
{
  "name": "QA",
  "values": [
    {
      "key": "baseUrl",
      "value": "https://qa-api.yourcompany.com",
      "enabled": true
    },
    {
      "key": "oktaTokenUrl",
      "value": "https://yourcompany-qa.okta.com/oauth2/default/v1/token",
      "enabled": true
    },
    {
      "key": "oktaClientId",
      "value": "0oa1234567abcdefg",
      "enabled": true
    },
    {
      "key": "oktaClientSecret",
      "value": "your-qa-client-secret",
      "enabled": true
    },
    {
      "key": "oktaScope",
      "value": "api.read api.write",
      "enabled": true
    }
  ]
}
```

Create matching files for dev, staging, and production with their respective Okta tenant URLs and credentials.

## Tips and Best Practices

1. **Use PKCE for Desktop Apps**: Authorization Code with PKCE is more secure for public clients like Xplorer
2. **Set Appropriate Scopes**: Only request the permissions you actually need
3. **Test with GitHub First**: GitHub OAuth is well-documented and works great for testing
4. **Keep Client Secrets Secure**: Don't commit OAuth credentials to version control — use environment files and keep them out of source control
5. **Use Environment Variables**: Store sensitive values like Client ID and Secret in environment files so you can switch between environments without editing the collection
6. **One Authentication Per Session**: Once authenticated, the token is cached for all requests in the collection

## Additional Resources

- [OAuth 2.0 RFC 6749](https://datatracker.ietf.org/doc/html/rfc6749)
- [PKCE RFC 7636](https://datatracker.ietf.org/doc/html/rfc7636)
- [GitHub OAuth Documentation](https://docs.github.com/en/developers/apps/building-oauth-apps/authorizing-oauth-apps)
- [Google OAuth 2.0 Documentation](https://developers.google.com/identity/protocols/oauth2)
