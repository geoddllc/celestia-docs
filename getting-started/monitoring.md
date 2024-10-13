---
description: >-
  Monitoring your Celestia nodes is critical to ensure they perform optimally,
  especially with the high disk IOPS requirements for syncing and maintaining
  blockchain data.
hidden: true
icon: chart-waterfall
cover: >-
  https://www.netdata.cloud/blog/2023-05-02-understanding-system-processes-states/img/stacked-netdata.png
coverY: 0
---

# Monitoring

**Why Use Netdata?**

* **Pre-built Graphs**: Netdata has in-built graphs for CPU, memory, network, and disk usage, which are crucial for monitoring a high-performance node like Celestia.
* **Anomalies Detection**: Netdata can detect anomalies in disk IOPS, CPU usage, memory, and network performance, helping you spot issues before they cause missed blocks or slow syncing.
* **Disk Usage Monitoring**: Since Celestia nodes require high disk IOPS, Netdata’s detailed disk usage graphs help you monitor the backlog and performance of your storage systems. This is particularly important as slow disk performance can lead to issues like missed blocks or slow syncing.

#### **Setting Up Netdata for Monitoring**

1.  **Install Netdata**:

    To install Netdata on your node, run the following command:

    ```bash
    <(curl -Ss https://my-netdata.io/kickstart.sh)
    ```
2.  **Access the Netdata Dashboard**:

    Once installed, access the Netdata dashboard via your browser. The default URL will be:

    ```bash
    http://<your-node-ip>:19999
    ```

    This dashboard will show live graphs for CPU, memory, disk, and network performance.\

3. **Key Metrics to Monitor for Celestia Nodes**:
   * **Disk IOPS and Usage**: High disk IOPS are critical for Celestia nodes. Look for spikes in disk usage or backlog, which could indicate that your storage system is underperforming.
   * **CPU and Memory Usage**: Keep an eye on CPU and memory usage to ensure that other services are not impacting node performance.
   * **Network Performance**: Monitor network throughput to ensure the node is not being affected by network congestion or bottlenecks.\

4. **Set Alerts**: Netdata allows you to set alerts for certain thresholds. Set alerts for:
   * High disk usage or IOPS backlog.
   * CPU usage spikes.
   * Memory usage reaching critical levels.

