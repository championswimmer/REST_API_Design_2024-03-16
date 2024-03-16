# Blogging Website

# Entities 

## User 
- id 
- created_at
- updated_at
- username
- email
- password
- image
- bio

## Article 
- id 
- created_at
- updated_at                    // deleted_at or active (for soft delete)
- slug
- title
- subtitle 
- body 
- author_id                     // reference to user
- likes

## Comment
- id 
- created_at
- updated_at  
- body
- author_id                    // reference to user
- article_id                   // reference to article

## Tags 
- id 
- created_at
- updated_at
- name

### Mapping Entities

#### Article - Tag (Tags)
- article_id
- tag_id

#### User - Article (Likes / Favourites)
- user_id
- article_id

#### User - User (Follows)
- follower_id 
- followee_id 

# Functional Requirements 

## Users 

- User can register
- User who has already registered, can login 
- Users can update their profile
- Users can see other user's profile
- Users can (un)follow other users

## Articles

- Guests/Users can fetch all articles
  - Filter by tags
  - Filter by authors
  - Sort by created_at
  - Sort by likes
- Guests/Users can fetch a single article
- Users can fetch articles written users whom they follow (Your Feed)
- Users can create new articles 
  - Required tags will be created and associated to article
- Users can update their own articles
- Users can delete their own articles 
- Users can (un)favourite an article

## Comments

- Guests/Users can fetch all comments for an article
- Users can comment on articles
- Users can delete their own comments