
<div style="text-align: justify;">

# Docker-Compose-Website-Hosting-Project
This is a project I hosted a website locally by using docker compose

# 🐳 Docker Compose Website Hosting Project

This project demonstrates how to use **Docker Compose** to containerize and host a simple local website. It includes:

- A **Flask API** (`api.py`) that returns a list of fruits
- A **PHP frontend** (`index.php`) that fetches and displays data from the API
- You will need three directories
- dcompose - mother directory
- product - sub-directory in dcompose containing api.py, dockerfile, and requirement.txt
- Website - a sub-directory in dcompose that contains index.php 
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

## Python Dependencies – product/requirements.txt
<pre lang="markdown"><code>```
flask
flask-restful
  
    ```</code></pre>

## PHP Frontend – website/index.php
<pre lang="markdown"><code>```
<!DOCTYPE html>
<html lang="en">
<head>
   <meta charset="UTF-8">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <title>Osman's Fruit Shop</title>
   <link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Roboto&display=swap" rel="stylesheet">
   <style>
       body {
           margin: 0;
           font-family: 'Roboto', sans-serif;
           background: linear-gradient(to right, #f9d423, #ff4e50);
           color: #fff;
           display: flex;
           flex-direction: column;
           align-items: center;
           justify-content: center;
           min-height: 100vh;
           animation: fadeIn 1s ease-in-out;
       }

       @keyframes fadeIn {
           from { opacity: 0; }
           to { opacity: 1; }
       }

       h1 {
           font-family: 'Pacifico', cursive;
           font-size: 3rem;
           margin-bottom: 20px;
           text-shadow: 2px 2px 4px #00000055;
       }

       ul {
           list-style: none;
           padding: 0;
           display: flex;
           flex-wrap: wrap;
           gap: 15px;
           justify-content: center;
       }

       li {
           background-color: rgba(255, 255, 255, 0.2);
           padding: 15px 25px;
           border-radius: 15px;
           font-size: 1.2rem;
           font-weight: bold;
           box-shadow: 0 4px 6px rgba(0,0,0,0.1);
           backdrop-filter: blur(10px);
           transition: transform 0.3s ease;
       }

       li:hover {
           transform: scale(1.1);
           background-color: rgba(255, 255, 255, 0.4);
       }
   </style>
</head>
<body>
   <h1>🍉 Welcome to Osman's Fruit Shop 🍍</h1>
   <ul>
       <?php
           $json = file_get_contents('http://fruit-service');
           $obj = json_decode($json);
           if (isset($obj->fruits) && is_array($obj->fruits)) {
               foreach ($obj->fruits as $fruit){
                   echo "<li>🍊 " . htmlspecialchars($fruit) . "</li>";
               }
           } else {
               echo "<li>No fruits available right now! 🍌</li>";
           }
       ?>
   </ul>
</body>
</html>
```</code></pre>


## Run

You first have to move to the main directory (dcompose)
<pre lang="markdown"><code>```
cd dcompose
```</code></pre>
You then build
<pre lang="markdown"><code>```
docker-compose up -d
```</code></pre>
This is what shows when building!
![building ](https://github.com/user-attachments/assets/b3acb58d-8784-4fed-a130-b4c5059708e1)

This is what happens when we build and run the URL
<pre lang="markdown"><code>```
HTTP://localhost:5000
```</code></pre>
This is what appears after everything is built.
![the website](https://github.com/user-attachments/assets/31946150-b824-4061-b5dd-86e784860f60)

## Conclusion

This project showcases the power and simplicity of Docker Compose in managing multi-container applications. By separating concerns into two services, a Flask REST API and a PHP-based frontend, we demonstrate how different technologies can be containerized and made to work together seamlessly in a local development environment.

Whether you're learning Docker, building microservices, or prototyping web applications, this setup provides a clean, modular, and reproducible foundation to build on.

Feel free to fork, extend, and explore!

</div>
