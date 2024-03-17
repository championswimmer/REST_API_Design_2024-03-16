# API - Social Media Site

Base URL: `https://api.chirper.com/v1/`

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
    "meta": {
    }
}
```

## Endpoints

### Users 

### Posts 

### Media


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


### HTTP Methods

- GET                   read/find/search
- POST                  create/submit 
- PUT                   create/replace
- PATCH                 update/modify
- DELETE                delete/remove
- OPTIONS               get allowed methods
- HEAD                  status/connectivity checks

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
