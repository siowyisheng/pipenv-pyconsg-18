![pipenv logo](https://i.imgur.com/R1qf6Vw.png "logo text")
---
A Python package manager using virtual environments. It creates virtualenvs in a standard location and automatically adds/removes packages to a Pipfile when they are [un]installed.

# New to virtual environments? :grimacing: (or skip ahead)

## Virtual environment basics
Different projects require different versions of Python and different package versions. A virtual environment is simply a set of modules and a version of Python. We can manage package versions between projects easily by having each project use its own virtual environment.

## Step by step
Imagine you are a developer in a web agency and you have a project(called old_project) with an using Python 2.7 and Django 1.11 and want to start another project(new_project) with Python 3 and Django 2.0. We can manage both projects concurrently with pipenv. :relaxed:

First, open up any shell and go into old_project's project folder.

Now, we just run `$ pipenv install django==1.11 --two` to install django into a newly created virtual environment. The `--two` option tells pipenv that we want to use Python 2.

```
$ pipenv install django==1.11 --two
Creating a virtualenv for this project…
Using /usr/local/bin/python2 (2.7.14) to create virtualenv…
⠋Running virtualenv with interpreter /usr/local/bin/python2
New python executable in /Users/yisheng/.virtualenvs/pipenvstuff-d4NfzhET/bin/python2.7
Also creating executable in /Users/yisheng/.virtualenvs/pipenvstuff-d4NfzhET/bin/python
Installing setuptools, pip, wheel...done.

Virtualenv location: /Users/yisheng/.virtualenvs/pipenvstuff-d4NfzhET
Creating a Pipfile for this project…
Installing django==1.11…
...

Adding django==1.11 to Pipfile's [packages]…
Pipfile.lock not found, creating…
Locking [dev-packages] dependencies…
Locking [packages] dependencies…
Updated Pipfile.lock (d5a021)!
Installing dependencies from Pipfile.lock (d5a021)…
...
To activate this project's virtualenv, run the following:
 $ pipenv shell
```

This first installed a copy of Python 2.7 (which was already on my machine), together with some basic packages, to a new folder(the virtual environment), and it tells me the location of that folder. It also created a `Pipfile` for the project, which stores the project's direct dependencies(and Python version). Anyone else working on this project will use the `Pipfile` to install all necessary dependencies.

It also installed the right version of Django, automatically added it to the Pipfile, and also automatically created a `Pipfile.lock`, which stores the exact version of the project's direct dependencies and sub-dependencies. We will use the `Pipfile.lock` to ensure that the production version of the app uses these exact package versions and is safe from any breaking updates.

Just like that, our virtual environment is all ready to go! :smile: We can continue to do `$ pipenv install pytest` and it will be installed into the existing virtual environment, Pipfile and Pipfile.lock.

```
$ pipenv install pytest
Installing pytest…
...
Adding pytest to Pipfile's [packages]…
Pipfile.lock (d5a021) out of date, updating to (fbff64)…
Locking [dev-packages] dependencies…
Locking [packages] dependencies…
Updated Pipfile.lock (fbff64)!
Installing dependencies from Pipfile.lock (fbff64)…
...
$ 
```

Whenever we want to work on the project, we use `$ pipenv shell` anywhere within the old_project's project folder. This _activates_ the virtual environment, and uses the Python version and packages from the virtual environment only, instead of packages installed globally on our machine. 

```
$ pipenv shell
Spawning environment shell (/bin/zsh). Use 'exit' to leave.
. /Users/yisheng/.virtualenvs/pipenvstuff-d4NfzhET/bin/activate
...
$
```

We can confirm that the project is using Django 1.11 with `$ pip show django`.

```
$ pip show django
Name: Django
Version: 1.11
...
$ 
```

Sure enough, we're using Django 1.11. 

We can easily create the virtual environment for new_project in the same way. First, we use `$ exit` to _deactivate_ the virtual environment, and then go into new_project's project folder and use `$ pipenv install django=2.0 --three` to setup a new virtual environment and install Django. 

Now, both your projects have their separate virtual environments and no longer need to share packages or Python versions. :sunglasses:


# Migrating from venv / virtualenvwrapper?

## Replacing the traditional requirements.txt
* `Pipfile` becomes the development `requirements.txt`
* `Pipfile.lock` becomes the production `requirements.txt`


## Usage
### Setup new project or project on new machine
| Task | With virtualenvwrapper | __With pipenv__   |
|---------------|---------------|-------|
| Setup new virtualenv | $ mkvirtualenv [project] | $ pipenv (--three OR --two) |
| Install all packages in a virtualenv | $ pip install -r requirements.txt | $ pipenv install --dev |
| Install non-dev packages in a virtualenv | _not able_ | $ pipenv install |


### Work on project
| Task          | With virtualenvwrapper | __With pipenv__   |
|---------------|---------------|-------|
| Activate the virtualenv | $ workon [project] | $ pipenv shell |
| Deactivate the virtualenv | $ deactivate | $ exit |


### Add or remove package
| Task          | With virtualenvwrapper | __With pipenv__   |
|---------------|---------------|-------|
| Install a project dependency | (activated) $ pip install (package) | $ pipenv install (package) |
| Install a project dev dependency | _not able_ | $ pipenv install pytest --dev |
| Install local package | $ pip install (path) | $ pipenv install -e (path) |
| Remove a project dependency | (activated) $ pip uninstall (package) | $ pipenv uninstall [package] |
| Remove all unused dependencies | _not able_ | $ pipenv clean |
| Remove all project dependencies | $ pip uninstall -r requirements.txt -y | $ pipenv uninstall --all
* Note: pipenv automatically adds or removes the packages from the Pipfile.


### Freeze dependencies for production
| Task          | With virtualenvwrapper | __With pipenv__   |
|---------------|---------------|-------|
| Freeze project dependencies | $ pip freeze > requirements.txt | $ pipenv lock |


### Upgrade project dependencies
| Task          | With virtualenvwrapper | __With pipenv__   |
|---------------|---------------|-------|
| Upgrade project dependencies | _not able_ | $ pipenv update |
| List project outdated dependencies | _not able_ | $ pipenv update --outdated |
| List project direct dependencies | _not able_ | $ pipenv graph |


## Troubleshooting
### Windows
Pipenv fails on Git Bash ([github issue](https://github.com/pypa/pipenv/issues/970)). Instead, use powershell, cmd, cmder or another shell.
