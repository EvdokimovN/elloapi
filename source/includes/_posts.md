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
```shell
curl -G https://ello.co/api/v2/posts/11322508/comments
     -d "access_token=<token>"
```

### HTTP Request
`GET https://ello.co/api/v2/posts/<id>/comments`

Return all users commented on the post and their comments specified by <a href="#user">User</a> and <a href="#comment">Comment</a> data types

## GET Users reposted this post
```shell
curl -G https://ello.co/api/v2/posts/11323555/reposters
     -d "access_token=<token>"

curl -G https://ello.co/api/v2/posts/~tkd-_engpxhhy3w4yq9yug/reposters
     -d "access_token=<token>"          
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
curl -G https://ello.co/api/v2/posts/11323555/lovers
     -d "access_token=<token>"

curl -G https://ello.co/api/v2/posts/~tkd-_engpxhhy3w4yq9yug/lovers
     -d "access_token=<token>"   
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

## DELETE post

```shell
curl -G https://ello.co/api/v2/posts/11323555
     -H "authorization: Bearer <private_token>"
     -d "access_token=<token>"

curl -G https://ello.co/api/v2/posts/~tkd-_engpxhhy3w4yq9yug
     -H "authorization: Bearer <private_token>"
     -d "access_token=<token>"   
```
### HTTP Request 
`DELETE https://ello.co/api/v2/posts/<id>`

Deletes post
