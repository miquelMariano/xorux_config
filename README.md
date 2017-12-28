Role Name
=========

This role configure a Xorux appliance to monitoring VSP Gx00 arrays

Requirements
------------

miquelMariano.hitachiCCI is required

See Dependencies

Role Variables
--------------

View vars/main.yml

Dependencies
------------

```
ansible-galaxy install miquelMariano.hitachiCCI
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
  vars:
    - firmware_version: 83-04-26
  user: root
  serial: 1
  roles:
   - role: miquelMariano.xorux_config
```

Usage
-------

```
ansible-playbook playbooks/xorux.yml -i inventory/servers -e "servers=xorux-prod update_mode=true"
```

License
-------

BSD

Author Information
------------------

[miquelMariano.github.io](https://miquelmariano.github.io)  | [@miquelMariano](https://twitter.com/miquelMariano)
