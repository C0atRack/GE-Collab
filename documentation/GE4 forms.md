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
-have a nested class called Meta:  `class Meta:`
-have a model variable that references what model it is derived from: `model = User`
-have a field variable that has a list of all the attributes of the model as strings. The attributes must be identical to the attributes of the model on the model's page but as a string.  `fields =["paramater1", "Parameter2"]

##Creating the HTML 
The HTML file should include the following to make the form work:
```HTML
<form action='' method ="*The METHOD*">
{% csrf_token%}
<table>
</form>
```


##Urls
The urls.py file needs to be updated to include the new path
```python
urlpatterns=[
path('form page/<argument type:passed argument>', views.*views class*, name = "*project name*"),
]
```
