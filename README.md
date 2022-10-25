RKE2
=========

The role will install RKE2 on a couple of pre-existing, pre-configured Linux servers.

Requirements
------------

Pre configured Linux servers.

Role Variables
--------------

The first master node, cant call "home" to port 9345 in order to register.
So in order to distinguish between the initial and other masters, put configuration in the inventory for
your initial master node. inventory/{stage|prod|test}/host_vars/the_hostname.yml

rke2_initial_master: true


Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

Misc
-------

    - name: Run curl command
      ansible.builtin.command:
        cmd: curl -sfL https://get.rke2.io | INSTALL_RKE2_CHANNEL=stable sh -
        creates: https://rpm.rancher.io/public.key

License
-------

BSD

Author Information
------------------

Jostein Martinsen
