![pipenv logo](https://i.imgur.com/R1qf6Vw.png "logo text")
---
A python package manager using virtual environments. It creates virtualenvs in a standard location and automatically adds/removes packages to a Pipfile when they are [un]installed.

## Virtual environment basics
Different projects require different versions of python and different package versions. A virtual environment is simply a set of modules and a version of python. We can manage package versions between projects easily by having each project use its own virtual environment.


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
| Remove a project dependency and sub-dependencies | _not able_ | $ pipenv uninstall [package] |
| Remove a project dependency only | (activated) $ pip uninstall (package) | (activated) $ pip uninstall (package) |
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
