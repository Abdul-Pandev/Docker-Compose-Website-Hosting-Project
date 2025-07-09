# Docker-Compose-Website-Hosting-Project
This is a project I hosted a website locally by using docker compose

# 🐳 Docker Compose Website Hosting Project

This project demonstrates how to use **Docker Compose** to containerize and host a simple local website. It includes:

- A **Flask API** (`api.py`) that returns a list of fruits
- A **PHP frontend** (`index.php`) that fetches and displays data from the API

## 📁 Project Structure



## 🔧 Prerequisites

Make sure you have the following installed:

- [Docker](https://www.docker.com/products/docker-desktop)
- [Docker Compose](https://docs.docker.com/compose/install/)

## 📦 Docker Compose Configuration
<pre lang="markdown"><code>```
  version: "3"

services:
  fruit-service:
    build: ./product
    volumes:
      - ./product:/usr/src/app
    ports:
      - 5001:80

  website:
    image: php:apache
    volumes:
      - ./website:/var/www/html
    ports:
      - 5000:80
    depends_on:
      - fruit-service
      
 ```</code></pre>

## Code for api.py
<pre lang="markdown"><code>```
  
from flask import Flask
from flask_restful import Resource, Api

# create a flask object
app = Flask(__name__)
api = Api(app)

# creating a class for Fruits that will hold
# the accessors
class Fruits(Resource):
    def get(self):
        # returns a dictionary with fruits
        return {
            'fruits': [
                'Mango',
                'Kulikuli',
                'Gaya',
                'Tama',
                'Shinkaaafa',
                'Sakoro',
                'Apple',
                'Orange',
                'Rambutan'
            ]
        }

# adds the resources at the root route
api.add_resource(Fruits, '/')

# if this file is being executed then run the service
if __name__ == '__main__':
    # run the service
    app.run(host='0.0.0.0', port=80, debug=True)

  ```</code></pre>
