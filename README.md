# django-heroku-deploy

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
```
