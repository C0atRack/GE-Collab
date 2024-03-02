# Static File Setup
By Vincent Faragalli

### Pre Requesites:
1. Running Django
2. Working virtual environment with python
3. Completion of Defining URI path and view
4. Working HTML Template

### Step 1
- In the portfolio folder add a new directory/folder named static
- Then create a folder named "images" In that folder 

It should look like the image below

![2](https://github.com/C0atRack/GE02-Collab/assets/105195883/308c9401-efd3-4381-8e39-88fcbf9a05c1)

Next, download the [UCCS Logo](https://brand.uccs.edu/sites/g/files/kjihxj1416/files/inline-images/uccs-signature-email.gif) and save it to the images folder


![3](https://github.com/C0atRack/GE02-Collab/assets/105195883/69875970-8559-401c-9fcb-070417c0e61f)

## Step 2
#### Update the settings.py file in the portfolio_project
At the top of that file add the following code
``` Python
import os

from pathlib import path
```

#### At the bottom of the same settings file add
This will allow the reading and displaying of any gif file in the static directory
The path is to the specific "images" folder that contains the UCCS logo


``` Python
# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/4.2/howto/static-files/

STATIC_URL = 'static/'

STATICFILES_DIRS = [
os.path.join(BASE_DIR, 'static')
]

MEDIA_URL = '/images/'

```

## Step 3
To add the image information to the base template first open the base_template file and add the following above <!DOCTYPEhtml>
``` Python
{% load static %}

<!DOCTYPE html>

```
#### Then replace 

``` Python
<a class="navbar-brand" href="#">Navbar</a>

```
#### With 
``` Python
<img src="{% static 'images/uccs_logo.gif' %}">

```
#### Now run your server and open the [page](http://127.0.0.1:8000) and you should see the UCCS logo 





