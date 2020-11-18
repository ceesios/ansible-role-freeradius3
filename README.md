

freeradius
=========

Role that installs and configures freeradius 3 on Ubuntu Bionic. It will remove any unmanaged configuration to ensure a clean setup of freeradius.

This role might need some work for your situation! I will try to add soms functionality when i find the time for it.
Some examples that are not (yet) included in the role and will be cleaned up (deleted).

- proxy config
- trigger config
- templates config
- panic.gdb
- dictionary config
- policy.d

Other stuff that could be better:
- actual cleanup of unmanaged config files
- sites should be templated
- other os releases must be added

The role uses a single dict for configuration. This is so that all defaults will be overridden if you create your own configuration. wich we recommend. Use ansible merge strategy if you would like to configure the role on multiple levels such as the defaults.


Requirements
------------
-

Role Variables
--------------

| var_name | required | default | description |
| -------- | -------- | ------- | ----------- |
| name | yes/no | - | some description |

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in
regards to parameters that may need to be set for other roles, or variables that
are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables
passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: freeradius, x: 42 }

License
-------

See meta/main.yml

Author Information
------------------

See meta/main.yml