---
description: 'To upgrade your Autonity Validator node, follow the steps below:'
---

# Upgrade the Autonity Validator Node

***

#### **1. Update the Playbook Variables**

Before running the upgrade, edit the Ansible playbook `upgrade-node.yml` to specify the version you want to upgrade to. Update the following variable:

```yaml
vars:
  autonity_version: "v0.14.2"  # Replace with the desired version
```

#### **2. Run the Upgrade Playbook**

Once the version is updated, run the following command to initiate the upgrade:

```bash
ansible-playbook -i hosts.ini upgrade_autonity_validator.yml
```

This will:

* Stop the current validator service.
* Fetch the specified version from the repository.
* Build the new version.
* Replace the existing binary.
* Restart the validator service with the new version.
