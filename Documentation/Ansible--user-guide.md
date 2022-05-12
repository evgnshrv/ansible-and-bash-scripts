# Ansible User Guide

# Table of Contents
- [Ansible concepts](#ansible-concepts)
- [Installing Ansible](#installing-ansible)
- [Ansible ad hoc commands](#ansible-ad-hoc-commands)
- [Ansible Playbooks](#ansible-playbooks)

## Ansible concepts

**Control node** — any machine with Ansible installed.

**Managed nodes** — the network devices (and/or servers) you manage with Ansible. Managed nodes are also sometimes called “hosts”.

**Inventory** — a list of managed nodes. An inventory file is also sometimes called a “hostfile”.

**Collections** — collections are a distribution format for Ansible content that can include playbooks, roles, modules, and plugins.

**Modules** — the units of code Ansible executes. Each module has a particular use. You can invoke a single module with a task, or invoke several different modules in a playbook. Starting in Ansible 2.10, modules are grouped in collections.

**Tasks** — the units of action in Ansible. You can execute a single task once with an ad hoc command.

**Ad-hoc command** — a simple one-off task.

**Playbooks** — ordered lists of tasks, saved so you can run those tasks in that order repeatedly. Playbooks can include variables as well as tasks. Playbooks are written in YAML.

## Installing Ansible

[Installing Ansible](https://docs.ansible.com/ansible/latest/installation_guide/)

## Ansible ad hoc commands

An Ansible ad hoc command uses the /usr/bin/ansible command-line tool to automate a single task on one or more managed nodes. Ad hoc commands are great for tasks you repeat rarely.

**Usage:** ansible <host-pattern> [-f forks] [-m module_name] [-a args]

**Use cases for ad hoc tasks:**  
	- **rebooting servers:** ansible <Name-of-server-group> -a "/sbin/reboot"  
	- **managing files (copy):** ansible <Name-of-server-group> -m ansible.builtin.copy -a "src=/path/to/file dest=/path/to/file"  
	- **managing files (change permissions and owner):** ansible <Name-of-server-group> -m ansible.builtin.file -a "dest=/path/to/file mode=600 owner=user1 group=group1"  
	- **managing packages (ensure a package is installed without updating it):** ansible <Name-of-server-group> -m ansible.builtin.yum -a "name=<Package-name> state=present"  
	- **managing packages (ensure a package is at the latest version):** ansible <Name-of-server-group> -m ansible.builtin.yum -a "name=<Package-name> state=latest"  
	- **managing users and groups (change password):** ansible <Name-of-server-group> -m user -a "name=<User-name> update_password=always password={{ newpassword|password_hash('sha512') }}" -b --extra-vars "newpassword=<User-password>"  
	- **gathering facts:** ansible <Name-of-server-group> -m ansible.builtin.setup

## Ansible Playbooks 

Playbooks record and execute Ansible’s configuration, deployment, and orchestration functions. They can describe a policy you want your remote systems to enforce, or a set of steps in a general IT process.