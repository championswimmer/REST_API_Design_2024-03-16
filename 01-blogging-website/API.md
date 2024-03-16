# API 

Base URL:   `https://api.blogging.site/v1/`

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

#### `POST /users/login` - Login user

#### `PATCH /users/me` 🔐 - Update user profile

#### `GET /users/{username}` 🔐 - Fetch user profile

#### `PUT /users/{username}/follow` 🔐 - Follow user

#### `DELETE /users/{username}/follow` 🔐 - Un-follow user

#### `GET /users/{username}/followers` - Fetch followers of user


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

#### `PATCH /articles/{slug}` 🔐 - Update article

#### `DELETE /articles/{slug}` 🔐 - Delete article

#### `PUT /articles/{slug}/like` 🔐 - Like article

#### `DELETE /articles/{slug}/like` 🔐 - Unlike article


### Comments

#### `GET /articles/{slug}/comments` - Fetch all comments of an article

#### `POST /articles/{slug}/comments` 🔐 - Create new comment

#### `DELETE /articles/{slug}/comments/{id}` 🔐 - Delete comment