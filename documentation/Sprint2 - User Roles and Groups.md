# User Roles and Groups
There are many ways to control access to features and pages on a web app. 
one of the most powerful and simple is groups. Django has tools for user groups built in which makes using them incredibly easy. 
Groups can be added in the admin app that Django has built in. 

![The groups page in admin](https://github.com/C0atRack/GE02-Collab/blob/main/images/groups/adding%20groups.JPG)
The groups can be checked in several ways, but here is the code to create a decorator that can be used. 
```python
from django.http import HttpResponse
from django.shortcuts import redirect

def allowed_users(allowed_roles=[]):
        def decorator(view_func):
                def wrapper_func(request,*args,**kwargs):
                        print('role',allowed_roles)
                        group= None
                        if request.user.groups.exists():
                                group=request.user.groups.all()[0].name
                        if group in allowed_roles:
                                return view_func(request, *args, **kwargs)
                        else:
                                return HttpResponse('You are not authorized to use this function '+str( request.user.groups.all()[1].name) )
                return wrapper_func
        return decorator
```
By placing this code above a view function, it will check the first role of the current user and prevent that view from being used if the user does not have the correct role. 
```python
login_required(login_url="login")
@allowed_users(allowed_roles=["web-designer"])
def MarkAdded(request, Artwork_id):
    artwork=Artwork.objects.get(pk=Artwork_id)
    artwork.needs_to_be_added=False
    artwork.save()
    return redirect('index')
```
