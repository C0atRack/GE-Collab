# Stub Pages

## Problem Description:

In Django you can use `{% url "<url path name>"}` in a HTML link tag to have Django automatically populate the link. For example if we have the following `urlpattern` setup:

```
urlpatterns = [
    path('', views.index, name="index"),
    path('login', views.login, name="login"),
]
```

And the following snipped from the template HTML in `index.html`:

```
<! Other HTML Code>

	<a class="nav-link" href="{% url 'login' %}?next={{ request.path }}">Login</a>

<! Other HTML Code>
...
```

Rendering this HTML template using `render(request, index.html)` will generate the following HTML:

```
<! Other HTML Code>
	<a class="nav-link" href="/login?next=/">Login</a>
<! Other HTML Code>
```

Notice how the `href="/login` in the above HTML matches the url path defined by `path('login', views.login, name="login")` in `urlpatterns`.
This is a very clever trick that allows you to change the url of a view without having to edit every single instance of the link in a link tag.

The only downside is that this template trick only works when Django can find a url path to substitute it with. If `path('login', views.login, name="login")` was missing, browsing to `/` in a web browser will generate an error very similar to the one below:

![Django fails to find a path with the name "login" to substitute in for `{% url "<url path name>"}`}](https://github.com/C0atRack/GE02-Collab/blob/main/images/Doc%20Issues/Django%20Template%20Render%20Issue.png)

## Solution:

While the ideal solution would be wait until you have created your view and registed it in `urlpatterns`, sometimes you just want to get it working without having everything done. In such a case, using a stub view can be the solution. A stub is essentially a placeholder. It doesn't actually implement the functionality of the thing it's standing in for, but it allows you to test other parts of your project as if it was done.

To create a stub view to an app, perform the following steps:

1. In your app's HTML template folder, add the following file called `stub.html`:
	```
	<body>
    	<h1> Sorry, {{request.path}} isn't availible yet!</h1>
	</body>
	```
*This HTML file will essentially report that the path the client is trying to visit does not yet exist.*

1. In your Django app's `views.py`, add the following view:
	```
	#Catch all for pages not yet done
	def stub(request):
	    #Render the stub.html page
	    return render(request, 'example_app/stub.html')
	```
1. Add the stub view to your `urlpatterns` for any path that you want a placeholder for. In the case of a missing login page:
	```
	urlpatterns = [
    	path('', views.index, name="index"),
    	#Stub page for login view
    	path('login', views.stub, name="login"),
	]
	```
After restarting the Django Web Server you will not longer encounter the error!
![After the fix, the index page renders correctly!](https://github.com/C0atRack/GE02-Collab/blob/main/images/Doc%20Issues/Django%20Template%20Render%20Issue%20Solved.png)