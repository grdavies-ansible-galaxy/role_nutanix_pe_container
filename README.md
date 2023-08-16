# Nutanix Role for Prism Element storage container create/update

This Ansible role will create or update storage containers on a Nutanix Prism cluster. It can also remove the default container created during the clusters creation.


## Role Variables

| Variable                           | Required | Default | Choices                                                                         | Comments                                                                                                                                           |
|------------------------------------|----------|---------|---------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| nutanix_host                       | yes      |         |                                                                                 | The IP address or FQDN for the Prism (Element only) to which you want to connect.                                                                  |
| nutanix_username                   | yes      |         |                                                                                 | A valid username with appropriate rights to access the Nutanix API.                                                                                |
| nutanix_password                   | yes      |         |                                                                                 | A valid password for the supplied username.                                                                                                        |
| nutanix_port                       | no       | 9440    |                                                                                 | The Prism TCP port.                                                                                                                                |
| validate_certs                     | no       | no      | yes / no                                                                        | Whether to check if Prism UI certificates are valid.                                                                                               |
| nutanix_containers_remove_default  | no       | True    | True or False                                                                   | If set to True the default container will be removed if it exists.                                                                                 |
| nutanix_containers_list            | no       | []      |                                                                                 | List of containers. For container dict keys see table below.                                                                                       |

### Container dict
| Variable                           | Required | Default | Choices                                                                         | Comments                                                                                                                                           |
|------------------------------------|----------|---------|---------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| name                               | yes      |         |                                                                                 |                                                                                                                                                    |
| state                              | yes      |         | present / absent                                                                                |                                                                                                                                    |
| rf                                 | no       | 2       | 2 or 3                                                                          |                                                                                                                                                    |
| compression                        | no       | False   | True or False                                                                   |                                                                                                                                                    |
| compression_delay_in_secs          | no       | 0       |                                                                                 | 0 = inline compression.                                                                                                                            |
| dedupe_cache                       | no       | False   | True / False                                                                   |                                                                                                                                                     |
| dedupe_capacity                    | no       | False   | True / False                                                                   |                                                                                                                                                     |
| erasure_coding                     | no       | False   | True / False                                                                   |                                                                                                                                                     |


## Dependencies

NA

## Example Playbook

```
- hosts: localhost
  gather_facts: false
  roles:
    - role: grdavies.role_nutanix_pe_container
  vars:
    nutanix_host: 10.38.185.37
    nutanix_username: admin
    nutanix_password: nx2Tech165!
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
