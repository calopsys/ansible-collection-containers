<!-- BEGIN_ANSIBLE_DOCS -->
# Ansible Role: calopsys.containers.docker
Version: 1.1.0

This role installs, manages and configures the Docker daemon on Debian systems.


## Requirements

| Platform | Versions |
| -------- | -------- |

## Role Arguments


### Entrypoint: main

Install and configure a Docker instance on Debian systems.

|Option|Description|Type|Required|Default|
|---|---|---|---|---|
| calopsys_docker_config_daemon_template | Local path to custom Docker daemon template configuration file | str | no |  |
| calopsys_docker_compose_workdir | Working directory of the compose application. | str | no | /opt/compose |
| calopsys_docker_compose_template | Local path to the Docker compose template file. | str | no |  |
| calopsys_docker_compose_wait_timeout | The amount of seconds to wait for services to be running/healthy. | int | no | 300 |



## Dependencies
None.

## Example Playbook

```
- hosts: all
  tasks:
    - name: Importing role: calopsys.containers.docker
      ansible.builtin.import_role:
        name: calopsys.containers.docker
      vars:
```

## License

MIT

## Author and Project Information
Calopsys @ Calopsys

Issues: [tracker](https://github.com/calopsys/ansible-collection-containers/issues)
<!-- END_ANSIBLE_DOCS -->
