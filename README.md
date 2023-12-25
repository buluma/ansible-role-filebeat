# Ansible role [filebeat](https://galaxy.ansible.com/ui/standalone/roles/buluma/filebeat/documentation)

Filebeat for Linux.

|GitHub|Version|Issues|Pull Requests|Downloads|
|------|-------|------|-------------|---------|
|[![github](https://github.com/buluma/ansible-role-filebeat/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-filebeat/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-filebeat.svg)](https://github.com/buluma/ansible-role-filebeat/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-filebeat.svg)](https://github.com/buluma/ansible-role-filebeat/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-filebeat.svg)](https://github.com/buluma/ansible-role-filebeat/pulls/)|[![Ansible Role](https://img.shields.io/ansible/role/d/buluma/filebeat)](https://galaxy.ansible.com/ui/standalone/roles/buluma/filebeat/documentation)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-filebeat/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: true

  pre_tasks:
    - name: Update apt cache.
      apt: update_cache=true cache_valid_time=600
      when: ansible_os_family == 'Debian'

    - name: Install test dependencies (RedHat).
      package: name=which state=present
      when: ansible_os_family == 'RedHat'

    - name: Install test dependencies.
      package: name=curl state=present

    - name: Set the java_packages variable (Ubuntu).
      ansible.builtin.set_fact:
        java_packages:
          - openjdk-8-jdk
      when: ansible_distribution == 'Ubuntu'

  roles:
    - role: buluma.java
    - role: robertdebock.elasticsearch
    - role: buluma.logstash
    - role: buluma.filebeat
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-filebeat/blob/master/defaults/main.yml):

```yaml
---
filebeat_version: 7.x
filebeat_package: filebeat
filebeat_package_state: present

filebeat_create_config: true
filebeat_template: "filebeat.yml.j2"

filebeat_inputs:
  - type: log
    paths:
      - "/var/log/*.log"

filebeat_output_elasticsearch_enabled: false
filebeat_output_elasticsearch_hosts:
  - "localhost:9200"

filebeat_output_logstash_enabled: true
filebeat_output_logstash_hosts:
  - "localhost:5044"

filebeat_enable_logging: false
filebeat_log_level: warning
filebeat_log_dir: /var/log/mybeat
filebeat_log_filename: mybeat.log

filebeat_ssl_dir: /etc/pki/logstash
filebeat_ssl_certificate_file: ""
filebeat_ssl_key_file: ""
filebeat_ssl_insecure: "false"

filebeat_elastic_cloud_enabled: false
filebeat_elastic_cloud_id: ""
filebeat_elastic_cloud_username: ""
filebeat_elastic_cloud_password: ""
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-filebeat/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | Version |
|-------------|--------|--------|
|[buluma.java](https://galaxy.ansible.com/buluma/java)|[![Ansible Molecule](https://github.com/buluma/ansible-role-java/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-java/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-java.svg)](https://github.com/shadowwalker/ansible-role-java)|
|[robertdebock.elasticsearch](https://galaxy.ansible.com/buluma/robertdebock.elasticsearch)|[![Ansible Molecule](https://github.com/buluma/robertdebock.elasticsearch/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/robertdebock.elasticsearch/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/robertdebock.elasticsearch.svg)](https://github.com/shadowwalker/robertdebock.elasticsearch)|
|[buluma.logstash](https://galaxy.ansible.com/buluma/logstash)|[![Ansible Molecule](https://github.com/buluma/ansible-role-logstash/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-logstash/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-logstash.svg)](https://github.com/shadowwalker/ansible-role-logstash)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-filebeat/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[EL](https://hub.docker.com/repository/docker/buluma/enterpriselinux/general)|all|
|[Debian](https://hub.docker.com/repository/docker/buluma/debian/general)|all|
|[Ubuntu](https://hub.docker.com/repository/docker/buluma/ubuntu/general)|all|

The minimum version of Ansible required is 2.12, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-filebeat/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-filebeat/blob/master/CHANGELOG.md)

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-filebeat/blob/master/LICENSE)

## [Author Information](#author-information)

[Shadow Walker](https://buluma.github.io/)


Template inspired by [Robert de Bock](https://github.com/robertdebock)
