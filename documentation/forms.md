# Forms in Django
By Brett Ford

Django has tools that assist in the creation and editing of html forms for web apps.

## Purpose

## How to accomplish it
1. Create the forms pthon file
1. Create a class for each form you want on forms.py
1. write a html script for the form being displayed
1. import the forms classes into the views.py file
1. Add the url to the urls python file

##Creating the model on the forms page
The model should:
-inherit ModelForm
-have a nested class called Meta:  `class Meta:`
-have a model variable that refrences what model it is derived fron: `model = User`
-have a fielsd variable that has a list of all the artibutes of the model as strings. The atributes must be identical to the atributes of the model on the models page but as a string.  `fields =["paramater1","Parameter2"]

##Creating the html 
The html file should include the following to make the form work:
` <form action='' method ="`The METHOD`">`
`{% csrf_token%}`
`<table>`
`</form>`

##Urls
The urls.py file needs to be updated to include the new path
`path('
