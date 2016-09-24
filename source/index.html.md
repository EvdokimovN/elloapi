---
title: Ello | Unofficial API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - posts
  - user
  - errors
  - data


search: true
---

# Introduction

This is unofficial documentation for <a href='ello.co'>Ello</a> API. The documentation is based on scrapping Ello's website

# Authentication
All API request must be signed with token as URL parameter. Steps below will show how to acquire one.
## Getting public token
> To recieve public token, use this code:


```shell
# Send GET request to /webapp-token
curl https://ello.co/api/webapp-token
```

```json
{"token":
    {"access_token":"token_string",
      "token_type":"bearer",
      "expires_in":604800,
      "scope":"public scoped_refresh_token",
      "created_at":1473748758,
      "expires_at":"2016-09-20T06:39:18.199Z"
    }
}
```



There is no implicit authorization as of yet. When you send GET request to retrieve any Ello page your browser automatically sends another
request to

`https://ello.co/api/webapp-token`

which responds with <a href='#token'>Token</a> data type. Token is a complex struct but what we need is an `acces_token` field. It's a public access token
which allows you to perform all GET requests and used to login user.

## Loging in and recieving private token
```shell
curl https://ello.co/api/oauth/login
-H   "authorization: Bearer <public_token>"
-H   "Content-Type: application/json"
-X   POST
-d   '{"email:""<your_email>", "password":"<your_password>"}'

```
> Notice how this structure doesn't have "token" as its top field

```json
{
  "access_token":"token_string",
  "token_type":"bearer",
  "expires_in":604800,
  "refresh_token":"25990061a3bda23e80ee2bc14c8bbcd1bd68b01e7830b2133954bba04eeb7572",
  "scope":"public scoped_refresh_token",
  "created_at":1473769469
}
```
To acquire private token you need to authorize yourself with your account credentials and public access token by posting to

`https://ello.co/api/oauth/login`

This will authorize you as if you logged in to the site

<aside class="notice">
This step is unnecesery if you only need to GET publicly available information
</aside>





