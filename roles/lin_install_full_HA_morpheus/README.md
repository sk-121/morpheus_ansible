lin_install_3node_HA_morpheus
=========================

This ansible role will deploy a 3 node HA Morpheus cluster. The goal is to install all parts of morphues to a working state. 

### Requirements
Currently Morpheus requires some network setup for the 3 node install. 
Right now this role will only run on CentOS

### Tasks

| Task Number | Tasks Play | Description |
|:------------|:-----------|:------------|
| 1           | gate.yml   | Run testing on the machine             |
| 2 | centos_perc.yml | Install percona on a CentOS machine |
| 3 | morpheus_db_setup.yml | Run steps to setup the morpheus DB on the percona cluster |
| 4 | centos_rabbit.yml | Install RabbitMQ on CentOS machine |


### Global Variables

| Variable | Default Value | Description | Required |
|:---------|:--------------|:------------|:---------|
|          |               |             |          |

### Role Variables

| Variable | Default Value | Description | Required |
|:---------|:--------------|:------------|:---------|
|          |               |             |          |

### Extra Variables

| Variable | Default Value | Description | Required |
|:---------|:--------------|:------------|:---------|
|          |               |             |          |

### Registered Variables

| Variable | Default Value | Description | Required |
|:---------|:--------------|:------------|:---------|
|          |               |             |          |

### Ansible Facts

| Fact | Description |
|:-----|:------------|
|      |             |

### Dependencies

* None

### Example Playbook

### Ansible Base Command Line

### Ansible AWX

### Morpheus 

### License

N/A

### Author Information

|         |           |
|:--------|:----------|
| Contact |           |
| Email   | mailto:// |
| Version |           |