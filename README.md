# for Python 2
Python 2 has no built-in mechanism for virtual environments, we use mkvirtualenv.

To install it, in the default python environment (which means grab a shell, and it's done) run `pip install virtualenv` and also `pip install virtualenvwrapper`.

## Virtualenv short howto
First, have a `$WORKON_HOME` env var. Better put this in your `.bashrc`

    export WORKON_HOME=~/yourpath-to-python-envs

### Useful basic commands
First the super-basics:

- Create an environment: `mkvirtualenv data-analysis`
- List environments: `lsvirtualenv`
- Switch to an environment: `workon data-analysis`
- Search and install packages: `pip search ...` and `pip install ...`
- When in an environment, list packages: `lssitepackages`

### Less basic stuff
It's more about automating:

#### Automatically install package
Add the command to be executed after each `mkvirtualenv` to the appropriate `postmkvirtualenv`:

    echo 'pip install sphinx' >> $WORKON_HOME/postmkvirtualenv

#### Prompt configuration

    function _prompt_pyvenv() {
      if [ -n "${VIRTUAL_ENV}" ]; then
        echo "(`basename ${VIRTUAL_ENV}`)"
      else
        echo '' 
      fi
    }

and set your prompt to be

    PROMPT='%{$fg[green]%}$(_prompt_pyvenv)%{$reset_color%}'
 
I personally like it as right prompt (thank you zsh)

# for Python 3.3 and above
Python 3.3 has a built-in venv (virtualenvs). Let's use it.

## Create a venv
I've create a small custom zsh function called `mkvenv` which does the following:

1. create (using pyvenv) and activate the environment
2. install distribute and pip
3. deactivate and cleanup the setuptools-?.?.?.tar.gz source

Usage:

    mkvenv my-nice-environment

## activate the venv
A custom shell function `acton` (reminiscent of `workon`) activates an environment and sets up the right prompt.

Usage:

    acton my-nice-environment

## provision the env
You can use the ordinary

    pip install ipython

or use the package list I prepared:

    venv-provision data-science

Both of these commands autocomplete, so check for your options
