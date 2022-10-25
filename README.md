RKE2
=========

The role will install RKE2 on a couple of pre-existing, pre-configured Linux servers.

Requirements
------------

Pre configured Linux servers in accordance to the RKE2 manual.

Role Variables
--------------

The first master node, cant call "home" to port 9345 in order to register.
So in order to distinguish between the initial and other masters, put configuration in the inventory for
your initial master node. inventory/{stage|prod|test}/host_vars/the_hostname.yml

rke2_initial_master: true


Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.


Example Inventory
------------------

This inventory example, is to show server and agent installation using a stage environment as shown in the inventory example


* inventory/stage/group_vars/k8sServers.yml
* inventory/stage/group_vars/k8sWorkers.yml

```
---

rke2_cluster_group_name: syscl1
rke2_servers_group_name: syscl1_masters
rke2_agents_group_name:  syscl1_workers

# Loadbalancer listening at k8s api port
rke2_api_ip: 192.168.1.100

rke2_cluster_registration_address: cluster1.somedomain.com

# The loadbalancer should listen to this also
rke2_cluster_registration_port: 9345

rke2_additional_sans:
  - "{{ rke2_cluster_registration_address }}"

rke2_token: P4ssw0rd36s5bis7909da5ec4supers3cr3t
```

For only the initial master, its really important to set:

```
rke2_active_server: true
```



Example Playbook
----------------

- name: Install RKE
  hosts: k8sServers, k8sWorkers
  become: True
  gather_facts: True

  roles:
    - rke2

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
