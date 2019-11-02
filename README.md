# DDRPS
A deployment base for Docker, Django, React, and PostgreSQL

## Current software versions (change if needed)

- Docker-compose: 3
- Python: python:3.8.0-buster
- Django: 2.2.6
- Psycopg2-binary: 2.8.4
- Gunicorn: 19.9.0
- Node: 12
- PostgreSQL: 12

## Instructions

1. Make sure the system building the Docker container has the necessary initial dependencies (node/npm, create-react-app, python3, pip3, django, psycopg2-binary, gunicorn)
2. Run `django-admin startproject <project name>` in backend directory
3. Run `create-react-app .` in frontend directory (may need to temporarily remove Dockerfile so npm doesn't complain)
4. In `docker-compose.yml` and `/backend/.env.dev` (or if production, `.env.prod` and `.env.prod.db`), change the default values of the PostgreSQL DB/user/password and django secret key
5. In Django's `/backend/projectname/settings.py`, be sure to change the following entries to this:

        SECRET_KEY = os.environ.get("SECRET_KEY")

        DEBUG = int(os.environ.get("DEBUG", default=0))

        ALLOWED_HOSTS = os.environ.get("DJANGO_ALLOWED_HOSTS").split(" ")

         DATABASES = {
             'default': {
                'ENGINE': 'django.db.backends.postgresql_psycopg2',
                'NAME': os.environ.get("SQL_DATABASE"),
                'USER': os.environ.get("SQL_USER"),
                'PASSWORD': os.environ.get("SQL_PASSWORD"),
                'HOST': os.environ.get("SQL_HOST"),
                'PORT': os.environ.get("SQL_PORT"),
            }
        }

6. Run `docker-compose build` or `docker-compose build -f docker-compose.prod.yml`
7. To start, run `docker-compose up`
8. To stop, run `docker-compose down`, with the optional `-v` argument to erase persistent volumes `node_modules` and `postgres_data`

