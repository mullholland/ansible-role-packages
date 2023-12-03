# [Ansible role packages](#packages)

Install packages which do not need customization.

|GitHub|Downloads|Version|
|------|---------|-------|
|[![github](https://github.com/mullholland/ansible-role-packages/actions/workflows/molecule.yml/badge.svg)](https://github.com/mullholland/ansible-role-packages/actions/workflows/molecule.yml)|[![downloads](https://img.shields.io/ansible/role/d/mullholland/packages)](https://galaxy.ansible.com/mullholland/packages)|[![Version](https://img.shields.io/github/release/mullholland/ansible-role-packages.svg)](https://github.com/mullholland/ansible-role-packages/releases/)|
## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/mullholland/ansible-role-packages/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: true
  gather_facts: true
  vars:
    packages:
      - "ethtool"
    packages_group:
      - "bc"
    packages_host:
      - "zip"

    packages_debian:
      - "nethogs"

    packages_redhat:
      - "nano"

    packages_absent:
      - "bzip2"
    packages_absent_group:
      - "htop"
    packages_absent_host:
      - "mtr"
  roles:
    - role: "mullholland.packages"
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/mullholland/ansible-role-packages/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  become: true
  gather_facts: true

  tasks:
    - name: Install packages to test absent parts
      ansible.builtin.package:
        name:
          - "bzip2"
          - "unzip"
        state: present
```



## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/mullholland/ansible-role-packages/blob/master/defaults/main.yml):

```yaml
---
# global/group/host seperation is meant to allow merging of package groups
# according to groupmemberships

# packages are the same for all servers, regardless of ansible_os_family
# differentiates between global/group/host
packages: []
packages_group: []
packages_host: []

# packages_debian are only for debian/ubuntu ased systems
# differentiates between global/group/host
packages_debian: []
packages_debian_group: []
packages_debian_host: []

# packages_debian are only for redhat/Centos (rocky/almalinux/amazon) based systems
# differentiates between global/group/host
packages_redhat: []
packages_redhat_group: []
packages_redhat_host: []


# packages_absent is the same for all
# differentiates between global/group/host
packages_absent: []
packages_absent_group: []
packages_absent_host: []

# Initialise empty for later merging
packages_debian_merged: []
packages_redhat_merged: []
packages_absent_merged: []
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/mullholland/ansible-role-packages/blob/master/requirements.txt).


## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://mullholland.net) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/mullholland/ansible-role-packages/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/mullholland):

|container|tags|
|---------|----|
|[EL](https://hub.docker.com/r/mullholland/enterpriselinux)|all|
|[Amazon](https://hub.docker.com/r/mullholland/amazonlinux)|Candidate|
|[Fedora](https://hub.docker.com/r/mullholland/fedora/)|all|
|[Ubuntu](https://hub.docker.com/r/mullholland/ubuntu)|all|
|[Debian](https://hub.docker.com/r/mullholland/debian)|all|

The minimum version of Ansible required is 2.10, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/mullholland/ansible-role-packages/issues).

## [License](#license)

[MIT](https://github.com/mullholland/ansible-role-packages/blob/master/LICENSE).

## [Author Information](#author-information)

[Mullholland](https://mullholland.net)
