# Nutanix Role for Prism Element storage container create/update

This Ansible role will create or update storage containers on a Nutanix Prism cluster. It can also remove the default container created during the clusters creation.

## Input Variables

| Variable                                      | Required | Default | Choices                                                                         | Comments                                                                                                                                           |
|-----------------------------------------------|----------|---------|---------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| role_nutanix_pe_container_host                | yes      |         |                                                                                 | The IP address or FQDN for the Prism (Element only) to which you want to connect.                                                                  |
| role_nutanix_pe_container_host_username       | yes      |         |                                                                                 | A valid username with appropriate rights to access the Nutanix API.                                                                                |
| role_nutanix_pe_container_host_password       | yes      |         |                                                                                 | A valid password for the supplied username.                                                                                                        |
| role_nutanix_pe_container_host_port           | no       | 9440    |                                                                                 | The Prism TCP port.                                                                                                                                |
| role_nutanix_pe_container_host_validate_certs | no       | false   | true or false                                                                   | Whether to check if Prism UI certificates are valid.                                                                                               |
| role_nutanix_pe_container_debug               | no       | false   | true or false                                                                   | Enable debugging output.                                                                                                                           |
| role_nutanix_pe_container_remove_default      | no       | true    | true or false                                                                   | If set to True the default container will be removed if it exists.                                                                                 |
| role_nutanix_pe_container_list                | no       | []      |                                                                                 | List of containers. For container dict keys see table below.                                                                                       |

### Container dict

| Variable                           | Required | Default | Choices                                                                         | Comments                                                                                                                                           |
|------------------------------------|----------|---------|---------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| name                               | yes      |         |                                                                                 |                                                                                                                                                    |
| state                              | yes      |         | present / absent                                                                |                                                                                                                                    |
| rf                                 | no       | 2       | 1, 2 or 3                                                                       |                                                                                                                                                    |
| compression                        | no       | false   | true or false                                                                   |                                                                                                                                                    |
| compression_delay_in_secs          | no       | 0       |                                                                                 | 0 = inline compression.                                                                                                                            |
| dedupe_cache                       | no       | false   | true / false                                                                    |                                                                                                                                                     |
| dedupe_capacity                    | no       | false   | true / false                                                                    |                                                                                                                                                     |
| erasure_coding                     | no       | false   | true / false                                                                    |                                                                                                                                                     |

## Dependencies

- grdavies.role_nutanix_prism_api

## Example Playbook

```YAML
- hosts: localhost
  gather_facts: false
  roles:
    - role: grdavies.role_nutanix_pe_container
  vars:
    role_nutanix_pe_container_host: 10.38.67.37
    role_nutanix_pe_container_host_username: admin
    role_nutanix_pe_container_host_password: nx2Tech454!
    prism_containers_list:
      - name: example
        state: present
        rf: 2
        compression: True
        compression_delay_in_secs: 0
        dedupe_cache: False
        dedupe_capacity: False
        erasure_coding: False
      - name: example_2
        state: present
        rf: 2
        compression: True
        compression_delay_in_secs: 60
        dedupe_cache: True
        dedupe_capacity: True
        erasure_coding: False
```

## License

See LICENSE.md

## Author Information

Ross Davies
