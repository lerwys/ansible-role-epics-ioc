Ansible Role EPICS IOC
=========================

[![CI](https://github.com/lerwys/ansible-role-epics-ioc/workflows/CI/badge.svg)](https://github.com/lerwys/ansible-role-epics-ioc/actions?query=workflow%3ACI)
![Latest tag](https://img.shields.io/github/tag/lerwys/ansible-role-epics-ioc.svg?style=flat)
[![Latest release](https://img.shields.io/github/release/lerwys/ansible-role-epics-ioc.svg?style=flat)](https://github.com/lerwys/ansible-role-epics-ioc/releases)
[![BSD License](https://img.shields.io/github/license/lerwys/ansible-role-epics-ioc.svg?style=flat)](LICENSE)

This Ansible role clone and install EPICS IOCs.

## Requirements

- ansible >= 2.10
- molecule >= 3.0

## Role Variables

```yaml
epics_ioc_pkg_version_debian_git: ""
epics_ioc_pkg_version_debian_make: ""
epics_ioc_pkg_version_debian_procserv: ""
epics_ioc_pkg_version_debian_telnet: ""
epics_ioc_pkg_version_debian_netcat_openbsd: ""
```

Package versions for Debian. Leave empty for the latest


```yaml
epics_ioc_pkg_version_redhat_git: ""
epics_ioc_pkg_version_redhat_make: ""
epics_ioc_pkg_version_redhat_procserv: ""
epics_ioc_pkg_version_redhat_telnet: ""
epics_ioc_pkg_version_redhat_netcat_openbsd: ""
```

Package versions for RedHat. Leave empty for the latest


```yaml
epics_ioc_git_username: "user"
```

Default git username. Used if not set


```yaml
epics_ioc_git_useremail: "user@ansible_default.com"
```

Default git useremail. Used if not set


```yaml
epics_ioc_carepeater_systemd_executable: "/usr/bin/caRepeater"
```

Specify caRepeater absolute path executable


```yaml
epics_ioc_carepeater_systemd_path: "/etc/systemd/system"
```

Specify caRepeater systemd service path


```yaml
epics_ioc_carepeater_systemd_state: started
```

Specify caRepeater systemd service state

```yaml
epics_ioc_carepeater_systemd_enabled: true
```

Specify caRepeater systemd service enabled

```yaml
epics_ioc_carepeater_systemd_port: 5065
```

Specify caRepeater port to be run

```yaml
epics_ioc_env_epics_ioc_log_port: 7004
```

Specify IOC log port.
Used if not defined at the epics_ioc_repos list items.


```yaml
epics_ioc_carepeater_systemd_user: nobody
```

Specify caRepeater user to be run


```yaml
epics_ioc_group_name: softioc
```

Specify EPICS IOC group name


```yaml
epics_ioc_user_name: softioc
```

Specify EPICS IOC user name. Used as the default if not
defined at the epics_ioc_repos list items


```yaml
epics_ioc_gid:
```

Specify EPICS IOC GID. Leave empty for automatic assignment

```yaml
epics_ioc_systemd_state: started
```

Specify IOC systemd state. Used as the default if not
defined at the epics_ioc_repos list items

```yaml
epics_ioc_systemd_enabled: true
```

Specify IOC systemd enabled. Used as the default if not
defined at the epics_ioc_repos list items

```yaml
epics_ioc_systemd_coresize: 2147483647
```

Specify IOC coresize. Used as the default if not
defined at the epics_ioc_repos list items

```yaml
epics_ioc_systemd_enable_console_port: true
```

Specify IOC enable console port. Used as the default if not
defined at the epics_ioc_repos list items


```yaml
epics_ioc_systemd_console_port: 4051
```

Specify IOC console port. Used as the default if not
defined at the epics_ioc_repos list items

```yaml
epics_ioc_systemd_enable_unix_domain_socket: true
```

Specify IOC enable unix domain socket. Used as the default if not
defined at the epics_ioc_repos list items

```yaml
epics_ioc_systemd_procserv_timefmt: "%c"
```

Specify IOC procServ time format. Used as the default if not
defined at the epics_ioc_repos list items

```yaml
epics_ioc_systemd_procserv_start_script: "st.cmd"
```

Specify IOC start script. Used as the default if not
defined at the epics_ioc_repos list items


```yaml
epics_ioc_epics_base_dir: /usr/lib/epics

```

Select where EPICS base libraries are installed. Used as the default
if not defined at the epics_ioc_repos list items.

```yaml
epics_ioc_overwrite_release_file: true
```

Select if we want to overwrite the RELEASE file or not. Used as
as default if not defined at the epics_ioc_repos list items.


```yaml
epics_ioc_release_filename: RELEASE
```

Select default name of the destination RELEASE file, if not
defined at the epics_ioc_repos list items.

```yaml
epics_ioc_clone_path: "/usr/local/lib/iocapps"
```

Select epics IOC clone path (as well as install). Used if not
defined at the epics_ioc_repos list items.

```yaml
epics_ioc_boot_dir: "iocBoot/ioc{{ epics_host_arch }}"
```

Select epics IOC boot directory. Used if not
defined at the epics_ioc_repos list items.
epics_host_arch will, in most cases, be defined
at "epics" role

```yaml
epics_ioc_autosave_base_dir: "/var/lib"
```

Select epics IOC autosave base directory. Used if not
defined at the epics_ios_repos list items.


```yaml
epics_ioc_epics_ioc_modules: []
```

Select which EPICS modules are going to be templated in
RELEASE file. Used as a default if not defined at the
epics_ios_repos list items.

Example:

```yaml
epics_ioc_epics_ioc_modules:
 - ASYN=/usr/lib/epics
 - CALC=/usr/lib/epics
 - STREAM=/usr/lib/epics
```


```yaml
epics_ioc_repos: []
```

Groups of repositories to clone and install. This should be set when calling the role.

Check the task/clone-install.yml for all actions available.

Example:

```yaml
- name: tekScope EPICS IOC
  org_url: https://github.com/brunoseivam
  repo_name: tekScope
  repo_version: master
  repo_stash: true
  clone_path: /tmp
  install_via_makefile: true
  epics_ioc_modules:
    - ASYN=/usr/lib/epics
    - CALC=/usr/lib/epics
    - STREAM=/usr/lib/epics
  epics_ioc_overwrite_release_file: true
  epics_ioc_release_filename: RELEASE
  epics_base_dir: /usr/lib/epics
  epics_manage_user: true
  epics_ioc_user: ioc
  # Leave empty or omit for automatic assignment
  epics_ioc_uid:
  make_install_targets:
    - distclean
    - all
  force_version: true
```

## Example Playbooks

`playbook.yml:`
```yaml
---
- hosts: all
  tasks:
  - import_role:
      name: "{{ playbook_dir }}"
```

`playbook-complete.yml:`
```yaml
---
- hosts: all

  vars:
    epics_packages_extra:
      - epics-asyn-dev
      - epics-stream-dev
      - epics-calc-dev

    epics_ioc_repos:
      - name: tekScope EPICS IOC
        org_url: https://github.com/brunoseivam
        repo_name: tekScope
        repo_version: master
        repo_stash: true
        clone_path: /tmp
        install_via_makefile: true
        epics_ioc_modules:
          - ASYN=/usr/lib/epics
          - STREAM=/usr/lib/epics
          - CALC=/usr/lib/epics
        epics_ioc_overwrite_release_file: true
        epics_ioc_release_filename: RELEASE
        epics_base_dir: /usr/lib/epics
        epics_ioc_boot_dir: iocBoot/ioclinux-x86_64
        epics_manage_user: true
        epics_manage_autosave_dir: true
        epics_ioc_user: ioc
        # Leave empty or omit for automatic assignment
        epics_ioc_uid:
        # Leave empty or omit to default
        epics_ioc_systemd_state: started
        # Leave empty or omit to default
        epics_ioc_systemd_enabled: true
        # Leave empty or omit to undefined
        epics_ioc_systemd_requires:
          - network.target
        # Leave empty or omit to undefined
        epics_ioc_systemd_wants:
          - network.target
        # Leave empty or omit to undefined
        epics_ioc_systemd_after:
          - network.target
        # Leave empty or omit to undefined
        epics_ioc_systemd_requires_mounts_for: []
        # Leave empty or omit to default
        epics_ioc_systemd_coresize:
        # Leave empty or omit to default
        epics_ioc_systemd_enable_console_port: true
        # Leave empty or omit to default
        epics_ioc_systemd_console_port:
        # Leave empty or omit to default
        epics_ioc_systemd_enable_unix_domain_socket:
        # Leave empty or omit to default
        epics_ioc_systemd_unix_domain_socket:
        # Leave empty or omit to default
        epics_ioc_systemd_procserv_timefmt:
        # Leave empty or omit to default
        epics_ioc_systemd_procserv_start_script:
        # Environment variables shall be passed in a dictionary, if
        # not list below
        epics_ioc_env: {}
        # Leave empty or omit to make variable undefined
        epics_ioc_env_epics_ca_addr_list: "127.0.0.1"
        # Leave empty or omit to make variable undefined
        epics_ioc_env_epics_ca_auto_addr_list: true
        # Leave empty or omit to make variable undefined
        epics_ioc_env_epics_ca_max_array_bytes: 10000000
        # Leave empty or omit to make variable assume default value
        epics_ioc_env_epics_ioc_log_port: 7004
        # Leave empty or omit for undefined variable
        epics_ioc_env_epics_ca_sec_file: ""
        # Leave empty or omit for undefined variable
        epics_ioc_env_epics_ioc_log_inet: ""
        # Only used if epics_manage_autosave_dir is set to true
        epics_ioc_autosave_base_dir: /var/lib
        make_install_targets:
          - distclean
          - all
        force_version: true

  roles:
    - role: lerwys.epics_ioc
```

## Install Prerequisites

```
ansible-galaxy install -r requirements.yml
```

## Example Commmand

```bash
ansible-playbook -i host, -u user -k --ask-become-pass playbook.yml
```

## Tests

Tests are performed using Molecule. To run them with python virtualenv, issue:

```bash
    bash -c "\
        cd ../ && \
        virtualenv env --python python3 && \
        source env/bin/activate && \
        cd ansible-role-epics-ioc && \
        pip3 install ansible molecule \
            molecule-docker testinfra \
            yamllint ansible-lint flake8 \
            docker && \
        molecule test"
```

Optionally, you can specify dns servers to be used for both
provisioner create and run (docker in our case), by using
the following variables:


```bash
    export DNS_SERVER1="<DNS server 1>"
    export DNS_SERVER2="<DNS server 2>"
```

This can be used, for instance, in hosts that have non-default
DNS configurations that docker can't access, such as when
using local systemd-resolv DNS (e.g., 127.x.y.z) or when DNS
servers are set via DHCP with local non-routable IP addresses
(e.g., 10.x.y.z).

## Troubleshooting

If you use a host system with SELinux enabled you might get an error when using
Ansible like the following:

```bash
    "msg": "Aborting, target uses selinux but python bindings (libselinux-python) aren't installed!"
```

If that happens, it might be because virtualenv does not have access to libselinux
and it can't be installed via pip.

A workaround might be to manually copy the librar files into the virtualenv
so that Ansible has access to it.

On a Fedra 29 system, using python3-7, the following fixes the issue:

```bash
    cp -r /usr/lib64/python3.7/site-packages/selinux env/lib64/python3.7/site-packages/
    cp -r /usr/lib64/python3.7/site-packages/_selinux.cpython-37m-x86_64-linux-gnu.so env/lib64/python3.7/site-packages/
```

Be advised, that the python versions might differ and the library names, as well.

## License

BSD 2-clause
