Role Name
=========

Ansible Role that leverages NSO and Netbox to create and deploy interconnects, both IPv4 and IPv6 to Network Elements

Requirements
------------

Netbox Application with some default configs
NSO package that pushes the config to the devices

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

main.yml, can be overwritten with your own variables

```
netbox_url: http://127.0.0.1:8000
netbox_token: 0123456789abcdef0123456789abcdef01234567

nso_url: http://127.0.0.1:8080/jsonrpc
nso_username: admin
nso_password: admin

site_name: site

interconnect:
  name: A-int-to-Z-int
  prefix_role: interconnects 
  type: 1000BASE-T (1GE)
  device_interfaces:
  - device: Device-1
    intf_number: 0/0/0/0
  - device: Device-2
    intf_number: 0/0/0/0

parent_ipv4_prefix: 172.16.0.128/25
parent_ipv6_prefix: fd00:0:0:1::/64

ipv4_prefix_length: 30
ipv4_prefix_mask: 255.255.255.0
ipv6_prefix_length: 126
```

Dependencies
------------

collections:
  - cisco.nso
  - netbox.netbox

Example Playbook
----------------

```
- name: Create Interconnect
  include_role:
    name: interconnect
  vars:
    netbox_url: "{{ netbox.url }}"
    netbox_token: "{{ netbox.token }}"
    nso_url: "{{ nso.url }}"
    nso_username: "{{ nso.username }}"
    nso_password: "{{ nso.password }}"
    site_name: SDFKY
    interconnect:
      name: P01-PE01-SDFKY
      prefix_role: interconnects 
      type: 1000BASE-T (1GE)
      device_interfaces:
      - device: SDFKYP01
        intf_number: 0/0/0/17
      - device: SDFKYPE01
        intf_number: 0/0/0/23
    parent_ipv4_prefix: "{{ ipv4.core_interconnect }}"
    parent_ipv6_prefix: "{{ ipv6.core_interconnect }}"
```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
