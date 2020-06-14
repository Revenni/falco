revenni.falco
=========

Ansible role providing falco+sysdig deployment.

Falco custom rules can be defined in ```templates/falco_rules_local.yaml.j2```.

[![Platforms](http://img.shields.io/badge/platforms-ubuntu-lightgrey.svg?style=flat)](#)
[![Platforms](http://img.shields.io/badge/platforms-debian-lightgrey.svg?style=flat)](#)
[![Licence](https://img.shields.io/badge/Licence-MIT-blue.svg)](https://tldrlegal.com/license/mit-license)

Requirements
------------

* None

Role Variables
--------------

### Generic variables (declared in defaults/main.yml + overridden in vars/main.yml)
* ```falco_rules_files``` (default list, minus k8) - List of rule files
* ```falco_json_output``` (true) - json output - needs to be true for slack integration
* ```falco_json_include_output_property``` (true) - output property

* ```falco_output_rate``` (1) - falco output per second after burst below
* ```falco_output_rate_burst``` (1000) - falso output burst

* ```falco_syslog_output_enabled``` (true) - log to syslog

* ```falco_file_output_enabled``` (false) - output to file
* ```falco_file_output_keepalive``` (false) - keepalive
* ```falco_file_output_filename``` (./events.txt) - filename to store output in

* ```falco_file_stdoutput_enabled``` (true) - output to stdout

* ```falco_webserver_enabled``` (false) - enable webserver for k8 event listening
* ```falco_webserver_listen_port``` (8765) - webserver port
* ```falco_webserver_k8s_audit_endpoint``` (/k8s_audit) - webserver endpoint
* ```falco_webserver_ssl_enabled``` (false) - webserver ssl?
* ```falco_webserver_ssl_cert``` (/etc/falco/falco.pem) - path to ssl cert

* ```falco_slack_enabled``` (false) - enable slack notifications
* ```falco_slack_webhook``` (https://hooks.slack.com/services/...) - slack webhook url

* ```falco_http_output_enabled``` ( false) - http output
* ```falco_http_url``` ( http://some.url) - url for output

[gRPC docs](https://falco.org/docs/grpc/)
* ```falco_grpc_enabled``` (false) - enable grpc
* ```falco_grpc_bind_address``` (127.0.0.1:5600) - bind address
* ```falco_grpc_threadiness``` (8) - threadiness
* ```falco_grpc_private_key``` (/etc/falco/certs/server.key) - private key
* ```falco_grpc_private_cert_chain``` (/etc/falco/certs/server.crt) - certificate chain
* ```falco_grpc_private_root_certs``` (/etc/falco/certs/ca.crt) - root CA
* ```falco_grpc_output_service``` (false) - buffer in memory until read


Dependencies
------------

* None

Example Playbook
----------------

    - hosts: all
      become: true
      roles:
         - { role: revenni.falco, tags: revenni.falco }

License
-------

MIT

Author Information
------------------
* [Vince Hillier](https://revenni.com) | [@email](mailto:vince@revenni.com) | [twitter](https://twitter.com/vincedotca)
