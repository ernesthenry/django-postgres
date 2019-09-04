# django-postgres

## Getting Started
This tutorial takes you through on how to set up a postgres database for a django application.

## Getting Started

### Prerequisites (Tools used)


* [Python 3.5](https://www.python.org)
* [Django](https://www.djangoproject.com/)
* [Git](https://git-scm.com/)
* [Virtualenv](https://realpython.com/python-virtual-environments-a-primer/)
* [Pip](https://pip.pypa.io/en/stable/installing/)

### Clone the project

```
git clone https://github.com/ernesthenry/django-postgres.git
```

## Installation

### Navigate to the project directory
```
cd project_folder
```


### create a virtual environment:

```
virtualenv venv
```

### Activate the virtual environment:

```
 source venv\bin\activate
```

Once your virtual environment is active, you can install Django with pip . We will also install the psycopg2 package that will allow us to use the database we configured:

```
pip install django psycopg2
```

### Install requirements from the requirements.txt file:

```
pip3 install -r requirements.txt
```

### Navigate to the main project root directory

```
cd myproject
```
### Run the Application:

```
python3  manage.py runserver
```


### Database installation and set up

The following apt commands will get you the packages you need on ubuntu:
```
sudo apt-get update
sudo apt-get install python-pip python-dev libpq-dev postgresql postgresql-contrib
```        
With the installation out of the way, we can move on to create our database and database user

### Create a Database and Database User

During the Postgres installation, an operating system user named postgres was created to correspond to the postgres PostgreSQL administrative user. We need to change to this user to perform administrative tasks:

```
sudo -u postgres psql
```

First, we will create a database for our Django project. We will call our database **myproject**.

```
CREATE DATABASE myproject;
```

Next, we will create a database user which we will use to connect to and interact with the database.

```
CREATE USER myprojectuser WITH PASSWORD 'anypassword';
```

Afterwards, we'll modify a few of the connection parameters for the user we just created. This will speed up database operations.

```
ALTER ROLE myprojectuser SET client_encoding TO 'utf8';
ALTER ROLE myprojectuser SET default_transaction_isolation TO 'read committed';
ALTER ROLE myprojectuser SET timezone TO 'UTC';
```

Then give our database user access rights to the database we created:

```
GRANT ALL PRIVILEGES ON DATABASE myproject TO myprojectuser;
```

### Configure the django database settings

Open the main Django project settings file located within the child project directory:

cd project_folder/myproject/settings.py

Towards the bottom of the file, you will see a DATABASES section that looks like this:

```
. . .
DATABASES = {
'default': {
'ENGINE': 'django.db.backends.sqlite3',
'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
}
}
. . .
```
This is currently configured to use SQLite as a database. We need to change this so that our PostgreSQL database is used instead.
```
. . .
DATABASES = {
'default': {
'ENGINE': 'django.db.backends.postgresql_psycopg2',
'NAME': 'myproject',
'USER': 'myprojectuser',
'PASSWORD': 'anypassword',
'HOST': 'localhost',
'PORT': '',
}
}
. . .
```
Make the changes so that they look like the ones we used when setting up our postgres database.
When you are finished, save and close the file.



## Author of the codebase

> ##### Kato Ernest Henry 