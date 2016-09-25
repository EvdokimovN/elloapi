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