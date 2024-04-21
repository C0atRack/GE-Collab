## Project Exploration - Media
#### Kass Ramirez

### Overview
Images uploaded by users are different than static images, as they should not be directly uploaded to the database for security reasons. 
Rather, their links should be uploaded to the database to be referenced in your forms later. Forms that allow users to upload images will 
also need to be modified to accept the request.FILES method in addition to the standard request.POST method. This guide will demonstrate 
and explain how to do all of this, step-by-step.

### Add MEDIA_URL to settings.py


### Add MEDIA_ROOT to settings.py


### Add STATICFILES_DIRS


### Modify urls.py


### Add Image Field to Model


### Migrate the Database


### Add Multipart Form-Data Encoding to Form


### Update forms.py


### Add request.FILES to View Function


### Modify Template to Show Image


### Create Image Tag


