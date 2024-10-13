---
description: >-
  This page provides a set of useful commands for managing and monitoring your
  Celestia validator and bridge nodes. From checking logs to managing services,
  these commands will help you efficiently hand
icon: gauge-max
---

# Quick Commands

***

### **Service Operations ⚙️**

#### **Check Logs**

To monitor the logs of your Celestia service in real-time:

```bash
sudo journalctl -u celestia-appd -f
```

***

#### **Start Service**

To start the Celestia service:

```bash
sudo systemctl start celestia-appd
```

***

#### **Stop Service**

To stop the Celestia service:

```bash
sudo systemctl stop celestia-appd
```

***

#### **Restart Service**

To restart the Celestia service:

```bash
sudo systemctl restart celestia-appd
```

***

***

#### **Enable Service at Boot**

To ensure that the Celestia service starts automatically when the server boots:

```bash
sudo systemctl enable celestia-appd
```

***

#### **Disable Service**

To disable the Celestia service from starting on boot:

```bash
sudo systemctl disable celestia-appd
```

***

### **Node Info**

To check the status of the node and retrieve information such as sync status:

```bash
celestia-appd status 2>&1 | jq
```

***

### **Future Plans: Ansible Cron for Weekly Delegation**

In the future, we will add an Ansible cron job that automates the delegation of testnet rewards to yourself every week. Stay tuned for more updates on automating this process with a playbook!
