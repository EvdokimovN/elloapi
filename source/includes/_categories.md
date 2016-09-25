# Categories

## GET Recent/Featured posts

```shell

curl -G 'https://ello.co/api/v2/cateories/posts/recent'
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
curl -G 'https://ello.co/api/v2/categories/fashion/posts/recent'
     -d 'access_token=<token>' 
```

### HTTP Request 
`GET https://ello.co/api/v2/categories/<category>/posts/recent`

Returns recent posts from specified category. Response is similar to previous request

Parameter | Type | Optional | Default | Description
--------- | ------- | -----------|--------------|------------
per_page | Integer | true | 25 | Specifies how many posts to return
before | String | true | NULL | Coded time 