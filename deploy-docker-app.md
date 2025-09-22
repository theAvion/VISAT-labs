# Deploy a Simple Application in Docker

This guide shows how to deploy a simple Python Flask application inside
Docker.

------------------------------------------------------------------------

## 1. Create the Application

Make a folder for your app:

``` bash
mkdir flask-docker-app
cd flask-docker-app
```

Inside it, create a file called `app.py`:

``` python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello, Docker World!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

------------------------------------------------------------------------

## 2. Add `requirements.txt`

This tells Docker what dependencies to install:

    flask

------------------------------------------------------------------------

## 3. Write a Dockerfile

Create a file named `Dockerfile` in the same folder:

``` dockerfile
# Use an official Python image
FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Copy requirements and install dependencies
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

# Copy the application code
COPY . .

# Expose port
EXPOSE 5000

# Command to run the app
CMD ["python", "app.py"]
```

------------------------------------------------------------------------

## 4. Build the Docker Image

Run this command inside the project directory:

``` bash
docker build -t flask-docker-app .
```

------------------------------------------------------------------------

## 5. Run the Container

``` bash
docker run -d -p 5000:5000 flask-docker-app
```

Now open <http://localhost:5000> in your browser, and you should see:

    Hello, Docker World!

------------------------------------------------------------------------

Pillere, You just deployed a simple app in Docker!
