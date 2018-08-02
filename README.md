Role Name
=========

This role configure a Xorux appliance to monitoring VSP Gx00 arrays

Install from Ansible Galaxy
------------------------------------

`ansible-galaxy install miquelmariano.xorux_config`

Requirements
------------

miquelMariano.hitachiCCI is required

See Dependencies

Role Variables
--------------

`firmware_version`
Export Tool version must match the SVP firmware version.
```
$ raidqry -l -I300 
  No  Group    Hostname     HORCM_ver   Uid   Serial#   Micro_ver     Cache(MB)
   1    ---   localhost   01-35-03-08     0   471234    83-01-28/00      320000
```

Dependencies
------------

```
ansible-galaxy install miquelmariano.hitachicci
```

Example Playbook
----------------

```yaml
##USAGE
#ansible-playbook playbooks/xorux.yml -i inventory/servers -e "servers=xorux-prod update_mode=true"

#This play is executed when update_mode var is "true" and ensure that role is up to date. By default update var is "false"
- hosts: ansible
  user: root
  tasks:
    - name: Ensure that role are up to date
      command: ansible-galaxy install --force {{ item }}
      with_items:
        - miquelMariano.xorux_config
      when:
        - update_mode | default(False)
      tags: update
      ignore_errors: yes

#Role folder must be exist. If not, the playbook not found role and fails. You shoud make dir manually "mkdir /etc/ansible/my_role"
- name: Xorux appliance configuration
  hosts: "{{ servers }}:!localhost"
  user: root
  serial: 1
  roles:
   - role: miquelMariano.xorux_config
```

Usage
-------

```
ansible-playbook playbooks/xorux.yml -i inventory/servers -e "servers=xorux-prod firmware_version=83-04-26 update_mode=true"
```

License
-------

BSD

Author Information
------------------

[miquelMariano.github.io](https://miquelmariano.github.io)  | [@miquelMariano](https://twitter.com/miquelMariano)
