# Django DetailView Class

By Brennan R.

## Synopsis 

Django's `DetailView` is a class that simplifies the task of creating detail/information views, such as a project information page. With proper setup, the `DetailView` class can reduce the code needed to create such a view.\

## Creating a `DetailView`

1. In your apps `views.py`, add the following import to the top of your file to import the class:
	```python
	from django.views.generic import DetailView
	```

1. Then, somewhere in `views.py` create a class that inherits from the `DetailView` class. 
	1. A good rule of thumb is to name the class `<ModelName>DetailView`. For example, for a DetailView of a `Project` Model. Within this class, 

	```python
	class ProjectDetailView(DetailView):
	```

1. Within that class, create a member variable called `model`, and set it equal to the model class. For example, for the same `Project` model the DetailView will now look like:

	```python
	class ProjectDetailView(DetailView):
		model = Project
	```
1. Now within your apps `urls.py`, add the new view you created. The general format for adding the path is:

	```
	path('<resource location>/<int:pk>', views.<Name of new detailview>.as_view(), name="________")
	```

	1. When using a `DetailView`, you want to make sure that at the end of the resource path you add `<int:pk>`. This lets `DetailView` know the id of the object model to select for when it comes time to create the template file.

	1. In the instance of the `ProjectDetailView`, this is what should be added to `urls.py`:

		```python
		urlpatterns = [
			#Other paths above
			path('project-detail/<int:pk>', views.ProjectDetailView.as_view(), name="project-detail"),
		]
	```
1. Create a new HTML template within you app's `templates/<app_name>/` and call it `<lowercase name of model>_detail.html`. 
	1. For the `ProjectDetailView` example, the added template should be named `project_detail.html`
	1. For now you can leave this file blank. The next section will talk more about what to put inside this file.

When a client browses to a resource that uses a `DetailView`, the `DetailView` will perform the following actions:

- Using the `pk` argument, it will find the model object with a matching id.
- It will create a new render context, and map `context["object"]` to the previously found object.
- Render the `<model name>_detail.html` template file
- Send the rendered html file to the client.

This means from a developer standpoint, once you setup the `DetailView` all that needs to be done is writing the code in the template file to display the model's information.

## Using a HTML Template for the `DetailView`

As previously stated, when a `DetailView` based resource is browsed to, the view will map `context["object"]` to the requested object. This means within the `<model name>_detail.html`, you can access any field of the model just by doing `{{object.<field name>}}`.

Going back to the Project Model example again, say. the model had a field called `description`. Displaying the description in the template file can be accomplished like so:

```html
<p>{{object.description}}</p>
```

## Adding more items to a `DetailView`'s Template Render Context

By default the `DetailView` only adds the requested object into the template render context. However, if additional information needs to be added, then follow the below steps:

1. Within your detail view class, add a new function called `get_context_data` like shown below.

	```python
	class <ModelName>DetailView(DetailView)
	    def get_context_data(self, **kwargs):
	        context = super().get_context_data(**kwargs)
	        return context
	```
1. Within this function, after `context = super().get_context_data(**kwargs)`, additional key-value pairs can be added to the context. For example:

	```python
	class <ModelName>DetailView(DetailView)
	    def get_context_data(self, **kwargs):
	        context = super().get_context_data(**kwargs)
	        #Add more information to the render context
	        context["new_key"] = "NewValue"
	        return context
	```


### Getting the ID of the currently requested object

If you need to know the ID of the currently requested object in order to perform some database query, the easiest way to access it is via `context["object"].id`. For example:
```python
class PrimaryModelDetailView(DetailView)
    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)
        #Add more information to the render context
        context["OtherObjects"] = OtherModel.objects.all().filter(PrimaryModelID=context["object"].id)
        return context
```

## Resources
- [https://docs.djangoproject.com/en/4.2/ref/class-based-views/generic-display/#detailview](Django 4.2 DetailView Documentation)