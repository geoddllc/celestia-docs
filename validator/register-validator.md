---
icon: registered
---

# Register Validator

This guide walks you through the steps required to register your validator node on the Celestia Mocha-4 testnet. It includes instructions for quick-syncing your node, creating or recovering a wallet, and registering a validator. Additionally, the playbooks for automating these steps are referenced for easier execution.

***

### **1. Quick Sync**

Quick sync downloads the entire data directory from a third-party provider, allowing your node to synchronize faster. This method ensures that your node has all the necessary blockchain data from a snapshot.

#### **Steps for Quick Sync:**

To quick-sync your node from a snapshot, follow these steps manually or run the **Quick Sync Playbook**:

```bash
cd $HOME
rm -rf ~/.celestia-app/data
mkdir -p ~/.celestia-app/data
SNAP_NAME=$(curl -s https://snaps.qubelabs.io/celestia/ | \
    egrep -o ">mocha-4.*tar" | tr -d ">")
aria2c -x 16 -s 16 -o celestia-snap.tar "https://snaps.qubelabs.io/celestia/${SNAP_NAME}"
tar xf celestia-snap.tar -C ~/.celestia-app/data/
```

Alternatively, use the **Quick Sync Playbook** to automate this process:

```bash
ansible-playbook -i hosts.ini playbooks/snapshot_sync.yml -l <target-host>
```

***

### **2. Create or Recover a Wallet**

After syncing, you need to create a wallet or restore an existing one to participate in the network.

#### **Create a New Wallet:**

To create a new wallet, run the following command manually:

```bash
celestia-appd keys add $WALLET
```

{% hint style="info" %}
Don’t forget to save the mnemonic
{% endhint %}

#### **Recover an Existing Wallet:**

To recover an existing wallet using your mnemonic phrase:

```bash
celestia-appd keys add $WALLET --recover
```

#### **Save Wallet and Validator Addresses:**

```bash
WALLET_ADDRESS=$(celestia-appd keys show $WALLET -a)
VALOPER_ADDRESS=$(celestia-appd keys show $WALLET --bech val -a)
echo "export WALLET_ADDRESS=$WALLET_ADDRESS" >> $HOME/.bash_profile
echo "export VALOPER_ADDRESS=$VALOPER_ADDRESS" >> $HOME/.bash_profile
source $HOME/.bash_profile
```

***

### **3. Check Sync Status**

Before proceeding with validator registration, make sure your node is fully synced. Run the following command manually:

```bash
celestia-appd status 2>&1 | jq
```

If your node is fully synced, the output will show `"false"` for `catching_up`.

***

### **4. Fund Your Wallet**

To create a validator, you’ll need to fund your wallet with testnet tokens. You can request tokens in the Celestia Discord channel by providing your wallet address.

Once you have received the testnet tokens, check your balance:

```bash
celestia-appd query bank balances $WALLET_ADDRESS
```

***

### **5. Create a Validator**

Once your wallet is funded and your node is fully synced, you can create a validator by running the following command manually:

```bash
celestia-appd tx staking create-validator \
--amount 1000000utia \
--from $WALLET \
--commission-rate 0.1 \
--commission-max-rate 0.2 \
--commission-max-change-rate 0.01 \
--min-self-delegation 1 \
--pubkey $(celestia-appd tendermint show-validator) \
--moniker "test-validator" \
--identity "" \
--website "https://myvalidatorwebsite.com" \
--details "I love blockchain ❤️" \
--chain-id mocha-4 \
--gas auto --gas-adjustment 1.5 --gas-prices 0.005utia \
-y
```

Alternatively, you can automate this process by running the **Validator Registration Playbook**:

```bash
ansible-playbook -i hosts.ini playbooks/register_validator.yml -l <target-host>
```

This playbook will:

* Check if your node is fully synced.
* Prompt you to ensure that your wallet is funded.
* Create a validator using the specified variables (e.g., `wallet_name`, `amount_stake`, `moniker`, `details`, and `website`).

***

### **6. Automating with Playbooks**

* **Quick Sync**: Use the **Quick Sync Playbook** to automate syncing from a snapshot.
* **Validator Registration**: Use the **Validator Registration Playbook** to automate the process of registering your validator.

You can refer to these playbooks to simplify the process for both quick-syncing and validator creation, avoiding repetitive manual steps.
