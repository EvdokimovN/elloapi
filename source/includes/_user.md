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
