
# Django Unit-testing with Selenium

By Brennan Romero

## Synopsis

While most unit tests verify only back-end code (ex. testing model methods), Selenium can be used to test the front-end of a Django Web app (the portion the client will see and interact with). It is important to make sure that the client will be able to use the website as it is intended. Selenium tests this functionality by opening up a real web browser and performing the expected interactions with the website. 

## Setup

### **NOTE:**

This guide assumes you are using [Firefox](https://www.mozilla.org/en-US/firefox/new/) as your web browser of choice. While Selenium does have support for Chrome and Edge, this guide will not cover how to setup Selenium to use other browsers.

Follow the instructions to download and install Selenium from the following link: [https://selenium-python.readthedocs.io/installation.html](https://selenium-python.readthedocs.io/installation.html)

Make sure to install Selenium version `4.6.0`, as this version will automatically install the web drivers required to control the web browser.

This guide has only been tested under `Alpine Linux v3.19` using Firefox. Your mileage may vary

## Initial Setup

To use Selenium within a Django test, include the following modules at the top of your Python file:
```python
from selenium.webdriver.firefox.webdriver import WebDriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.select import Select
from selenium.webdriver.support.wait import WebDriverWait
from django.contrib.staticfiles.testing import StaticLiveServerTestCase
from django.urls import reverse
```

These modules will include:

- The `WebDriver` needed to control Firefox
- The `By` selection utility (Needed to find )
- The module needed to select an option from a list on forms
- The `WebDriverWait` utility (useful for waiting for a page to load)
- Django's `StaticLiveServerTestCase`, which is needed for the test to start the test web server that will host any static files.
- Django's `reverse` utility, which is great for getting resource paths.

## Adding a `tests` module to you Django App

When Django looks for unit tests to run, it will look for any tests within your Django apps `tests.py` or `tests` Python module. For organization purposes, it is better to create a `tests` Python module inside of your Django app folder.

To do this:

1. If you haven't already, remove the `tests.py` file inside your Django application.
1. Create a new folder called `tests`
1. Inside that folder, create a blank file named `__init__.py`. This is necessary as a folder is not a detectable Python module until this file is present within a directory.

Now that you have a `tests` module, create a new Python file to write you Selenium tests. I would name it something along the lines of `test_integrations.py`. This is the file we will be adding tests to in this guide.

## Test Class Template

When creating a Selenium test, you will want to use the following template:

```python

class ExampleSeleniumTest(StaticLiveServerTestCase):
	# Un-comment if you are using fixtures
    # serialized_rollback = True
    # fixtures = []

    @classmethod
    def setUpClass(cls):
        super().setUpClass()
        # Open up Firefox so Selenium can control it
        cls.selenium = WebDriver()
        # Have Selenium wait up to 10 seconds before erroring out
        cls.selenium.implicitly_wait(10)
    
    @classmethod
    def tearDownClass(cls) -> None:
        cls.selenium.quit()
        super().tearDownClass()
    
    def test_example(self):
    	# Test Code goes here

```

This class will:

- Setup a Selenium WebDriver
- Close the WebDriver when done

Some things of note:

- The `cls` in the setUpClass and tearDownClass are aliases to the more traditional term `self`.
- If you need to perform actions prior to running the test (such as creating Stub data), you can do so within the `setUpClass` method
- If you are using fixtures to preload the database with data or creating any instances of models, you are going to want to uncomment `serialized_rollback = True`. This let's Django know to reset the database once the test has completed.
    - This is very important if you have multiple tests that use different fixtures as without this the test will commonly error out stating the database was unable to add duplicate data.


To add a test, create a method with the prefix `test_` within this class. The `test_` is necessary in order for Django to be able to detect and run the test.

## Using Selenium within a test case

If you used the template above, when Django runs your test case it will bring up a Firefox instance, as well as start hosting its web server.

Inside of a test case, this instance of Firefox can be controlled using `self.selenium`'s WebDriver methods.

### Navigating to your Web App

You can put an address into Firefox's address bar by using the `.get()` method of `self.selenium`. It takes a single argument, which is the url you want to navigate Firefox to.

To navigate to the index page of your web app, use the following code snippet:
```python
self.selenium.get(self.live_server_url)
```

`self.live_server_url` is a attribute inherited by the `StaticLiveServer` class, which as the name suggests contains the URL of the web server that Django is hosting.


### Interacting with the Web App

To interact with elements on your web app, Selenium needs to be able to find them. Once it's found the element, it can perform actions with it, such as clicking it or sending text.

Finding elements is done using `self.selenium.find_element`. It takes in two arguments, a strategy (From the `By` module), and a value.

For example, to find an element with a HTML id of `loginLink`:
```HTML
<a id="loginLink" role="link" class="btn btn-outline-primary me-2" href="{% url 'login' %}">Login</a>
```
can be done with the following code:
```python
self.selenium.find_element(By.ID, "loginLink")
```

`By.ID` is my favorite way of finding elements on a web app, but it does require that you have id's attached to your HTML tags. 

**On Django-created forms, most if not all input elements can be found by id by searching for `id_<fieldname>`.**

*There are other ways of using `find_element`. You can find more information [here](https://www.selenium.dev/documentation/webdriver/elements/finders/).*

Once you have found an element, you can either assign that value to a Python variable, or directly interact with it via a method call.
Some notable methods:

- `.click()` will click on the found element
- `.send_keys(<text>)` will type \<text\> into the website
- `.clear()` will delete the text from text input areas
    - **NOTE** If the element you are working on uses field validators (like in an HTML Form). If you test is erroring out, you may need to instead send `Ctrl + A` and `Delete`:
    ```python
    # Include at the top of your file
    from selenium.webdriver.common.keys import Keys

    # Find the element
    elem = self.selenium.find_element(By.ID, "<id>")
    elem.send_keys(Keys.CONTROL + "a")
    elem.send_keys(Keys.DELETE)

    ```

For example, to find the register account button, add data to the fields, and click submit, here is some sample code:
```python
    def test_signup(self):
        self.selenium.get(self.live_server_url)
        self.selenium.find_element(By.ID, "signupLink").click()
        # Fill in form data
        self.selenium.find_element(By.ID, "id_first_name").send_keys("Hello")
        self.selenium.find_element(By.ID, "id_last_name").send_keys("World")
        email = "world@example.com"
        self.selenium.find_element(By.ID, "id_email").send_keys(email)
        password = "nd2!nklSD@"
        self.selenium.find_element(By.ID, "id_password1").send_keys(password)
        self.selenium.find_element(By.ID, "id_password2").send_keys(password)
        self.selenium.find_element(By.ID, "register_submit").click()
```

### Uploading files

Selenium is not able to interact with the upload-file dialog required to upload a file on a form. Instead what you can do is send the file input element the path to the file you wish to upload. When the form is submitted, the browser will attach the file to the form when it sends it.

Sample code:

```python
fileInput = self.selenium.find_element(By.CSS_SELECTOR, "input[type='file']")
fileInput.send_keys(<path to file>)
```

## Tips for Creating Tests

When creating a test, think about the interactions a user will perform. The goal with Selenium is to mimic these interactions within code and make sure they work as expected.
Lo-Fi mock ups are great for planning how the code will interact with your web app.