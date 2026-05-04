---
title: Authenticating to the REST API
intro: Authenticate to the GitHub REST API to access protected endpoints and increase rate limits.
shortTitle: Authenticating
versions:
  fpt: "*"
  ghec: "*"
  ghes: "*"
category:
  - Authenticate API requests
---

## About authentication

Many REST API endpoints require authentication or return additional information when authenticated. Authenticated requests also have higher rate limits.

To authenticate a request, include an authentication token with the required permissions.

You can generate a token using:
- A personal access token (PAT)
- A GitHub App installation token
- The `GITHUB_TOKEN` in a GitHub Actions workflow

Use the token in the `Authorization` header:

```shell
curl --request GET \
  --url "https://api.github.com/octocat" \
  --header "Authorization: Bearer YOUR_TOKEN" \
  --header "X-GitHub-Api-Version: 2022-11-28"

## OAuth app authentication with callback

OAuth apps use a redirect-based authentication flow that returns an authorization code to your application.

### Authorization flow

1. Redirect the user to GitHub's authorization endpoint:

```shell
GET https://github.com/login/oauth/authorize \
  ?client_id=YOUR_CLIENT_ID \
  &redirect_uri=YOUR_CALLBACK_URL \
  &scope=repo,user \
  &state=RANDOM_STRING
