Role Name
=========

This role configure a Xorux appliance to monitoring VSP Gx00 arrays

Requirements
------------

miquelMariano.hitachiCCI is required

See Dependencies

Role Variables
--------------

Optionaly define {{ SN_VSP1}} and {{ SN_VSP2 }} variables

Dependencies
------------

```
ansible-galaxy install miquelMariano.hitachiCCI
```

Example Playbook
----------------

```yaml
- hosts: ansible
  user: root
  tasks:
     - name: Ensure that role are up to date
       command: ansible-galaxy install --force {{ item }}
       with_items:
          - miquelMariano.hitachiCCI
       when:
          - update_mode | default(False)
       tags: update
       ignore_errors: yes

- hosts: "{{ servers }}"
  user: root
  roles:
    - role: miquelMariano.hitachiCCI
```

Usage
-------

`ansible-playbook playbooks/xorux.yml -i hosts -e "servers=xorux install=true update_mode=true" --tags=install`

License
-------

BSD

Author Information
------------------

[miquelMariano.github.io](https://miquelmariano.github.io)  | [@miquelMariano](https://twitter.com/miquelMariano)
