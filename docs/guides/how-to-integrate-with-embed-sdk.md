---
layout: default
title: Embed SDK Usage Guide
parent: Guides
nav_order: 12
---

# YourStake Embed SDK
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## Requirements
- First YourStake must register your oauth application in our system. Once that is done you will receive the following: 
`client_id`, `redirect_uri`, `code_challenge`, `code_challenge_method` and `user_email`.

## Authentication Overview
<img src="{{ site.baseurl }}/assets/images/embed-oauth-overview.png">

## Getting an Authorization Code
- In order to initialize the embed you will first need to perform a server-side request to retrieve an authorization code. 
- NOTE: It is important that the request is made server-side to avoid exposing the value for the `HTTP_AUTHORIZATION` header on the frontend.
- To get this authorization code make a server-side GET request to https://www.yourstake.org/api/v1/auth/embed/authorize/
- The `HTTP_AUTHORIZATION` header must be the `Basic [insert encoded string]` where the encoded string is the base64 encoding of: "[client_id]:[client_secret]" (without the square brackets).

**Query Parameters (* denotes that the parameter is required)**


| Parameter     | Description                   |
|:--------------|:------------------------------|
|**response_type***|must be set to the word `code` |
|**client_id***|must be set to the `client_id` that you were provided after initial registration in our system. |
|**scope***|must be set to `write` |
|**redirect_uri***|must be set to the `redirect_uri` that you were provided after initial registration in our system |
|**code_challenge***|must be set to the `code_challenge` that you were provided after initial registration in our system |
|**code_challenge_method***|must be set to `S256` |
|**user_email***|must be set to the `user_email` that you were provided after initial registration in our system |

Example request:
```http
GET https://www.yourstake.org/api/v1/auth/embed/authorize/?response_type=code&client_id=...&scope=write&redirect_uri=...&code_challenge=...&code_challenge_method=S256&user_email=... HTTP/1.1
Authorization: Basic [base64 encoded string]
```

Sample response:
```json
{"code": "a valid auth code here"}
```

## Getting the Embed SDK File
- In order to fetch the embed sdk, include the following script somewhere on the page (preferably in the head to ensure that it can load quickly enough relative to the rest of the page):
```html
<script type="application/javascript" src="[insert path to yourstake sdk js file]"></script>
```
- The "latest" sdk file can be found at: [https://d1sax13m7bgtnp.cloudfront.net/embed/yourstake-embed-sdk-latest.js](https://d1sax13m7bgtnp.cloudfront.net/embed/yourstake-embed-sdk-latest.js)
- Specific versions will be available at: https://d1sax13m7bgtnp.cloudfront.net/embed/yourstake-embed-sdk-[insert version tag].js

## Initializing the Embed
- After the YourStake embed script has been loaded on the page ([instructions here](#getting-the-embed-sdk-file)), the Yourstake embed constructor will be accessible at `window._YourStakeEmbed`.
- In order to initialize it you will need to provide the following:
    - `clientId`: this should be set to the `client_id` from initial registration
    - `authCode`: this should be set to the authorization code from the response of the server-side request to `api/v1/auth/embed/authorize/`
    - `pkceCodeVerifier`: this should be set to the `code_challenge` from initial registration
    - `oauthRedirectUri`: this should be set to the `redirect_uri` from initial registration
    - `targetElementIdentifier`: this should be set to the id of the html element that the embed's iframe should be rendered inside of
    - `initialPage`: this should be set to the key of the page you want to load initially. Currently supported values are `report-builder` (default) and `behavioral-questionnaire`.
    - `slug`: A partial url that will be appended to the iframe url. When using `behavioral-questionnaire` this should be set to the custom questionnaire slug for your org. Not needed for `report-builder`.
    - `width`: this will specify the width of the iframe. It can be any valid css width value.
    - `height`: this will specify the height of the iframe. It can be any valid css height value.
- Here is an example:
```
window._YS_EMBED = new window._YourStakeEmbed({
    clientId: clientId,
    authCode: code,
    pkceCodeVerifier: pkceCodeVerifier,
    oauthRedirectUri: oAuthRedirectUri,
    targetElementIdentifier: "ys-embed-container",
    initialPage: 'report-builder',
    width: '100%',
    height: '90vh',
});
```
- The YourStake iframe will then authenticate the session via oauth using the information provided to the sdk.
