# Django Setup on Linux

**This guide requires the use of a Linux terminal.**

## Installing Visual Studio Code

Header over to the [Visual Studio Code](https://code.visualstudio.com/) website and download package for your system. 

- For Ubuntu and other Debian based systems choose the .deb file and install with 

		sudo apt install ./path/to/file/location/code_1.XX.X-XXXX_amd64.deb

	- *Hint: While typing hitting tab will tell bash to try and autocomplete what you were typing. This is very useful in this step when typing the filepath to the deb.*
	- *This also works when typing `code_1.XX.X-XXXX_amd64.deb`. If you type in `code` and hit tab, bash will fill in the rest of the name for you!*

- For RedHat, Fedora, and other RHEL based systems, follow the instructions on the site to install Visual Studio Code.

## Check Installed Python Version

Most stanard Linux distributions come with Python 3 preinstalled. However, since Python 3 is integral to many parts of the operating system, most distributions will not update the version past the patch number. For example as of Feb. 11 2024, Ubuntu 22.04.3 LTS ships with Python 3.10.12. To check which version of Python you have on your system open a terminal and run the following command:

```
python3 --version
```

The result of the command will be in the following form: `Python 3.##.#`
If the version of Python reported is anything but `Python 3.11.X` follow the steps below.

Otherwise, you can jump to [Installing PIP (if missing)](#installing-pip-if-missing)


## Using Python 3.11 using Dev Containers

A method to use Python 3.11 on a system with a different version is to the Dev Containers Extention for Visual Studio Code. Dev Containers utilizes Docker to run a separate Linux system inside of your current distribution. By selecting the proper image you can use a Linux system that comes with Python 3.11 installed for development. Best of all, Dev Containers will appear mostly seamless while using Visual Studio Code and you will be able to use all of the normal Python debugging features.

### Installing Docker (If not already present)

To verify if Docker is installed on your system, try running the following command in a terminal:
```
docker help 
```

If running this command results in a messages stating `Command docker not found`, follow the instructions below. Otherwise, you can skip to [Allow Docker Access from a non-root User](#allow-docker-access-from-a-non-root-user).

Navigate to the [Install Docker Engine](https://docs.docker.com/engine/install/) page. You do not want to use the linke that says `Docker Desktop for XXX`, instead click on your Linux distribution. Then, follow the listed instructions to install Docker. 

### Allow Docker Access from a non-root User

In order for Visual Studio Code to be able to access the Docker Daemon post installation, you must add your user to the `docker` group. To do so run the following command in a terminal.

```
sudo usermod -aG docker $USER
```

Afterwards, reboot to make the changes go into affect. To verify, run `docker run hello-world` in a terminal. If you see a welcome message, you can proceed to the next section. If you get an error stating connection to the docker daemon failed or the like, make sure you user is a member of the `docker` group.

### Install the Dev Containers Extension

1. Open Visual Studio Code
1. Click on **Extensions** tab the left-hand side bar. *The icon looks like a set of blocks*
1. In the search bar type **Dev Containers**
	![Dev Container Extension in Visual Studio Code Extension Tab](https://github.com/C0atRack/GE02-Collab/blob/main/images/Doc-Linux%20DevContainer/Doc-Linux%20DevContainer%2001%20Finding%20Dev%20Container%20Extention.png)
1. Click on the **Dev Containers** option, and then press install.
	![Showing the install button](https://github.com/C0atRack/GE02-Collab/blob/main/images/Doc-Linux%20DevContainer/Doc-Linux%20DevContainer%2002%20Installing%20Dev%20Container%20Extention.png)
	![Showing Dev Containers has now been installed](https://github.com/C0atRack/GE02-Collab/blob/main/images/Doc-Linux%20DevContainer/Doc-Linux%20DevContainer%2003%20Dev%20Container%20Extension%20Installed.png)

### Start a Project with Dev Containers with Python 3.11 Image 

The following steps will guide you on creating a Django project within a Python 3.11 image:

1. Create a folder using your Linux distributions file explorer to house your project.
1. Within Visual Studio Code, click on **File**, then **Open Folder**. Browse to the folder you created previously.
	1. If a prompt appears asking if you trust the code in the folder, click on whichever prompt confirms that you trust the contents.
1. Once the Visual Studio Code has opened, press `Ctrl+Shift+p` to bring up the command pallet. Once open, begin typing in `Dev Containers: Add` into the text box. Once an option that reads **Dev Containers: Add Dev Container Configuration files...** appears, click on it.
	![Opening the command palete](https://github.com/C0atRack/GE02-Collab/blob/main/images/Doc-Linux%20DevContainer/Doc-Linux%20DevContainer%2004%20Command%20Palette.png)
1. Afterwards, hit enter or click the option that says **Add configuration to user data folder**
	![Add Dev Container Configuration Files Prompt](https://github.com/C0atRack/GE02-Collab/blob/main/images/Doc-Linux%20DevContainer/Doc-Linux%20DevContainer%2005%20Add%20Config.png)
1. Type in `Python 3` and select the top option that reads **Python 3 devcontainers**
	![Add Dev Container COnfiguration Files Prompt](https://github.com/C0atRack/GE02-Collab/blob/main/images/Doc-Linux%20DevContainer/Doc-Linux%20DevContainer%2006%20Select%20Python%203.png)
1. You will then be presented with a number of Python versions alongside the version of Debian linux they run under. Click on the option that reads **3.11-bookworm**.
	![Selecting the 3.11-bookworm option](https://github.com/C0atRack/GE02-Collab/blob/main/images/Doc-Linux%20DevContainer/Doc-Linux%20DevContainer%2007%20Select%203_11_bookworm.png)
1. Click **OK** on the **Select Features** menu.
	![Skipping adding any features to the container](https://github.com/C0atRack/GE02-Collab/blob/main/images/Doc-Linux%20DevContainer/Doc-Linux%20DevContainer%2008%20Skip%20Select%20Features.png)
1. Dev Containers has now created the `devcontainer.json` file within a folder called `.devcontainer`. A prompt will appear offering to reopen the folder in Dev Container. Click on the button that says **Reopen in container**. Visual Studio Code will reload.
	![Clicking reopen in container](https://github.com/C0atRack/GE02-Collab/blob/main/images/Doc-Linux%20DevContainer/Doc-Linux%20DevContainer%2009%20Reopen%20in%20Container.png)
1. Open Visual Studio Code reopens, wait for Dev Containers to finish starting up the Docker container. It will take a while to start as it has to pull many Docker images and install extensions to allow for remote debugging.
	![Dev Container waiting for Docker](https://github.com/C0atRack/GE02-Collab/blob/main/images/Doc-Linux%20DevContainer/Doc-Linux%20DevContainer%2010%20Dev%20Container%20Starting.png)
	![Dev Container waiting for Docker](https://github.com/C0atRack/GE02-Collab/blob/main/images/Doc-Linux%20DevContainer/Doc-Linux%20DevContainer%2011%20Dev%20Container%20Started.png)
1. Once you windows looks like the picture below, click on the **+**/**New Terminal Button** at the top of the terminal windows. You will be dropped into a bash shell inside of the container.
	![Open new bash shell](https://github.com/C0atRack/GE02-Collab/blob/main/images/Doc-Linux%20DevContainer/Doc-Linux%20DevContainer%2012%20Open%20New%20Shell.png)
	![Open new bash shell](https://github.com/C0atRack/GE02-Collab/blob/main/images/Doc-Linux%20DevContainer/Doc-Linux%20DevContainer%2013%20New%20Shell.png)
1. (Optionally) You can now check the version of Python using `python3 --version`


Success! You now have a working Python 3.11 environment to develop your Django application in! You can now follow the general steps to setup your Django virtual environment and run your project. Do keep in mind however, you will need to use the terminal **within** Visual Studio Code for these steps, as that is the environment in which Python 3.11 is availible.

## Installing PIP (if missing)

If you are using Python 3.11 within a Dev Container, PIP will automatically be installed.
If you are using your distributions Python interpreter, follow [this guide](https://linuxconfig.org/install-pip-on-linux) from LinuxConfig.org to install pip on your system.


# Sources/Resources
- [Python in a container | Visual Studio Code Documentation](https://code.visualstudio.com/docs/containers/quickstart-python)
- [Developing inside a Container | Visual Studio Code Documentation](https://code.visualstudio.com/docs/devcontainers/containers)