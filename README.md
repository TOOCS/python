[![Build Status](https://travis-ci.org/FlorianKempenich/ansible-role-python-virtualenv.svg?branch=master)](https://travis-ci.org/FlorianKempenich/ansible-role-python-virtualenv) [![Ansible Role](https://img.shields.io/ansible/role/23205.svg)](https://galaxy.ansible.com/FlorianKempenich/python-virtualenv)

# Ansible role: `python-virtualenv`
Installs (if necessary) `python` and `python3`, along with `pipenv` to manage the virtualenvs.

> **Note on default python version:**  
> By default `pipenv` will use the `python` version that `virtualenv` defaults to. This might be inconsistent accross OS.
> 
> To explicitely state the default `python` version to use, set the env variable `PIPENV_DEFAULT_PYTHON_VERSION` in your `~/.bashrc` / `~/.zshrc`.  
> (eg. `export PIPENV_DEFAULT_PYTHON_VERSION=3.7`)
> 
> You can also use one of the following to create a virtualenv with a specific version of `python`:
> * **`pipenv --two`:** Creates a virtual env with the default python 2 version
> * **`pipenv --three`:** Creates a virtual env with the default python 3 version
> * **`pipenv --python X.Y`:**  Creates a virtual env with the specific python version X.Y

## Requirements
This role is only working on Ubuntu/Debian & OSX.

## Role Variables
This playbook will install the latest versions and is not customizable.

## Example Playbook
```
- hosts: sandbox
  roles:
      - FlorianKempenich.python-virtualenv
```

## License
MIT

## Author Information
Follow me on Twitter: [@ThisIsFlorianK](https://twitter.com/ThisIsFlorianK)  
Find out more about my work: [Florian Kempenich - Personal Website](https://floriankempenich.com)
