eucalyptus-initialize
=====================

Gets all components ready for configuration and the Eucalyptus configuration

** *WARNING !!!* **
*This role has to be used in the deployment of Eucalyptus cloud !*

Requirements
------------

hosts:

- clc | Cloud Controller
- ufs | User Facing Services
- walrus | S3 builtin-backend
- cc | Cluster Controllers
- sc | Storage Controllers
- nc | Node Controllers


Role Variables
--------------

This variable MUST NOT BE CHANGED if you are not an Eucalyptus engineer

| Name | Default | Description | Note
|--- |--- |--- |---
| euca_db_path | /var/lib/eucalyptus/db/data | Eucalyptus CLC Database directory | DO NOT CHANGE
| networking_mode | None | Eucalyptus networking mode | Must be the same for all roles
| use_vlans| true | Eucalyptus using VLANs for instances traffic | None

Dependencies
------------

Before running this role, you will need 

- JohnPreston.eucalyptus-network
- JohnPreston.eucalyptus-setup

** *WARNING !!!* **
* If you run JohnPreston.eucalyptus-network, networking facts of your machines will have changed. Run this role separately in a playbook.*


Example Playbook
----------------

```
##############################################################
#
# Networking has to be configured first in case of any change
#

- hosts: all
  roles:
  - JohnPreston.eucalyptus-network
  - JohnPreston.eucalyptus-setup
  vars:
  - networking_mode: MANAGED
  - use_vlans: false

- hosts: all
  roles:
  - JohnPreston.eucalyptus-initialize
  vars:
  - networking_mode: MANAGED
  - use_vlans: false

```

License
-------

Apache

Author Information
------------------

John Preston [John Mille]
