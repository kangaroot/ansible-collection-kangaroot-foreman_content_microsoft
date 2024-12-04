# Ansible collection: kangaroot.foreman_content_microsoft

Collection for configuring Microsoft repositories in a Foreman/Katello installation.

The Microsoft repositories that can be configured from this collection are:

- Azure CLI[^1]:
  - EL (rpm OS)[^2]
  - Debian 9 (Stretch)
  - Debian 10 (Buster)
  - Debian 11 (Bullseye)
  - Debian 12 (Bookworm)
  - Ubuntu 20.04 (Focal Fossa)
  - Ubuntu 22.04 (Jammy Jellyfish)
  - Ubuntu 24.04 (Noble Numbat)

- Edge[^1]:
  - EL (rpm OS)[^2]
  - Debian/Ubuntu

- Visual Studio Code[^1]:
  - EL (rpm OS)[^2]
  - Debian/Ubuntu

- Microsoft Linux Software Repository - PROD[^1]:
  - RHEL 7
  - RHEL 8[^2]
  - RHEL 9[^2]
  - Debian 9 (Stretch)
  - Debian 10 (Buster)
  - Debian 11 (Bullseye)
  - Debian 12 (Bookworm)
  - Ubuntu 20.04 (Focal Fossa)
  - Ubuntu 22.04 (Jammy Jellyfish)
  - Ubuntu 24.04 (Noble Numbat)

- Microsoft SQL Server 2017:
  - RHEL 7
  - RHEL 8
  - Ubuntu 18.04 (Bionic Beaver)

- Microsoft SQL Server 2019:
  - RHEL 7
  - RHEL 8
  - Ubuntu 20.04 (Focal Fossa)

- Microsoft SQL Server 2022:
  - RHEL 8
  - RHEL 9
  - Ubuntu 20.04 (Focal Fossa)
  - Ubuntu 22.04 (Jammy Jellyfish)

- Microsoft SQL Server 2025:
  - RHEL 9
  - Ubuntu 22.04 (Jammy Jellyfish)

[^1]: Enabled by default when enabling Microsoft repositories.
[^2]: Enabled by default when enabling a specific Microsoft product repository.

## Requirements and Dependencies

Ansible Core 2.13.0 or higher is required for the roles in the collection.

The roles in this collection must be imported by the `kangaroot.foreman` collection. It is possible to directly use the roles in this collection but not recommended.

The `kangaroot.foreman` collection requires the `theforeman.foreman` and `theforeman.operations` collections. To install the required collections, execute:

```shell
ansible-galaxy collection install -r requirements.yml
```

in the collection directory.

## Collection Variables

The `group_vars` directory contains example vars files for the important variables used in the collection roles.

## Usage

The variable `foreman_content_roles` from the `foreman` role in the `kangaroot.foreman` collection contains a list content roles to import.

Add this collection content role to the `foreman_content_roles` list of content roles to import in your playbook project variables.

For example, add the `foreman_content_roles` variable in your `group_vars/foreman.yml` file of your playbook project:

```yaml
# Foreman content roles to include
foreman_content_roles:
  # Package only content
  - kangaroot.foreman_content_microsoft.foreman_content_microsoft
  - ...

  # OS content
  - kangaroot.foreman_content_rocky.foreman_content_rocky
  - ...

  # Builtin content
  - kangaroot.foreman_content_builtin.foreman_content_builtin
```

Also ensure that the Microsoft repositories are enabled and at least one of the available Microsoft product and/or OS related repositories is enabled as well by setting the appropriate enable variables:

```yaml
foreman_enable_microsoft: true
foreman_enable_microsoft_azure_cli: false
foreman_enable_microsoft_edge: false
# foreman_enable_microsoft_vscode: "{{ foreman_enable_microsoft | bool }}"
# foreman_enable_microsoft_prod: "{{ foreman_enable_microsoft | bool }}"
# foreman_enable_microsoft_prod_el8: "{{ foreman_enable_microsoft_prod | bool }}"
# foreman_enable_microsoft_prod_el9: "{{ foreman_enable_microsoft_prod | bool }}"
# foreman_enable_microsoft_mssql_server_2017: false
# foreman_enable_microsoft_mssql_server_2019: false
# foreman_enable_microsoft_mssql_server_2022: false
# foreman_enable_microsoft_mssql_server_2025: false
```

In your playbook, add a task to execute the `kangaroot.foreman.foreman` role:

```yaml
- name: Run kangaroot.foreman roles
  hosts: foreman
  roles:
    - kangaroot.foreman.foreman
```

