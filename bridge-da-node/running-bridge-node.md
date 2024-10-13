---
icon: binary-circle-check
---

# Running Bridge Node

***

After installing the bridge node binary using the [Ansible playbook from the Quick Start guide](../getting-started/quickstart.md), you can now proceed with setting up and running your Celestia Bridge node. This guide walks you through connecting the bridge node to a validator, syncing with an archival RPC node, and checking sync status.

### **1: Initialize the Bridge Node**

Before starting the bridge node, it needs to be configured and initialized to connect with your validator.

#### **Configure and Initialize the Bridge Node:**

```sh
celestia bridge init --core.ip <RPC_NODE_IP> --p2p.network mocha
```

**`<RPC_NODE_IP>`**: This needs to be the IP of an archival RPC node. The bridge node requires an archival node to sync from block zero up to the current block height. This process may take several days or even weeks depending on the node's performance and network speed.

For more detailed information on the bridge node, you can refer to the official [Celestia Bridge Node documentation](https://docs.celestia.org/nodes/bridge-node).

***

### **2: Restore the Existing Key**

If you already have a key that was used on a previous bridge node, you can restore it to the new node setup.

#### **Restore Your Key:**

```sh
KEY_NAME="my_celes_key"
cd ~/celestia-node
./cel-key add $KEY_NAME --keyring-backend test --node.type bridge --recover --p2p.network mocha
```

**`$KEY_NAME`**: This should be the name of your existing key that you are restoring. Ensure you have the mnemonic phrase ready for this process.

**`--recover`**: This flag is used to recover an existing key using the mnemonic phrase.

**Start Bridge Node**

```sh
sudo systemctl restart celestia-bridge && sudo journalctl -u celestia-bridge -f
```

***

### **3: Check the Bridge Node Sync Status**

Once the bridge node is initialized and connected, it will begin syncing from the archival node. You can monitor the sync progress using the following command:

#### **Check Bridge Node Sync Status:**

```shell
celestia header sync-state --node.store ~/.celestia-bridge-mocha-4/
```

This command will provide you with the current sync status, allowing you to monitor how far along your bridge node is in the syncing process.
