## Unit Testing
#### Kass Ramirez

### Overview
Unit tests test one piece of code independently of other code. They are also the fast type of test you can run on your code. When an assertion fails in a unit test, you will get an `AssertionError`, otherwise the unit test doesn't do anything.

#### Example of a unit test
```
def add_numbers(first, second):
  return first + second

def test_add_numbers():
  assert add_numbers(5, 3) == 8
```

### How to Create a Unit Test
Before creating any unit tests, you need to first set up a testing directory in your project. Do this by:
1. Deleting the tests.py file from your app folder
2. Creating a folder within your app directory entitled "tests"
3. Create 5 files within the tests folder: __init__.py, tests_urls.py, tests_views.py, tests_models.py, tests_forms.py

#### Testing URLs
1. Import the necessary modules with this:
```
from django.test import SimpleTestCase
from django.urls import reverse, resolve
from <your_app> import <your_view_functions>
```   
2. Create class:
```
class TestUrls(SimpleTestCase):

  def test_<name_of_a_url_pattern>_url_resolves(self):
    url = reverse('<url_name>')
    print(resolve(url))
    self.assertEquals(resolve(url).func, <your_view_function_name>)
```
Here is an example of this for the url pattern created for the index view:
![image](https://github.com/C0atRack/GE02-Collab/assets/111933432/aa55038e-9969-4507-bf21-e90d3693ffb3)

You can then test your program in your terminal with this command: `python manage.py test <your_app_name>`
and you should see something like this:
![image](https://github.com/C0atRack/GE02-Collab/assets/111933432/5c5f6954-a800-4598-b28d-a7dd1541c3cf)

3. Copy the function created in step 2 and do the same thing for your other urls

**Note**: 
- For class based views, you will need to use `self.assertEquals(resolve(url).func.view_class, <your_generic_view_function_name>)`
- For urls with 1 parameter, you will need to set your args in the test like so:
`url = reverse('<url_name', args=['1'])` **<-- For an int parameter**
- For urls with multiple parameters, you will need to set your kwargs like so:
`url = reverse('<url_name>', kwargs={'param1': 'value1', 'param2': 'value2'})`

[Video Tutorial for Testing URLs](https://youtu.be/0MrgsYswT1c?si=eAd0i4iaSEcdCQ1w)

### Testing Views
[Video Tutorial for Testing Views](https://youtu.be/hA_VxnxCHbo?si=HDfK0Bj04tHhfEF7)

### Testing Models
[Video Tutorial for Testing Models](https://youtu.be/IKnp2ckuhzg?si=eMAgQvkT2GuvhNiw)

### Testing Forms
[Video Tutorial for Testing Forms](https://youtu.be/zUl-Tf-UEzw?si=YvvivbsCQIHB0LfJ)
