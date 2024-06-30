#  Docker Kittygram and CI/CD
![workflow](https://github.com/ender0615/kittygram_final/actions/workflows/main.yml/badge.svg?event=push)
### About ⭐

Kittygram is a social network for sharing photos of beloved pets. It is a fully functional project consisting of a Django backend application and a React frontend application.

### Features 🚀

- the project is launched with Docker containers;
- automatic testing for compliance with PEP8;
- if the tests pass successfully, the images are updated on Docker Hub;
- containers are launched on the server from the updated images;
- automation using GitHub Actions on push to the main branch.

### Architecture

![](https://pictures.s3.yandex.net/resources/s2_10_1697630524.png)

Containers:
- kittygram_gateway - gateway
- kittygram_backend - backend
- kittygram_frontend - frontend
- postgres:13.10 - db

Volumes:
- `static` - for storing static files of the backend and frontend containers. Access to this volume should also be available to the gateway container so that Nginx can serve these files.
- `media` - for storing files uploaded by users. Access to this volume should be available to both the backend and gateway containers so that Nginx can serve these files.
- `pg_data` - for storing PostgreSQL data from the db container.

### Technology stack ⚙️

- Python 3.10.2
- Django 3.2.3
- Django REST Framework 3.12.4
- Pytest 6.2.4
- Gunicorn 20.1.0
- Nginx
- PostgreSQL 13.10
- Docker

### Installation 🛠️

1. Download docker-compose.yml from https://github.com/ender0615/kittygram_final/blob/main/docker-compose.yml

2. Create .env file and add environment variables
```
touch .env
```
3. Add environment variables

4. Run Dockercompose
```
sudo docker compose -f docker-compose.yml pull
sudo docker compose -f docker-compose.yml down
sudo docker compose -f docker-compose.yml up -d
```

5. Make migrations and collect static
```
sudo docker compose -f docker-compose.yml exec backend python manage.py migrate
sudo docker compose -f docker-compose.yml exec backend python manage.py collectstatic
sudo docker compose -f docker-compose.yml exec backend cp -r /app/collected_static/. /backend_static/static/ 
```

### Autodeploy with Git Hub Action

Add variables to repository's Secrets:

- `DOCKER_PASSWORD` - Docker Hub password
- `DOCKER_USERNAME` - Docker Hub username
- `HOST` - Server IP
- `SSH_KEY` - SSH-key to access server
- `SSH_PASSPHRASE` - passphrase to access server
- `TELEGRAM_TO` - Telegram user ID
- `TELEGRAM_TOKEN` - Telegram user token
- `USER` - username to access server


### Env variables 🔑

- `POSTGRES_DB` - DB
- `POSTGRES_USER` - username to DB
- `POSTGRES_PASSWORD` - password to DB
- `DB_NAME` - DB name
- `DB_HOST` = db
- `DB_PORT` = 5432
- `SECRET_KEY` - Django key
- `DEBUG` - True/False
- `ALLOWED_HOSTS`

### Authors 👤

- [Ratmir Khashagulgov](https://github.com/ender0615)
- [Igor Shkoda](https://github.com/Port-tf) - reviewer
