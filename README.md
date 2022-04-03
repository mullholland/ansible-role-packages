# [packages](#packages)

|GitHub|GitLab|
|------|------|
|[![github](https://github.com/mullholland/ansible-role-packages/workflows/Ansible%20Molecule/badge.svg)](https://github.com/mullholland/ansible-role-packages/actions)|[![gitlab](https://gitlab.com/mullholland/ansible-role-packages/badges/master/pipeline.svg)](https://gitlab.com/mullholland/ansible-role-packages)|[![quality](https://img.shields.io/ansible/quality/unset)](https://galaxy.ansible.com/mullholland/packages)|

Install packages which do not need customization.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
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
packages_merged: []
packages_debian_merged: []
packages_redhat_merged: []
packages_absent_merged: []
```


## [Example Playbook](#example-playbook)

This example is taken from `molecule/default/converge.yml` and is tested on each push, pull request and release.
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

The machine needs to be prepared in CI this is done using `molecule/default/prepare.yml`:
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





## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/mullholland):

-   [debian9](https://hub.docker.com/r/mullholland/docker-molecule-debian9)
-   [debian10](https://hub.docker.com/r/mullholland/docker-molecule-debian10)
-   [debian11](https://hub.docker.com/r/mullholland/docker-molecule-debian11)
-   [ubuntu1804](https://hub.docker.com/r/mullholland/docker-molecule-ubuntu1804)
-   [ubuntu2004](https://hub.docker.com/r/mullholland/docker-molecule-ubuntu2004)
-   [centos7](https://hub.docker.com/r/mullholland/docker-molecule-centos7)
-   [centos-stream8](https://hub.docker.com/r/mullholland/docker-molecule-centos-stream8)
-   [centos-stream9](https://hub.docker.com/r/mullholland/docker-molecule-centos-stream9)
-   [ubi8](https://hub.docker.com/r/mullholland/docker-molecule-ubi8)
-   [fedora34](https://hub.docker.com/r/mullholland/docker-molecule-fedora34)
-   [fedora35](https://hub.docker.com/r/mullholland/docker-molecule-fedora35)
-   [amazonlinux](https://hub.docker.com/r/mullholland/docker-molecule-amazonlinux)
-   [rockylinux8](https://hub.docker.com/r/mullholland/docker-molecule-rockylinux8)
-   [almalinux8](https://hub.docker.com/r/mullholland/docker-molecule-almalinux8)

The minimum version of Ansible required is 2.10, tests have been done to:

-   The previous versions.
-   The current version.
-   The [devel](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-devel-from-github-with-pip) version.





If you find issues, please register them in [GitHub](https://github.com/mullholland/ansible-role-packages/issues)

## [License](#license)

MIT


## [Author Information](#author-information)

[Mullholland](https://github.com/mullholland)

## [Special Thanks](#special-thanks)

Template inspired by [Robert de Bock](https://github.com/robertdebock)
