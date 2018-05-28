# Pipenv
Package manager for virtual environments
creates a virtualenv in a standard location.
Automatically adds/removes packages to a Pipfile when they are un/installed.


Pipfile
Pipfile.lock
replace requirements.txt

| Task          | With virtualenvwrapper | With pipenv   |
|---------------|---------------|-------|
| Setup new virtual environment | $ mkvirtualenv [project] | $ pipenv (--three|--two) |
| Activate the virtual environment | $ workon [project] | $ pipenv shell |
| Install non-dev packages in a virtual environment | _not able_ | $ pipenv install |
| Install all packages in a virtual environment | $ pip install -r requirements.txt | $ pipenv install --dev |
| Get a list of top-level dependencies | _not able_ | $ pipenv graph |
| Install a project dependency | (activated) $ pip install (package) | (activated) $ pip install (package) |
| Install a project dev dependency | _not able_ | $ pipenv install pytest --dev |
| Remove a project dependency only | (activated) $ pip uninstall  | (activated) $ pip uninstall |
| Remove a project dependency and its sub-dependencies | _not able_ | $ pipenv uninstall [module] |
| Remove all project dependencies | $ pip uninstall -r requirements.txt -y | $ pipenv uninstall --all


$ pipenv graph
$ pipenv install -e
$ pipenv install pytest --dev
$ pipenv uninstall 


## Setup New Virtual Environment
pipenv --three
pipenv --two
pipenv --python 3.6|2.7

pipenv lock
pipenv shell
pipenv freeze

## Install Packages from Pipfile

$ pipenv install
$ pipenv install --dev


Locate the virtualenv:

$ pipenv --venv

Locate the Python interpreter:

$ pipenv --py


## Need
* Update top-level dependencies
* Fix all production dependencies

## Setup


## Basic Usage
### Windows
FAILS on git bash
cmd
powershell
cmder

### Mac

### Linux



## Troubleshooting

