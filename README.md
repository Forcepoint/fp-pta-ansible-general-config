# general-config

Apply general configuration. Should be on all Ansible hosts.

## Requirements

None

## Role Variables

### REQUIRED

None

### OPTIONAL

* general_config_pip_index_url: The URL for the python index. If omitted, the default as specified by pip is used.
* general_config_pip_cert: The path to the cert for pip to verify the pip index's certificate with.
  If omitted, the default is used as specified by pip. Note that the cert needs to be in PEM format.

## Dependencies

This role is dependent upon the PTA Ansible Role ntp. That role must be included in your requirements file as well.

* ntp

## Example Playbook

    - name: general configuration
      hosts: all
      vars:
        general_config_pip_index_url: https://artifactory.COMPANY.com/artifactory/api/pypi/files.pythonhosted.org/simple
        general_config_pip_cert: /etc/pki/ca-trust/custom/COMPANY.pem
      roles:
        - role: general-config

## License

BSD-3-Clause

## Author Information

Jeremy Cornett <jeremy.cornett@forcepoint.com>
