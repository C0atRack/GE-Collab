## Django 4.2 Setup For Windows 10 or 11
##### Written by Kass Ramirez

### Python Compatibility
The allowed versions are Python 3.8 to 3.11. Past Django 4.2.8, 3.12 is also supported.  
To install a new version of Python: [Dowload Python Here](https://www.python.org/downloads/)

#### To Check Installed Versions
1. Open Windows Powershell or Command Prompt
1. Enter the following command: `py -3 -V`
     1. Your terminal will display all versions of Python installed within your PATH variable.

The Windows installer incorporates pip3 (the Python package manager) by default. You can list installed packages with the command `py -3 -m pip list`

### Setting up Virtual Environment
1. Within Windows Powershell navigate to your project directory.
1. Create a Python venv with the built-in venv module (Python 3.4 and later)  
     1. Use this command and choose a name for the venv directory: `python -m venv <directory>`  
     1. For older versions, use this set of commands:   
   ```
   pip install virtualenv
   virtualenv [directory]
   ```
### Activating Virtual Environment
When you activate your venv, you are changing your PATH variable so the Scripts directory of your venv is put in front of everything else.
1. To activate in Windows Powershell
     ```
     <venv_directory>\Scripts\Activate.ps1
     ```
1. To activate in cmd.exe
   ```
   <venv_directory>\Scripts\activate.bat
   ```
Upon activating your virtual environment, you should see the name of your virtual environment before the cursor prompt as show below.
<!--insert image 'Windows Setup Activation' here -->
![Windows Setup Activate Venv](https://github.com/C0atRack/GE02-Collab/blob/main/images/Windows%20Setup%20Images/Windows%20Setup%20Activation.png?raw=true)
### Install django in virtual environment
Assuming you are now in your virtual environment, install Django with this command
```
pip install django
```
To specifically install version 4.2, use: 
```
pip install django==4.2
```
<!--insert image 'Windows Setup Install' here -->
![Windows Setup Install](https://github.com/C0atRack/GE02-Collab/blob/main/images/Windows%20Setup%20Images/Windows%20Setup%20Install.png?raw=true)
### Update pip
Upon using a pip command, you may have received a notice that a new release is available.
<!-- insert image 'Windows setup update' here -->
![Windows Setup Update](https://github.com/C0atRack/GE02-Collab/blob/main/images/Windows%20Setup%20Images/Windows%20Setup%20Update.png?raw=true)
To update pip, use this command
```
python -m pip install --upgrade pip
```
<!-- insert 'Windows Setup Update 2' here -->
![Windows Setup Update 2](https://github.com/C0atRack/GE02-Collab/blob/main/images/Windows%20Setup%20Images/Windows%20Setup%20Update%202.png?raw=true)
### Create Django project
To create a Django 4.2 project, use this command. Note "django_project" can be replaced with whatever name you want to give the project.  
```
django-admin startproject django_project
```

You will benefit from reorganizing your directory with this set of commands:
```
mv django_project/manage.py ./
mv django_project/django_project/* django_project
rm -r django_project/django_project/
```
### Run server
To run a server, use this and just ignore the migration warnings: `python manage.py runserver`

### Confirm Django installation
You can confirm that your server is running succesfully by going to [http://localhost:8000/](http://localhost:8000/)
<!-- insert image 'Windows Setup Confirmation' here --> 

### Open Multiple Terminals
To make things easier, open up two more Powershell tabs. One for:
- venv to run commands
- venv starting server and stopping server
- git/gihub commands

For the other tab using venv, you will have to activate the venv again in the terminal.

### Create requirements file
From within your new tab with the virtual environment open, create a requirements file of what is installed.
```
pip freeze > requirements.txt
```
<!-- insert image 'Windows Setup Requirements' here -->

For more info, see: [List installed Python packages](https://note.nkmk.me/en/python-pip-list-freeze/)  

### Manage project in IDE
For this example, we will be using VS Code.
1. Open the project in Visual Studio Code
2. In Visual Studio Code, go to `File -> Open Folder`
3. Select the folder that contains your Django project. 
<!-- insert image 'Windows Setup IDE' here -->

### Deactivating a virtual environment
   
### Deleteing a virtual environment

For more information on setting up a Django venv, see: [Setting up a Django development environment](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/development_environment)  
For more on the specific virtual environment tool suggested by Deb, see: [Python virtualenv](https://python.land/virtual-environments/virtualenv)  

## Troubleshooting
### Scripts disabled from running on your system
![Scripts disabled step #1](https://github.com/C0atRack/GE02-Collab/blob/main/images/Windows%20Setup%20Troubleshooting%201.png?raw=true)  

1. Navigate to [about_Execution_Policies](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.4)  
2. Determine your preferred execution policy. Each has a description on the Microsoft website.
3. Run the Windows Powershell as an Administrator
<!-- Insert image 'Windows Setup Troubleshooting 2' here -->
![Windows Setup troubleshooting 2](https://github.com/C0atRack/GE02-Collab/blob/main/images/Windows%20Setup%20Images/Windows%20Setup%20Troubleshooting%202.png?raw=true)  

4. Set your execution policy with this command:  
   `Set-ExecutionPolicy -ExecutionPolicy <policy_name>`
5. Enter 'y' when prompted
6. Refer back to Activating Virtual Environment
