# Forms in Django
By Brett Ford

Django has tools that assist in the creation and editing of HTML forms for web apps.

## Purpose

## How to accomplish it
1. Create the forms python file
1. Create a class for each form you want on forms.py
1. write a html script for the form being displayed
1. import the forms classes into the views.py file
1. Add the URL to the URLs python file

##Creating the model on the forms page
The model should:
-inherit ModelForm
-have a nested class called Meta:  
-have a model variable that references what model it is derived from: ``
-have a field variable that has a list of all the attributes of the model as strings. The attributes must be identical to the attributes of the model on the model's page but as a string.  
```python
class UserForm(ModelForm):
  class Meta:
    model = User
    fields =["paramater1", "Parameter2"]
```
## Creating the HTML 
The HTML file should include the following to make the form work:
```HTML
<form action='' method ="*The METHOD*">
{% csrf_token%}
<table>
</form>
```


## Urls.py
The urls.py file needs to be updated to include the new path. This needs to include the passed argument that will be needed in the form. For instance, to update a user's information, the user primary key needs to be passed. 
```python
urlpatterns=[
path('form page/<argument type:passed argument>', views.*views class*, name = "*project name*"),
]
```
## views.py


## The Views.py
The form is created as a function under the views page. it receives as arguments the request that will be used as well as the key that will connect it to the database. it needs the form as a variable in function and 


