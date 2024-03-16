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

#### User - Article (Likes / Favourites)

#### User - User (Follows)

# Functional Requirements 

