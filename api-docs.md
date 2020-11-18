# API Docs

### Authentication

All requests are required to have an `Authorization` header with a value `Token {your_token}` . This can be retrieved from the login endpoint.

### POST /auth/users/

Creates a new user. Will give a bad status code if the password doesn't pass Django's built-in password validation.

Example post data for a teacher user:

```javascript
{ 
    "username": "myTeacherUsername",
    "password": "myPassword",
    "is_teacher": true
}
```

Example post data for a student user:

```javascript
{ 
    "username": "myStudentUsername",
    "password": "myPassword",
    "is_teacher": false,
    "class_code": "classCode"
}
```

### POST /auth/token/login/

Creates an authentication token to access endpoints with. This will return a json with only a `token` . This is the token you use for authorization.

## Questions

```javascript
{
    "id": 2,
    "body": "What is the definition of opportunity cost?",
    "times_answered": 54,
    "times_correct": 38,
    "tags": [
        "Economics"
    ],
    "answer": [
        2
    ],
    "level": 1,
    "choices": [
        {
            "id": 5,
            "body": "a pizza",
            "times_chosen": 2,
            "question": 2
        },
        {
            "id": 6,
            "body": "a choice",
            "times_chosen": 5,
            "question": 2
        },
        {
            "id": 7,
            "body": "the loss of potential gain from other alternatives when one alternative is chosen",
            "times_chosen": 38,
            "question": 2
        },
        {
            "id": 8,
            "body": "the cost of giving some an opportunity",
            "times_chosen": 9,
            "question": 2
        }
    ]
}
```

### GET /questions/

Gets all questions associated with the class code associated with the authenticated user.

Can also use `tag` or `level` to filter the question by a tag or level id. \(The level must be in the class associated with that account\)

### POST /questions/

Adds a new question.

### GET /questions/{question\_id}/

Gets question with id `question_id`.

### PUT /questions/{question\_id}/

Updates the question.

### DELETE /questions/{question\_id}/

Deletes the question.

## Results

```javascript
{
            "id": 112,
            "level": 1,
            "distance": 1204.41968,
            "player_id": 20,
            "award_list": [
                "gold medal"
            ],
            "player_name": "studentD"
        }
```

### GET /results/summary/

Gets paginated results.

### GET /players/{player\_id}/results/

Get paginated results by players.

### POST /players/{player\_id}/results/

Add a new result of a game play.

### GET /levels/{levels\_id}/results/

Gets all results for a given level paginated.



## Players

### GET /players/{player\_id}/

Get a particular player.

### GET /players/me/

Get your player \(including your id\) based on your authentication. If you are not logged in as a player, this endpoint will return a 401.

## Teachers

```javascript
{
    "id": 9,
    "name": "teacher",
    "class_code": "$DJE"
}
```

### GET /teachers/me

Get your teacher based on your authentication. If you are not logged in as a teacher, this endpoint will return a 401.

## Levels

```javascript
{
            "id": 5,
            "name": "Critical Consumerism"
}
```

### GET /levels/

Get a list of all of the levels.

### POST /levels/

Add a new level.

### GET /levels/{level\_id}/

Get a particular level.

### DELETE /levels/{level\_id}/

Deletes a particular level.



