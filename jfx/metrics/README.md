# Ansible collection Metrics

[![Software License](https://img.shields.io/badge/license-MIT-informational.svg?style=flat)](LICENSE)
[![Pipeline Status](https://gitlab.com/op_so/ansible/metrics/badges/main/pipeline.svg)](https://gitlab.com/op_so/ansible/metrics/pipelines)
[![semantic-release: angular](https://img.shields.io/badge/semantic--release-angular-e10079?logo=semantic-release)](https://github.com/semantic-release/semantic-release)

An [Ansible](https://www.ansible.com/) collection that deploys metrics tools on Ubuntu and Debian.

[![GitLab](https://shields.io/badge/Gitlab-informational?logo=gitlab&style=flat-square)](https://gitlab.com/op_so/ansible/metrics) The main repository.

[![Github](https://shields.io/badge/Github-informational?logo=github&style=flat-square)](https://github.com/jfx/ansible-collection-metrics) Deployment repository.

[![Ansible Galaxy](https://shields.io/badge/Ansible_Galaxy-informational?logo=ansible&style=flat-square)](https://galaxy.ansible.com/jfx/metrics) Ansible Galaxy collection.

This collections includes:

| Roles                                        | Description                                                                            |
| -------------------------------------------- | -------------------------------------------------------------------------------------- |
| [blackbox_exporter](#blackbox_exporter-role) | A role that installs/updates Blackbox exporter on Ubuntu and Debian Operating Systems. |
| [grafana](#grafana-role)                     | A role that installs/updates Grafana on Ubuntu and Debian Operating Systems.           |
| [prometheus](#prometheus-role)               | A role that installs/updates Prometheus on Ubuntu and Debian Operating Systems.        |

## blackbox_exporter role

A role that installs/updates [Blackbox exporter](https://github.com/prometheus/blackbox_exporter) on Ubuntu and Debian Operating Systems.

### blackbox_exporter role dependencies

- `jfx.common.install_opt` role for pre-installation of Prometheus.

### blackbox_exporter role variables

| Variables     | Description                                                    | Default      |
| ------------- | -------------------------------------------------------------- | ------------ |
| `bbe_version` | Version of Blackbox exporter. Example: `0.22.0`                | **Required** |
| `bbe_arch`    | Binary architecture of Blackbox exporter: `amd64`, `arm64` ... | `amd64`      |

### blackbox_exporter files

- `blackbox_exporter.service`:
A default `blackbox_exporter.service` systemd file is defined but could be overridden by a file located in `{{ playbook_dir }}/files/` directory.

## Grafana role

A role that installs/updates [Grafana](https://grafana.com/oss/grafana/) on Ubuntu and Debian Operating Systems.

### Grafana role dependencies

-

### Grafana role variables

-

### Grafana files

- `grafana.ini`:
A default `grafana.ini` configuration file is defined but could be overridden by a `grafana.ini.j2` file located in `{{ playbook_dir }}/templates/` directory.

## Prometheus role

A role that installs/updates [Prometheus](https://prometheus.io/) on Ubuntu and Debian Operating Systems.

### Prometheus role dependencies

- `jfx.common.install_opt` role for pre-installation of Prometheus.

### Prometheus role variables

| Variables      | Description                                             | Default      |
| -------------- | ------------------------------------------------------- | ------------ |
| `prom_version` | Version of Prometheus. Example: `2.40.1`                | **Required** |
| `prom_arch`    | Binary architecture of Prometheus: `amd64`, `arm64` ... | `amd64`      |

### Prometheus files

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
    - role: grafana
```

## Authors

- **FX Soubirou** - *Initial work* - [GitLab repositories](https://gitlab.com/op_so)

## License

This program is free software: you can redistribute it and/or modify it under the terms of the MIT License (MIT). See the [LICENSE](https://opensource.org/licenses/MIT) for details.
