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
- cc | Cluster Controllers
- sc | Storage Controllers
- nc | Node Controllers
- walrus | S3 builtin-backend


Role Variables
--------------

This variable MUST NOT BE CHANGED if you are not an Eucalyptus engineer

| Name | Default | Description | Note
|--- |--- |--- |---
| cpu_overcommit | 1 | Defines the factor of overcommitting for Compute nodes | None
| networking_mode | None | Eucalyptus networking mode | Must be the same for all roles
| use_vlans| true | Eucalyptus using VLANs for instances traffic | None
| managed_addrpernet | 32 | Number of IP addresses per security group | MANAGED modes only
| managed_max_vlan | 4096 | Max VLAN TAG usable for Security groups | MANAGED only
| managed_min_vlan | 1 | Min VLAN  TAG usable for Security Groups | MANAGED only
| instance_dns_domain | eucalyptus.internal | Default domain name search for instances | None
| instance_dns_servers | ["8.8.8.8"] | List of DNS Servers for instances | must be IP Addresses
| pub_ips | [""] | List of IP addresses used for public traffic of instances | Can be ranges or single address
| clusters | {} | Object which contains informations about each AZ (1/CC) | Change values to yours
| vlan_routes | [] | List of subnets to be added to the system for a multi-cluster / multi-vlan | Advanced users only


Dependencies
------------

Before running this role, you will need 

- JohnPreston.eucalyptus-network
- JohnPreston.eucalyptus-setup

** *WARNING !!!* **
- * These roles are not in the meta dependencies, therefore they wont be downloaded and installed. *
- * If you run JohnPreston.eucalyptus-network, networking facts of your machines will have changed. Run this role separately in a playbook.*


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
  - cpu_overcommit: 4
  - instance_dns_servers: ["8.8.8.8", "10.1.1.254"]

```

License
-------

Apache

Author Information
------------------

John Preston [John Mille]
