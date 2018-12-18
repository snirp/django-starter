# Django starter templates with a choice of authentication
This is a collection of mildly opinionated Django starter templates. The main goal is to get started quickly in common cases and avoid repetition or bad practices during setup. With this I am able to address some personal gripes. Not everyone may share these and it's open to discussion what exeactly represents "best practice". 

You can check out a specific branch to start with the authentication method you prefer.

## Features

+ A basic custom user model `users.models.User` that inherits from `AbstractBaseUser`
+ Easy choice between `username`, `email` or `username_email` authentication methods
+ Fully compatible with `allauth` views and templates for account management
+ Emails sent in the development phase are intercepted and sent to an address you choose

## Installed libraries:

+ django-debug-toolbar - [docs](https://django-debug-toolbar.readthedocs.io)
+ django-extensions - [docs](https://django-extensions.readthedocs.io)
+ psycopg2 - [docs](http://initd.org/psycopg/docs/)
+ django-allauth - [docs](https://django-allauth.readthedocs.io)
+ django-email-bandit - [docs](https://django-email-bandit.readthedocs.io/en/latest/)

## Configuration choices
The following is true about the configuration choices:

+ Default Django folder layout, with the name of the project and the project-folder simply: `project`
+ Confidentional and environment-specific settings are managed in a `.env` file (environmental variables)
+ A `base` settings file is extended with phase-specific settings files (`development`, `production`, etc)
+ The debug-toolbar will only be activated when `DEBUG` is set to `True`
+ Postgres is the default database engine

# Get started
Follow these steps to get started:

## Checkout authentication method
You can checkout one of the following braches, each representing a different authentication method:
+ `auth/username` (authenticate with username) - password has to be entered twice; email address is not required.
+ `auth/email` (authenticate with email address) - users have no username, the email will serve as the username field
+ `auth/mixed` (authenticate with email or username) - both username and email are required

The following commands take care of initializing a git repository, checking out the desired branch into your master and installing the dependencies. You may want to initialize an empty github repository to serve as your remote first. In your empty project folder do:
```
git init
git remote add django-starter git://github.com/snirp/django-starter.git
git fetch --all
git checkout -b master django-starter/<branchname>
git remote rm django-starter
git remote add origin <your/repo/address.git>
```

## Create database

Replace the values of `my_database`, `my_user`, and `my_password` with your own values. 
```
psql
postgres=# CREATE DATABASE my_database;
postgres=# CREATE USER my_user WITH ENCRYPTED PASSWORD 'my_password';
postgres=# GRANT ALL PRIVILEGES ON DATABASE my_database TO my_user;
postgres=# \q
```

## Set environment variables and settings

The triple dotted `...env` file holds a template for your environmental settings. Proceed as follows:

1. Double check that `.gitignore` has a line with `.env`, so git will not track the (confidential) environment settings.
1. Rename from ...env to .env (`mv ...env .env`)
1. Follow the instruction in the file to edit passwords, secret keys and environment-specific settings to suit your environment. The database settings should match the values of the Postgres database you created.

Configure `BANDIT_EMAIL` in `project/settings/development.py` to match your email address to use during development.

## Edit settings, apply migrations and get started

Commit the changes and run the project in a pipenv shell with the variables from `.env`:
```
git add -A
git commit -m "Initial commit, django template from github.com/snirp/django-starter"
git push --set-upstream origin master
pipenv install
pipenv shell
(project)$ python manage.py migrate
(project)$ python manage.py createsuperuser
(project)$ python manage.py runserver
```

You can edit the Site settings in the admin to match your project.

# What's next?
With Allauth, adding OAuth authentication by third party providers is a breeze. Check out their docs to get started.

Other recommended libraries:
+ Django REST Framework
+ ...
