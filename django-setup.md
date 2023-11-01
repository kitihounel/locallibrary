# Django Setup

## Installing Django

Once you've created a virtual environment, and called workon to enter it, you can use pip3 to install Django.

```bash
pip3 install django~=4.2 # check the current stable version when doing this 
```

You can test that Django is installed by running the following command (this just tests that Python can find the Django module):

```bash
python3 -m django --version
```

## Testing Your Installation

We can create a new skeleton site called **firstsite** using the `django-admin` tool as shown below. After creating the site you can navigate into the folder where you will find the main script for managing projects, called `manage.py`.

```bash
cd /path/to/your/projects/folder
django-admin startproject firstsite
cd firstsite
```

We can run the development web server from within this folder using manage.py and the runserver command, as shown below.

```bash
python3 manage.py runserver
```

Once the server is running you can view the site by navigating to the following URL on your local web browser: `http://127.0.0.1:8000`.

## Creating a SubApp

To create an application that will live inside our main project, run the following command. Make sure to run this command from
the same folder as your project's `manage.py`.

```bash
python3 manage.py startapp mysubapp
```
