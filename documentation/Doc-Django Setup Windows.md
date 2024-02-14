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
<!--insert image 'Windows Setup Install' here -->
![Windows Setup Install](https://github.com/C0atRack/GE02-Collab/blob/main/images/Windows%20Setup%20Images/Windows%20Setup%20Install.png?raw=true)
### Update pip
Upon using a pip command, you may have received a notice that a new release is available.
<!-- insert image 'Windows setup update' here -->
To update pip, use this command
```
python -m pip install --upgrade pip
```
<!-- insert 'Windows Setup Update 2' here -->
![Windows Setup Update 2](https://github.com/C0atRack/GE02-Collab/blob/main/images/Windows%20Setup%20Images/Windows%20Setup%20Update%202.png?raw=true)
### Create Django project

### Run server

### Confirm Django installation

### Create requirements file

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
