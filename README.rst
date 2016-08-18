Syslog-ng role
##############
.. sectnum::

Context
========

A role to use syslog-ng with Ansible.

Playbook example
=====================
::

   syslog_ng_group: root
   syslog_ng_user: root
   syslog_ng_config_version: 3.5
   syslog_ng_config_dir: "/etc/syslog-ng"
   syslog_ng_config_file: "{{ syslog_ng_config_dir }}/syslog-ng.conf"

   syslog_use_dns: 'yes'
   syslog_use_fqdn: 'yes'
   syslog_keep_hostname: 'yes'
   syslog_include: True

   syslog_sources_configuration_udp:
   - syslog_source_name:
   - syslog_udp_ip :
   - syslog_udp_port :
  
   ========= OR
   
   syslog_sources_configuration_tcp:
   - syslog_source_name:
   - syslog_tcp_ip :
   - syslog_tcp_port :
   - syslog_tcp_max_connections :
       
   syslog_destinations: |-
   syslog_filters: |-
   syslog_log: |-

   
