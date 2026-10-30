<!-- DOCSIBLE START -->
# Ansible Role: role_docker


role_docker to install docker


## Table of Contents

- [Requirements](#requirements)
- [Dependencies](#dependencies)
- [Role Variables](#role-variables)
- [Task Overview](#task-overview)
- [Example Playbook](#example-playbook)
- [Documentation Maintenance](#documentation-maintenance)
- [License](#license)
- [Author Information](#author-information)

## Requirements



- Ansible >= 2.9


- Supported platforms:
  - AlmaLinux (7, 8, 9)



## Dependencies


This role requires the following roles and collections:




  
    
  

  
    
  

  
    
  

  
    
  



**Roles:**

- [role_base](https://github.com/ginanck/role_base.git) (version: master)




**Collections:**

- `community.docker` (>= 4.8.1)

- `community.general` (>= 6.6.1)

- `ansible.posix` (>= 1.5.4)



To install all dependencies:
```bash
ansible-galaxy install -r meta/install_requirements.yml
```


## Role Variables

**These are static variables with lower priority**



#### File: defaults/main.yml

| Var | Type | Value |
|-----|------|-------|
| [docker_compose_binary_path](defaults/main.yml#L4) | str | `/usr/local/bin/docker-compose` |
| [docker_compose_url](defaults/main.yml#L5) | str | `https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)` |
| [docker_config_dir](defaults/main.yml#L27) | str | `/etc/docker` |
| [docker_containerd_socket](defaults/main.yml#L58) | str | `/run/containerd/containerd.sock` |
| [docker_daemon_config_path](defaults/main.yml#L28) | str | `{{ docker_config_dir }}/daemon.json` |
| [docker_daemon_config_preserve_unmanaged](defaults/main.yml#L31) | bool | `True` |
| [docker_daemon_options](defaults/main.yml#L35) | dict |  |
| [docker_dns](defaults/main.yml#L49) | list |  |
| [docker_enable_tcp](defaults/main.yml#L63) | bool |  |
| [docker_live_restore](defaults/main.yml#L43) | bool | `True` |
| [docker_log_driver](defaults/main.yml#L38) | str | `json-file` |
| [docker_log_max_file](defaults/main.yml#L40) | str | `5` |
| [docker_log_max_size](defaults/main.yml#L39) | str | `100m` |
| [docker_packages_install](defaults/main.yml#L17) | list |  |
| [docker_packages_install.0](defaults/main.yml#L18) | str | `docker-ce` |
| [docker_packages_install.1](defaults/main.yml#L19) | str | `docker-ce-cli` |
| [docker_packages_install.2](defaults/main.yml#L20) | str | `containerd.io` |
| [docker_packages_remove](defaults/main.yml#L7) | list |  |
| [docker_packages_remove.0](defaults/main.yml#L7) | str | `docker` |
| [docker_packages_remove.1](defaults/main.yml#L9) | str | `docker-client` |
| [docker_packages_remove.2](defaults/main.yml#L10) | str | `docker-client-latest` |
| [docker_packages_remove.3](defaults/main.yml#L11) | str | `docker-common` |
| [docker_packages_remove.4](defaults/main.yml#L12) | str | `docker-latest` |
| [docker_packages_remove.5](defaults/main.yml#L13) | str | `docker-latest-logrotate` |
| [docker_packages_remove.6](defaults/main.yml#L14) | str | `docker-logrotate` |
| [docker_packages_remove.7](defaults/main.yml#L15) | str | `docker-engine` |
| [docker_registry_mirrors](defaults/main.yml#L52) | list |  |
| [docker_repo_url](defaults/main.yml#L6) | str | `https://download.docker.com/linux/centos/docker-ce.repo` |
| [docker_systemd_dropin_dir](defaults/main.yml#L56) | str | `/etc/systemd/system/docker.service.d` |
| [docker_systemd_dropin_path](defaults/main.yml#L57) | str | `{{ docker_systemd_dropin_dir }}/10-role-docker.conf` |
| [docker_tcp_port](defaults/main.yml#L64) | int | `2375` |
| [docker_tls_ca_path](defaults/main.yml#L68) | str |  |
| [docker_tls_cert_path](defaults/main.yml#L66) | str |  |
| [docker_tls_key_allowed_modes](defaults/main.yml#L72) | list |  |
| [docker_tls_key_allowed_modes.0](defaults/main.yml#L73) | str | `0400` |
| [docker_tls_key_allowed_modes.1](defaults/main.yml#L74) | str | `0440` |
| [docker_tls_key_allowed_modes.2](defaults/main.yml#L75) | str | `0600` |
| [docker_tls_key_allowed_modes.3](defaults/main.yml#L76) | str | `0640` |
| [docker_tls_key_path](defaults/main.yml#L67) | str |  |
| [docker_tls_port](defaults/main.yml#L65) | int | `2376` |
| [docker_tls_verify](defaults/main.yml#L69) | bool | `True` |
| [docker_userland_proxy](defaults/main.yml#L46) | bool |  |
| [docker_users](defaults/main.yml#L22) | list |  |
| [docker_verify_runtime](defaults/main.yml#L82) | bool | `True` |




## Task Overview


This role performs the following tasks:


### File: `tasks/verify.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [Read the managed daemon configuration](tasks/verify.yml#L) | ansible.builtin.slurp | No | N/A |
| [Assert the managed daemon configuration is valid JSON](tasks/verify.yml#L) | ansible.builtin.assert | No | N/A |
| [Assert the systemd drop-in is present](tasks/verify.yml#L) | ansible.builtin.stat | No | N/A |
| [Assert the systemd drop-in exists](tasks/verify.yml#L) | ansible.builtin.assert | No | N/A |
| [Show the Docker client version](tasks/verify.yml#L) | ansible.builtin.command | No | N/A |
| [Display the Docker version](tasks/verify.yml#L) | ansible.builtin.debug | No | N/A |
| [Check the Docker daemon is reachable](tasks/verify.yml#L) | ansible.builtin.command | Yes | N/A |
| [Display the Docker daemon status](tasks/verify.yml#L) | ansible.builtin.debug | Yes | N/A |




### File: `tasks/preflight.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [Assert TLS material is supplied when TCP is enabled](tasks/preflight.yml#L) | ansible.builtin.assert | Yes | N/A |
| [Stat the TLS material](tasks/preflight.yml#L) | ansible.builtin.stat | Yes | N/A |
| [Assert the TLS material exists](tasks/preflight.yml#L) | ansible.builtin.assert | Yes | N/A |
| [Assert the TLS key permissions are not world readable](tasks/preflight.yml#L) | ansible.builtin.assert | Yes | N/A |
| [Assert plain TCP is not requested alongside TLS](tasks/preflight.yml#L) | ansible.builtin.assert | Yes | N/A |




### File: `tasks/configure.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [Ensure the Docker configuration directory exists](tasks/configure.yml#L) | ansible.builtin.file | No | N/A |
| [Stat an existing daemon configuration](tasks/configure.yml#L) | ansible.builtin.stat | Yes | N/A |
| [Read an existing daemon configuration](tasks/configure.yml#L) | ansible.builtin.slurp | Yes | N/A |
| [Start from an empty existing configuration](tasks/configure.yml#L) | ansible.builtin.set_fact | No | N/A |
| [Parse the existing daemon configuration](tasks/configure.yml#L) | ansible.builtin.set_fact | Yes | N/A |
| [Drop stale TLS settings when TCP is disabled](tasks/configure.yml#L) | ansible.builtin.set_fact | Yes | N/A |
| [Build the managed daemon configuration](tasks/configure.yml#L) | ansible.builtin.set_fact | No | N/A |
| [Add the TLS listener settings](tasks/configure.yml#L) | ansible.builtin.set_fact | Yes | N/A |
| [Apply extra daemon options](tasks/configure.yml#L) | ansible.builtin.set_fact | Yes | N/A |
| [Merge the existing and managed configurations](tasks/configure.yml#L) | ansible.builtin.set_fact | No | N/A |
| [Write the managed daemon configuration](tasks/configure.yml#L) | ansible.builtin.template | No | N/A |
| [Ensure the systemd drop-in directory exists](tasks/configure.yml#L) | ansible.builtin.file | No | N/A |
| [Write the systemd drop-in](tasks/configure.yml#L) | ansible.builtin.template | No | N/A |
| [Ensure the Docker service is enabled and started](tasks/configure.yml#L) | ansible.builtin.systemd | No | N/A |




### File: `tasks/install_debian.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [Update apt package index](tasks/install_debian.yml#L) | ansible.builtin.apt | No | N/A |
| [Install prerequisites](tasks/install_debian.yml#L) | ansible.builtin.apt | No | N/A |
| [Create /etc/apt/keyrings directory](tasks/install_debian.yml#L) | ansible.builtin.file | No | N/A |
| [Install Docker Repo](tasks/install_debian.yml#L) | ansible.builtin.include_tasks | No | N/A |
| [Install Docker packages](tasks/install_debian.yml#L) | ansible.builtin.apt | No | N/A |




### File: `tasks/main.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [Include Docker installation tasks](tasks/main.yml#L) | ansible.builtin.include_tasks | No | N/A |
| [Add users to docker group](tasks/main.yml#L) | ansible.builtin.user | Yes | N/A |
| [Validate the requested daemon exposure](tasks/main.yml#L) | ansible.builtin.include_tasks | No | N/A |
| [Configure the Docker daemon](tasks/main.yml#L) | ansible.builtin.include_tasks | No | N/A |
| [Verify Docker configuration and runtime](tasks/main.yml#L) | ansible.builtin.include_tasks | No | N/A |




### File: `tasks/install_redhat.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [Install dnf-plugins-core](tasks/install_redhat.yml#L) | ansible.builtin.dnf | No | N/A |
| [Install Docker Repo](tasks/install_redhat.yml#L) | ansible.builtin.include_tasks | No | N/A |
| [Install Docker packages](tasks/install_redhat.yml#L) | ansible.builtin.dnf | No | N/A |




### File: `tasks/repo/RedHat.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [Add Docker CE repository](tasks/repo/RedHat.yml#L) | ansible.builtin.shell | No | N/A |




### File: `tasks/repo/Ubuntu.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [Download Docker's official GPG key](tasks/repo/Ubuntu.yml#L) | ansible.builtin.get_url | No | N/A |
| [Get architecture](tasks/repo/Ubuntu.yml#L) | ansible.builtin.command | No | N/A |
| [Get Ubuntu codename](tasks/repo/Ubuntu.yml#L) | ansible.builtin.shell | No | N/A |
| [Add Docker repository to Apt sources](tasks/repo/Ubuntu.yml#L) | ansible.builtin.apt_repository | No | N/A |




### File: `tasks/repo/Debian.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [Download Docker's official GPG key](tasks/repo/Debian.yml#L) | ansible.builtin.get_url | No | N/A |
| [Get architecture](tasks/repo/Debian.yml#L) | ansible.builtin.command | No | N/A |
| [Get Debian codename](tasks/repo/Debian.yml#L) | ansible.builtin.shell | No | N/A |
| [Add Docker repository to Apt sources](tasks/repo/Debian.yml#L) | ansible.builtin.apt_repository | No | N/A |






## Example Playbook

```yaml
---
- hosts: all
  become: yes
  roles:
    - role: role_docker

      vars:
        docker_compose_binary_path: /usr/local/bin/docker-compose
        docker_compose_url: https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)
        docker_repo_url: https://download.docker.com/linux/centos/docker-ce.repo

```

## License


license (GPL-2.0-or-later, MIT, etc)


## Author Information


**Author:** gkorkmaz




**GitHub:** [gkorkmaz](https://github.com/gkorkmaz)

---
*This documentation was automatically generated using [docsible](https://github.com/zbohm/docsible).*
<!-- DOCSIBLE END -->
