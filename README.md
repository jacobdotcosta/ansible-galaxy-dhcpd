Role Name
=========

Install and configure ISC DHCP service on RH based OS.

This role executes the installation of the ISC DHCP server and then generates a `dhcpd.conf` file with the dhcpd configuration.

Requirements
------------

None.

Role Variables
--------------

Variables direclty provided to the role:

| Variable | Default | Comments |
| --- | --- | --- |
| State | present | **present** installs dhcpd server. **absent** removes dhcpd server. |

Other variables required by the DHCP configuration.

Variables attached to the controller are the following:

```yaml
# Network
ip4_subnet: 192.168.0.0
ip4_netmask: 255.255.255.0
ip4_broadcast: 192.168.0.255
ip4_gateway: 192.168.0.1
ip4_dhcp_range_start: 192.168.0.200
ip4_dhcp_range_finish: 192.168.0.255

dns_server: 192.168.0.1

ntp_server: 0.es.pool.ntp.org

dhcp_domain_search:
  - "example.com"
  - "localdomain"
```

Each host requires the following variables to be added to DHCPD.

Either 1 NIC defined with the following values:

```oracle-sql
my_fqdn: abcd.example.com
my_mac: 00:00:00:00:00:00
my_ipv4: 192.168.0.123
```

Or in case multiple NIC are present:

```yaml
my_nics:
  - nic: eth0
    mac: 00:00:00:00:00:00
    ipv4: 192.168.0.10
    fqdn: host1.example.com
  - nic: eth1
    mac: 00:00:00:00:00:01
    ipv4: 192.168.0.11
    fqdn: host2.example.com
```

Dependencies
------------

None

Example Playbook
----------------

```yaml
- name: DHCP server install and config
  hosts: dhcp
  gather_facts: yes
  roles:
    - role: 'jacobdotcosta.ansible_galaxy_dhcpd'
      tags: [always,dhcpd]
```

License
-------

BSD

Author Information
------------------

Trikora Solutions SL

[url: www.trikorasolutions.com](http://www.trikorasolutions.com/)

[Linkedin - Trikora Solutions](https://www.linkedin.com/company/trikora-solutions-sl/)

[Linkedin - A.C.](linkd.in/ajcin/)

[Twitter - @trikorasolns](https://twitter.com/trikorasolns)
