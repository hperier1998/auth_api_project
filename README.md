# auth_apii
API for the Web Service class at Ynov Aix-en-Provence.

## Project Description
This project is a Django-based WebService allowing a simple user authentication with tokens.

## Table of contents
- [Installation](#Installation)
- [Running the API](#Running-the-API)
- [Using Postman to interact with the API](#Using-Postman-to-interact-with-the-API)

## Installation
Step 1. Clone the repository.

```git clone https://github.com/hperier1998/auth_api_project```

Step 2. Navigate to the project directory. 

```cd auth_api_project```

Step 3. Install the dependencies.

```pip install -r requirements.txt```

## Running the API
Step 1. Navigate to the project directory if you're not already there. 

Step 2. Run migrations to create database tables:

```python manage.py makemigrations```

```python manage.py migrate```

Step 3. Create a super user (admin user):

```python manage.py createsuperuser```

Then follow the instructions on screen.

Step 4. Run the Django server.

```python manage.py runserver```

The server should now be running at http://localhost:8000/ OR http://127.0.0.1:8000/.

You can access the API endpoints using this base URL.

## Using Postman to interact with the API
Step 1. Open Postman on your computer. ([Download Postman here](https://www.postman.com/downloads/))

Step 2. You can now start interacting with the API by using the following URLs.

Remember to set the correct **METHOD** in Postman.


### POST Requests

#### 1. Create a user account
Postman Configuration:
```
Method: 
POST

URL: 
http://127.0.0.1:8000/api/users/register/ 
OR 
http://localhost:8000/api/users/register/

Body: 
raw and JSON
```

Example of the JSON format to create a new user account.

```
{
    "username": "mynewynovuser",
    "email": "mynewynovuser@ynov.com",
    "password": "password123"
}
```

#### 2. Obtain a authentication token
Postman Configuration:
```
Method: 
POST

URL: 
http://127.0.0.1:8000/api/token/
OR 
http://localhost:8000/api/token/

Body: 
raw and JSON
```

Example of the JSON format to retrieve a token
```
{
    "username": "mynewynovuser",
    "password": "password123"
}
```

#### 3. Refresh a authentication token
Postman Configuration:
```
Method: 
POST

URL: 
http://127.0.0.1:8000/api/token/refresh/
OR 
http://localhost:8000/api/token/refresh/

Body: 
raw and JSON
```

Example of the JSON format to refresh a token
```
{
  "refresh": "<refresh_token>"
}
```
Replace the <refresh_token> with the refresh token of the user you wish to refresh the token for. The refresh token can be acquired by using the previous POST request number 2 to retrieve the authentication token

### GET Request

#### 4. View a user account
Postman Configuration:
```
Method: 
GET

URL: 
http://127.0.0.1:8000/api/users/<user_id>/
OR 
http://localhost:8000/api/users/<user_id>/

Headers: 
Add the key:                    Authorization
Add the value for the key :     Bearer <access_token>
```

Replace the <user_id> with the ID of the user you wish to view;

Replace the <access_token> with the access token of a user. The access token can be retrieved from the POST request number 2.

### PUT Request

#### 5. Edit a user account
Postman Configuration:
```
Method: 
PUT

URL: 
http://127.0.0.1:8000/api/users/<user_id>/
OR 
http://localhost:8000/api/users/<user_id>/

Headers: 
Add the key:                    Authorization
Add the value for the key :     Bearer <access_token>

Body: 
raw and JSON
```
Please note that the Bearer <access_token> has to either be the super user created previously, or the user which you are modifying the account for.

For example, if you are modifying <user_id> 2, you will need the <access_token> for the <user_id> 2 or the super user (admin).

Example of the JSON format to edit a user
```
{
  "username": "updateduser",
  "email": "updateduser@example.com",
  "password": "updatedpassword123"
}
```