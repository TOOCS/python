[![Build Status](https://travis-ci.org/TOOCS/python.svg?branch=master)](https://travis-ci.org/TOOCS/python) [![Ansible Role](https://img.shields.io/ansible/role/36196.svg)](https://galaxy.ansible.com/TOOCS/python)


# TOOCS / Ansible Role: `TOOCS.python`
> #### /!\ This role has been renamed - Old name: `FlorianKempenich.python-virtualenv` /!\

* Install multiple versions of python `python` using `asdf` (or `pyenv`)
* Install `pipenv` for all versions
* Optional: Install global pip packages for the default version of python

> ### TOOCS?
> TOOCS - The Opinionated One-Click Setups are a set of tools / ansible roles designed to setup a system in one click. They are a simple, reliable, way to setup a given tool. You can use them as is, or, inspecting their code, as a tutorial to follow step by step.
>
> They are, as their name suggests, opinionated: while they guarantee to setup the given tool in one click, they do **not** guarantee consistency in _how_ they achieve it, new releases might introduce breaking changes.  
> Read the code and make sure you understand what's happening!

## Requirements
This role is only working on MacOSX & Ubuntu/Debian.

## Role Variables
* ### `python_versions`
  * List of python version to install
  * The order in which they are listed will be the order in why they will be prioritized  
    Learn more about it: [List of _versions to install_ is ordered](https://github.com/TOOCS/asdf#for-each-language-the-list-of-versions-to-install-is-also-ordered)
  * **Required**

* ### `global_pip_packages`
  * List of pip packages to install
  * The packages will only be installed for the default version of python (the first in the list)
  * **Default:** `[]`

* ### `installation_method`
  * Valid values: `asdf`, `pyenv`
  * See [Installation Methods](#installation-methods)
  * **Default:** `asdf`

* ### `asdf_skip_shell_setup`
  * Skip the shell setup when installing `asdf`
  * See [Installation Methods](#installation-methods)
  * **Default:** `False`


## Installation Methods
### `asdf`
Prefered and default installation method using the `asdf` version manager

The installation and configuration of `asdf` as well as the python installation is delegated to another TOOCS: [TOOCS.asdf](https://github.com/TOOCS/asdf).

This TOOCS only takes care of installing the optional global pip modules.

#### Post install - with `asdf`: Shell configuration
* **If you are using `zsh`, you're all set!** Your shell has been automatically set up during the installation of `asdf`.

* **If you are NOT using `zsh` some manual setup is required, see:** [TOOCS/asdf - Non `zsh` Users](https://github.com/TOOCS/asdf#non-zsh-users)

* Alternatively, if `asdf` is already setup on your machine, you might want to skip the `asdf` automatic shell setup => Set the variable `asdf_skip_shell_setup` to `True`

---
### `pyenv`
Alternative version using the `pyenv` version manager

#### Post install - with `pyenv`: Shell configuration
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

---

## Example Playbook
```
- hosts: localhost
  tasks:
    - include_role:
        name: TOOCS.python
      vars:
        python_versions:
          - 3.7.0
          - 2.7.15
        global_pip_packages:
          - cheat
          - howdoi
          - ansible-droplet


# OR

- hosts: localhost
  tasks:
    - include_role:
        name: TOOCS.python
      vars:
        python_versions:
          - 3.7.0
        installation_method: asdf
        asdf_skip_shell_setup: True

# OR

- hosts: localhost
  tasks:
    - include_role:
        name: TOOCS.python
      vars:
        python_versions:
          - 3.7.0
        installation_method: pyenv
```

## License
MIT

## Author Information
Follow me on Twitter: [@ThisIsFlorianK](https://twitter.com/ThisIsFlorianK)  
Find out more about my work: [Florian Kempenich - Personal Website](https://floriankempenich.com)
