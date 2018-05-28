![pipenv logo](https://i.imgur.com/R1qf6Vw.png "logo text")
---
Python package manager for virtual environments. It creates a virtualenv in a standard location and automatically adds/removes packages to a Pipfile when they are [un]installed.

## Concept
* `Pipfile` becomes the development `requirements.txt`
* `Pipfile.lock` becomes the production `requirements.txt`


## Usage
### Setup new project
| Task          | With virtualenvwrapper | __With pipenv__   |
|---------------|---------------|-------|
| Setup new virtualenv | $ mkvirtualenv [project] | $ pipenv (--three OR --two) |


### Work on project
| Task          | With virtualenvwrapper | __With pipenv__   |
|---------------|---------------|-------|
| Activate the virtualenv | $ workon [project] | $ pipenv shell |
| Deactivate the virtualenv | $ deactivate | $ exit |


### Install all project packages
| Task          | With virtualenvwrapper | __With pipenv__   |
|---------------|---------------|-------|
| Install all packages in a virtualenv | $ pip install -r requirements.txt | $ pipenv install --dev |
| Install non-dev packages in a virtualenv | _not able_ | $ pipenv install |


### Add package
| Task          | With virtualenvwrapper | __With pipenv__   |
|---------------|---------------|-------|
| Install a project dependency | (activated) $ pip install (package) | $ pipenv install (package) |
| Install a project dev dependency | _not able_ | $ pipenv install pytest --dev |
| Install local package | $ pip install (path) | $ pipenv install -e (path) |
* Note: pipenv automatically adds the new package to the Pipfile.


### Remove package
| Task          | With virtualenvwrapper | __With pipenv__   |
|---------------|---------------|-------|
| Remove a project dependency and sub-dependencies | _not able_ | $ pipenv uninstall [package] |
| Remove a project dependency only | (activated) $ pip uninstall (package) | (activated) $ pip uninstall (package) |
| Remove all project dependencies | $ pip uninstall -r requirements.txt -y | $ pipenv uninstall --all
* Note: pipenv automatically removes the removed packages from the Pipfile.


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
