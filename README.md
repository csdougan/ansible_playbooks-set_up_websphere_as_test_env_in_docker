setup-was-container-dev-environment
=========

This role will create a local WAS development environment using Docker containers, including a containerized instance of Nexus to use
as the source for artifacts.    This uses the inventory file as a source for the ssh ports and containers to initialize.

To use this, define an inventory file as follows -

[jvms:children]
jvm_name_one
jvm_name_two

[jvm_name_one]
host_alias_1  ansible_ssh_host=locahost ansible_ssh_port=2222
host_alias_2  ansible_ssh_host=locahost ansible_ssh_port=2223
host_alias_3  ansible_ssh_host=locahost ansible_ssh_port=2224

[jvm_name_two]
host_alias_4  ansible_ssh_host=locahost ansible_ssh_port=2225
host_alias_5  ansible_ssh_host=locahost ansible_ssh_port=222


Requirements
------------
The creation of a requirements.yml to define which roles and the source repositories are to be used in your ansible project.
Version supports the use of git branches, tags or commit hashes. The contents of the requirements.yml are included in the 
readme files of each role for convenience. Dependencies for each role should be included in the role and therefore do not need
to be included in the requirements.yml file.

Dependencies
------------

Ansible >=2.1 is required (I think, since this supports ansible-galaxy offline)
git (configured to be able to access the repositories)
docker installed on local machine
the following docker images pulled to local machine:
  - cdougan/was_dev_with_profile
  - sonatype/nexus

Usage Example
----------------

To install the role dependencies run:
`ansible-playbook install_roles.yml`

This will run galaxy to install the roles and dependencies it assumes a working git/ansible install.

Cloning this repository to use in another project.

### Cloning this repository
If your code is already tracked by Git then set this repository as your "origin" to push to.
```
git clone https://wtr-wscm-sourcerepo.johnlewis.co.uk/scm/aan/example-playbook.git
mv example-playbook/* new_repo/
cd new_repo/
git remote set-url origin https://wtr-wscm-sourcerepo.johnlewis.co.uk/scm/aan/newrepo.git
git push -u origin master
```
	
Author Information
------------------

craig.dougan@waitrose.co.uk

Troubleshooting
------------------

If ansible-galaxy fails to clone the role try using git clone <repo_url> to see if there's a permission, certificate or git configuration issue.
