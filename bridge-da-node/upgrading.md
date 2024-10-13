---
icon: arrow-up-from-line
---

# Upgrading

To keep your Celestia Bridge node up to date with the latest features and network changes, you can quickly upgrade the node using the provided Ansible playbook. This method allows you to easily manage upgrades across one or more bridge nodes with minimal effort.

***

#### **Step 1: Update the Version in the Playbook**

Before executing the playbook, ensure that the `bridge_version` variable in your Ansible playbook is set to the latest version of the Celestia bridge node. You can update this in the playbook:

```yaml
vars:
  bridge_version: "v0.16.0"  # Update to the latest version
```

Refer to the [Celestia GitHub repository](https://github.com/celestiaorg/celestia-node) for the latest version number.

***

#### **Step 2: Run the Upgrade Playbook**

After updating the version, execute the Ansible playbook to upgrade your bridge node.

Use the following command to run the playbook:

```bash
ansible-playbook -i hosts.ini playbooks/upgrade_bridge.yml -l bridge-node-servers
```

#### **Explanation of the Command:**

**`-i hosts.ini`**: This specifies the inventory file where your server(s) are listed.

**`playbooks/upgrade_bridge.yml`**: The playbook file that handles the upgrade process for the bridge node.

**`-l bridge-node-servers`**: This limits the playbook execution to the group or host (in this case, bridge-node-servers) defined in your inventory file.

***

#### **Step 3: Verify the Upgrade**

After the playbook completes, verify that your bridge node has been upgraded and is running the correct version. You can check the status of the service with the following command:

```bash
sudo systemctl status celestia-bridge
```

You can also confirm the version of the running Celestia Bridge node:

```bash
celestia bridge version
```

This should match the version you set in the playbook.
