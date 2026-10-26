<!-- BEGIN_ANSIBLE_DOCS -->
# Ansible Role: calopsys.containers.podman
Version: 1.3.0
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
| calopsys_podman_group | The unix group of calopsys_podman_user. | str | no | `{{ calopsys_podman_user }}` |
| calopsys_podman_home | The home of calopsys_podman_user. | str | no | `/opt/{{ calopsys_podman_user }}` |
| calopsys_podman_uid | A custom UID for calopsys_podman_user. | int | no |  |
| calopsys_podman_gid | A custom GID for calopsys_podman_group. | int | no |  |
| calopsys_podman_containers_config_template | Local path to the template for the containers.conf configuration file. This file will be put under calopsys_podman_user homedir. | str | no | `containers.conf.j2` |
| calopsys_podman_tz | Sets the default timezone for all containers, in the default containers.conf template. | str | no | `UTC` |
| calopsys_podman_compose_version | The Debian package version of podman-compose that the role installs. The role fetches the package from snapshot.debian.org, which keeps every version that entered the Debian archive. Versions 1.5.0 and later exec a `CMD` healthcheck without `/bin/sh`, which images without a shell need. Trixie ships 1.3.0. | str | no | `1.6.0-1` |
| calopsys_podman_compose_deb_url | The URL of a podman-compose Debian package to install instead of the snapshot.debian.org file. Set it with `calopsys_podman_compose_deb_checksum` when the hosts have no access to snapshot.debian.org. The package must have the version `calopsys_podman_compose_version`. | str | no |  |
| calopsys_podman_compose_deb_checksum | The checksum of the package at `calopsys_podman_compose_deb_url`, in the `get_url` format, for example `sha256:<hex>`. Required when `calopsys_podman_compose_deb_url` is set. | str | no |  |
| calopsys_podman_registries | List of container registries to connect to podman user onto. | list of `dict` | no |  |
| calopsys_podman_registries_config_template | The ansible template for registries.conf. See https://github.com/containers/image/blob/main/docs/containers-registries.conf.5.md | str | no |  |
| calopsys_podman_application_name | The name of the application to deploy. This is used mainly for the systemd unit filename and the default application_dir. | str | no |  |
| calopsys_podman_application_dir | The base directory to deploy the application compose to. | str | no | `{{ calopsys_podman_home }}/{{ calopsys_podman_application_name }}` |
| calopsys_podman_application_dir_mode | The permissions to apply to the base directory to deploy the application compose to. | str | no | `0750` |
| calopsys_podman_application_directories | Additional directories for files needed for deployment. Will be used to put `calopsys_podman_application_files` inside. | list of `dict` | no |  |
| calopsys_podman_application_files | Additional files needed for deployment. Could be an env file, a configuration file mounted in the container or anything else. If in a subdirectory, the directory has to be created with `calopsys_podman_application_directories` first | list of `dict` | no |  |
| calopsys_podman_application_compose_template | Local path to the docker compose template for the application. | str | no |  |
| calopsys_podman_application_restart_policy | The restart policy to apply to the systemd unit of the application. | str | no | `on-abnormal` |
| calopsys_podman_application_rollback_enabled | Whether or not to trigger the rollback tasks if the deployment fails. | bool | no | `False` |
| calopsys_podman_application_timeout | The timeout for starting the application compose. | int | no | `300` |

#### Choices for main > calopsys_podman_application_restart_policy

|Choice|
|---|
| no |
| on-success |
| on-failure |
| on-abnormal |
| on-watchdog |
| on-abort |
| always |

## Dependencies

None.

## Example Playbook

```yaml
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
