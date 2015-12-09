# ansible-role-chaperone

[Ansible](https://github.com/ansible/ansible) role for developing,
testing and installing the Chaperone UI (Django) application.

## Requirements

This role currently supports only Debian/Ubuntu distros.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    chaperone_ui_port: 80

The port on which the Chaperone UI should listen for inbound (HTTP) requests.

    chaperone_allowed_hosts:
      - '*.vmware.local'
      - '*.vmware.com'
      - '*.corp.local'

The hostnames that the UI will serve (it will deny other connections).

    chaperone_answer_dir: "/var/lib/{{ chaperone_django_app }}"

The directory on which the UI should store the (YAML) answer files for inclusing in various plays.

    chaperone_prepare_files_dir: "/var/lib/{{ chaperone_django_app }}/prepare"

The directory in which files for preparing (see the Prepare menu) systems should exist.

    chaperone_log_dir: "/var/log/{{ chaperone_django_app }}"

The directory into which the UI should log operations. Note that the logs are read via
AJAX callbacks for disploy in various UI pages.

    django_app: "chaperone"

The name for the application.

    download_files: false

Whether to download ova and depot files and make them available at
http://<{{ django_app }}-ui>/downloads. These are large and can take a very
long time to pull.

## Example playbook

```
---
- hosts: chaperone-ui
  sudo: yes
  roles:
    - pip
    - apache
    - chaperone
  vars:
    chaperone_django_debug: "True"
    #chaperone_vcenter_port: 11443
  vars_files:
    - vars/ui.yml

```

# License and Copyright

Copyright 2015 VMware, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

## Author Information

This role was created in 2015 by [Jacob Cherkas and Tom Hite / VMware](http://www.vmware.com/).
