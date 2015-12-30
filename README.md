# ansible-role-chaperone

[Ansible](https://github.com/ansible/ansible) role for developing,
testing and installing the Chaperone UI (Django) application.

## Requirements

This role currently supports only Debian/Ubuntu distros.

## Role Variables

The following variables are available for overriding, with defaults provided:

```yaml
# The userid to use for rsync'ing the UI and ansible code
# to the UI Deployment server.
rsync_user_id: vmware

# Where to log Django operations
chaperone_log_dir: "/var/log/{{ django_app }}"

# Where to the answerfile should be created by UI 'Save's
chaperone_answer_dir: "/var/lib/{{ django_app }}"

# Where the django UI will look for additional files
chaperone_prepare_files_dir: "/var/lib/{{ django_app }}/prepare"

# Whether to include developer menu items in the UI.
chaperone_developer_menus: false

# Where to log Django operations for the admin UI
chaperone_admin_log_dir: "/var/log/{{ django_admin_app }}"

# Where to the admin answerfile should be created by UI 'Save's
chaperone_admin_answer_dir: "/var/lib/{{ django_admin_app }}"

# Where the django admin UI will look for additional files
chaperone_admin_prepare_files_dir: "/var/lib/{{ django_admin_app }}/prepare"

# Whether to allow debug level in the log files
django_debug: False

# Whether to allow template debug logs
django_template_debug: False

# The log level for the Apache server
apache_loglevel: info

# The port on which to expect vCenter to listen for API calls
vcenter_port: 443

# The full name of the django app (shows up in title UI pagees)
django_fullname: "VMware {{ django_shortname }}"

# The full name of the admin django app (shows up in title UI pagees)
django_admin_fullname: "VMware {{ django_shortname }} Administration"
```

## Example playbook

```yaml
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
