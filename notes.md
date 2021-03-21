start project `django-admin startproject hello_project .` 
migrate: `python manage.py migrate`
run `python manage.py runserver`

create new app `python manage.py startapp pages`
Register (add) new project to `hello_project/settings.py` INSTALLED_APPS
* Add url to `hello_project/urls.py` (do not forget import `include`)
* Add view `ages/views.py`
* Create a `urls.py` file within the pages app and link it
to home_page_view.

run `python manage.py runserver` to check if it's ok

create requirements.txt with ```pip freeze >reuirements.txt```

## time to switch to Docker.
A __Docker image__ is a snapshot (blueprint) in time of what a project contains.
A __Docker container__ is a running instance of an image.


Dockerfile
```
# Pull base image
FROM python:3.7

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Set work directory

WORKDIR /code

# Install dependencies
COPY requirements.txt requirements.txt /code/
RUN pip3 install -r requirements.txt

# Copy project
COPY . /code/
```
$ docker build .

create a docker-compose.yml file to control how to run the container that will be built based upon our Dockerfile image.

$ touch docker-compose.yml

```
version: '3.7'

services:
  web:
    build: .
    command: python code/hello/manage.py runserver 0.0.0.0:8000
    volumes:
      - .:/code
    ports:
      - 8000:8000
```

$ docker-compose up
chech, it works: `http://127.0.0.1:8000/`

to stop current container
Ctrl+ c
docker-compose down

