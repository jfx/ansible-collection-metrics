# Ansible reboot role

A role that install/update Blackbox exporter on Ubuntu and Debian.

[![Ansible Galaxy](https://shields.io/badge/Ansible_Galaxy-informational?logo=ansible&style=flat-square)](https://galaxy.ansible.com/jfx/system) Ansible Galaxy collection.

## Getting Started

### Requirements

In order to use:

* Minimal Ansible version: 2.10

### Dependencies

* `jfx.common.install_opt` role for pre-installation of Prometheus.

### Installation

* Download the `jfx.metrics` collection:

```shell
ansible-galaxy collection install jfx.metrics
```

* Then use the roles from the collection in the playbook:

example:

```yaml
- hosts: all

  collections:
    - jfx.common
    - jfx.metrics

  roles:
    - role: install_opt
      vars:
        io_product: blackbox_exporter
        io_version: "{{ blackbox_exporter_version }}"
        io_package_name: blackbox_exporter-{{ blackbox_exporter_version }}.linux-{{ arch }}
        io_package_ext: tar.gz
        io_download_link: https://github.com/prometheus/blackbox_exporter/releases/download/v{{ blackbox_exporter_version }}/{{ io_package_name }}.{{ io_package_ext }}
        io_temp_dir_keep: true
    - role: blackbox_exporter
      vars:
        bbe_version: "{{ blackbox_exporter_version }}"
        bbe_arch: "{{ arch }}"
```

### Blackbox exporter role variables

* `bbe_version`
  * Required - example: `0.22.0`
  * Description: Version of Blackbox exporter.
* `bbe_arch`
  * Default: `amd64`
  * Description: Binary architecture of Prometheus amd64|arm64 ...

### Blackbox exporter files

* `blackbox_exporter.service`:
A default `blackbox_exporter.service` systemd file is defined but could be overridden by a file located in `{{ playbook_dir }}/files/` directory.

## Authors

* **FX Soubirou** - *Initial work* - [GitLab repositories](https://gitlab.com/op_so)

## License

This program is free software: you can redistribute it and/or modify it under the terms of the MIT License (MIT). See the [LICENSE](https://opensource.org/licenses/MIT) for details.