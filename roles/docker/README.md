# Docker Role

This role installs and configures Docker on Debian systems.

## Usage

### Full Role

Include the role to install Docker, configure the daemon, and start the service:

```yaml
- name: "Install and configure Docker"
  ansible.builtin.include_role:
    name: calopsys.containers.docker
```

### Standalone Compose Task

Import only the compose task to deploy a Docker Compose application:

```yaml
- name: "Deploy compose application"
  ansible.builtin.import_role:
    name: calopsys.containers.docker
    tasks_from: compose.yml
  vars:
    calopsys_docker_compose_workdir: "/opt/compose"
    calopsys_docker_compose_template: "templates/myapp.compose.yml.j2"
```

**Variables:**
- `calopsys_docker_compose_workdir` - Working directory for the compose application (default: `/opt/compose`)
- `calopsys_docker_compose_template` - Local path to the compose template file (required)
