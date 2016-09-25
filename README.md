
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
curl -G 'https://ello.co/api/v2/posts' \
     -d 'terms=norway' \
     -d 'access_token=<token>'
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
curl -G 'https://ello.co/api/v2/posts/11323555' \
     -d 'access_token=<token>'

curl -G 'https://ello.co/api/v2/posts/~tkd-_engpxhhy3w4yq9yug' \
     -d 'access_token=<token>'          
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
Instead of numerical id the so called token (as seen in the URL) can be used preceeded with ~
</aside>

## GET Comments associated with the post
```shell
curl -G 'https://ello.co/api/v2/posts/11322508/comments' \
     -d 'access_token=<token>'
```

### HTTP Request
`GET https://ello.co/api/v2/posts/<id>/comments`

Return all users commented on the post and their comments specified by <a href="#user">User</a> and <a href="#comment">Comment</a> data types

## GET Users reposted this post
```shell
curl -G 'https://ello.co/api/v2/posts/11323555/reposters' \
     -d 'access_token=<token>' 

curl -G 'https://ello.co/api/v2/posts/~tkd-_engpxhhy3w4yq9yug/reposters' \
     -d 'access_token=<token>'           
```

```json
{
  "users": [
    {
      "id": "2826450",
      "href": "/api/v2/users/2826450",
      "username": "ellocreative",
      "name": "ElloCreative",
      "posts_adult_content": false,
      "views_adult_content": false,
      "has_commenting_enabled": true,
      "has_sharing_enabled": true,
      "has_reposting_enabled": true,
      "has_loves_enabled": true,
      "experimental_features": false,
      "relationship_priority": null,
      "bad_for_seo": false,
      "is_hireable": false,
      "posts_count": 102,
      "followers_count": 413,
      "following_count": 43,
      "loves_count": 87,
      "formatted_short_bio": "bio_in_html_form",
      "external_links_list": [],
      "background_position": null,
      "avatar": "avatar_data",
      "cover_image": "cover_image_data"
      }
  ]
}
```

### HTTP Request
`https://ello.co/api/v2/posts/<id>/reposters`

Return users reposted the post specified by array of <a href="#user">User</a> data type


Parameter | Type | Optional | Default | Description
--------- | ------- | -----------|--------------|------------
per_page | Integer | true | 25 | Specifies how many users to return

## GET User's liked this post

```shell
curl -G 'https://ello.co/api/v2/posts/11323555/lovers' \
     -d 'access_token=<token>'

curl -G 'https://ello.co/api/v2/posts/~tkd-_engpxhhy3w4yq9yug/lovers' \
     -d 'access_token=<token>'   
```

```json
{
  "users": [
    {
      "id": "2823047",
      "href": "/api/v2/users/2823047",
      "username": "masteroneself",
      "name": "MasterOneself",
      "posts_adult_content": false,
      "views_adult_content": false,
      "has_commenting_enabled": true,
      "has_sharing_enabled": true,
      "has_reposting_enabled": true,
      "has_loves_enabled": true,
      "experimental_features": false,
      "relationship_priority": null,
      "bad_for_seo": true,
      "is_hireable": false,
      "posts_count": 71,
      "followers_count": 2234,
      "following_count": 1296,
      "loves_count": 190469,
      "formatted_short_bio": "",
      "external_links_list": [
        {
          "url": "http://masteroneself.com",
          "text": "masteroneself.com"
        }
      ],
      "background_position": null,
      "avatar": "avatar_object",
      "cover_image": "cover_image_object"
  
}
```

### HTTP Request 
`GET https://ello.co/api/v2/posts/<id>/lovers`   

Return users liked the post specified by array of <a href="#user">User</a> data type


Parameter | Type | Optional | Default | Description
--------- | ------- | -----------|--------------|------------
per_page | Integer | true | 25 | Specifies how many users to return


## Flag post 

```shell
curl -X POST \
     'https://ello.co/api/v2/posts/11391900/flag/violence' \
     -H 'authorization: Bearer <private_token>' \
     -d 'access_token=<private_token>' 

curl -X POST 
     'https://ello.co/api/v2/posts/~uk8eejgz8bumfbh8_5sfmg/flag/spam' \
     -H 'authorization: Bearer <private_token>' \
     -d 'access_token=<private_token>' 
    
```

### HTTP Request
`POST https://ello.co/api/v2/posts/11389674/flag/<flag>`

Flags post as inapropriate. If succesfull responds with 204

flag | Disctiption
--------- | -------
spam | Spam
violence | Violence
copyright | Copyright Infingment
threatening | Threatening
hate_speech | Hate Speech
adult | Adult content that isn't marked NSFW
offensive | I don't like it 

## POST new post

```shell
curl -POST \
    'https://ello.co/api/v2/posts' \
    -d 'access_token=<private_token>' \
    -d `{"body":[{"kind":"text","data":"Don't you ever lie to me you beatiful creature"}]}`
```
```json
{
  "posts": {
    "id": "11400610",
    "href": "/api/v2/posts/11400610",
    "token": "xo3ajdgpo3lxth_asp5biw",
    "content_warning": null,
    "summary": [
      {
        "kind": "text",
        "link_url": null,
        "data": "<p>Don&apos;t you ever lie to me you beatiful creature</p>"
      }
    ],
    "content": [
      {
        "kind": "text",
        "link_url": null,
        "data": "<p>Don't you ever lie to me you beatiful creature</p>"
      }
    ],
    "created_at": "2016-09-25T12:29:40.737Z",
    "author_id": "1320192",
    "is_adult_content": false,
    "body": [
      {
        "kind": "text",
        "data": "Don't you ever lie to me you beatiful creature"
      }
    ],
    "comments_count": 0,
    "loves_count": 0,
    "reposts_count": 0,
    "views_count": 0,
    "views_count_rounded": "0",
    "loved": false,
    "reposted": false,
    "watching": false,
    "links": {
      "assets": []
    }
  }
}
```
### HTTP Request 
`POST https://ello.co/api/v2/posts`

Creates new post. Contents of the post specified in JSON body array. Each element in the array equivilent to Ello's "post bars". For "kind":"text" body is HTML text. For "kind":"image" body is image URL on Ello's servers. If succesfull returns JSON post representation.  



## DELETE post

```shell
curl -X DELETE \
     'https://ello.co/api/v2/posts/11323555' \
     -H 'authorization: Bearer <private_token>' \
     -d 'access_token=<token>' 

curl -X DELETE 
     'https://ello.co/api/v2/posts/~tkd-_engpxhhy3w4yq9yug' \
     -H 'authorization: Bearer <private_token>' \
     -d 'access_token=<token>' 
```
### HTTP Request 
`DELETE https://ello.co/api/v2/posts/<id>`

Deletes post. If succesfull reposnds with 204




# User
## GET Information about user

```shell
curl -G 'https://ello.co/api/v2/users/2706139' \
     -d "access_token=<token>" 

curl -G 'https://ello.co/api/v2/posts/~mariosupa' \
     -d 'access_token=<token>'          
```

### HTTP Request

`GET https://ello.co/api/v2/users/<id>`

Returns information about user as two data types: <a href="#user">User</a> and <a href="#linked">Linked</a>

Parameter | Type | Optional | Default | Description
--------- | ------- | -----------|--------------|------------
post_count | Boolean | true | true | Specifies to also return information linked to user 


## GET User's posts

```shell
curl -G 'https://ello.co/api/v2/users/2706139/posts' \
     -d 'access_token=<token>'

curl -G 'https://ello.co/api/v2/users/~mariosupa/posts' \
     -d 'access_token=<token>'          
```

```json
{
  "linked": {
    "users": ["not_shown"],
    "assets": ["not_shown"],
    "categories": ["not_shown"]
  },
  "posts" : ["not_shown"]
}
```

### HTTP Request 

`GET https://ello.co/api/v2/users/<id>/posts`

Returns user's posts in the form of <a href="#post">Posts</a> array with all data linked to the post in <a href="#linked">Linked</a> array



Parameter | Type | Optional | Default | Description
--------- | ------- | -----------|--------------|------------
per_page | Integer | true | 25 | Specifies how many posts to return
before | DateTime | true | NULL | Return posts created before specified time 
after | DateTime | true | NULL | Return posts created after specified time


<aside class="notice">Time should be in 2016-08-09T16:14:52.417Z format and URL encoded</aside>

# Categories

## GET Recent/Featured posts

```shell

curl -G 'https://ello.co/api/v2/cateories/posts/recent' \
     -d 'access_token=<token>' 
```

```json
{
  "linked": {
    "users": [
      "user_1_object",
      "user_2_object"
    ],
    "assets": [
      "asset_1_object",
      "asset_2_object",
      "asset_3_object"
    ],
    "categories": [
      "category_1_object",
      "category_2_object"
    ]
  },
  "posts": [
    "post_1_object",
    "post_2_object"
  ]
}
```
### HTTP Request
`GET https://ello.co/api/v2/cateories/posts/recent`

Returns recent posts AKA featured from all categories


Parameter | Type | Optional | Default | Description
--------- | ------- | -----------|--------------|------------
per_page | Integer | true | 25 | Specifies how many posts to return


## GET Recent posts from category
```shell
curl -G 'https://ello.co/api/v2/categories/fashion/posts/recent' \
     -d 'access_token=<token>' 
```

### HTTP Request 
`GET https://ello.co/api/v2/categories/<category>/posts/recent`

Returns recent posts from specified category. Response is similar to previous request

Parameter | Type | Optional | Default | Description
--------- | ------- | -----------|--------------|------------
per_page | Integer | true | 25 | Specifies how many posts to return
before | String | true | NULL | Coded time 

# Errors

You encounter following error codes while using Ello API:


Error Code | Meaning
---------- | -------
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You can't perform this request
404 | Not Found -- Either wrong API URL or wrong method
503 | Internal Server Error -- Server offline or wrong URL parameters

# Data Types


## Token

Field | Type | Description
--------- | -------- | -----------
access_token | String |String representing access_token used to authenticate API requests
token_type | String |Unknown
expires_in | Integer |Token expiration time in seconds
refresh_token | |Unknown
scope | String |Scope of particular token
created_at | Integer |Time of creation in UNIX time

## Post

Field | Type | Description
--------- | -------- | -----------
id | Integer | Post's internal id
href | String | API url without host leading to this post
token | String | Post's string id
content_warning | Unknown | Defaults to null. Might be not used
summary | Array | <table><tbody><tr><th>Field</th><th>Type</th><th>Description</th></tr><tr><td>kind</td><td>String</td><td>Posts can be represented by "text", "link", "photo"</td></tr><tr><td>link_url</td><td>String</td><td>Null if post has no links or assets</td></tr><tr><td>data</td><td>String</td><td>Contents escaped HTML  representation</td></tr></tbody></table>
contents | Array | <table><tbody><tr><th>Field</th><th>Type</th><th>Description</th></tr><tr><td>kind</td><td>String</td><td>Posts can be represented by "text", "link", "photo"</td></tr><tr><td>link_url</td><td>String</td><td>Null if post has no links or assets</td></tr><tr><td>data</td><td>String</td><td>Contents HTML representation</td></tr></tbody></table>
created_at | DateTime | Post time creation in 2016-09-25T12:29:40.737Z format
author_id | Integer | Author's internal id
is_adult_content | Boolean | Is NSFW
body | Array | JSON post representation as was sent with creation request
comments_count | Integer | Number of comments post has
loves_count | Integer | Number of lafter it reaches 1000 views to the neares tenthikes post has
views_count | Integer | Number of views post has
views_count_rounded | Integer | Number of views rounded to three significant digits
loved | Boolean | Does this post has likes
reposted | Boolean | Has this post been reposted
watching | Boolen | Is this post watched by some user
links | Array | Array of <a href="#asset-and-cover-image">Assets</a>


## Comment

Field | Type |Description
--------- | ------ |-----------
id  | Integer |  Comment's id
post_id | Intefer | Post's id to which this comment is attached
content | Array | <table><tbody><tr><th>Field</th><th>Type</th><th>Description</th></tr><tr><td>kind</td><td>String</td><td>Posts can be represented by "text", "link", "photo"</td></tr><tr><td>link_url</td><td>String</td><td>Null if post ha no links</td></tr><tr><td>data</td><td>String</td><td>Contents HTML representation</td></tr></tbody></table>
created_at | DateTime | DateTime of comment's creation
author_id | Integer | User ID of comment's author

## Asset and Cover Image

Field | Type | Description
--------- | -------- | -----------
Id | Integer | Asset Id
Attachment | Object | Consists of 6 fields: original, optimized, xhdpi, hdpi, mdpi, ldpi. Last would be referred as Inner Object
Inner Object | Object |<table><tbody> <tr> <th>Field</th> <th>Type</th> <th>Description</th> </tr><tr> <td>URL</td><td>String</td><td>Asset's URL</td></tr><tr> <td>metadata</td><td>Object</td><td> Original doesn't have this field <table> <tbody> <tr> <th>Field</th> <th>Type</th> <th>Description</th> </tr><tr> <td>size</td><td>Integer</td><td>Size in bites</td></tr><tr> <td>type</td><td>String</td><td>MIME type</td></tr><tr> <td>width</td><td>Integer</td><td>Width in px</td></tr><tr> <td>height</td><td>Integer</td><td>Height in px</td></tr></tbody></table></td></tr></tbody></table>
