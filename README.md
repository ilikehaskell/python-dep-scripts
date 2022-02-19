# python-dep-scripts
Utility scripts for a smooth Python experience with pyenv and Poetry

# Setup
To use these commands, put this in your `.zshrc`
```
eval "$(pyenv init -)"
alias newpyenv='source new-pyenv-script'
alias alpe='source activate-local-pyenv-script'
alias vpoetry='alpe 2>>/dev/null || newpyenv && poetry'
```

Put the `new-pyenv-script` and `activate-local-pyenv-script` files on your `PATH`

# Commands
- `alpe` - **a**ctivate **l**ocal **p**y**e**nv (virtualenv); looks after a .python-version file in the current directory and, if found, activates it; I found that commands with the `local` Python versions to be unstable, so always activating it is a good idea. 

- `newpyenv <name>` - creates a new pyenv-virtualenv with name <name> or, if the parameter is missing, the name of the current directory, then it runs `pyenv local <name>` and `pip update pip setuptools`
  
- `vpoetry` - **v**irtualenv**poetry**; creates a new pyenv virtualenv with the name of the current directory and sets it as local (if there is not already a local virtualenv) and activates the local `pyenv-virtualenv` , after which it runs `poetry` with any arguments you give it.

# A normal workflow
  Without the scripts, if you would setup a Poetry package with pyenv, you would type something like this:
  ```
  mkdir {package-name} && cd {package-name}
  pyenv virtualenv {current-python-version} {package-name}
  pyenv  activate {package-name}
  python3 -m pip install -U pip setuptools
  poetry init
  ```
 
With the scripts from this repo it becomes:
  ```
  mkdir {package-name} && cd {package-name}
  vpoetry init
  ```
  

# Why use pyenv/Poetry?
`pyenv` lets you easily switch between multiple versions of Python. It has the `pyenv-virtualenv` plugin which manages virtual environments across all Python versions. This means that you will have all your virtual environments regardless of Python version in one place - try `pyenv virtualenvs`. The `alpe` and `newpyenv` commands described in the section below are strictly for pyenv use. [Here's a great pyenv resource](https://realpython.com/intro-to-pyenv).

`Poetry` is a great tool for dependency management. It has a much better dependency resolver than pip and also offers a very friendly building and packaging solution for Python packages. It can save you lots of time on [arcane errors](https://youtu.be/QX_Nhu1zhlg?t=192). The problem with it is that it doesn't offer the same virtualenv experience as `pyenv` and you can't access from `pyenv` the virtual environments it creates. To get the best out of Poetry, use it together with pyenv. The `vpoetry` command from the below section streamlines the setup. 

  
