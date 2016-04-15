# Ansible Role: cloudstack-management

Ansible role that Install Apache Cloudstack Management.

## Requirements

None

## Role Variables

### `defaults/main.yml`

* `cloudstack_master: false`
* `cloudstack_node: false`
* `cloudstack_usage: false`
* `cloudstack_mysql_host: "127.0.0.1"`
* `cloudstack_mysql_port: 3306`
* `cloudstack_mysql_user: "cloud"`
* `cloudstack_mysql_password: "cloud"`
* `cloudstack_mysql_root_password: "password"`

* `cloudstack_templates_url: "http://127.0.0.1/cloudstack/systemvm"`
* `cloudstack_seckey: "password"`
* `cloudstack_nfs_mount_path: "/mnt/secondary"`
* `cloudstack_nfs_export_ip: "127.0.0.1"`
* `cloudstack_nfs_export_path: "/data/secondary"`
* `cloudstack_tmplt_diskspace: 5120000`
    - 如果管理端系统分区小于5120000 kilobytes,需要修改此参数.

* `cloudstack_systemvm_vmware:`
    ```
      enable: false
      template_name: "systemvm64template-4.4.1-7-vmware.ova"
    ```

* `cloudstack_systemvm_kvm:`
    ```
      enable: false
      template_name: "systemvm64template-4.4.1-7-kvm.qcow2.bz2"
    ```

## Dependencies

- cloudstack-common

## Example Playbook

    - name: Install Cloudstack Management master
      hosts: servers
      vars:
        cloudstack_repo: "http://cloudstack.apt-get.eu/centos"
        cloudstack_ver: "4.4"
        cloudstack_master: true
        cloudstack_usage: true
        cloudstack_mysql_host: "127.0.0.1"
        cloudstack_mysql_port: 3306
        cloudstack_mysql_user: "cloud"
        cloudstack_mysql_password: "cloud"
        cloudstack_mysql_root_password: "password"
        cloudstack_templates_url: http://cloudstack.apt-get.eu/systemvm/4.4"
        cloudstack_seckey: "password"
        cloudstack_nfs_export_ip: "127.0.0.1"
        cloudstack_nfs_export_path: "/data/secondary"
        cloudstack_tmplt_diskspace: 1020000
        cloudstack_systemvm_kvm:
          enable: true
          template_name: "systemvm64template-4.4.1-7-kvm.qcow2.bz2"
      roles:
        - cloudstack-common
        - cloudstack-management

    - name: Install Cloudstack Management node
      hosts: servers
      vars:
        cloudstack_repo: "http://cloudstack.apt-get.eu/centos"
        cloudstack_ver: "4.4"
        cloudstack_node: true
        cloudstack_mysql_host: "127.0.0.1"
        cloudstack_mysql_port: 3306
        cloudstack_mysql_user: "cloud"
        cloudstack_mysql_password: "cloud"
      roles:
        - cloudstack-common
        - cloudstack-management

## License

MIT / BSD

## Author Information

z@zstack.net
