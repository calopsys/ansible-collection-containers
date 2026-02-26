<!-- BEGIN_ANSIBLE_DOCS -->
# Ansible Role: calopsys.containers.podman
Version: 1.0.0

This role deploys a rootless podman base on a Debian system

Tags: system, linux, containers, podman, rootless

## Requirements

| Platform | Versions |
| -------- | -------- |
| Debian | trixie |

## Role Arguments


### Entrypoint: main

Installs and configures the podman rootless base on a Debian system.

|Option|Description|Type|Required|Default|
|---|---|---|---|---|
| calopsys_podman_unprivileged_port_start | Port number to pass to sysctl net.ipv4.ip_unprivileged_port. | str | no |  |
| calopsys_podman_user | The unix user that will be configured to manage the podman rootless containers. | str | yes |  |
| calopsys_podman_group | The unix group of calopsys_podman_user. | str | no | {{ calopsys_podman_user }} |
| calopsys_podman_home | The home of calopsys_podman_user. | str | no | /opt/{{ calopsys_podman_user }} |
| calopsys_podman_uid | A custom UID for calopsys_podman_user. | int | no |  |
| calopsys_podman_gid | A custom GID for calopsys_podman_group. | int | no |  |
| calopsys_podman_containers_config_template | Local path to the template for the containers.conf configuration file. This file will be put under calopsys_podman_user homedir. | str | no | containers.conf.j2 |
| calopsys_podman_tz | Sets the default timezone for all containers, in the default containers.conf template. | str | no | UTC |
| calopsys_podman_registries | List of container registries to connect to podman user onto. | list of 'dict' | no |  |
| calopsys_podman_registries_config_template | The ansible template for registries.conf. See https://github.com/containers/image/blob/main/docs/containers-registries.conf.5.md | str | no |  |
| calopsys_podman_application_name | The name of the application to deploy. This is used mainly for the systemd unit filename and the default application_dir. | str | no |  |
| calopsys_podman_application_dir | The base directory to deploy the application compose to. | str | no | {{ calopsys_podman_home }}/{{ calopsys_podman_application_name }} |
| calopsys_podman_application_dir_mode | The permissions to apply to the base directory to deploy the application compose to. | str | no | 0750 |
| calopsys_podman_application_compose_template | Local path to the docker compose template for the application. | str | no |  |
| calopsys_podman_application_sdnotify | Configures podman to send a systemd-notify to the systemd unit either when the container is started or when the container is healthy. Our default is `healthy`, which means we have to configure a healthcheck for every service of every compose file. See https://docs.podman.io/en/stable/markdown/podman-run.1.html#sdnotify-container-conmon-healthy-ignore | str | no | healthy |



## Dependencies
None.

## Example Playbook

```
- hosts: all
  tasks:
    - name: Importing role: calopsys.containers.podman
      ansible.builtin.import_role:
        name: calopsys.containers.podman
      vars:
        calopsys_podman_user: # required, type: str
```

## License

MIT

## Author and Project Information
Calopsys @ Calopsys

Issues: [tracker](https://github.com/calopsys/ansible-collection-containers/issues)
<!-- END_ANSIBLE_DOCS -->
