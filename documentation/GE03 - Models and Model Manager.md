# Creating Models and Model Manager
By Brett Ford

### Prerequisites
1. Activate the virtual environment
2. Have an active django project already started
3. Activate the server

### Creating Models
Creating a new model has three distinct steps. 
1. Writing the model
2. Adding the model to the admin app
3. Making migrations
To create a new model, you can open the models.py file under your project. This file will hold all of the models you wish to use and any business logic they will use. be sure that Models imports models from django.db.
#### from django.db import models
with this, we can use the built-in features from Django to create each of the models we would like. create a class with the class keyword and be sure it implements the models.Models class to give it the built-in functionality.
#### class Student(models.Model):
The class can now be populated with attributes that you believe it should have. The attributes that you give the class that describes the model will become the columns in the database that Django will create for your project. Many of the atributes you create will become fields for data to be entered into. Atributes that hold text can be created with the CharField function like this. 
#### atribute = models.CharField("An Attribute", max_length=200)
In addition to saving text, the attributes can be used to define relationships between models. 
#### employee = models.OneToOneField( Employee, on_delete=models.CASCADE, primary_key=True)
There are different relationships between models that can be built. to learn more about relationships between models see:
https://vertabelo.com/blog/one-to-one-relationship-in-database/
Once a model has been created, the model must be added to the admin.py file before it will appear as a database. be sure that the admin file imports the correct files.
#### from django.contrib import admin
#### from .models import *
after this, each model must be individually added with code in the admin file. 
#### admin.site.register(My_Model)
Once the model is added to the admin.py file, the user must perform a migration. First a migration file must be made, then it must be migrated. from the command line you can accomplish this with:
'   ./manage.py makemigrations'
'   ./manage.py migrate'
(This should tell Django to create a database table for each of your classes. For more information about migrating in Django see https://www.geeksforgeeks.org/django-basic-app-model-makemigrations-and-migrate/)
### Model Manager
Django has built in functionality to to access the database using the python command line. With this tool an administrator can see what objects they have without needing a scripting language. to access the ptyhon command line use:
'    python manage.py shell
    from portfolio_app.models import project
    project.objects.all()'
