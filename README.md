# ansible-role-supervio

[Ansible](https://github.com/ansible/ansible) role for developing,
testing and installing the SuperVIO UI (Django) application.

## Requirements

This role currently supports only Debian/Ubuntu distros.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    supervio_ui_port: 80

The port on which the SuperVIO UI should listen for inbound (HTTP) requests.

    supervio_allowed_hosts:
      - '*.vmware.local'
      - '*.vmware.com'
      - '*.corp.local'

The hostnames that the UI will serve (it will deny other connections).

    supervio_answer_dir: "/var/lib/supervio"

The directory on which the UI should store the (YAML) answer files for inclusing in various plays.

    supervio_prepare_files_dir: "/var/lib/supervio/prepare"

The directory in which files for preparing (see the Prepare menu) systems should exist.

    supervio_log_dir: "/var/log/supervio"

The directory into which the UI should log operations. Note that the logs are read via
AJAX callbacks for disploy in various UI pages.

    supervio_django_app: "supervio"

The name for the application.

    spuervi_download_files: false

Whether to download ova and depot files and make them available at
http://<supervio-ui>/downloads. These are large and can take a very
long time to pull.

## Example playbook

```
---
- hosts: supervio-ui
  sudo: yes
  roles:
    - pip
    - apache
    - supervio
  vars:
    supervio_django_debug: "True"
    #supervio_vcenter_port: 11443
  vars_files:
    - vars/ui.yml

```

## License

TBD

## Author Information

This role was created in 2015 by [Jacob Cherkas and Tom Hite / VMware](http://www.vmware.com/).
