# Ansible Grafana role

A role that installs/updates Grafana on Ubuntu and Debian.

[![Ansible Galaxy](https://shields.io/badge/Ansible_Galaxy-informational?logo=ansible&style=flat-square)](https://galaxy.ansible.com/jfx/system) Ansible Galaxy collection.

## Getting Started

### Requirements

In order to use:

* Minimal Ansible version: 2.10

### Dependencies

*

### Installation

* Download the `jfx.metrics` collection:

```shell
ansible-galaxy collection install jfx.metrics
```

* Then use the role from the collection in the playbook:

example:

```yaml
- hosts: all

  collections:
    - jfx.metrics

  roles:
    - role: grafana
```

## grafana role

A role that install/update [Grafana](https://grafana.com/oss/grafana/) on Ubuntu and Debian Operating Systems.

### grafana role dependencies

*

### grafana role variables

*

### grafana files

* `grafana.ini`:
A default `grafana.ini` configuration file is defined but could be overridden by a `grafana.ini.j2` file located in `{{ playbook_dir }}/templates/` directory.

## Authors

* **FX Soubirou** - *Initial work* - [GitLab repositories](https://gitlab.com/op_so)

## License

This program is free software: you can redistribute it and/or modify it under the terms of the MIT License (MIT). See the [LICENSE](https://opensource.org/licenses/MIT) for details.
