![pipenv logo](https://i.imgur.com/R1qf6Vw.png "logo text")
---
A Python package manager using virtual environments. It creates virtualenvs in a standard location and automatically adds/removes packages to a Pipfile when they are [un]installed.

# New to virtual environments? :grimacing: (or skip ahead)

## Virtual environment basics
Different projects require different versions of Python and different package versions. A virtual environment is simply a set of modules and a version of Python. We can manage package versions between projects easily by having each project use its own virtual environment.

## Step by step
Imagine you are a developer in a web agency and you have a project(called project1) with an using Python 2.7 and Django 1.11 and want to start another project(project2) with Python 3 and Django 2.0. We can manage both projects concurrently with pipenv. :relaxed:

For this step by step tutorial, we will need to have Python 2, Python 3 and [pipenv](https://github.com/pypa/pipenv#installation) installed. You can also just use Python 3, and replace --two with --three in the instructions.

First, let's open up any shell and create a new folder called 'workshop', and two other folders within it called 'project1' and 'project2'. 

```
$ mkdir workshop
$ cd workshop
$ mkdir project1
$ mkdir project2
```

Let's cd into the project1 folder.

```
$ cd project1
```

Now, let's run `pipenv install django==1.11 --two` to install django into a newly created virtual environment. The `--two` option tells pipenv that we want to use Python 2.

```
$ pipenv install django==1.11 --two
Creating a virtualenv for this project…
Using /usr/local/bin/python2 (2.7.14) to create virtualenv…
⠋Running virtualenv with interpreter /usr/local/bin/python2
New python executable in /Users/yisheng/.virtualenvs/project1-d4NfzhET/bin/python2.7
Also creating executable in /Users/yisheng/.virtualenvs/project1-d4NfzhET/bin/python
Installing setuptools, pip, wheel...done.

Virtualenv location: /Users/yisheng/.virtualenvs/project1-d4NfzhET
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

Several things happened here, so let's go through each of them. The command installed a copy of Python 2.7 (which was already on my machine), together with some basic packages, to a new folder(the virtual environment), and it tells me the location of that folder.

```
Virtualenv location: /Users/yisheng/.virtualenvs/project1-d4NfzhET
```

It's within `.virtualenvs/` in the user folder. The first half of the virtual environment's name is the project folder's name (where we ran `pipenv install django==1.11 --two`). The second half(d4NfzhET) is a string hashed from the project folder's path, so if you delete the virtual environment, and create it again from the same project folder, it will use the same folder name.

The command also created a `Pipfile` for the project, which stores the project's direct dependencies(and Python version). Anyone else working on this project will use the `Pipfile` to install all necessary dependencies.

```
Creating a Pipfile for this project…
```

Next, Django 1.11 was installed in the virtual environment and Pipenv added it to the Pipfile.

Pipenv also created a `Pipfile.lock`, which stores the exact version of the project's direct dependencies and sub-dependencies. On the production machine, we can run `pipenv sync` to install the exact package versions specified by `Pipfile.lock`, so that it will always be safe from breaking updates, even twenty years from now.

Just like that, our virtual environment is all ready to go! :smile: We can continue to do `pipenv install pytest` and it will be installed into the existing virtual environment and added to the `Pipfile` and `Pipfile.lock`.

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

We can automatically check for updates and upgrade our packages with the following workflow:

```
$ pipenv update --outdated
[any outdated packages appear here]
$ pipenv update
```

Do note that packages which have their exact version specified, like our `Django==1.11` will _not_ be updated with `pipenv update`.

Whenever we want to work on the project, we use `$ pipenv shell` anywhere within the project1 folder. This _activates_ the virtual environment, and uses the Python version and packages from the virtual environment only, instead of packages installed globally on our machine. 

```
$ pipenv shell
Spawning environment shell (/bin/zsh). Use 'exit' to leave.
. /Users/yisheng/.virtualenvs/project1-d4NfzhET/bin/activate
...
$
```

We can confirm that the project is using Django 1.11 with `pip show django`.

```
$ pip show django
Name: Django
Version: 1.11
...
$ 
```

Sure enough, we're using Django 1.11. We can run:

```
$ exit
```

to _deactivate_ the virtual environment,

Instead of activating and deactivating the virtual environment, we can also use `pipenv run [command]` to run the command from the virtual environment, like so:

```
$ pipenv run pip show django
```

This can be especially useful for writing shell scripts (or a crontab).

We can easily create the virtual environment for project2 in the same way. We can run:

```
$ cd project2
$ pipenv install django==2.0 --three
```

to setup a new virtual environment with Python 3 and install Django 2.0. 

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
