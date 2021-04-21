# Django in Docker

Docker Compose setup for Django/Postgres app. Based on [the tutorial from the Docker documenation](https://docs.docker.com/samples/django/).

## Prerequisites

[Docker and Docker Compose](https://docs.docker.com/get-docker/) are required to be installed in your system.

## Usage

Start your Django project with:

```docker
docker-compose run web django-admin startproject <your_project> .
```

Update `DATABASES` contant in `settings.py` module to point at the Postgres container:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'postgres',
        'USER': 'postgres',
        'PASSWORD': 'postgres',
        'HOST': 'db',
        'PORT': 5432,
    }
}
```

Also update `ALLOWED_HOSTS` contant in `settings.py` module:

```python
ALLOWED_HOSTS = ["*"]
```

Run the containers:

```docker
docker-compose up
```

Open your browser and navigate to `http://0.0.0.0:8000`. If you see the congratulations page then you are all set.

## Troubleshooting

If during the execution of the command `docker-compose up` you see an error like this:

```python
python: can't open file '/code/manage.py': [Errno 2] No such file or directory
```

Then you need to update the path to `manage.py` module in `docker-compose.yml` file:

```
command: python manage.py runserver 0.0.0.0:8000
```
