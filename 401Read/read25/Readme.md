# Table of contents

|Read No. | Name of chapter|
|:---------: |:--------------:|
|25|[Beginner’s Guide to Docker](Beginner’s-Guide-to-Docker.md)
|25|[Django for APIs - Library Website](Django-for-APIs-Library-Website.md)







# Beginner’s Guide to Docker
## Linux Containers
### Docker is really just Linux containers which are a type of virtualization.

### Virtualization has its roots at the beginning of computer science when large, expensive mainframe computers were the norm. How could multiple programmers use the same single machine? The answer was virtualization and specifically virtual machines which are complete copies of a computer system from the operating system on up.

### What’s the downside to a virtual machine? Size and speed. A typical guest operating system can easily take up 700MB of size. So if one physical server supports three virtual machines, that’s at least 2.1GB of disk space taken up along with separate needs for CPU and memory resources.

### Most computers rely on the same Linux operating system, so what if we virtualized from that level up instead? Wouldn’t that provide a lightweight, faster way to duplicate much of the same functionality?

### The answer is yes. And in recent years Linux containers, also known as “containerization,” has become increasingly popular. For most applications, a virtual machine provides far more resources than are needed and a container is more than sufficient.

### This, fundamentally, is what Docker is. A way to implement Linux containers!

## Install Docker
### To install Docker we need to [download the desktop app on our computer](https://www.docker.com/get-started) and create a free account. 

### Once Docker is done installing we can confirm the correct version is running. It should be at least version 19.
```
$ docker --version
```
## Hello, World

### To confirm Docker installed correctly we can run our first command ```docker run hello-world``` This will download an official image and then run the container. 

```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete
Digest: sha256:9572f7cdcee8591948c2963463447a53466950b3fc15a247fcad1917ca215a2f
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

### A good command to inspect Docker is ```docker info``` which we can run now. It will contain a lot of output but focus on the top lines which show we now have 1 container which is ```stopped``` and 1 image.
### Want to inspect just the current image?
```
$ docker image ls
REPOSITORY          TAG        IMAGE ID            CREATED             SIZE
hello-world         latest     fce289e99eb9        12 months ago       1.84kB
```
## Images and Containers
### Images and containers are the two fundamental concepts to grasp when you start with Docker. An image is a snapshot in time of what a project contains. A container is a running instance of the image.

### When we ran hello-world we used an official Docker image. We did not have to create the image ourself. But typically we will create custom images and we do so using a Dockerfile. We also will use docker-compose.yml files to run the containers.
## Images

### Ok, let’s create our own image for something more “real.” How about the Python programming language? We can create an image and container just for Python and later add on to it.

### First create a local directory on your computer for our code. I’ve chosen to make a code folder on my Desktop (I’m using an Apple computer) and then a python3.7 folder within that.
```
$ cd ~/Desktop
$ mkdir code && cd code
$ mkdir python3.7 && cd python3.7
```
### Now we need to define the image with a Dockerfile. This is similar to a Pipenv or a requirements.txt file; it is a list of all the requirements needed to build our image. It is simpler to have them all in one place rather than install each manually line-by-line.

### If you are on a Mac, you can create a new Dockerfile on the command line using the touch command.
```
$ touch Dockerfile
```
### With your text editor add the following single line of code to the Dockerfile.
```
# Dockerfile
FROM python:3.7-alpine
```
### Dockerfiles are read from top-to-bottom. The first instruction must be the FROM command which lets us import a base image to use for our image. This base image could be another Docker image or one we create entirely from scratch.

### In this case we’ll be using the official Docker image for Python 3.7, specifically the alpine version which includes only the bare minimum needed to run Python. The alpine version takes up 78MB of space versus full Python’s 923MB so it is a good option to start with!

## Image Builds
### With our instructions complete it’s time to “build” or create the image for the first time. Don’t forget that period ```.``` at the end of the command!
```
$ docker image build .
Sending build context to Docker daemon  2.048kB
Step 1/1 : FROM python:3.7-alpine
3.7-alpine: Pulling from library/python
c9b1b535fdd9: Pull complete
2cc5ad85d9ab: Pull complete
53a2fca3c2ea: Pull complete
30fce49de8b1: Pull complete
49bcb9571cc7: Pull complete
Digest: sha256:7655eea15dfd981eeb7d243af21e8561e967709caba938d50b136cdb992f3546
Status: Downloaded newer image for python:3.7-alpine
 ---> b2c276538711
Successfully built b2c276538711
```
### There will be a lot of output here ending with Successfully built and the hash id, b2c276538711, for the image. The actual id hashes may change by the time you read this post as each image continually updated by the Docker community.

### We can list all existing Docker images to confirm this new one has been built alongside the initial alpine image.
```
$ docker image ls
REPOSITORY      TAG             IMAGE ID            CREATED             SIZE
python          3.7-alpine      b2c276538711        3 days ago          97.7MB
hello-world     latest          fce289e99eb9        12 months ago       1.84kB
```
### There are currently two images: the hello-world image we previously downloaded and one for python we just built.

## Image Layers
### Every image is made up of one or more image layers. The base layer is often a flavor of Linux, like alpine. When we built the image for python:3.7-alpine this image had the id b2c276538711. But that image depended on five other images which were visible while building it:
```
c9b1b535fdd9: Pull complete
2cc5ad85d9ab: Pull complete
53a2fca3c2ea: Pull complete
30fce49de8b1: Pull complete
49bcb9571cc7: Pull complete
```
### This is called image layering and it exists for two main reasons. First, each image layer is immutable–unchanged–like a git commit. This helps ensure consistency when two developers build the same image. The second reason is performance. Docker caches the steps in a Dockerfile to speed up subsequent builds. When a change is made to a step, all steps following it will be executed from scratch.

### For this reason, order matters in a Dockerfile. Typically you want to put code that won’t change often at the top and code that will change at the end. 

## Containers
### Now that we have our Python image how do we run it? Well just as a Dockerfile is a list of image instructions there is also a docker-compose.yml file that is a list of container instructions.

### To demonstrate a real-world image and container example we will now “Dockerize” a basic Django web app.

### Creat new Django project and run the server tomake sure that everything is working fine 
### Stop the local server with the command Control+c. And exit the virtual environment by also typing exit.
## Dockerized Django
### We’ll now create a Dockerfile for our image which will completely replace our local dev environment, so this will have Python 3 and Django. Then we’ll add a docker-compose.yml for the container instructions. Make each file via the command line.
```
$ touch Dockerfile
$ touch docker-compose.yml
```
### This Dockerfile has several commands. RUN, COPY, and ADD each create a new layer.
```
# Dockerfile

# Python version
FROM python:3.7-alpine

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Set work directory
WORKDIR /code

# Install dependencies
COPY Pipfile Pipfile.lock /code/
RUN pip install pipenv && pipenv install --system

# Copy project
COPY . /code/
```
### Order matters in Dockerfiles since they are executed from top-to-bottom. First we use FROM to install python:3.7-alpine as our base image and set two environment variables with ENV. The first, PYTHONDONTWRITEBYTECODE will remove .pyc files from our container which is a good optimization. The second, PYTHONUNBUFFERED will buffer our output so it will look “normal” within Docker for us.

### Then we used the WORKDIR command to create and set /code as our default directory within Docker. That means if in the future we want to run a command like python manage.py runserver we don’t have to also specify it should be run in the /code folder.

### The Pipfile contains information on our software packages so we copy that over, too. (Technically we could use COPY Pipfile . and because of the WORKDIR setting it would still go in the /code folder!)

### And then we install Pipenv itself via pip and then run pipenv install to install the software packages in our Pipfile. Note that we added the --system tag so that software packages are available throughout the entire container, not within a virtual environment which is Pipenv’s default but doesn’t make sense here since the entire Docker container is a virtual environment.



### An important point to make here is that the order in a Dockerfile matters a lot. Because of layer caching when a step changes in the Dockerfile, all subsequent work needs to be redone.

### For example, the very last line here is COPY . /code. That means any code changes locally will be copied over. However there are no commands after that; nothing else needs to be rebuilt. If we had put this command earlier in the Dockerfile, say, before we install the Pipfile, then every time there is a local code change all our requirements would have to be reinstalled on the image. Wasteful.

### Without going too far down this rabbit hole, remember that order is extremely important for performance and managing image size.

### Now time for docker-compose.yml.
```
# docker-compose.yml
version: '3.7'

services:
  web:
    build: .
    command: python /code/manage.py runserver 0.0.0.0:8000
    volumes:
      - .:/code
    ports:
      - 8000:8000
```
### At the top we specify we’re using the 3.7 version of Docker Compose and then set up a service, which is running within our container.

### Multiple services can run within a Docker host–for example, we might add a db service for a running PostgreSQL database in the future–but for now we have a single web service.

### We tell it to build the current directory, execute runserver on startup which will start the Django server. Then volumes will sync our local directory to the Docker container. And as a final step we expose port 8000 which is Django’s default so the container will expose it, too.

### Instead of running separate commands to build the image and run the container we can do that with one now. Check this out!
```
$ docker-compose up --build
Creating network "djangoapp_default" with the default driver
Building webStep 1/6 : FROM python:3.7-alpine
...
Successfully built 047a6d848c5b
Successfully tagged djangoapp_web:latest
Recreating djangoapp_web_1 ... done
Attaching to djangoapp_web_1
web_1  | Performing system checks...
web_1  |
web_1  | Watching for file changes with StatReloader
web_1  | System check identified no issues (0 silenced).
web_1  |
web_1  | You have 17 unapplied migration(s). Your project may not work properly until you apply the migrati
ons for app(s): admin, auth, contenttypes, sessions.
web_1  | Run 'python manage.py migrate' to apply them.
web_1  | January 21, 2020 - 14:49:16
web_1  | Django version 3.0, using settings 'example_project.settings'
web_1  | Starting development server at http://0.0.0.0:8000/
web_1  | Quit the server with CONTROL-C.
```
### There will be a lot of output here but if it all worked you can now visit http://127.0.0.1:8000/ in your web browser and see that Django is running entirely within a container now.






# Django for APIs - Library Website
### The most important takeaway is that Django creates websites containing webpages, while Django REST Framework creates web APIs which are a collection of URL endpoints containing available HTTP verbs that return JSON.
### To illustrate these concepts, we will build out a basic Library website with traditional Django and then extend it into a web API with Django REST Framework.
## Traditional Django
### you can read this [Getting Started with Django](../read20/Readme.md)

## Django REST Framework
### Django REST Framework is added just like any other third-party app. On the command line type the below.

```
(library) $ pipenv install djangorestframework~=3.11.0
```
### Or if you are poetry user use this command:
```
(.venv) $ poetry add djangorestframework
```
### Add it to the INSTALLED_APPS config in our settings.py file. I like to make a distinction between third-party apps and local apps as follows since the number of apps grows quickly in most projects.
```python
# config/settings.py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    # 3rd party
    'rest_framework', # new

    # Local
    'books',
]
```
### Ultimately, our API will expose a single endpoint that lists out all books in JSON. So we will need a new URL route, a new view, and a new serializer file (more on this shortly).
### There are multiple ways we can organize these files however my preferred approach is to create a dedicated api app. That way even if we add more apps in the future, each app can contain the models, views, templates, and urls needed for dedicated webpages, but all API-specific files for the entire project will live in a dedicated api app.

### Let’s first create a new api app.
```
(library) $ python manage.py startapp api
```
### Then add it to INSTALLED_APPS.
```python
# config/settings.py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    # 3rd party
    'rest_framework',

    # Local
    'books',
    'api', # new
]
```
### The api app will not have its own database models so there is no need to create a migration file and run migrate to update the database.
## URLs
### Let’s start with our URL configs. Adding an API endpoint is just like configuring a traditional Django app’s routes. First at the project-level we need to include the api app and configure its URL route, which will be api/.
```python
# config/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/', include('api.urls')), # new
    path('', include('books.urls')),
]
```
### Then create a urls.py file within the api app.
```
(library) $ touch api/urls.py
```
### And update it as follows:
```python
# api/urls.py
from django.urls import path
from .views import BookAPIView

urlpatterns = [
    path('', BookAPIView.as_view()),
]
```
## Views
### Next up is our views.py file which relies on Django REST Framework’s built-in generic class views. These deliberately mimic traditional Django’s generic class-based views in format, but they are not the same thing.

### To avoid confusion, some developers will call an API views file apiviews.py or api.py. Personally, when working within a dedicated api app I do not find it confusing to just call a Django REST Framework views file views.py but opinion varies on this point.

### Within our views.py file, update it to look like the following:
```python
# api/views.py
from rest_framework import generics

from books.models import Book
from .serializers import BookSerializer


class BookAPIView(generics.ListAPIView):
    queryset = Book.objects.all()
    serializer_class = BookSerializer

```
### On the top lines we import Django REST Framework’s generics class of views, the models from our books app, and serializers from our api app (we will make the serializers next).

### Then we create a BookAPIView that uses ListAPIView to create a read-only endpoint for all book instances. 

### The only two steps required in our view are to specify the queryset which is all available books, and then the serializer_class which will be BookSerializer.

## A serializer translates data into a format that is easy to consume over the internet, typically JSON, and is displayed at an API endpoint. For now I want to demonstrate how easy it is to create a serializer with Django REST Framework to convert Django models to JSON.

### Make a serializers.py file within our api app.
```
(library) $ touch api/serializers.py
```
### Then update it as follows in a text editor.
```python
# api/serializers.py
from rest_framework import serializers

from books.models import Book


class BookSerializer(serializers.ModelSerializer):
    class Meta:
        model = Book
        fields = ('title', 'subtitle', 'author', 'isbn')

```
### On the top lines we import Django REST Framework’s serializers class and the Book model from our books app. We extend Django REST Framework’s ModelSerializer into a BookSerializer class that specifies our database model Book and the database fields we wish to expose: title, subtitle, author, and isbn.

## cURL
### We want to see what our API endpoint looks like. We know it should return JSON at the URL http://127.0.0.1:8000/api/. Let’s ensure that our local Django server is running:
```
(library) $ python manage.py runserver
```
### Now open a new, second command line console. We will use it to access the API running in the existing command line console.

### We can use the popular cURL program to execute HTTP requests via the command line. All we need for a basic GET request it to specify curl and the URL we want to call.
```
$ curl http://127.0.0.1:8000/api/
[  
   {  
      "title":"Django for Beginners",
      "subtitle":"Build websites with Python and Django",
      "author":"William S. Vincent",
      "isbn":"978-198317266"
   }
]
```
### The data is all there, in JSON format, but it is poorly formatted and hard to make sense of. Fortunately Django REST Framework has a further surprise for us: a powerful visual mode for our API endpoints.

## Browsable API
### With the local server still running in the first command line console, navigate to our API endpoint in the web browser at http://127.0.0.1:8000/api/.
![image](images/Django-rest.PNG)