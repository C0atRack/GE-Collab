# Define URI path and view
By Vincent Faragalli

### Pre Requesites
1. Django is installed
2. Working virtual environment with python
3. IDE installed -- Recommended Visual Studio Code

Open the portfolio directory in your IDE

![What the IDE should look like](https://github.com/C0atRack/GE02-Collab/blob/369e3bc160a17e927835ddd78bcba80ec9fdb00b/images/URI/faragalli-dir.png?raw=true)

Select the django_project/urls.py file to edit it and change the Url.py file so that it matches the following. 

``` Python
from django.contrib import admin
from django.urls import path, include
urlpatterns = [
path('admin/', admin.site.urls),
#connect path to portfolio_app urls
path('', include('portfolio_app.urls')),
]
```
The change is so that it will import the path function from django.urls and also include the URL patterns from porfolio_app.urls


Next Update the file portfolio_app/views.py so it matches the following 
``` Python
from django.shortcuts import render
from django.http import HttpResponse
# Create your views here.
def index(request):

# Render the HTML template index.html with the data in the context variable.
   return HttpResponse('home page')

```
Next, Create a new file called urls.py in the portfolio_app directory and add the code below:
This code imports the path and views functions for URL patterns
The path commands define a URL pattern where it will call either the "index" function or the "login" function
The stub function is for the later HTML documentation
``` Python
from django.urls import path
from . import views

urlpatterns = [
 path('', views.index, name="index"),
 #TODO: idk
 path('login', views.stub, name="login"),
]


```
Next run the server from the virtual envioroment by using the command `python manage.py runserver`

Now open http://127.0.0.1:8000 and you should see the home page

![What it looks like if working correctly](https://github.com/C0atRack/GE02-Collab/blob/b9db39a06f21f278a94f2cbed3afb2d4cf447af7/images/URI/website.png)

#### For the next part of creating an HTML Template
Change the protfolio_app/views.py to the following
``` Python
from django.shortcuts import render
from django.http import HttpResponse

def index(request):
# Render index.html
 return render( request, 'portfolio_app/index.html')

def stub(request):
 return render(request, 'portfolio_app/stub.html')
 

```
This is done so that when the web application is opened instead of displaying 'hello world' it goes to an HTML document with the code that will be used for the web application.
If you try and go back to your local port it will not work. This will be fixed in the HTML Template documentation 
