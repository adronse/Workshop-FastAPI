# Workshop 1 - FastAPI :open_book:

During this workshop, you will create a simple backend using the python web framework FastAPI

FastAPI is a modern, fast (high-performance), web framework for building APIs with Python 3.6+ based on standard Python type hints.

Please make sure to read each step carefully, as very useful links are given with the instructions.

Every Python files contains TODO instructions. Take a look at them to get more details and context about the task.

## Step 0 : Initialization :rocket:

First, download and extract the `source.zip` file [here](https://github.com/adronse/Workshop-FastAPI/blob/main/source.zip).
It contains all necessary files, but for the moment they're empty :wink:

The project structure should be the following :

```
.
├── requirements.txt
├── step1
│   └── main.py
├── step2
├── step3
├── step4
└── step5

```

At the root directory, create a virtual environment like so:
   - python3 -m venv (NAME_ENV)
   - source (NAME_ENV)/bin/activate
Then, run `pip install -r requirements.txt` at the root of the downloaded folder.

## Step 1 : Running the backend server

As said before, the web framework you'll use to create your backend is FastAPI.
It's all based on standard Python 3.6 type declarations (thanks to Pydantic). No new syntax to learn. Just standard modern Python.

FastAPI uses the ASGI server implementation you can see that like the as the "node server".

### To launch the server

- cd step1/

- If you have been following the instructions run: uvicorn main:app

- You should see a prompt telling you the server is running on http://127.0.0.1:8000

- Go to http://127.0.0.1:8000/docs you should see an awesome interface with your different endpoints ! (You should have only one tho)

- In the next steps, make sure to launch the server in the directories (To test step2: cd into step2 then uvicorn)

## Step 2 : Greet user :gear:

Now that your server is up and running lets define some controllers or routes, this is basically the endpoints of your server, lets say you have a mobile app or a web server. Those endpoints will be called to retrieve some data like fetching a database, authenticate a user etc..
Use the example in the step1 to return a response body that says: "Hello, [Your name]"

## Step 3 : Endpoint with path parameters :test_tube:

It is quite common for website to have parameters in the url, like epitech.intra/user/johndoe

Lets define an endpoint with a path parameter.
There is a hint in your files, you should find out easily.


## Step 4 : Endpoint with a request body

When you need to send data from a client (let's say, a browser) to your API, you send it as a request body.

A request body is data sent by the client to your API. A response body is the data your API sends to the client.

Your API almost always has to send a response body. But clients don't necessarily need to send request bodies all the time.

To declare a request body, you use Pydantic models with all their power and benefits
See your file in step4 for futhermore instructions.

## Step 5 : It gets harder

Your goal will be to create a new user into firebase, dont worry you wont have to setup anything 
Futhermore instructions in the step5 folder

To know if you create a new user correctly ask me to look if the user was created.

### Authors

[Adrien Ronse](https://github.com/adronse)
