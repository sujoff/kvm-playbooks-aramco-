# Ansible Playbook for Cockpit and KVM Installation

This repository contains Ansible playbooks for installing Cockpit with `cockpit-machines` on five Linux hosts. The playbooks ensure the removal of any existing KVM installation before performing a fresh installation of KVM, Cockpit, and Cockpit Machines.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Host Configuration](#host-configuration)
- [Ansible Playbooks](#ansible-playbooks)
- [Using Ansible Vault](#using-ansible-vault)
- [Deployment](#deployment)

## Prerequisites
- **Ansible** installed on the control node.
- **SSH access** to target hosts with necessary privileges.
- **Python3** installed on target hosts.
- **`ansible-vault`** configured for securely passing credentials.

## Host Configuration
Define your target Linux hosts in `/etc/ansible/hosts` as follows:

```ini
[linux]
192.168.8.150 ansible_user=<user> ansible_password=<password> ansible_python_interpreter=/usr/bin/python3 ansible_ssh_common_args='-o StrictHostKeyChecking=no' ansible_port=<ssh_port>
192.168.8.151 ansible_user=<user> ansible_password=<password> ansible_python_interpreter=/usr/bin/python3 ansible_ssh_common_args='-o StrictHostKeyChecking=no' ansible_port=<ssh_port>
192.168.8.152 ansible_user=<user> ansible_password=<password> ansible_python_interpreter=/usr/bin/python3 ansible_ssh_common_args='-o StrictHostKeyChecking=no' ansible_port=<ssh_port>
192.168.8.153 ansible_user=<user> ansible_password=<password> ansible_python_interpreter=/usr/bin/python3 ansible_ssh_common_args='-o StrictHostKeyChecking=no' ansible_port=<ssh_port>
192.168.8.154 ansible_user=<user> ansible_password=<password> ansible_python_interpreter=/usr/bin/python3 ansible_ssh_common_args='-o StrictHostKeyChecking=no' ansible_port=<ssh_port>
```
> **Note:** Replace `<user>`, `<password>`, and `<ssh_port>` with actual values. If the SSH port is unchanged, remove the `ansible_port` parameter.

## Ansible Playbooks
This repository includes two playbooks:
1. **SSH Port Change Playbook**: Modifies the SSH port on target hosts.
2. **Deployment Playbook**: Installs KVM, Cockpit, and `cockpit-machines` after removing existing KVM installations.

## Using Ansible Vault
Ansible Vault is used to securely channel, store and manage sensitive information like root passwords.

To create a secure vault file for the root password, use:
```sh
ansible-vault create sudo_pass.yml
```
Add the vault file as a variable in your playbook:
```yaml
vars_files:
    - sudo_pass.yml
```

## Deployment
To execute the playbooks, run:
```sh
ansible-playbook -i /etc/ansible/hosts sshchangeport.yml --ask-vault-pass #If required, run it.
ansible-playbook -i /etc/ansible/hosts cockpit-kvm.yml --ask-vault-pass
```
Now, you're good to go.

---

💡 **Happy Deployment!** 🚀