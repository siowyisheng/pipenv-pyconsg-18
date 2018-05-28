# Pipenv
Package manager for virtual environments
creates a virtualenv in a standard location.
Automatically adds/removes packages to a Pipfile when they are un/installed.


Pipfile
Pipfile.lock
replace requirements.txt

| Task          | Old           | New   |
| ------------- |:-------------:| -----:|
| Setup new virtual environment | right-aligned | $1600 |
| Install packages in a virtual environment | centered      |   $12 |
| Get a list of top-level dependencies | are neat      | $ pipenv graph |
| Install a project dependency | are neat      |    $1 |
| Install a project dev dependency | are neat      |    $1 |
| Remove a project dependency | are neat      | $ pipenv uninstall [module] |



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

