# Podman Role

This Ansible role installs and configures rootless Podman on Debian systems.

## Usage

### Basic Installation

To install Podman and create a user:

```yaml
- name: "Install Podman"
  ansible.builtin.import_role:
    name: calopsys.containers.podman
  vars:
    calopsys_podman_user: "app"
    calopsys_podman_group: "app"
    calopsys_podman_home: "/opt/app"
    calopsys_podman_tz: "UTC"
```

### Deploy Application with Compose

To deploy an application using a compose file:

```yaml
- name: "Create application."
  ansible.builtin.import_role:
    name: calopsys.containers.podman
    tasks_from: compose.yml
  vars:
    calopsys_podman_user: "app"
    calopsys_podman_application_name: "app"
    calopsys_podman_application_compose_template: "app.compose.yml"
```

### Complete Example

```yaml
- name: "Deploy Podman and application"
  hosts: all
  become: true
  tasks:
    - name: "Install Podman"
      ansible.builtin.import_role:
        name: calopsys.containers.podman
      vars:
        calopsys_podman_user: "app"
        calopsys_podman_group: "app"
        calopsys_podman_home: "/opt/app"
        calopsys_podman_tz: "UTC"

    - name: "Deploy application"
      ansible.builtin.import_role:
        name: calopsys.containers.podman
        tasks_from: compose.yml
      vars:
        calopsys_podman_user: "app"
        calopsys_podman_application_name: "app"
        calopsys_podman_application_compose_template: "app.compose.yml"
```

## Variables

See `REFERENCE.md` for complete variable documentation.

## Testing

Run molecule tests:
```bash
make molecule role=podman
```