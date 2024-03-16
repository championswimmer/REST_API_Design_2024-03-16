# API 

Base URL:   `https://api.blogging.site/v1/`

## Authentication

```
Authorization: Token <token>
```

## Generic Responses 

### Success 
```json
{
    "status": "success",
    "code": 200,
    "message": "Success message",
    "data": {},
    "meta": {
        "page": 1,
        "limit": 10,
        "total_pages": 100
    }
}
```

### Error

```json 
{
    "status": "error",
    "code": 400,
    "message": "Bad Request",
    "data": null,
    "meta": {}
}
```


## Endpoints

> HTTP Methods -> verb 
> Entities/Resources -> noun 
> 
> GET         fetch/find/read
> POST        create/submit
> PUT         create (with id)/replace/overwrite
> PATCH       update/modify existing 
> DELETE      delete 
> OPTIONS     find possible methods
> HEAD

### Users

#### `POST /users` - Signup/Register user

**Responses**
- 201 - Created
- 409 - Conflict (User already exists)
- 400 - Bad Request (Validation error)


#### `POST /users/login` - Login user 

**Request Body** 
```
{
    "email": "arnav09@mail.com"
    "password": "pass09"
}
```

**Responses** 
- 200 - OK 
    ```
    {
        "status": "success",
        "code": 200,
        "message": "Success message",
        "data": {
            "user": {
                "username": "arnav09",
                "email": "arnav09@mail.com",
                "token": "<token>"
            }
        },
        "meta": {
            "page": 1,
            "limit": 10,
            "total_pages": 100
        }
    }
    ```
- 404 - Not Found (User not found)
- 401 - Unauthorized (Invalid credentials)

#### `PATCH /users/me` 🔐 - Update user profile

**Responses**
- 202 - Accepted
- 401 - Unauthorized (Invalid credentials)
- 400 - Bad Request (Validation error)

#### `GET /users/{username}` 🔐 - Fetch user profile

**Responses**
- 200 - OK
- 401 - Unauthorized (Invalid credentials) 
- 404 - Not Found (User not found)

#### `PUT /users/{username}/follow` 🔐 - Follow user

**Responses**
- 202 - Accepted
- 401 - Unauthorized (Invalid credentials)
- 404 - Not Found (User not found)

#### `DELETE /users/{username}/follow` 🔐 - Un-follow user

**Responses**
- 202 - Accepted
- 401 - Unauthorized (Invalid credentials)
- 404 - Not Found (User not found)

#### `GET /users/{username}/followers` - Fetch followers of user

**Responses**
- 200 - OK
- 401 - Unauthorized (Invalid credentials) 
- 404 - Not Found (User not found)

### Articles 

#### `GET /articles` 📄 - Fetch all articles
- Query Params 
  - `tags=tag1,tag2` - Filter by tags
  - `author=username` - Filter by author
  - `sort=new` - Sort by created_at desc 
  - `sort=popular` - Sort by likes desc
  - `limit=10&page=1` - Pagination

#### `GET /articles?only_following=true` 🔐 - Fetch articles written by users whom the logged in user follows

#### `GET /articles/{slug}` - Fetch single article 

#### `POST /articles` 🔐 - Create new article

**Responses**
- 201 - Created
- 401 - Unauthorized (Invalid credentials)
- 400 - Bad Request (Validation error)

#### `PATCH /articles/{slug}` 🔐 - Update article

**Responses**

- 202 - Accepted
- 404 - Not Found (Article not found)
- 401 - Unauthorized (Invalid credentials)
- 403 - Forbidden (User is not the author)
- 400 - Bad Request (Validation error)

#### `DELETE /articles/{slug}` 🔐 - Delete article

**Responses**

- 202 - Accepted
- 404 - Not Found (Article not found)
- 401 - Unauthorized (Invalid credentials)
- 403 - Forbidden (User is not the author)
- 400 - Bad Request (Validation error)

#### `PUT /articles/{slug}/like` 🔐 - Like article

#### `DELETE /articles/{slug}/like` 🔐 - Unlike article


### Comments

#### `GET /articles/{slug}/comments` - Fetch all comments of an article

#### `POST /articles/{slug}/comments` 🔐 - Create new comment

#### `DELETE /articles/{slug}/comments/{id}` 🔐 - Delete comment


## Notes 

### POST vs PUT 

- `POST /articles` - creates an article
  - server decides the id of this new article 
- `PUT /articles/{id}` - creates an article with a specific id 
  - client decides the id of this new article
  - cannot use with eg: auto-incrementing ids
  - can be used if using uuids/guids 