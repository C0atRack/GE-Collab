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
Create a template with the same name you assigned `template_name` to in the view function. 

**Note:** Generic views look for templates in `/application_name/the_model_name_list.html` within the `/application_name/templates/` directory.

A list view template works the same as any other template. You should extend your base template first and then replace the block content. Below is an example of creating a list of students through the use of `containers`:
```{python}
<!-- inherit from base.html-->
{% extends "portfolio_app/base_template.html" %}


<!-- Replace block content in base_template.html -->
<!-- Use generic class view to display a list view of active students -->
{% block content %}
    <h1>Student List</h1>
    <!-- Template code to process students in list -->
    {% if student_list %}
        <div class="container">
            {% for student in student_list %}
            <div class="row py-2">
                <div class="col-sm-auto">
                    <!-- Get url for current student -->
                    <ul>
                        <li><a href="{{ student.get_absolute_url }}">{{ student.name }}</a></li>
                    </ul>
                </div>
                <div class="col-md-auto">
                    <!-- Button to view current student's portfolio -->
                    <a href="{{ student.get_absolute_url }}" class="btn btn-primary">View</a>
                </div>
            </div>
            {% endfor %}
        </div>            
    {% else %}
        <p>There are no students registered.</p>
    {% endif %}
{% endblock %}
```
