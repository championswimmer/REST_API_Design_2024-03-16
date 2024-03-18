# API - Social Media Site

Base URL: `https://api.chirper.com/v1/`

**Authentication**

Headers:

```http
Authorization: Token <token>
```

## Generic Responses

### Success

```json
{
  "status": "success",
  "code": 201,
  "message": "Post created successfully",
  "data": {},
  "meta": {
    "page": 1,
    "limit": 10,
    "total": 100
  }
}
```

### Errors

```json
{
  "status": "error",
  "code": 400,
  "message": "Bad Request",
  "data": {},
  "meta": {}
}
```

## Endpoints

### Users

#### `POST /users` - Register/signup user

- 201 - Created
- 409 - Conflict (User already exists)
- 400 - Bad Request (Validation error)

#### `POST /users/login` - Login user

- 200 - OK
- 400 - Bad Request (Validation error)
- 401 - Unauthorized (Invalid Credentials)
- 404 - Not found (User not found)

#### `GET /users` - Search users

- `?display_name=Arnav` // contains or like %Arnav%
- `?username=arnav` // contains or like %arnav%

**Responses**

- 200 - OK
- 401 - Unauthorized (Invalid credentials)
- 404 - Not Found (User not found)

#### `GET /users/{@username/userid}` - Get user profile

**Responses**

- 200 - OK
- 401 - Unauthorized (Invalid credentials)
- 404 - Not Found (User not found)

#### `PATCH /users/me` 🔐 - Update user profile

**Responses**

- 202 - Accepted (Queued, profile update will likely succeed)
- 400 - Bad Request (Validation error)
- 401 - Unauthorized (Invalid Credentials)

#### `PUT /users/{username}/follow` 🔐 - Follow a user

- 200 - OK
- 400 - Bad Request (Validation error)
- 401 - Unauthorized (Invalid Credentials)

#### `DELETE /users/{username}/follow` 🔐 - Un/Follow a user

**Responses**

- 200 - OK (Unfollow successful)
- 202 - Accepted (Queued, Will likely succeed)
- 204 - No Content (Unfollow successful, no entity)
- 400 - Bad Request (Validation error)
- 401 - Unauthorized (Invalid Credentials)
- 404 - Not Found (User with `username` not found)

### Posts

#### `GET /users/{username}/posts` - Get all posts of a user

- `?sort=created_at` // sort by created_at
- `?sort=likes` // sort by likes
- `?page=1&limit=10` // pagination

**Responses**

- `200 OK` - Success
- `404 Not Found` - User not found

#### `GET /posts` - Get all posts

- `?display_name=Arnav` // filter by name
- `?sort=created_at` // sort by created_at
- `?sort=likes` // sort by likes
- `?page=1&limit=10` // pagination
- `?only_following=true` 🔐 // only posts of people I follow
- `?reply_to_post_id=123` // only replies to post with id = 123
- `?quoted_post_id=123` // only quotes of post with id = 123
  - `?is_retweet=true` // only retweets (body = null)

**Responses**

- `200 OK` - Success
  - Can be empty array `[]` in data
- 401 - Unauthorized (Invalid credentials)

#### `POST /posts` 🔐 - Create a new post

- body : `{body, ...}`
- body : `{media: [media_id, ...], ...}` if media is present
- body : `{reply_to_post_id}` - if it is a reply
- body : `{quoted_post_id}` - if it is a quote
  **Responses**

- 200 - OK
- 201 - Post created
- 401 - Unauthorized (Invalid credentials)

#### `GET /posts/{postid}` - Get a post

**Responses**

- 200 - OK
- 401 - Unauthorized (Invalid credentials)
- 404 - Not Found (Post not found)

#### `PUT /posts/{postid}/like` 🔐 - Like a post

**Responses**

- 200 - OK
- 202 - Accepted
- 401 - Unauthorized (Invalid credentials)
- 404 - Not Found (Post not found)

#### `DELETE /posts/{postid}/like` 🔐 - Unlike a post

**Responses**

- 200 - OK (Unlike successful)
- 202 - Accepted (Queued, Will likely succeed)
- 204 - No Content (Unlike successful, no entity)
- 400 - Bad Request (Validation error)
- 401 - Unauthorized (Invalid Credentials)
- 404 - Not Found (Post with `postid` not found)

#### `GET /posts/{postid}/likes` - Get all users who have liked

**Responses**

- 200 - OK
- 401 - Unauthorized (Invalid credentials)
- 404 - Not Found

### Media

#### `POST /media` 🔐 - Upload media

- body : `<bytes>` // media file : multipart/streaming

**Responses**

- 200 - OK
- 401 - Unauthorized (Invalid credentials)
- 415 - Unsupported Media Type

#### `DELETE /media/{mediaid}` 🔐 - Delete media

**Responses**

- 200 - OK
- 202 - Accepted
- 401 - Unauthorized (Invalid credentials)
- 404 - Not Found (Media not found)

## Notes

### REST API Principles

- Entities/Resources
  - goes into URL path
  - nouns
  - /users, /posts
  - when referring to "collections" -> always use plural
- Actions / Operations
  - use the HTTP method for this
  - verbs
  - eg: create, update, delete
  - POST, PUT, PATCH, DELETE
- Qualifiers / Filters / Modifiers
  - /posts?liked_by={userid}
  - /posts?created_before={timestamp}&created_after={timestamp}
  - /users?has_image=true

### HTTP Methods

- GET read/find/search
- POST create/submit
- PUT create/replace
- PATCH update/modify
- DELETE delete/remove
- OPTIONS get allowed methods
- HEAD status/connectivity checks

### POST vs PUT for creating a resource

`POST /posts`

- body : `{body, media, ...}`
- creates a new post
- server generates the id for this post
- response will have the new id

`PUT /posts/123`

- body : `{body, media, ...}`
- creates a new post with id = 123
- client is specifying the id for this post
- will replace post with id = 123 if it exists

### PUT vs PATCH for updating a resource

CASE A: Post with id = 123 exists
`{ a: 10, b: 20 }`

CASE B: Post with id = 123 does not exist

`PUT /posts/123`

- body : `{ b: 30, c: 40 }`
- replaces the post with id = 123 with `{ b: 30, c: 40 }`
- CASE A: `{ b: 30, c: 40 }`
- CASE B: `{ b: 30, c: 40 }`

`PATCH /posts/123`

- body : `{ b: 30, c: 40 }`
- CASE A: `{ a: 10, b: 30, c: 40 }`
- CASE B: 404 Not Found
