# Creating Models and Model Manager
By Brett Ford

### Prerequisites
1. Activate the virtual environment
2. Have an active django project already started
3. Activate the server

### Creating Models
To create a new model, you can open the models.py file under your project. This file will hold all of the models you wish to use and any business logic they will use. be sure that Models imports models from django.db.
#### from django.db import models
with this, we can use the built-in features from Django to create each of the models we would like. create a class with the class keyword and be sure it implements the models.Models class to give it the built-in functionality.
#### class Student(models.Model):
The class can now be populated with attributes that you believe it should have. The attributes that you give the class that describes the model will become the columns in the database that Django will create for your project. Many of the atributes you create will become fields for data to be entered into. Atributes that hold text can be created with the CharField function like this. 
#### atribute = models.CharField("An Attribute", max_length=200)
In addition to saving text, the attributes can be used to define relationships between models. 
#### employee = models.OneToOneField( Employee, on_delete=models.CASCADE, primary_key=True)
https://vertabelo.com/blog/one-to-one-relationship-in-database/

