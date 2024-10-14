# Quick Start

Memory updated

Here’s a quick start guide incorporating both the Autonity and Oracle node setup, as requested:

***

## Quickstart Guide for Autonity and Oracle Nodes

This guide will walk you through setting up both the Autonity and Oracle nodes using Ansible playbooks.

***

### **1. Prerequisites**

Before you begin, ensure your system meets the following requirements:

#### **Hardware Requirements**

**Autonity Node:**

* 8 CPU Cores
* 16GB RAM
* 500GB SSD/NVMe storage (recommended)

**Oracle Node:**

* 8 CPU Cores
* 16GB RAM
* 500GB SSD/NVMe storage (recommended)

#### **Operating System**

* Ubuntu 20.04 or later

#### **Software Requirements**

* Ansible installed on your local machine
* SSH access to the target servers (password login should be disabled for security)

***

#### **2. Installation and Setup**

**Step 1: Install Ansible**

If you haven't installed Ansible yet, use the following command on your local machine:

```bash
bashCopy codesudo apt update
sudo apt install ansible
```

**Step 2: Clone the Ansible Playbooks Repository**

Clone the repository that contains the Ansible playbooks for setting up Autonity and Oracle nodes:

```bash
bashCopy codegit clone https://github.com/yourrepo/autonity-oracle-ansible-playbooks.git
cd autonity-oracle-ansible-playbooks
```

**Step 3: Configure the Ansible Hosts File**

Edit the `hosts.ini` file to reflect your server details. Example:

```ini
iniCopy code[autonity-node]
autonity-server ansible_host=203.189.67.106 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa

[oracle-node]
oracle-server ansible_host=203.189.67.107 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa
```

Replace `ansible_host` and `ansible_user` with your actual server IP addresses and usernames.

***

#### **3. Setting Up Nodes**

**Step 1: Run the Autonity Node Playbook**

To set up the Autonity node, use the following command:

```bash
bashCopy codeansible-playbook -i hosts.ini playbooks/install_autonity.yml -l autonity-node
```

This playbook will install the required dependencies, Go, build Autonity, and configure it as a SystemD service.

**Step 2: Run the Oracle Node Playbook**

To set up the Oracle node, use this command:

```bash
bashCopy codeansible-playbook -i hosts.ini playbooks/install_oracle.yml -l oracle-node
```

This will install the Oracle node software and configure it accordingly.
