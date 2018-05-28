# Pipenv
Package manager for virtual environments creates a virtualenv in a standard location. It automatically adds/removes packages to a Pipfile when they are un/installed.


## Concept
* `Pipfile` becomes the development `requirements.txt`
* `Pipfile.lock` becomes the production `requirements.txt`


## Need
* Update top-level dependencies
* Fix all production dependencies


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

### Add packages
| Task          | With virtualenvwrapper | __With pipenv__   |
|---------------|---------------|-------|
| Install a project dependency | (activated) $ pip install (package) | (activated) $ pip install (package) |
| Install a project dev dependency | _not able_ | $ pipenv install pytest --dev |
| Install local package | $ pip install (path) | $ pipenv install -e (path) |
Note: pipenv automatically adds the new package to the Pipfile.

### Other tasks
| Task          | With virtualenvwrapper | __With pipenv__   |
|---------------|---------------|-------|
| Get a list of top-level dependencies | _not able_ | $ pipenv graph |
| Remove a project dependency only | (activated) $ pip uninstall  | (activated) $ pip uninstall |
| Remove a project dependency and sub-dependencies | _not able_ | $ pipenv uninstall [module] |
| Remove all project dependencies | $ pip uninstall -r requirements.txt -y | $ pipenv uninstall --all
| Fix project dependencies | $ pip freeze > requirements.txt | $ pipenv lock |


## Other tasks
| Task          | With virtualenvwrapper | With pipenv   |
|---------------|---------------|-------|
| Upgrade project dependencies | _not able_ | $ pipenv update |
| Locate the virtualenv | $ workon [project] | $ pipenv --venv |
| Locate the Python interpreter | _not able_ | $ pipenv --py |
| Install all packages in a virtual environment | $ pip install -r requirements.txt | $ pipenv install --dev |
| Get a list of top-level dependencies | _not able_ | $ pipenv graph |
| Install a project dependency | (activated) $ pip install (package) | (activated) $ pip install (package) |
| Install a project dev dependency | _not able_ | $ pipenv install pytest --dev |
| Remove a project dependency only | (activated) $ pip uninstall  | (activated) $ pip uninstall |
| Remove a project dependency and its sub-dependencies | _not able_ | $ pipenv uninstall [module] |
| Remove all project dependencies | $ pip uninstall -r requirements.txt -y | $ pipenv uninstall --all
| Fix project dependencies | $ pip freeze > requirements.txt | $ pipenv lock |


## Troubleshooting
### Windows
Pipenv fails on Git Bash ([github issue](https://github.com/pypa/pipenv/issues/970)). Instead, use powershell, cmd, cmder or another shell.
