# general-config

Apply general configuration. Should be on all Ansible hosts.

For information about PTA and how to use it with this Ansible role please visit https://github.com/Forcepoint/fp-pta-overview/blob/master/README.md

## Requirements

None

## Role Variables

### REQUIRED

None

### OPTIONAL

* general_config_pip_index_url: The URL for the python index. If omitted, the default as specified by pip is used.
* general_config_pip_cert: The path to the cert for pip to verify the pip index's certificate with.
  If omitted, the default is used as specified by pip. Note that the cert needs to be in PEM format.
* general_config_git_lfs_yum_repo_base_url: The base url to use for the Git LFS yum repository.
* general_config_git_lfs_yum_repo_gpg_key: The url to the gpg key for the Git LFS yum repository.
* general_config_git_lfs_yum_repo_sslcacert: The path to the cert for yum to verify SSL connections with the yum repository.
* general_config_git_https_server: The path to a git server to use with the cert provided by sslcainfo.
* general_config_git_sslcainfo: The path to a certificate to verify HTTPS connections with a git server.
* general_config_ca_certs_download: A list of public CA certificates to download and then import into the OS keystore.
* general_config_ca_certs_copy: A list of public CA certificates to copy to the host and then import into the OS keystore.

## Dependencies

This role is dependent upon the PTA Ansible Role ntp. That role must be included in your requirements file as well.

* ntp

## Example Playbook

    - name: general configuration
      hosts: all
      vars:
        general_config_pip_index_url: https://artifactory.COMPANY.com/artifactory/api/pypi/files.pythonhosted.org/simple
        general_config_pip_cert: /etc/pki/ca-trust/custom/COMPANY.pem
        general_config_git_lfs_yum_repo_base_url: "https://artifactory.COMPANY.com/artifactory/packagecloud.io/github/git-lfs/el/{{ ansible_distribution_major_version }}/$basearch"
        general_config_git_lfs_yum_repo_gpg_key: https://artifactory.COMPANY.com/artifactorypackagecloud.io/github/git-lfs/gpgkey
        general_config_git_lfs_yum_repo_sslcacert: /etc/pki/ca-trust/custom/COMPANY.pem
        general_config_git_https_server: https://gitlab.COMPANY.com/
        general_config_git_sslcainfo: /etc/pki/ca-trust/custom/COMPANY.pem
        general_config_ca_certs_download:
          - https://artifactory.COMPANY.com/artifactory/certs/COMPANY.pem
          - https://artifactory.COMPANY.com/artifactory/certs/strange-intermediate-ca.pem
        general_config_ca_certs_copy:
          - files/COMPANY.pem
          - files/strange-intermediate-ca.pem
        ntp_server: ntp.COMPANY.com
      roles:
        - role: general-config

## License

BSD-3-Clause

## Author Information

Jeremy Cornett <jeremy.cornett@forcepoint.com>
