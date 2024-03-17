# Social Media Site 
Basic features of Twitter/Mastodon type website. 
Posts, reposts, reply-posts, quotes, likes, follows
Posts can have 1 media 

## Entities 

### User 
- id
- created_at
- updated_at
- username
- email
- password
- image_id                 // references (media.id)
- bio


### Post 
- id
- created_at
- updated_at
- deleted_at
- user_id               // references (user.id)
- body
- reply_to_post_id      // references (post.id)
- reply_parent_post_id  // references (post.id)
- quoted_post_id        // references (post.id)


### Media 
- id
- created_at
- updated_at
- deleted_at
- media_type            // image, video, gif
- media_url             // url

### Mapping Tables 

#### User Follow 
- id
- created_at
- updated_at
- follower_id
- followee_id

#### Post Media
- id
- created_at
- updated_at
- post_id
- media_id

#### Post Like
- id
- created_at
- post_id
- user_id

## Functional Requirements



## Notes 

![](./post_relationship.png)