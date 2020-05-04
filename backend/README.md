# Full Stack Trivia API Backend

## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Enviornment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by navigating to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/)  is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in app.py and can reference models.py. 

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server. 

## Database Setup
With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:
```bash
psql trivia < trivia.psql
```

## Running the server

From within the `backend` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```

Setting the `FLASK_ENV` variable to `development` will detect file changes and restart the server automatically.

Setting the `FLASK_APP` variable to `flaskr` directs flask to use the `flaskr` directory and the `__init__.py` file to find the application. 

## Tasks

One note before you delve into your tasks: for each endpoint you are expected to define the endpoint and response data. The frontend will be a plentiful resource because it is set up to expect certain endpoints and response data formats already. You should feel free to specify endpoints in your own way; if you do so, make sure to update the frontend or you will get some unexpected behavior. 

1. Use Flask-CORS to enable cross-domain requests and set response headers. 
2. Create an endpoint to handle GET requests for questions, including pagination (every 10 questions). This endpoint should return a list of questions, number of total questions, current category, categories. 
3. Create an endpoint to handle GET requests for all available categories. 
4. Create an endpoint to DELETE question using a question ID. 
5. Create an endpoint to POST a new question, which will require the question and answer text, category, and difficulty score. 
6. Create a POST endpoint to get questions based on category. 
7. Create a POST endpoint to get questions based on a search term. It should return any questions for whom the search term is a substring of the question. 
8. Create a POST endpoint to get questions to play the quiz. This endpoint should take category and previous question parameters and return a random questions within the given category, if provided, and that is not one of the previous questions. 
9. Create error handlers for all expected errors including 400, 404, 422 and 500. 

REVIEW_COMMENT
```
This README is missing documentation of your endpoints. Below is an example for your endpoint to get all categories. Please use it as a reference for creating your documentation and resubmit your code. 

Endpoints
GET '/categories'
GET ...
POST ...
DELETE ...

GET '/categories'
- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Request Arguments: None
- Returns: An object with a single key, categories, that contains a object of id: category_string key:value pairs. 
{'1' : "Science",
'2' : "Art",
'3' : "Geography",
'4' : "History",
'5' : "Entertainment",
'6' : "Sports"}

```


## Testing
To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python3 test_flaskr.py
```

## API Reference

### Getting Started

- Base URL: At present this app can only be run locally and is not hosted as a base URL. The backend app is hosted at the default, ```http://127.0.0.1:5000/```, which is set as a proxy in the frontend configuration.
- Authentication: This version of the application does not require authentication or API keys.

### Error Handling
Errors are returned as JSON objects in the following format:
```
{
    "success": False, 
    "error": 404,
    "message": "Not found"
}
```
The API will return two error types when requests fail:
- 404: Resource Not Found
- 422: Not Processable

### Endpoints

#### GET /categories
- General:
    - Get all categories. Returns a success value, list of category objects and total number of categories.
- Sample: ```curl http://127.0.0.1:5000/categories```
```
{
   "success" : true,
   "categories" : {
      "4" : "History",
      "1" : "Science",
      "3" : "Geography",
      "6" : "Sports",
      "2" : "Art",
      "5" : "Entertainment"
   },
   "total_categories" : 6
}
```

#### GET /questions/?page=<page_number>
- General:
    - Get all questions. Returns paginated (10 per page) list of question objects, total number of questions, list of category objects and success value
- Sample: ```curl http://127.0.0.1:5000/questions```
```
{
   "questions" : [
      {
         "difficulty" : 4,
         "question" : "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?",
         "category" : 5,
         "answer" : "Apollo 13",
         "id" : 2
      },
      {
         "difficulty" : 4,
         "question" : "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?",
         "category" : 5,
         "id" : 4,
         "answer" : "Tom Cruise"
      },
      {
         "id" : 5,
         "answer" : "Maya Angelou",
         "difficulty" : 2,
         "question" : "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?",
         "category" : 4
      },
      {
         "question" : "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?",
         "difficulty" : 3,
         "category" : 5,
         "answer" : "Edward Scissorhands",
         "id" : 6
      },
      {
         "category" : 4,
         "question" : "What boxer's original name is Cassius Clay?",
         "difficulty" : 1,
         "answer" : "Muhammad Ali",
         "id" : 9
      },
      {
         "id" : 10,
         "answer" : "Brazil",
         "difficulty" : 3,
         "question" : "Which is the only team to play in every soccer World Cup tournament?",
         "category" : 6
      },
      {
         "question" : "Which country won the first ever soccer World Cup in 1930?",
         "difficulty" : 4,
         "category" : 6,
         "answer" : "Uruguay",
         "id" : 11
      },
      {
         "difficulty" : 2,
         "question" : "Who invented Peanut Butter?",
         "category" : 4,
         "id" : 12,
         "answer" : "George Washington Carver"
      },
      {
         "question" : "What is the largest lake in Africa?",
         "difficulty" : 2,
         "category" : 3,
         "answer" : "Lake Victoria",
         "id" : 13
      },
      {
         "answer" : "Agra",
         "id" : 15,
         "question" : "The Taj Mahal is located in which Indian city?",
         "difficulty" : 2,
         "category" : 3
      }
   ],
   "total_questions" : 18,
   "categories" : {
      "4" : "History",
      "2" : "Art",
      "5" : "Entertainment",
      "1" : "Science",
      "3" : "Geography",
      "6" : "Sports"
   },
   "success" : true
}
```

#### DELETE /questions/<int:question_id>
- General:
    - Deletes an existing question with given ID. Returns deleted id, list of questions objects, success value and number of remaining questions.
- Sample: ```curl -X DELETE http://127.0.0.1:5000/questions/4```
```
{
  "deleted": 4, 
  "questions": [
    {
      "answer": "Apollo 13", 
      "category": 5, 
      "difficulty": 4, 
      "id": 2, 
      "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
    }, 
    {
      "answer": "Maya Angelou", 
      "category": 4, 
      "difficulty": 2, 
      "id": 5, 
      "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
    }, 
    {
      "answer": "Edward Scissorhands", 
      "category": 5, 
      "difficulty": 3, 
      "id": 6, 
      "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
    }, 
    {
      "answer": "Muhammad Ali", 
      "category": 4, 
      "difficulty": 1, 
      "id": 9, 
      "question": "What boxer's original name is Cassius Clay?"
    }, 
    {
      "answer": "Brazil", 
      "category": 6, 
      "difficulty": 3, 
      "id": 10, 
      "question": "Which is the only team to play in every soccer World Cup tournament?"
    }, 
    {
      "answer": "Uruguay", 
      "category": 6, 
      "difficulty": 4, 
      "id": 11, 
      "question": "Which country won the first ever soccer World Cup in 1930?"
    }, 
    {
      "answer": "George Washington Carver", 
      "category": 4, 
      "difficulty": 2, 
      "id": 12, 
      "question": "Who invented Peanut Butter?"
    }, 
    {
      "answer": "Lake Victoria", 
      "category": 3, 
      "difficulty": 2, 
      "id": 13, 
      "question": "What is the largest lake in Africa?"
    }, 
    {
      "answer": "Agra", 
      "category": 3, 
      "difficulty": 2, 
      "id": 15, 
      "question": "The Taj Mahal is located in which Indian city?"
    }, 
    {
      "answer": "Escher", 
      "category": 2, 
      "difficulty": 1, 
      "id": 16, 
      "question": "Which Dutch graphic artist\u2013initials M C was a creator of optical illusions?"
    }
  ], 
  "success": true, 
  "total_questions": 17
}
```

#### POST /questions
- General:
    - Creates a new question with given inputs. Returns success value, question id, paginated list of question objects and number of total questions.
- Sample: ```curl http://127.0.0.1:5000/questions -X POST -H "Content-Type: application/json" -d '{"question": "What time is it", "answer": "None of your business", "difficulty": "4", "category": "1"}'```
```
{
  "created": 52, 
  "questions": [
    {
      "answer": "Apollo 13", 
      "category": 5, 
      "difficulty": 4, 
      "id": 2, 
      "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
    }, 
    {
      "answer": "Maya Angelou", 
      "category": 4, 
      "difficulty": 2, 
      "id": 5, 
      "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
    }, 
    {
      "answer": "Edward Scissorhands", 
      "category": 5, 
      "difficulty": 3, 
      "id": 6, 
      "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
    }, 
    {
      "answer": "Muhammad Ali", 
      "category": 4, 
      "difficulty": 1, 
      "id": 9, 
      "question": "What boxer's original name is Cassius Clay?"
    }, 
    {
      "answer": "Brazil", 
      "category": 6, 
      "difficulty": 3, 
      "id": 10, 
      "question": "Which is the only team to play in every soccer World Cup tournament?"
    }, 
    {
      "answer": "Uruguay", 
      "category": 6, 
      "difficulty": 4, 
      "id": 11, 
      "question": "Which country won the first ever soccer World Cup in 1930?"
    }, 
    {
      "answer": "George Washington Carver", 
      "category": 4, 
      "difficulty": 2, 
      "id": 12, 
      "question": "Who invented Peanut Butter?"
    }, 
    {
      "answer": "Lake Victoria", 
      "category": 3, 
      "difficulty": 2, 
      "id": 13, 
      "question": "What is the largest lake in Africa?"
    }, 
    {
      "answer": "Agra", 
      "category": 3, 
      "difficulty": 2, 
      "id": 15, 
      "question": "The Taj Mahal is located in which Indian city?"
    }, 
    {
      "answer": "Escher", 
      "category": 2, 
      "difficulty": 1, 
      "id": 16, 
      "question": "Which Dutch graphic artist\u2013initials M C was a creator of optical illusions?"
    }
  ], 
  "success": true, 
  "total_questions": 18
}
```

#### POST /questions/search
- General:
    - Search questions based on a search term. Returns any questions for whom the search term is a substring of the question.
- Sample: ```curl http://127.0.0.1:5000/questions/search -X POST -H "Content-Type: application/json" -d '{"searchTerm": "time"}'```
```
{
  "questions": [
    {
      "answer": "One", 
      "category": 2, 
      "difficulty": 4, 
      "id": 18, 
      "question": "How many paintings did Van Gogh sell in his lifetime?"
    }, 
    {
      "answer": "None of your business", 
      "category": 1, 
      "difficulty": 4, 
      "id": 52, 
      "question": "What time is it"
    }
  ], 
  "success": true, 
  "total_questions": 2
}
```

#### GET /categories/<int:category_id>/questions
- General:
    - Fetches questions from a given category. Returns current category, list of question objects, success value and total number of questions.
- Sample: ```curl http://127.0.0.1:5000/categories/3/questions```
```
{
  "current_category": 3, 
  "questions": [
    {
      "answer": "Lake Victoria", 
      "category": 3, 
      "difficulty": 2, 
      "id": 13, 
      "question": "What is the largest lake in Africa?"
    }, 
    {
      "answer": "Agra", 
      "category": 3, 
      "difficulty": 2, 
      "id": 15, 
      "question": "The Taj Mahal is located in which Indian city?"
    }, 
    {
      "answer": "a lot", 
      "category": 3, 
      "difficulty": 5, 
      "id": 25, 
      "question": "how much woud could a wood chuck chuck if it could chuck wood?"
    }
  ], 
  "success": true, 
  "total_questions": 3
}
```

#### POST /quizzes
- General:
    - Returns a random question within a given category that is not one of the previous questions. Returns success value and a list of a question object.
- Sample: ```curl http://127.0.0.1:5000/quizzes -X POST -H "Content-Type: application/json" -d '{"previous_questions": [], "quiz_category": {"type": "Science", "id": "1"}}'```
```
{
  "question": {
    "answer": "The Liver", 
    "category": 1, 
    "difficulty": 4, 
    "id": 20, 
    "question": "What is the heaviest organ in the human body?"
  }, 
  "success": true
}
```

## Deployment N/A

## Authors
Eugene

## Acknowledgments
Udacity!
