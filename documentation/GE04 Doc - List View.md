## How to Create a List View
#### Written by Kass Ramirez

A list view page displays a list of all requested model instances. 

### Create a Class-Based View
You can define your own view function to query the requested model instances the same way as other view functions. However,
there are class-based generic view functions that already follow Django best practices and implement many commonly desired features, including the list view.

To start, copy the following code into your `views.py` file.
```{python}
from django.views import generic
```

Then you can create a new view class with the following, but replace "YourModel" with the name of the model you want to create a list view for:
```{python}
class YourModelViewList(generic.ListView):
    model = YourModel
```

It will likely be helpful to override some of the default behaviors of the generic view function. Some common examples are demonstrated here:
```{python}
class YourModelListView(generic.ListView):
    model = YourModel
    context_object_name = 'YourModel_list'   # Your own name for the list as a template variable
    queryset = YourModel.objects.filter(title='example') # Get instances of YourModel with titles "example"
    template_name = 'YourModel/your_template_name_list.html'  # Specify your own template name/location
```

### Create a URL Pattern
Now open `/<your_application>/urls.py` and add a new path for your list view. 

In the example code below, a url pattern for a student list view is added.
```{python}
urlpatterns = [
    path('', views.index, name='index'),
    path('students/', views.StudentListView.as_view(), name='students'),
]
```
If index variables are needed in the url pattern, you can include them in the pattern using `<int:pk>` where `int` is the type and `pk` is the variable name. Multiple variables may be used in a url pattern if needed.

**Note:** When using a generic view, you must include `.as_view()` to properly call the function.

### Create List View Template


