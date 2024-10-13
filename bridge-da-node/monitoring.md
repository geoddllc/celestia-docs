---
icon: chart-waterfall
---

# Monitoring

For monitoring your Celestia Bridge node’s performance and sync status, the Chaintrails team has developed a public dashboard. By following these steps, you can easily track your node’s health and sync progress in real-time.

#### **Step 1: Retrieve Your Node ID**

To monitor your bridge node, you first need to get your node's unique **Node ID**. Use the following command:

```bash
celestia p2p info --node.store ~/.celestia-bridge-mocha-4/
```

This will return your Node ID, which is required to view your node's data on the Chaintrails dashboard.

***

#### **Step 2: Access the Public Dashboard**

Once you have your Node ID, you can monitor your node's performance using the Chaintrails dashboard:

1. Visit the following URL: [Chaintrails Bridge Node Dashboard](https://mocha-metrics.chaintrails.io/d/fdz036p9r5pmoe/foundation-bridge-node-overview?orgId=1\&refresh=5s\&var-ds=cdv9016f5siyoc\&var-instance\_id=12D3KooWLsr1rNBLovTGd2kyViwYdUH3STttQ9UHwkKKXt8DY5HN\&var-network=mocha-4%2FBridge\&var-job=cel-foundation-otel-testnet-collector\&from=now-30m\&to=now)
2. **Replace the Node ID**: In the dropdown for `node_id`, replace the current value with **your Node ID** that you retrieved in Step 1.
3. The dashboard will then display your Bridge node's sync status, performance metrics, and other real-time data.
