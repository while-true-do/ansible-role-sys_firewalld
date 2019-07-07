<!--
name: README.md
description: This file contains important information for the repository.
author: while-true-do.io
contact: hello@while-true-do.io
license: BSD-3-Clause
-->

<!-- github shields -->
[![Github (tag)](https://img.shields.io/github/tag/while-true-do/ansible-role-sys_firewalld.svg)](https://github.com/while-true-do/ansible-role-sys_firewalld/tags)
[![Github (license)](https://img.shields.io/github/license/while-true-do/ansible-role-sys_firewalld.svg)](https://github.com/while-true-do/ansible-role-sys_firewalld/blob/master/LICENSE)
[![Github (issues)](https://img.shields.io/github/issues/while-true-do/ansible-role-sys_firewalld.svg)](https://github.com/while-true-do/ansible-role-sys_firewalld/issues)
[![Github (pull requests)](https://img.shields.io/github/issues-pr/while-true-do/ansible-role-sys_firewalld.svg)](https://github.com/while-true-do/ansible-role-sys_firewalld/pulls)
<!-- travis shields -->
[![Travis (com)](https://img.shields.io/travis/com/while-true-do/ansible-role-sys_firewalld.svg)](https://travis-ci.com/while-true-do/ansible-role-sys_firewalld)
<!-- ansible shields -->
[![Ansible (min. version)](https://img.shields.io/badge/dynamic/yaml.svg?label=Min.%20Ansible%20Version&url=https%3A%2F%2Fraw.githubusercontent.com%2Fwhile-true-do%2Fansible-role-sys_firewalld%2Fmaster%2Fmeta%2Fmain.yml&query=%24.galaxy_info.min_ansible_version&colorB=black)](https://galaxy.ansible.com/while_true_do/sys_firewalld)
[![Ansible (platforms)](https://img.shields.io/badge/dynamic/yaml.svg?label=Supported%20OS&url=https%3A%2F%2Fraw.githubusercontent.com%2Fwhile-true-do%2Fansible-role-sys_firewalld%2Fmaster%2Fmeta%2Fmain.yml&query=galaxy_info.platforms%5B*%5D.name&colorB=black)](https://galaxy.ansible.com/while_true_do/sys_firewalld)
[![Ansible (tags)](https://img.shields.io/badge/dynamic/yaml.svg?label=Galaxy%20Tags&url=https%3A%2F%2Fraw.githubusercontent.com%2Fwhile-true-do%2Fansible-role-sys_firewalld%2Fmaster%2Fmeta%2Fmain.yml&query=%24.galaxy_info.galaxy_tags%5B*%5D&colorB=black)](https://galaxy.ansible.com/while_true_do/sys_firewalld)

# Ansible Role: sys_firewalld

An Ansible role to install and configure firewalld.

## Motivation

[Firewalld](https://firewalld.org/) is the firewall manager for most RedHat
Derivates like Fedora, CentOS or Oracle Linux. Installing and configuring
firewalld is a very common task for most operators.

## Description

This role installs and configures firewalld.

-   install packages
-   start services
-   configure rules like ports, services and interfaces

## Requirements

Used Modules:

-   [Ansible Package Module](https://docs.ansible.com/ansible/latest/modules/package_module.html)
-   [Ansible Service Module](https://docs.ansible.com/ansible/latest/modules/service_module.html)
-   [Ansible Firewalld Module](https://docs.ansible.com/ansible/latest/modules/firewalld_module.html)

## Installation

Install from [Ansible Galaxy](https://galaxy.ansible.com/while_true_do/sys_firewalld)
```
ansible-galaxy install while_true_do.sys_firewalld
```

Install from [Github](https://github.com/while-true-do/ansible-role-sys_firewalld)
```
git clone https://github.com/while-true-do/ansible-role-sys_firewalld.git while_true_do.sys_firewalld
```

## Usage

### Role Variables

```
---
# defaults file for while_true_do.sys_firewalld

## Package Management
wtd_sys_firewalld_package:
  - firewalld
# State can be present|latest|absent
wtd_sys_firewalld_package_state: "present"

## Service Management
wtd_sys_firewalld_service: "firewalld"
# State can be started|stopped
wtd_sys_firewalld_service_state: "started"
wtd_sys_firewalld_service_enabled: true

## Configuration Management
wtd_sys_firewalld_conf: []
# You can specify the rules as shown below.
# State and zone are defaulting and you don't need to define them.
# - State can be enabled|disabled
# - Zone is depending on the zones defined for your system
#
# - service: httpd
#   state: enabled  (defaults to enabled)
#   zone: public    (defaults to public)
#
# - port: 80/tcp
#   state: enabled  (defaults to enabled)
#   zone: public    (defaults to public)
#
# - source: 192.168.0.0/24
#   state: enabled  (defaults to enabled)
#   zone: public    (defaults to public)
#
# - interface: eth0
#   state: enabled  (defaults to enabled)
#   zone: public    (defaults to public)
#
# - masquerade: true
#   state: enabled  (defaults to enabled)
#   zone: public    (defaults to public)
#
# - rich_rule: rule service name="ftp" audit limit value="1/m" accept
#   state: enabled  (defaults to enabled)
#   zone: public    (defaults to public)
```

### Example Playbook

Running Ansible
[Roles](https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html)
can be done in a
[playbook](https://docs.ansible.com/ansible/latest/user_guide/playbooks_intro.html).

#### Simple

```
---
- hosts: all
  roles:
    - role: while_true_do.sys_firewalld
```

#### Configure a server for public web access

```
- hosts: all
  roles:
    - role: while_true_do.sys_firewalld
      wtd_sys_firewalld_conf:
        - service: http
        - service: https
        - service: ssh
          zone: internal

```

## Known Issues

1.  RedHat Testing is currently not possible in public, due to limitations
    in subscriptions.
2.  Some services and features cannot be tested properly, due to limitations
    in docker.
3.  Firewalld and ansible_firewalld are untested for Debian Based Systems

## Testing

Most of the "generic" tests are located in the
[Test Library](https://github.com/while-true-do/test-library).

Ansible specific testing is done with
[Molecule](https://molecule.readthedocs.io/en/stable/).

Infrastructure testing is done with
[testinfra](https://testinfra.readthedocs.io/en/stable/).

Automated testing is done with [Travis CI](https://travis-ci.com/while-true-do).

## Contribute

Thank you so much for considering to contribute. We are very happy, when somebody
is joining the hard work. Please fell free to open
[Bugs, Feature Requests](https://github.com/while-true-do/ansible-role-sys_firewalld/issues)
or [Pull Requests](https://github.com/while-true-do/ansible-role-sys_firewalld/pulls) after
reading the [Contribution Guideline](https://github.com/while-true-do/doc-library/blob/master/docs/CONTRIBUTING.md).

See who has contributed already in the [kudos.txt](./kudos.txt).

## License

This work is licensed under a [BSD-3-Clause License](https://opensource.org/licenses/BSD-3-Clause).

## Contact

-   Site <https://while-true-do.io>
-   Twitter <https://twitter.com/wtd_news>
-   Code <https://github.com/while-true-do>
-   Mail [hello@while-true-do.io](mailto:hello@while-true-do.io)
-   IRC [freenode, #while-true-do](https://webchat.freenode.net/?channels=while-true-do)
-   Telegram <https://t.me/while_true_do>
