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



### File: `defaults/main.yml`

| Variable | Default Value | Description |
|----------|---------------|-------------|
| `docker_compose_binary_path` | `/usr/local/bin/docker-compose` | None |
| `docker_compose_url` | `https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)` | None |
| `docker_repo_url` | `https://download.docker.com/linux/centos/docker-ce.repo` | None |
| `docker_packages_remove` | `[]` | None |
| `docker_packages_remove.0` | `docker` | None |
| `docker_packages_remove.1` | `docker-client` | None |
| `docker_packages_remove.2` | `docker-client-latest` | None |
| `docker_packages_remove.3` | `docker-common` | None |
| `docker_packages_remove.4` | `docker-latest` | None |
| `docker_packages_remove.5` | `docker-latest-logrotate` | None |
| `docker_packages_remove.6` | `docker-logrotate` | None |
| `docker_packages_remove.7` | `docker-engine` | None |
| `docker_packages_install` | `[]` | None |
| `docker_packages_install.0` | `docker-ce` | None |
| `docker_packages_install.1` | `docker-ce-cli` | None |
| `docker_packages_install.2` | `containerd.io` | None |
| `docker_users` | `[]` | None |
| `docker_enable_tcp` | `False` | None |
| `docker_tcp_port` | `2375` | None |




## Task Overview


This role performs the following tasks:


### `verify.yml`


- **Enable and start Docker service**
- **Verify Docker installation with hello-world**
- **Remove hello-world container after verification**
- **Display Docker verification result**
- **Show Docker version**
- **Display Docker version**


### `install_debian.yml`


- **Update apt package index**
- **Install prerequisites**
- **Create /etc/apt/keyrings directory**
- **Install Docker Repo**
- **Install Docker packages**


### `main.yml`


- **Include Docker installation tasks**
- **Add users to docker group**
- **Configure Docker systemd service**
- **Verify Docker installation**


### `install_redhat.yml`


- **Install dnf-plugins-core**
- **Install Docker Repo**
- **Install Docker packages**


### `repo/RedHat.yml`


- **Add Docker CE repository**


### `repo/Ubuntu.yml`


- **Download Docker's official GPG key**
- **Get architecture**
- **Get Ubuntu codename**
- **Add Docker repository to Apt sources**


### `repo/Debian.yml`


- **Download Docker's official GPG key**
- **Get architecture**
- **Get Debian codename**
- **Add Docker repository to Apt sources**




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

## Documentation Maintenance

### Updating Dependencies

1. **Update** `meta/main.yml`:
   ```yaml
   documented_requirements:
     - src: https://github.com/user/role.git
       version: master
     - name: collection.name
       version: 1.0.0
   ```

2. **Sync** `meta/install_requirements.yml` with the same requirements

3. **Regenerate** documentation:
   ```bash
   pre-commit run --all-files
   ```

### Template Updates

- Edit `.docsible_template.md` for structure changes
- Test with: `docsible --role . --md-template .docsible_template.md -nob -com -tl`
- Commit both template and generated README.md

### Quick Checklist

When updating dependencies:
- [ ] Add to `meta/main.yml` → `documented_requirements`
- [ ] Add to `meta/install_requirements.yml`
- [ ] Run `pre-commit run --all-files`
- [ ] Verify generated README.md
- [ ] Commit all changes

## License


license (GPL-2.0-or-later, MIT, etc)


## Author Information


**Author:** gkorkmaz




**GitHub:** [gkorkmaz](https://github.com/gkorkmaz)

---
*This documentation was automatically generated using [docsible](https://github.com/zbohm/docsible).*
<!-- DOCSIBLE END -->
