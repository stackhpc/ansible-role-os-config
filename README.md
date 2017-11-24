stackhpc.os-config
==================

[![Build Status](https://www.travis-ci.org/stackhpc/ansible-role-os-config.svg?branch=master)](https://www.travis-ci.org/stackhpc/ansible-role-os-config)

Add openstack client config file to default location of
`/etc/openstack/clouds.yaml`

Requirements
------------

No requirements beyond installing Ansible.

Role Variables
--------------

`os_config_content` is a string that is written out into the config file.
Its often best setting that as an inline vault variable.

Dependencies
------------

There are no requirements for any other Ansible roles.

Example Playbook
----------------

While you probably want to use and inline vault variable, here is a nice
example of using this role in a playbook:

    ---
    - hosts: all
      vars:
        my_cloud_config: |
          ---
          clouds:
            mycloud:
              auth:
                auth_url: http://openstack.example.com:5000
                project_name: p3
                username: user
                password: secretpassword
              region: RegionOne
      roles:
        - { role: stackhpc.os-config, os_config_content: "{{ my_cloud_config }}" }

An easy way to this example is:

.. code-block::

    sudo yum install python-virtualenv libselinux-python

    virtualenv .venv --system-site-packages
    . .venv/bin/activate
    pip install -U pip
    pip install -U ansible

    ansible-galaxy install stackhpc.os-config

    ansible-playbook -i "localhost," -c local test.yml

License
-------

Apache 2

Author Information
------------------

http://www.stackhpc.com
