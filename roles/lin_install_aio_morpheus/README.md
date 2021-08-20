lin_install_aio_morpheus
=========================

This ansible role will deploy Morpheus All in one Appliance on several type of major OS's.

### Requirements
OS's currently supported"
  * CentOS
  * RedHat
  * Ubuntu

### Tasks

| Task Number | Tasks Play       | Description                                |
|:------------|:-----------------|:-------------------------------------------|
| 1           | gate.yml         | Run testing on the machine                 |
| 1.1         | assert           | Test for OS version                        |
| 1.2         | set_fact         | Set fact to list space available on /opt   |
| 1.3         | assert           | fail if there is not at least 5GB for /opt |
| 2           | main.yml         | Install Morpheus App                       |
| 3           | Block for RHEL   | Steps for RHEL variants                    |
| 3.1         | get_url          | Download the rpm                           |
| 3.2         | yum              | Install the local rpm                      |
| 4           | Block for Debian | Step for Debian variants                   |
| 4.1         | get_url          | Download the .deb                          |
| 4.2         | apt              | Install the local deb                      |
| 5           | command          | Run Morpheus reconfigure                   |
| 6           | debug            | Output stdout_lines from the reconfigure   |


### Global Variables

| Variable | Default Value | Description | Required |
|:---------|:--------------|:------------|:---------|
|          |               |             |          |

### Role Variables

| Variable  | Default Value | Description              | Required |
|:----------|:--------------|:-------------------------|:---------|
| m_release | 5.3.2-1       | Morpheus release version | yes      |

### Extra Variables

| Variable | Default Value | Description | Required |
|:---------|:--------------|:------------|:---------|
|          |               |             |          |

### Registered Variables

| Variable         | Default Value | Description                                 | Required |
|:-----------------|:--------------|:--------------------------------------------|:---------|
| opt_avail        | N/A           | Store the availabe size left in /opt        |          |
| morph_config_out |               | Used to store the output of the reconfigure | N/A      |

### Ansible Facts

| Fact                               | Description    |
|:-----------------------------------|:---------------|
| ansible_distribution_major_version | version number |
| ansible_distribution               | Linux Version  |

### Dependencies

* Machine where this Appliance will be installed must have internet access.

### Example Playbook
```
- name: Install Moprheus Full HA
  hosts: all
  become: True
  pre_tasks:
    - name: include global_vars.yml
      include_vars: ./vars/global_vars.yml

    - name: Get packages
      package_facts:
      
  tasks:
    - name: Install full HA environment
      include_role: 
        name: lin_install_aio_morpheus
```
### Ansible Base Command Line

* ansible-playbook -i machinename, lin_install_aio_morpheus.yml -u username -k

### Ansible AWX

* n/a

### Morpheus 

* n/a

### License

N/A

### Author Information

|         |                 |
|:--------|:----------------|
| Contact | Todd A. Kearney |
| Email   | mailto://       |
| Version | 0.1             |