## Django 4.2 Setup For Windows 10
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
1. To activate in Windows Powershell
     ```
     <venv_directory>\Scripts\Activate.ps1
     ```
1. To activate in cmd.exe
   ```
   <venv_directory>\Scripts\activate.bat
   ```
### Install django in virtual environment

### Upgrade pip

### Create Django project

### Run server

### Confirm Django installation

### Create requirements file

### Deactivating a virtual environment
   
### Deleteing a virtual environment

For more information on setting up a Django venv, see: [Setting up a Django development environment](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/development_environment)  
For more on the specific virtual environment tool suggested by Deb, see: [Python virtualenv](https://python.land/virtual-environments/virtualenv)  

### Troubleshooting
#### Scripts disabled from running on your system
