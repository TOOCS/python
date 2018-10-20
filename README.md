[![Build Status](https://travis-ci.org/FlorianKempenich/ansible-role-python-virtualenv.svg?branch=master)](https://travis-ci.org/FlorianKempenich/ansible-role-python-virtualenv) [![Ansible Role](https://img.shields.io/ansible/role/23205.svg)](https://galaxy.ansible.com/FlorianKempenich/python-virtualenv)

# Ansible role: `python-virtualenv`

* Uses `pyenv` to install setup your `python` work environment.
* `pyenv` support multiple paralel versions of `python`, the exact list of `python` versions installed by this role, as well how they are prioritized, is entirely customizable.
* Finally, for each installed version of `python`, `pipenv` is installed to manage the virtual enviroments
* On MacOSX it uninstalls versions of `python` previously installed via `homebrew`.

## Requirements
This role is only working on MacOSX & Ubuntu/Debian.

### Post install: Shell configuration
Since `pyenv` is used to manage the different `python` versions, it needs to be activated in your shell.

**Simply add these lines to the corresponding files:**

* #### `~/.zshrc` / `~/.bashrc`
```
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
```
* #### `~/.zlogin` / `~/.bash_profile`
```
if command -v pyenv 1>/dev/null 2>&1; then
    eval "$(pyenv init -)"
fi
```

The reason we're splitting the initialisation between these two files is to ensure smooth operation with both `pyenv` and `pipenv`. That way, the `pyenv` activation is only done once per login shell and does not interfere with the sub-shell started with `pipenv shell`.  
Learn more about it: [Pyenv Issue #184 - Wrong Python inside of 'pipenv shell'](https://github.com/pypa/pipenv/issues/184#issuecomment-424411432)


## Role Variables
* ### `python_versions`
  * List of python version to install
  * The order in which they are listed will be the order in why they will be prioritized via `pyenv`  
    Learn more about it: [Pyenv - Multiple Global versions](https://github.com/pyenv/pyenv/blob/master/COMMANDS.md#pyenv-global-advanced)
  * **Required**

## Example Playbook
```
- hosts: sandbox
  tasks:
    - include_role:
        name: FlorianKempenich.python-virtualenv
      vars:
        python_versions:
          - 3.7.0
          - 2.7.15
```

## License
MIT

## Author Information
Follow me on Twitter: [@ThisIsFlorianK](https://twitter.com/ThisIsFlorianK)  
Find out more about my work: [Florian Kempenich - Personal Website](https://floriankempenich.com)
