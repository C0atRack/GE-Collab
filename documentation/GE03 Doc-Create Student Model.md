# Create Student Model
By Vincent Faragalli

### Pre Requesites
1. Django is installed
2. Working virtual environment with python
3. IDE installed -- Recommended Visual Studio Code
4. Super User Created and Login to Admin Pannel

In the portfolio directry open the models.py and add the following
```Python
class Student(models.Model):

#List of choices for major value in database, human readable name
MAJOR = (
('CSCI-BS', 'BS in Computer Science'),
('CPEN-BS', 'BS in Computer Engineering'),
('BIGD-BI', 'BI in Game Design and Development'),
('BICS-BI', 'BI in Computer Science'),
('BISC-BI', 'BI in Computer Security'),
('CSCI-BA', 'BA in Computer Science'),
('DASE-BS', 'BS in Data Analytics and Systems Engineering')
)
name = models.CharField(max_length=200)
email = models.CharField("UCCS Email", max_length=200)
major = models.CharField(max_length=200, choices=MAJOR, blank = True)
```
##### Next Edit the admin.py file to allow access to the Student class
At the top after import models add the following code:
```Pyhton
from django.urls import reverse
```
Below the email variable change and add the following
```Python
major = models.CharField(max_length=200, choices=MAJOR_CHOICES)

#Define default String to return the name for representing the Model object."
def __str__(self):
return self.name

#Returns the URL to access a particular instance of MyModelName.
#if you define this method then Django will automatically
# add a "View on Site" button to the model's record editing screens in the Admin site
def get_absolute_url(self):
return reverse('student-detail', args=[str(self.id)])
```
##### Re-run the server and the student class should appear
![image](https://github.com/C0atRack/GE02-Collab/assets/105195883/d59d8981-c4e5-4877-b7bb-01f957944940)

##### Now that the student class has been added play around with it and try the following
- Add a student with only a name and email
- Create a student
- Remove an added student
- Add another student and re-fresh the page
- See if the names are appearing in the admin login








