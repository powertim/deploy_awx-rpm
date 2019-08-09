# deploy_awx-rpm
Deploy HA cluster for [AWX-RPM](https://github.com/MrMEEE/awx-build)

<p align="center">
  <img alt="AWX-RPM" src="https://awx.wiki/user/pages/01.blog/logo-updated/awx-rpm-logo.svg">
</p>

## Summary
This playbook is intended to configure a full stack of:
- 1 or more external database server with PostgreSQL 10 (cluster configuration not implemented yet)
- 2 or more (3 as recommended minimum) AWX worker nodes in clustered configuration

## Audience
RHEL7 / CentOS7 system administrators with knowledge of Ansible.

## Inventory
An inventory file must be used with the following structure:
```
[db]
db_server_hostname

[nodes]
awx_worker_node_#1_hostname
awx_worker_node_#2_hostname
awx_worker_node_#3_hostname
```
## Variables
All variables are configurable at the [group_vars](https://github.com/powertim/deploy_awx-rpm/tree/master/group_vars) level:
- **db**:
  - **default_db_disk_mount:** mount point of the disk used for storing PostgreSQL data
  - **db_disk_src:** device used for the disk mounted for storing PostgreSQL data
  - **db_disk_fs_type:** filesystem used for the disk mounted for storing PostgreSQL data
- **nodes**
  - **awx_repo**: name of the Satellite repository which contains [AWX-RPM](https://github.com/MrMEEE/awx-build) binaries
  - **awx_dependencies_repo:** name of the Satellite repository which contains dependencies used by [AWX-RPM](https://github.com/MrMEEE/awx-build) binaries
  - **rabbitmq_repo:** name of the Satellite repository which contains RabbitMQ binaries
  - **erlang_repo:** name of the Satellite repository which contains Erlang binaries used by RabbitMQ
  - **epel_repo:** name of the Satellite repository for EPEL

## Prerequisites
- Ansible 2.7 installed on 1 server as minimum configuration
- Passwordless SSH authentication for 1 user on all nodes

## Execution
```
$ ansible-playbook -i inventory deploy_awx-rpm.yml
```

## Known issues
- Idempotence not fully working
- Re-running the playbook can throw errors (most related to django)

## Contributing
Any help is welcome !
Main milestones are:
- Adaptating for use without Satellite repositories
- Supporting CentOS7 x86_64 (only tested on RHEL7 x86_64 now)
- Improving idempotence

Feel free to submit pull requests on [dev](https://github.com/powertim/deploy_awx-rpm/tree/dev) branch and your ideas to improve this work.

## Reporting issues
All issues can be submitted in the appropriate [section](https://github.com/powertim/deploy_awx-rpm/issues).
I will provide my help as best effort to anyone, so if you want to help me, you're welcome !

## License
[MIT](https://github.com/powertim/deploy_awx-rpm/blob/master/LICENSE)
