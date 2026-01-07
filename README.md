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
| [docker_enable_tcp](defaults/main.yml#L26) | bool |  |
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
| [docker_repo_url](defaults/main.yml#L6) | str | `https://download.docker.com/linux/centos/docker-ce.repo` |
| [docker_tcp_port](defaults/main.yml#L27) | int | `2375` |
| [docker_users](defaults/main.yml#L22) | list |  |




## Task Overview


This role performs the following tasks:


### File: `tasks/verify.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [Enable and start Docker service](tasks/verify.yml#L) | ansible.builtin.systemd | No | N/A |
| [Verify Docker installation with hello-world](tasks/verify.yml#L) | ansible.builtin.command | No | N/A |
| [Remove hello-world container after verification](tasks/verify.yml#L) | ansible.builtin.command | Yes | N/A |
| [Display Docker verification result](tasks/verify.yml#L) | ansible.builtin.debug | No | N/A |
| [Show Docker version](tasks/verify.yml#L) | ansible.builtin.command | No | N/A |
| [Display Docker version](tasks/verify.yml#L) | ansible.builtin.debug | No | N/A |




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
| [Configure Docker systemd service](tasks/main.yml#L) | ansible.builtin.template | No | N/A |
| [Verify Docker installation](tasks/main.yml#L) | ansible.builtin.include_tasks | No | N/A |




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
