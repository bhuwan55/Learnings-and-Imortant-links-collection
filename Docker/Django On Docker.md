# Basic Setup For Django Using Docker

### 1. Create a requirements.txt file
**requirements.txt**
```text
Django>=2.1.3,<2.2.0
djangorestframework>=3.9.0,<3.10.0
```

### 2. Create a Dockerfile for creating custom image (Image Setup)

**Dockerfile**

```yml
# pull the python image
FROM python:3.7-alpine
MAINTAINER  suryabhusal

ENV PYTHONUNBUFFERED 1

# COPY [source] [destination]
COPY ./requirements.txt /requirements.txt

# installing the dependencies
RUN pip install --upgrade pip
RUN pip install -r requirements.txt

# create a directory inside the container to store project code
RUN mkdir /app
WORKDIR /app
COPY ./app /app

# for runing the user with development privilages
RUN adduser -D devUser 
USER devUser
```

### 3. Create a docker-compose file

**docker-compose.yml**

```yml
version: "3"

services:
  app:
    build:
      context: .
    ports:
      - "8000:8000"
    volumes:
      - ./app:/app
    command: >
      sh -c "python manage.py migrate && python manage.py runserver 0.0.0.0:8000"
```

### 4. Build a docker custom image
```docker-compose build```

> Image is build using the docker-compose file.

### 5. Create a django project using the service app
``docker-compose run app sh-c "django-admin startproject <project_name>"``

### 6. Run the project
``docker-compose up``
