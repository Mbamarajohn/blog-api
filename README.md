A Blog API 

Requirements
​
Users should have a first_name, last_name, email, password, (you can add other attributes you want to store about the user)
A user should be able to sign up and sign in into the blog app
Use JWT as authentication strategy and expire the token after 1 hour
A blog can be in two states; draft and published
Logged in and not logged in users should be able to get a list of published blogs created
Logged in and not logged in users should be able to to get a published blog
Logged in users should be able to create a blog.
When a blog is created, it is in draft state
The owner of the blog should be able to update the state of the blog to published
 The owner of a blog should be able to edit the blog in draft or published state
 The owner of the blog should be able to delete the blog in draft or published state
The owner of the blog should be able to get a list of their blogs. 
The endpoint should be paginated
It should be filterable by state
Blogs created should have title, description, tags, author, timestamp, state, read_count, reading_time and body.
The list of blogs endpoint that can be accessed by both logged in and not logged in users should be paginated, 
default it to 20 blogs per page. 
It should also be searchable by author, title and tags.
It should also be orderable by read_count, reading_time and timestamp
When a single blog is requested, the api should return the user information(the author) with the blog. The read_count of the blog too should be updated by 1
Come up with any algorithm for calculating the reading_time of the blog.
Write tests for all endpoints
Create an ERD for entities and show relationships
Use Winston and ensure functions and processes are logged

Note:
The owner of the blog should be logged in to perform actions



Setup
Install NodeJS, mongodb
pull this repo
update env with example.env
run npm start
Base URL
somehostsite.com
https://www.heroku.com/free



Models

see ERD link
https://drawsql.app/teams/blogapi/diagrams/blogapi


APIs

Signup User

Route: /signup

Method: POST

Body:
{
  "email": "doe@example.com",
  "password": "Password1",
  "firstname": "jon",
  "lastname": "doe",
}


Responses
Success

{
    message: 'Signup successful',
    user: {
        "email": "doe@example.com",
        "password": "Password1",
        "firstname": "jon",
        "lastname": "doe",
        "username": 'jon_doe",
    }
}

Login User

Route: /login
Method: POST
Body:
{
  "passwordField": "Password1",
  "email": 'jon_doe@gmail.com",
}


Responses
Success

{
    message: 'Login successful',
    token: 'sjlkafjkldsfjsd'
}


Create Post
Route: /posts
Method: POST
Header
Authorization: Bearer {token}
Body:
{
  "title": "Nigeria and Justice",
  "tags": "Nigeria",
  "description": "Women do not suffer the most when it comes to dealing with societal constructs, without spaeaking up",
  "body": "Nigeria should stop ostracizing men and as well stop making them feel less of a human for showing emotions. Society feels no matter what calamity might have befallen a woman, he should never shed tears, that is totally wrong. ”.",
  "author": "Wole Soinka"
}



Responses
Success

- Body:
{
  "status": true,
  "blogPost": {
    "title": "Nigeria and Justice",
    "description": "Women do not suffer the most when it comes to dealing with societal constructs, without spaeaking up",
    "author": "Wole Soinka",
    "body": "Nigeria should stop ostracizing men and as well stop making them feel less of a human for showing emotions. Society feels no     matter what calamity might have befallen a woman, he should never shed tears, that is totally wrong. That must indeed be amazing to       those who hold themselves, or situations in which they are involved, higher than anointed standards—and that approximates an immense     proportion of the world.    
    "readCount": 0,
    "state": "draft",
    "readTime": 1,
    "tags": [
      "Nigeria"
    ],
    
    "_id": "6360ff37a3eb884508f1620f",
    "createdAt": "2022-11-01T11:12:55.873Z",
    "updatedAt": "2022-11-01T11:12:55.873Z",
    
    "__v": 0
  }
}



Get a Post
Route: /posts/:id

Method: GET

Responses

Success

- Body:

{
  "status": true,
  "blogPost": {
  
    "_id": "6360ff37a3eb884508f1620f",
    "title": "Nigeria and Justice",
    
    "description": "Women do not suffer the most when it comes to dealing with societal constructs, without spaeaking up",
    "author": "Wole Soinka",
    
    "body": "Nigeria should stop ostracizing men and as well stop making them feel less of a human for showing emotions. Society feels no matter what calamity might have befallen a woman, he should never shed tears, that is totally wrong. 
    "state": "draft",
    "readCount": 3,
    "readTime": 1,
    "tags": [
      "Nigeria"
    ],
    
    "createdAt": "2022-11-01T11:12:55.873Z",
    "updatedAt": "2022-11-02T01:18:20.265Z",
    
    "__v": 0
  }




Get All Posts
Route: /posts

Method: GET

Responses

Success

- Body:

{
 "status": true,
 "blogPost": [
 
   {
     "_id": "6360fd82a3eb884508f1620d",
     "title": "Women are dying in silence",
     "description": "Women do not suffer the most when it comes to dealing with societal constructs, without spaeaking up",
     "author": "Imole Yinka",
     "body": "Society should stop ostracizing men and as well stop making them feel less of a human for showing emotions. Society feels        no matter what calamity might have befallen a woman, he should never shed tears, that is totally wrong.",
     
     "readCount": 1,
     "readTime": 1,
     "tags": [
       "Women"
     ],
     "createdAt": "2022-11-01T11:05:38.702Z",
     "updatedAt": "2022-11-02T01:21:50.463Z",
     "__v": 0
   },
   
{
 "status": true,
 
 "blogPost": {
 
   "_id": "6360ff37a3eb884508f1620f",
   "title": "Nigeria and Justice",
   "description": "Women do not suffer the most when it comes to dealing with societal constructs, without spaeaking up",
   "author": "Wole Soinka",
   "body": "Nigeria should stop ostracizing men and as well stop making them feel less of a human for showing emotions. Society feels no      matter what calamity might have befallen a woman, he should never shed tears, that is totally wrong. 
   "state": "draft",
   "readCount": 3,
   "readTime": 1,
   "tags": [
     "Nigeria"
   ],
   "createdAt": "2022-11-01T11:12:55.873Z",
   "updatedAt": "2022-11-02T01:18:20.265Z",
   
   "__v": 0
 },
 
  {
     "_id": "6360ff37a3eb884508f1620f",
     "title": "Nigeria and Justice",
     
     "description": "Women do not suffer the most when it comes to dealing with societal constructs, without spaeaking up",
     
     "author": "Wole Soinka",
     
     "body": "Nigeria should stop ostracizing men and as well stop making them feel less of a human for showing emotions. Society feels        no matter what calamity might have befallen a woman, he should never shed tears, that is totally wrong. That must indeed be              amazing to those who hold themselves, or situations in which they are involved, higher than anointed standards—and that                  approximates an    immense proportion of the world. Among them are those in whom the man dies at the sight of what is patently            wrong—betrayal of standards; corruption and dishonesty; tyranny.Wole Soyinka was in the midst of the mix when Nigeria began to            totter towards what could be seen as the certain deterioration of values and, being alive, he spoke out. For his pains, he was put        into solitary confinement for several months. And while manifest injustice reigned and disintegration reared its head, Wole              Soyinka was released into an environment of tyranny which attempted to thrive under the insincerity of the slogan: “To Keep              Nigeria One Is A Task That Must Be Done.” Unrepentant, Soyinka had a ready riposte even on his way from prison: “To keep Nigeria          one, justice must be done”.",
     "state": "published",
     "readCount": 5,
     "readTime": 1,
     "tags": [
       "Nigeria"
     ],
     
     "createdAt": "2022-11-01T11:12:55.873Z",
     "updatedAt": "2022-11-02T09:52:43.170Z",
     "__v": 0
   },
   
   ]

   
### Update a Post
Route: /posts/edit/:id
Method: PATCH
Header
Authorization: Bearer {token}
- Body: 

{
  "state": "published"
  
}
Responses
Success

{
  "status": true,
  "blogPost": {
  
    "_id": "636242d64e852bf2689b3de7",
    
    "title": "Gulliver's travels",
    "description": "Our country do not suffer the most when it comes to dealing with societal constructs, without spaeaking up",
    "author": "chinua achebe",
    
    "owner": "635ea348769123203814f325",
    
    "body": "Our country should stop ostracizing men and as well stop making them feel less of a human for showing emotions. Society         feels no matter what calamity might have befallen a woman, he should never shed tears, that is totally wrong. That must indeed be         amazing to those who hold themselves, or situations in which they are involved,tyranny. He spoke out. For Nigeria, we were  put into     solitary confinement for several months. And while manifest injustice reigned and disintegration reared its head, Wole Soyinka was       released into an environment of tyranny which attempted to thrive under the insincerity of the slogan: “To Keep Nigeria One Is A Task     That Must Be Done.” Unrepentant, Soyinka had a ready riposte even on his way from prison: “To keep Nigeria one, justice must be           done”.",
    "state": "published",
    "readCount": 0,
    "readTime": 1,
    "tags": [
      "Fiction"
    ],
    "createdAt": "2022-11-02T10:13:42.835Z",
    "updatedAt": "2022-11-02T10:41:14.730Z",
    "__v": 0
  }
}

Delete a Post
Route: /posts/delete/:id

Method: DELETE

Header

Authorization: Bearer {token}
Body:

Response:

- Body:

{
 "status": true,
 "blogPost": {
   "acknowledged": true,
   "deletedCount": 1
 }
 
Contributor
Mbamara John
