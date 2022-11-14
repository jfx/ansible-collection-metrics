# Ansible collection Metrics

[![Software License](https://img.shields.io/badge/license-MIT-informational.svg?style=flat)](LICENSE)
[![Pipeline Status](https://gitlab.com/op_so/ansible/metrics/badges/main/pipeline.svg)](https://gitlab.com/op_so/ansible/metrics/pipelines)
[![semantic-release: angular](https://img.shields.io/badge/semantic--release-angular-e10079?logo=semantic-release)](https://github.com/semantic-release/semantic-release)

An [Ansible](https://www.ansible.com/) collection that deploys metrics tools on Ubuntu and Debian.

[![GitLab](https://shields.io/badge/Gitlab-informational?logo=gitlab&style=flat-square)](https://gitlab.com/op_so/ansible/metrics) The main repository.

[![Github](https://shields.io/badge/Github-informational?logo=github&style=flat-square)](https://github.com/jfx/ansible-collection-metrics) Deployment repository.

[![Ansible Galaxy](https://shields.io/badge/Ansible_Galaxy-informational?logo=ansible&style=flat-square)](https://galaxy.ansible.com/jfx/metrics) Ansible Galaxy collection.

This collections includes:

## Prometheus role

A role that install/update [Prometheus](https://prometheus.io/) on Ubuntu and Debian Operating Systems.

### Dependencies

- `jfx.common.install_opt` role for pre-installation of Prometheus.

### prometheus role variables

- `prom_version`
  - Required - example: `2.40.1`
  - Description: Version of prometheus.
- `prom_arch`
  - Default: `amd64`
  - Description: Binary architecture of Prometheus amd64|arm64 ...

### prometheus files

- `prometheus.service`:
A default `prometheus.service` systemd file is defined but could be overridden by a file located in `{{ playbook_dir }}/files/` directory.

- `prometheus.yml`:
A default `prometheus.yml.j2` config file is defined but could be overridden by a file located in `{{ playbook_dir }}/templates/` directory.

## Getting Started

### Requirements

In order to use:

- Minimal Ansible version: 2.10

### Installation

- Download the `jfx.common` and `jfx.metrics` collection:

```shell
ansible-galaxy collection install jfx.common
ansible-galaxy collection install jfx.metrics
```

- Then use the roles from the collection in the playbook:

example:

```yaml
- hosts: all

  collections:
    - jfx.common
    - jfx.metrics

  roles:
    - role: install_opt
      vars:
        io_product: prometheus
        io_version: "{{ prometheus_version }}"
        io_package_name: prometheus-{{ prometheus_version }}.linux-{{ arch }}
        io_package_ext: tar.gz
        io_download_link: https://github.com/prometheus/prometheus/releases/download/v{{ prometheus_version }}/{{ io_package_name }}.{{ io_package_ext }}
        io_temp_dir_keep: true
    - role: prometheus
      vars:
        prom_version: "{{ prometheus_version }}"
        prom_arch: "{{ arch }}"
```

## Authors

- **FX Soubirou** - *Initial work* - [GitLab repositories](https://gitlab.com/op_so)

## License

This program is free software: you can redistribute it and/or modify it under the terms of the MIT License (MIT). See the [LICENSE](https://opensource.org/licenses/MIT) for details.
