# Syslog-ng Ansible role

[![The MIT License](https://img.shields.io/badge/license-MIT-orange.svg?style=flat-square)](http://opensource.org/licenses/MIT)

This role manages configuration of `syslog-ng` server and makes sure that it's installed.

## Requirements & Dependencies

### Ansible
It was tested on the following versions:
 * 1.9

### Operating systems

Currently the module was only tested on Debian.

### Role variables

 * `syslog_ng_conf_file`: string, the path to `syslog-ng.conf`
 * `syslog_ng_conf_dir`: string, where are the config files
 * `syslog_ng_user`: the owner group of `syslog-ng.conf`
 * `syslog_ng_group`: the owner user of `syslog-ng.conf`
 * `syslog_ng_remote_loggers`: dict of remote centralized loggers servers


Optional:
 * `ca_certificate`: string, the root ca certificate.
 * `ca_private_key`: string, the private key from root ca certificate.
 * `syslog_cert_name`: string, name of certificate used for syslog-ng

Almost all of them has default values in `defaults/main.yml`.


### Mode specific variables

syslog-ng support plaintext and traffic encryption with TLS (SSL). [More info](http://www.syslog-ng.com/doc/v8-stable/tutorials/tls_cert_summary.html)

#### Without Encryption (PlainText)

*Example*:

```yaml
  vars:
    syslog_ng_remote_sources:
      insecure_source:
        ip: "{{ ansible_eth0.ipv4.address }}"
        proto: "tcp"
        port: 514
        log_dir: "/space/log"

        loggers:
          log_auth:
            filter: "facility(auth, authpriv) and not filter(f_debug);"
            log_file: "$HOST/system/$YEAR/$MONTH/$DAY/auth.log"

          log_apache:
            filter: "facility(local6) and not filter(f_debug);"
            log_file: "$HOST/application/$YEAR/$MONTH/$DAY/apache_$PROGRAM.log"
```

#### With SSL Encryption:


Generate And Autosign root CA:

```
  # Generate key for root CA
  openssl genrsa -des3 -out root-ca.key 2048
  # Self sign CA
  openssl req -new -x509 -days 3650 -key root-ca.key -out root-ca.crt
```

*Example*:

```yaml
  vars:
    syslog_ng_remote_sources:
      secure_source:
        ip: "{{ ansible_eth0.ipv4.address }}"
        proto: tls
        port: 10514
        ca_dir:  "{{ syslog_ng_config_dir }}/ssl/ca"
        key_file: "{{ syslog_ng_config_dir }}/ssl/{{ syslog_cert_name }}-key.pem"
        cert_file: "{{ syslog_ng_config_dir }}/ssl/{{ syslog_cert_name }}-crt.pem"
        log_dir: "/space/log"

        loggers:
          log_auth:
            filter: "facility(auth, authpriv) and not filter(f_debug);"
            log_file: "$HOST/system/$YEAR/$MONTH/$DAY/auth.log"

          log_apache:
            filter: "facility(local6) and not filter(f_debug);"
            log_file: "$HOST/application/$YEAR/$MONTH/$DAY/apache_$PROGRAM.log"

    syslog_cert_name: "syslog"
    ca_certificate: "root-ca.pem"
    ca_private_key: "root-ca-key.pem"

    syslog_cert_subj:
      name: 'syslog-example'
      domains: ["{{ ansible_fqdn }}"]
      country: 'FR'
      state: 'France'
      city: 'Paris'
      organization: 'example'
      unit: ''
      email: 'syslog@example.com'
      days: 365
```

### Contribution
If you find a bug, please open an issue on [GitHub](https://github.com/d2si/ansible-syslog-ng/issues).

If you want to hack some features into this role, please open an issue and we will talk about that.


### Authors

`ansible-syslog-ng` role was written by:
- Laurent Bernaille | [e-mail](mailto:laurent.bernaille@gmail.com) | [Twitter](https://twitter.com/lbernail) | [GitHub](https://github.com/lbernail)
- François Gouteroux | [e-mail](mailto:francois.gouteroux@gmail.com) | [Twitter](https://twitter.com/fgouteroux) | [GitHub](https://github.com/fgouteroux)
