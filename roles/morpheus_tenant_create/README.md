create_tenant
=========================

This role will create a tenant with morpheus. The role also creates default groups for production and non-production resources for both VMware and Azure cloud types. 

### Requirements
This role will need to be run by a user with access rights to create tenants and groups.
Role should be run directly on the morpheus server. 

### Tasks
| Task Number | Tasks Play        | Action        | Description                                                                                   |
|:------------|:------------------|:--------------|:----------------------------------------------------------------------------------------------|
| 1           | gate.yml          |               |                                                                                               |
| 1.1         |                   | uri           | Test to make sure that morpheus is reachable.                                                 |
| 1.2         |                   | assert        | If the website is not reachable fail and report status if it was reachable report and move on |
| 2           | main.yml          |               |                                                                                               |
| 2.1         |                   | include_tasks | Include the gate with tag always.                                                             |
| 2.2         |                   | include_tasks | Include debug with tag debug.                                                                 |
| 2.3         |                   | include tasks | Include create_tenant with tag tenant.                                                        |
| 3.0         | debug.yml         |               |                                                                                               |
| 3.1         |                   | debug         | Print Debug msg from gate ping_chk.                                                           |
| 4.0         | create_tenant.yml |               |                                                                                               |
| 4.1         |                   | uri           | POST Get the access token for the user.                                                       |
| 4.2         |                   | uri           | POST Create Tenant using variables.                                                           |
| 4.3         |                   | debug         | Print status of tenant createion.                                                             |
| 4.4         |                   | uri           | POST build the default groups for Production resources and Non-production resources.          |
| 4.5         |                   | uri           | POST Assign the Default AD source for the tenant.                                             |

### Global Variables

| Variable | Default Value | Description | Required |
|:---------|:--------------|:------------|:---------|
|          |               |             |          |

### Role Variables

| Variable    | Default Value               | Description                                                                          | Required |
|:------------|:----------------------------|:-------------------------------------------------------------------------------------|:---------|
| domain      |                             | Domain to be used in connection to AD and url settings.                              |   Y      |
| m_base_url  |                             | URL to access the morpheus API.                                                      |   Y      |
| ad_url      |                             | URL of AD connection used to create a user-source in the API.                        |   Y      |
| ad_password |                             | AD user password for user that has access to read AD.                                |   Y      |
| ad_user     |                             | AD User with read access.                                                            |   Y      |
| m_username  |                             | Morpheus Username that has administrative rights to cerate tenants and user-sources. |   Y      |
| m_password  | Morpheus password for user. |                                                                                      |   Y      |
### Extra Variables

| Variable           | Default Value | Description                                                  | Required |
|:-------------------|:--------------|:-------------------------------------------------------------|:---------|
| tenant_name        |               | Name of tenant, this will be joined with the default domain. |     y    |
| tenant_description |               | Description of tenant purpose                                |     y    |
### Registered Variables

| Variable       | Default Value | Description                                                     | Required |
|:---------------|:--------------|:----------------------------------------------------------------|:---------|
| ping_chk       |               | used to check if morpheus is reachable                          |          |
| login          |               | used to store login information to use token as auth method     |          |
| tenant_results |               | used to store status of creating the tenant                     |          |
| user_source    |               | used to store the status of creating the user source for tenant |          |

### Ansible Facts

| Fact             | Description          |
|:-----------------|:---------------------|
| ansible_hostname | This is the hostname |

### Dependencies

* None

### Example Playbook

### Ansible Base Command Line
```
ansible-playbook -i <morpheus server>, setup_morpheus.yml --tags tenant -e tenant_name=<name> -e tenant_number=<integer> -e tenant_description=<description> -u <user with root access> -bk --ask-vault-password
```

### License

GPLv3 or later

### Author Information

|         |                                     |
|:--------|:------------------------------------|
| Contact | Todd A. Kearney                     |
| Email   | mailto://todd.kearney8424@gmail.com |
| Version | 0.0.3                               |