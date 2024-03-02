# Django Project/App Setup

## Difference between a Django Project and an App

A Django Project is a collection of Django Apps. Django Apps come in the form of Python Modules that you "install" to your Django Project via the projects `INSTALLED_APPS` list defined in `settings.py`.

## Open a Command Line Interface and Activate Your Virtual Environment in your Project Directory

If you have not already, make sure to activate your virtual environment that you have Django installed in. 

1. Open up your operating systems command line interface:
    1. For Windows, open up a Powershell Window or Command Prompt on your machine. 
    1. For Linux, this will be whichever terminal emulator ships with your Linux Distribution. 
        1. If you are using a Dev Container for development, make sure to use the terminal provide by the **Terminal** tab of the Visual Studio Code window. **You must use this terminal for all of the commands below**
1. Using the `cd` command, change your working directory to the folder you created when [Setting up your Virtual Env and Django Install](Link coming soon)
    1. For Windows, remember directories are delimited by a `\`
    1. On Linux, remember directories are delimited by a `/`
1. Activate your virtual environment.
    1. For Windows, follow the instructions in [Doc-Django Setup Windows](https://github.com/C0atRack/GE02-Collab/blob/main/documentation/GE02%20Doc-Django%20Setup%20Windows.md#activating-virtual-environment) document.
    1. If you are on Linux, run `source <venv_directory>/bin/activate`

## Creating a Django Project

To create a Django Project, run the following command below. Feel free to replace `example_project` with any name you would like:

`django-admin startproject example_project`

**This guide will continue to assume your project name is `example_project`. If you have not named your project this, you must replace `example_project` with your projects name in any following steps.**

After running this command, a new folder will be created in your working directory with the name provided in the command. Within this directory will be two items, a folder with the name of the project and a file called `manage.py`.

## *Optional: Reorganize Project Structure*

Feel free to move the contents of the `example_project` folder to the working directory of your project using your file explorer. 

Before Reorganization:

```
Project Folder
└── example_project
    ├── example_project
    └── manage.py
```

After Reorganization:
```
Project Folder
├── example_project
└── manage.py
```

## Test Your Django Project

If you haven't performed the above step, change directory in your terminal to the location of `mangage.py`. Then, run the following command to verify that your Django Project works:

**Ignore any warning about unapplied migrations.**
```
python3 manage.py runserver
```

In a web browser, browse to [http://localhost:8000](http://localhost:8000). If you see the below image, you have successfully started you Django Project!

![Web browser view when Django Project has been launched successfully](https://github.com/C0atRack/GE02-Collab/blob/main/images/Doc%20Django%20Project%20and%20App/01%20Django%20App%20Success.png)

To stop the Django server, go back to the terminal you run the previous command in and hit `Ctrl+c`.

## Adding an App to your Django Project

In this section, we will be adding an app called `example_app` to your Django project. Feel free to call it any other valid Python module name, however keep in mind you will need to replace `example_app` with your app name for the rest of the steps.

1. [Open a CMD/Terminal and activate your virtual environment](#open-a-command-line-interface-and-activate-your-virtual-environment-in-your-project-directory) if you have not already.
1. Change directories using `cd` to the same folder that contains `manage.py`
1. Open your project folder in Visual Studio Code or in the editor of your choice
1. Run the below command to create the `example_app` app.
    ```
    django-admin startapp example_app
    ```
    1. Your app will be contained within a folder called `example_app`. Your project directory should resemble the forms below:
        ```
        If you reorganized your project directory:

        Project Folder/
        ├── example_project/
        ├── example_app/
        └── manage.py


        If you did not reorganize your project directory:

        Project Folder/
        └── example_project/
            ├── example_project/
            ├── example_app/
            └── manage.py
        ```
1. "Install" your app in your Django Project. You do this by adding the name of your application folder to the `INSTALLED_APPS` list in `example_project/settings.py` in quotes:
    ```
    # Application definition
    INSTALLED_APPS = [
        "django.contrib.admin",
        "django.contrib.auth",
        "django.contrib.contenttypes",
        "django.contrib.sessions",
        "django.contrib.messages",
        "django.contrib.staticfiles",
        #Your example_app goes here
        "example_app",
    ]
    ```
 **Make sure you leave a trailing `,` at the end of `"example_app"` so that you can add other apps later.**

Success! You have created a Django App and installed it into your Django Project. To add functionality to your app, such as creating views, urls, and templates, you can follow [Doc - URI paths and View](https://github.com/C0atRack/GE02-Collab/blob/main/documentation/GE02%20Doc-URI%20paths%20and%20View.md).

# Tools Used
- [tree.nathfriend.io](https://tree.nathanfriend.io/) to make the file-path ascii art.
