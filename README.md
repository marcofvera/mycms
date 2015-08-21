# mycms
This is docker stack example using docker-compose. Making a Django with Wagtail and Postgresql.

## Prerequisite
It's necessary to install docker and docker-compose to use all this code in your environment.

- Docker: https://docs.docker.com/installation/
- Docker Compose: https://docs.docker.com/compose/install/

## Setup
Clone repo
```
git clone git@github.com:marcofvera/mycms.git
cd mycms
```
### Create new project
If you don't have any code yet you can create a new one (If you already have created skip those steps):
- Build the web container
```
docker-compose build web
```
- Start your database
```
docker-compose up -d db
```
- Create a project
```
docker run -v `pwd`/web:/code --rm mycms_web wagtail start mysite
```
- To verify whether everything is ok look at mysite path inside the web path:
```
ls web/
```
- Change the database settings in `web/mysite/mysite/settings/base.py`
```
From:

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}

To:

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'HOST': 'db',
        'NAME': 'postgres',
        'USER': 'postgres',
        'PASSWORD': 'mypassword',
    }
}
```
- Initialize the data
```
docker-compose run web python manage.py migrate
```
- Create super user
```
docker-compose run web python manage.py createsuperuser
Username (leave blank to use 'root'): admin
Email address:
Password:
Password (again):
Superuser created successfully.
```

### Run

To run the docker stack in background execute:
```
docker-compose up -d
```

Access the admin URL: http://[your-hostname]:8002/admin/login/?next=/admin/
