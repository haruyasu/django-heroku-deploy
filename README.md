# django-heroku-deploy

## requirements-dev.txt

```
Django~=3.2.6
dj-database-url==0.5.0
dj-static==0.0.6
python-decouple==3.3
```

## requirements.txt

```
-r requirements-dev.txt
gunicorn
psycopg2
```

## Procfile

```
web: gunicorn mysite.wsgi --log-file -
```

## runtime.txt

```
python-3.8.7
```

## wsgi.py

```
import os
from dj_static import Cling
from django.core.wsgi import get_wsgi_application

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'mysite.settings')

application = Cling(get_wsgi_application())
```

## settings.py

```
from pathlib import Path
from decouple import config
from dj_database_url import parse as dburl

ALLOWED_HOSTS = ['*']

default_dburl = 'sqlite:///' + str(BASE_DIR / "db.sqlite3")

DATABASES = {
    'default': config('DATABASE_URL', default=default_dburl, cast=dburl),
}

STATIC_URL = '/static/'
STATIC_ROOT = str(BASE_DIR / 'staticfiles')
```

## heroku.com

Create new app

## terminal

```
heroku login
heroku plugins:install heroku-config
heroku git:remote -a django--deploy
heroku config:push
↑.envの内容が反映される
git push heroku main
heroku run python3 manage.py migrate
heroku run python3 manage.py createsuperuser
```
