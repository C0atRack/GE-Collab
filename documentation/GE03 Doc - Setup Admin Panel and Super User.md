## Django Admin Site Setup
##### Written by Kass Ramirez

### 1. Create Models
Before accessing your admin site, you will want to have some models with data fields created already in your `models.py` file.

### 2. Perform Migrations
Django uses an Object-Relational-Mapper (ORM) to map model definitions in the Django code to the data structure used by the underlying database. Django tracks the changes made to model definitions and can create database migration scripts to automatically migrate the underlying data structure in the database to match the model. Django automatically created several admin site models when the website was created as well.

1. Open up your command line terminal (bash or Windows Powershell)
1. Move to your project directory with the `cd` command
1. Run these commands:
```
   python3 manage.py makemigrations
   python3 manage.py migrate
```
4. Run your server with: `python3 manage.py runserver`
5. Open your website here: [http://localhost:8000/](http://localhost:8000/)

![Perform migrations](https://github.com/C0atRack/GE02-Collab/blob/main/images/GE03Doc%20-%20Admin%20Setup/Migrations.png?raw=true)

**Note**: You'll need to run these commands every time your models change in a way that will affect the structure of the data being stored.

### 3. Register models
Open `admin.py` in the catalog application (/django-locallibrary-tutorial/catalog/admin.py). Then insert this code with your own model names into the `admin.py` file:
```
from .models import <myModelClass>

admin.site.register(<myModelClass>)
```
![Register Models](https://github.com/C0atRack/GE02-Collab/blob/main/images/GE03Doc%20-%20Admin%20Setup/RegisterModels.png?raw=true)

### 4. Create a Superuser
To log into the admin site, you need a user account with Staff status enabled and permissions to manage all objects. You can create a superuser with full access to the site using **manage.py**.

1. Go to your project directory in a command terminal
2. Run this command: `python3 manage.py createsuperuser`
   i. You will be prompted for a username, email, and password. Store your password safely and don't forget it.
4. Rerun the server with `python3 manage.py runserver`

### 5. Log in Admin Site
Open your website's admin page here: [http://localhost:8000/admin](http://localhost:8000/admin)

Login using the credentials you just created. You should not see something like this:
![Admin Site](https://github.com/C0atRack/GE02-Collab/blob/main/images/GE03Doc%20-%20Admin%20Setup/AdminSite1.png?raw=true)

This example shows an example registered model called `Students`. You should see the models you created and registered in the same area.

