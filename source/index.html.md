---
title: API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
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


# Posts
## Search posts 
```shell
#Use -G flag to convinietly pass URL parameters
curl -G https://ello.co/api/v2/posts
     -d "terms=norway"
     -d "access_token=<token>"
```
### HTTP Request
`GET https://ello.co/api/v2/posts?terms=<search_parameter>`
### URL Parameters
Parameter | Type | Optional | Default | Description
--------- | ------- | -----------|--------------|------------
terms | String | false | NULL | Query parameter 
per_page | Integer | true | 25 | Specifies how many posts to show


## GET Information about particular post
```shell
curl -G https://ello.co/api/v2/posts/11323555
     -d "access_token=<token>"

curl -G https://ello.co/api/v2/posts/~tkd-_engpxhhy3w4yq9yug
     -d "access_token=<token>"          
```

> Part of the response is not shown due to its size

```json
{
  "posts": {
    "id": "11323555",
    "href": "/api/v2/posts/11323555",
    "token": "tkd-_engpxhhy3w4yq9yug",
    "content_warning": null,
    "summary": [],
    "content": [],
    "created_at": "2016-09-15T11:17:28.267Z",
    "author_id": "812695",
    "is_adult_content": false,
    "body": [],
    "comments_count": 0,
    "loves_count": 1,
    "reposts_count": 0,
    "views_count": 21,
    "views_count_rounded": "21",
    "loved": false,
    "reposted": false,
    "links": {}
    },
  "linked": {}
}
```

### HTTP Request
`GET https://ello.co/api/v2/posts/<post_id>`

Returns informations about paticular post including information about its author, comments, shares, likes

<aside class="notice">
Instead of numerical post id the so called token (as seen in the post's respected URL) can be used preceeded with ~
</aside>

## GET Comments associated with the post
```
curl -G https://ello.co/api/v2/posts/11322508/comments
     -d "access_token=<token>"
```

### HTTP Request
`GET https://ello.co/api/v2/posts/<id>/comments`

Return all users commented on the post and their comments specified by <a href="#user">User</a> and <a href="#comment">Comment</a> data types