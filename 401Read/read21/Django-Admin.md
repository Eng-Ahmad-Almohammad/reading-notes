# Django-Admin
## Overview
### The Django admin application can use your models to automatically build a site area that you can use to create, view, update, and delete records. This can save you a lot of time during development, making it very easy to test your models and get a feel for whether you have the right data. The admin application can also be useful for managing data in production, depending on the type of website. The Django project recommends it only for internal data management (i.e. just for use by admins, or people internal to your organization), as the model-centric approach is not necessarily the best possible interface for all users, and exposes a lot of unnecessary detail about the models. 

## Registering models 
### As example, we have thess models: Author, Genre, Book, BookInstance 
### Register the models by copying the following text into the bottom of the file. This code imports the models and then calls admin.site.register to register each of them.
```python
from .models import Author, Genre, Book, BookInstance

admin.site.register(Book)
admin.site.register(Author)
admin.site.register(Genre)
admin.site.register(BookInstance)
```

## Creating a superuser
### In order to log into the admin site, we need a user account with Staff status enabled. In order to view and create records we also need this user to have permissions to manage all our objects.  You can create a "superuser" account that has full access to the site and all needed permissions using manage.py.
### Call the following command, in the same directory as manage.py, to create the superuser. You will be prompted to enter a username, email address, and strong password.
```
python3 manage.py createsuperuser
```
### Once this command completes a new superuser will have been added to the database. Now restart the development server so we can test the login:
```
python3 manage.py runserver
```
## Logging in and using the site
### o login to the site, open the /admin URL (e.g. http://127.0.0.1:8000/admin) and enter your new superuser userid and password credentials (you'll be redirected to the login page, and then back to the /admin URL after you've entered your details).

### This part of the site displays all our models, grouped by installed application. You can click on a model name to go to a screen that lists all its associated records, and you can further click on those records to edit them. You can also directly click the Add link next to each model to start creating a record of that type.
