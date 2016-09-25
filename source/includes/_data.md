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

## Comment

Field | Type |Description
--------- | ------ |-----------
id  | Integer |  Comment's id
post_id | Intefer | Post's id to which this comment is attached
content | Array | <table><tbody><tr><th>Field</th><th>Type</th><th>Description</th></tr><tr><td>kind</td><td>String</td><td>Posts can be represende by "text", "link", "photo"</td></tr><tr><td>link_url</td><td>String</td><td>Null if post ha no links</td></tr><tr><td>data</td><td>String</td><td>Contents HTML representation</td></tr></tbody></table>
created_at | DateTime | DateTime of comment's creation
author_id | Integer | User ID of comment's author



