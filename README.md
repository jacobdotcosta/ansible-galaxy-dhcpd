Role Name
=========

Install and configure ISC DHCP service.

This role executes the installation of the ISC DHCP server and then generates a `dhcpd.conf` file with the dhcpd configuration.

Requirements
------------

None

Role Variables
--------------

The dhcpd template is generated with information provided by variables.

Conceptually, generic variables should be stored either associated to the dhcpd host or to a more generic group variable file.

```
# Network
ip4_subnet: 192.168.237.0
ip4_netmask: 255.255.255.0
ip4_broadcast: 192.168.237.255
ip4_gateway: 192.168.237.1
ip4_dhcp_range_start: 192.168.237.230
ip4_dhcp_range_finish: 192.168.237.255

dns_server: 192.168.237.1
ntp_server: 0.es.pool.ntp.org
dhcp_domain_search:
  - "domain1.com"
  - "domain2.io"
  - "localdomain"
```

On the other hand, host specific variables such as fqdn, mac and ip address should be stored in each host_vars file.

```oracle-sql
my_fqdn: abcd.domain1.com
my_mac: 00:00:00:00:00:00
my_ipv4: 192.168.237.123
```

The jinja2 template uses these gathered variables.

The `ansible_host` var cannot be used to calculate the *fqdn* because it's always replaced by the host targeted by the ansible role.

Dependencies
------------

None

Example Playbook
----------------

    - name: DHCP server install and config
      hosts: dhcp
      gather_facts: yes
      roles:
        - role: 'ansible-galaxy-dhcpd'
          tags: [always,dhcpd]

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

