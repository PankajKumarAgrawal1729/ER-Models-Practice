## Social Media Platform

A social media app allows users to post content, follow each other, and react to posts. Users can belong to groups. This exercise focuses on recursive (unary) relationships and ternary relationships.


### Requirements

- Each user has a User ID, username, email, bio, and profile picture URL.
- A user can follow other users. Following is a directed relationship (A follows B ≠ B follows A).
- Each post has a Post ID, content text, timestamp, and media URL (optional).
- A post is created by one user. A user can create many posts.
- Users can react to posts with a reaction type (Like, Love, Haha, Sad, Angry).
- Users can belong to multiple groups. A group has a Group ID and name.
- A user can be an admin of a group (a user can admin multiple groups).


<details>
  <summary>💡 Show Hints (attempt first!)</summary>

- 💡 FOLLOWS is a unary (recursive) relationship on USER — the same entity on both sides
- 💡 REACTS_TO is M:N between USER and POST with ReactionType as an attribute
- 💡 BELONGS_TO is M:N between USER and GROUP
- 💡 ADMINS is a separate relationship (1:N from USER to GROUP, or M:N if multiple admins per group)
- 💡 Media URL is optional — you can show this with partial participation or a nullable attribute notation
</details>

<details>
    <summary>Reveal Answer & Diagram</summary>

<details>
<summary>ER Diagram</summary>
           
- [ER diagram](https://github.com/PankajKumarAgrawal1729/ER-Models-Practice/blob/main/Social%20Media%20Platform/ERDiagram.png)
    </details>
 <details>
        <summary>Entities & Rels</summary>

- Entities
    - USER
    - POST
    - GROUP
- Relationships
    - FOLLOWS (unary/recursive) USER ↔ USER (M:N)
    - CREATES USER ↔ POST (1:N)
    - REACTS_TO USER ↔ POST (M:N)
        - Attributes: ReactionType, ReactedAt
    - BELONGS_TO USER ↔ GROUP (M:N)
    - ADMINS USER ↔ GROUP (M:N)
    </details>

    <details>
        <summary>Analysis</summary>

#### ✦ Key Concepts in This Exercise

##### Unary (Recursive) Relationship — FOLLOWS
- FOLLOWS connects USER to itself. In ER notation, draw a loop from USER back to USER through the FOLLOWS diamond. Label the two roles: 'follower' and 'followee'. This is M:N because one user can follow many, and be followed by many.

##### Role Labels on Recursive Relationships
- When an entity participates more than once in a relationship, you MUST add role labels to the connecting lines. For FOLLOWS: the USER on one end is the 'follower', the USER on the other end is the 'followee'.

##### ReactionType as Relationship Attribute
- ReactionType (Like, Love, Haha) belongs on REACTS_TO, not on POST or USER. A single user can react to many posts with different types, and a post can have many reactions from different users.

- ⚠️ Don't draw FOLLOWS as a regular relationship between two separate entities — there's only ONE User entity
- ⚠️ Don't forget role labels (follower/followee) on the recursive relationship
- ⚠️ REACTS_TO must be M:N, not 1:N — one post gets many reactions, one user reacts to many posts
- ⚠️ ADMINS and BELONGS_TO should be two separate relationships, even though both connect USER and GROUP
    </details>
</details>

#### Self Assessment — How did your diagram compare?

- [x] I drew FOLLOWS as a unary (recursive) relationship on USER
- [x] I added role labels 'follower' and 'followee' to the FOLLOWS relationship lines
- [x] I placed ReactionType on the REACTS_TO relationship
- [x] I recognised that ADMINS and BELONGS_TO are two separate relationships
- [x] I correctly identified all M:N relationships