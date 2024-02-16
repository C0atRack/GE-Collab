# Define URI path and view
By Vincent Faragalli

### Pre Requesites
1. Django is installed
2. Working virtual environment with python
3. IDE installed -- Recommended Visual Studio Code

Open the portfolio directory and select the django_project/urls.py file to edit it.

*picure of the directory open*

In the Url.py file update the code so that it matches the following. *Need to change to correct code* 

The change is so that it will import the path function from django.urls and also include the URL patterns from porfolio_app.urls
``` Python from django.contrib import admin
from django.urls import path, include
urlpatterns = [
path('admin/', admin.site.urls),
#connect path to portfolio_app urls
path('', include('portfolio_app.urls')),
]
```
Next Update the file portfolio_app/views.py so it matches the following *ALSO NEED TO CHANGE*
``` Python
from django.shortcuts import render
from django.http import HttpResponse
# Create your views here.
def index(request):

# Render the HTML template index.html with the data in the context variable.
   return HttpResponse('home page')

```
Next, Create a new file called urls.py in the portfolio_app directory and add the following code:
``` Python
from django.urls import path
from . import views

urlpatterns = [
#path function defines a url pattern
#'' is empty to represent based path to app
# views.index is the function defined in views.py
# name='index' parameter is to dynamically create url
# example in html <a href="{% url 'index' %}">Home</a>.
path('', views.index, name='index'),
]

```
Next run the server from the virtual envioroment by using the command 'python manage.py runserver'
Now open 	Open http://127.0.0.1:8000  and you should see home page
*ADD LINK TO THE THIING AND ADD PICTURE OF WHAT THE HOMEPAGE SHOULD LOOK LIKE*

#### For the next part of creating an HTML Template
Change the protfolio_app/views.py to the following
``` Python
from django.shortcuts import render
from django.http import HttpResponse
# Create your views here.
def index(request):
# Render index.html
return render( request, 'portfolio_app/index.html')

```
If you try and go back to your local port it will not work. This will be fixed in the HTML Template documentation 
