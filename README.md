# Social Media System Database Schema
This is a database schema for a social media system that includes tables for users, photos, comments, likes, follows, tags, and photo tags.

# Getting Started
To use this schema, you will need to have a MySQL database set up. You can then use the SQL statements in this schema to create the necessary tables.

# Tables
users
The users table contains information about users on the social media system. The table has the following columns:

+ id (integer, primary key): Unique identifier for the user.
+ username (varchar(255), unique, not null): The user's username, which must be unique.
+ created_at (timestamp, default now()): The date and time when the user was created.

# photos
The photos table contains information about photos that have been uploaded to the social media system. The table has the following columns:

+ id (integer, primary key): Unique identifier for the photo.
+ image_url (varchar(255), not null): The URL where the photo can be accessed.
+ user_id (integer, not null): The ID of the user who uploaded the photo.
+ created_at (timestamp, default now()): The date and time when the photo was uploaded.
+ FOREIGN KEY(user_id) REFERENCES users(id): A foreign key constraint that ensures that the user_id column references a valid user in the users table.

# comments
The comments table contains information about comments that have been made on photos in the social media system. The table has the following columns:

+ id (integer, primary key): Unique identifier for the comment.
+ comment_text (varchar(255), not null): The text of the comment.
+ photo_id (integer, not null): The ID of the photo that the comment was made on.
+ user_id (integer, not null): The ID of the user who made the comment.
+ created_at (timestamp, default now()): The date and time when the comment was made.
+ FOREIGN KEY(photo_id) REFERENCES photos(id): A foreign key constraint that ensures that the photo_id column references a valid photo in the photos table.
+ FOREIGN KEY(user_id) REFERENCES users(id): A foreign key constraint that ensures that the user_id column references a valid user in the users table.

# likes
The likes table contains information about likes that have been made on photos in the social media system. The table has the following columns:

+ user_id (integer, not null): The ID of the user who made the like.
+ photo_id (integer, not null): The ID of the photo that the like was made on.
+ created_at (timestamp, default now()): The date and time when the like was made.
+ PRIMARY KEY(user_id, photo_id): A composite primary key that ensures that each user can only like a photo once.
+ FOREIGN KEY(user_id) REFERENCES users(id): A foreign key constraint that ensures that the user_id column references a valid user in the users table.
+ FOREIGN KEY(photo_id) REFERENCES photos(id): A foreign key constraint that ensures that the photo_id column references a valid photo in the photos table.

# follows
The follows table contains information about followers and followees in the social media system. The table has the following columns:


+ followee_id (integer, not null): The ID of the user who is being followed.
+ created_at (timestamp, default now()): The date and time when the follow relationship was created.
+ PRIMARY KEY(follower_id, followee_id): A composite primary key that ensures that each follow relationship is unique.
+ FOREIGN KEY(follower_id) REFERENCES users(id): A foreign key constraint that ensures that the follower_id column references a valid user in the users table.
+ FOREIGN KEY(followee_id) REFERENCES users(id): A foreign key constraint that ensures that the followee_id column references a valid user in the users table.

# tags
The tags table contains information about tags that have been added to photos in the social media system. The table has the following columns:

+ id (integer, primary key): Unique identifier for the tag.
+ tag_name (varchar(255), unique): The name of the tag, which must be unique.
+ created_at (timestamp, default now()): The date and time when the tag was created.

# photo_tags
The photo_tags table contains information about which tags have been added to which photos in the social media system. The table has the following columns:

+ photo_id (integer, not null): The ID of the photo that the tag was added to.
+ tag_id (integer, not null): The ID of the tag that was added to the photo.
+ PRIMARY KEY(photo_id, tag_id): A composite primary key that ensures that each tag can only be added to a photo once.
+ FOREIGN KEY(photo_id) REFERENCES photos(id): A foreign key constraint that ensures that the photo_id column references a valid photo in the photos table.
+ FOREIGN KEY(tag_id) REFERENCES tags(id): A foreign key constraint that ensures that the tag_id column references a valid tag in the tags table.

# Conclusion
This schema provides a basic structure for a social media system that includes users, photos, comments, likes, follows, tags, and photo tags. You can use this schema as a starting point for your own social media system, or modify it to fit your specific needs.
