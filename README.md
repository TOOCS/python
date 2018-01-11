[![Build Status](https://travis-ci.org/FlorianKempenich/ansible-role-nvm-node-npm.svg?branch=master)](https://travis-ci.org/FlorianKempenich/ansible-role-nvm-node-npm) [![Ansible Role](https://img.shields.io/ansible/role/23202.svg)](https://galaxy.ansible.com/FlorianKempenich/nvm-node-npm)

# Ansible role: `python-virtualenv`
Install `python` and `python3`, along with `virtualenv` and `virtualenvwrapper` for `python3`.

> **Warning:**  
> To avoid conflicts with virtual environement, this role will UN-INSTALL any existing installation of `virtualenv` and `virtualenvwrapper` for **Python 2**.
> And only install a version for **Python 3**

## Requirements
This role is only working on Ubuntu/Debian & OSX.

For `virtualenvwrapper` to work, do not forget to add these lines to your `.bashrc`/`.zshrc`:
```
mac_os_identifier=Darwin
if [ "$(uname)" '==' $mac_os_identifier ]; then
    export VIRTUALENVWRAPPER_PYTHON=/usr/local/bin/python3
else
    export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
fi

export WORKON_HOME=$HOME/.virtualenvs
export PROJECT_HOME=$HOME/Dev/Python
source /usr/local/bin/virtualenvwrapper.sh
```

See the official documentation of `virtualenvwrapper` for more info: [Shell statup file - official documentation](https://virtualenvwrapper.readthedocs.io/en/latest/install.html#shell-startup-file)


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
Find out more about my work: [Florian Kempenich](https://floriankempenich.com)
