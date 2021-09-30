morpheus_initial_setup
=========================

This Role will complete a initial setup of the Main tenant in morpheus. 
This is the base tenant that everything spawns from. Role uses ansible vault for sensitve 
variables.

### Requirements
Network connectivity to the morpheus API is needed.

### Tasks

| Task Number | Tasks Play | Action | Description                                                                                              |
|:------------|:-----------|:-------|:---------------------------------------------------------------------------------------------------------|
| 1           | gate.yml   |        |                                                                                                          |
| 1.1         |            | uri    | URL access check                                                                                         |
| 1.2         |            | assert | Fail if code can not reach the URL and report that it was not reachable if it is reachable let user know |
| 2           | main.yml   |        |                                                                                                          |
| 2.1 | | include | Include gate for testing |
| 2.2 | | include | Include debug using tag degbug |
| 2.3 | | include | Include initial setup using tag initial | 
| 3.0 | debug.yml | | Used to debug role setting |
| 3.1 | | debug | Print message about ping check on the URL using tag debug |
| 4.0 | initial_setup.yml | |
| 4.1 | | uri | Create the main tenant to start with in morpheus | 


### Global Variables

| Variable | Default Value | Description | Required |
|:---------|:--------------|:------------|:---------|
|          |               |             |          |

### Role Variables

| Variable   | Default Value | Description                                                    | Required |
|:-----------|:--------------|:---------------------------------------------------------------|:---------|
| domain     |               | Domain for morpheus url                                        | Y        |
| m_base_url |               | Uses ansible hostname to build the url along with the domain   | Y        |
| m_password |               | Default password for user that is created during initial setup | Y        |

### Extra Variables

| Variable | Default Value | Description | Required |
|:---------|:--------------|:------------|:---------|
|          |               |             |          |

### Registered Variables

| Variable | Default Value | Description | Required |
|:---------|:--------------|:------------|:---------|
| ping_chk        |               | Check for url access to morpheus             |          |

### Ansible Facts

| Fact | Description |
|:-----|:------------|
| ansible_hostname     | Hostname of machine            |

### Dependencies

* None

### Example Playbook
```
- name: Install Morpheus
  hosts: all
  become: true
  pre_tasks:
    - name: include global_vars.yml
      include_vars: ./vars/global_vars.yml

    - name: Get packages
      package_facts:

  tasks:
    - name: Morpheus initial setup
      include_role:
        name: morpheus_initial_setup
        apply:
          tags:
            - initial
      tags: 
        - initial
        - debug

    - name: Morpheus tenant setup
      include_role:
        name: morpheus_tenant_create
        apply:
          tags:
            - tenant
      tags:
        - tenant
        - debug
```

### Ansible Base Command Line
```
ansible-playbook -i <Morpheus Machine>, setup_morpheus.yml -u <user with root> -bk --tags intial,debug --ask-vault-password
```


### License

GPLv3 or later

### Author Information

|         |           |
|:--------|:----------|
| Contact | Todd A. Kearney          |
| Email   | mailto://todd.kearney8424@gmail.com |
| Version | 0.0.2          |