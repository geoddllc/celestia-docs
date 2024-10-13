---
icon: file-zipper
---

# ZFS Storage (optional)

Enabling ZFS compression on your Data Availability (DA) node is a powerful way to improve storage efficiency by compressing data in real-time. However, ZFS compression can be CPU-intensive, so using a high-end CPU is recommended to handle the compression workload without affecting node performance.

***

#### **Requirements**

Before proceeding, ensure you meet the following requirements:

* **Bare Metal Server**: The server should have 64GB or more RAM and a high-end CPU to handle the compression tasks efficiently.
* **Available Disk**: At least one unpartitioned disk to create the ZFS pool.

***

#### **Steps to Enable ZFS Compression**

**Step 1: Identify Your Disk**

List the available disks on your system to find the one you’ll use for creating the ZFS pool:

```bash
lsblk --nodeps -o name
```

Note the name of the disk you want to use (e.g., `/dev/nvme0n1`).

**Step 2: Set ZFS Variables**

Define distinct names for your ZFS pool and dataset:

```bash
ZFS_POOL_NAME="mypool" 
ZFS_DATASET_NAME="dataset1"
```

**Step 3: Install ZFS Utilities**

Install the ZFS utilities on your system:

```bash
sudo apt update
sudo apt install zfsutils-linux
```

**Step 4: Create the ZFS Pool**

Create a ZFS pool on the disk you identified:

```bash
zpool create $ZFS_POOL_NAME /dev/nvme0n1
```

{% hint style="info" %}
If you have multiple disks available, you can create the pool using more than one disk:
{% endhint %}

```bash
zpool create $ZFS_POOL_NAME /dev/nvme0n1 /dev/nvme1n1
```



**Step 5: Create the ZFS Dataset**

Once the pool is created, create the dataset for storing Celestia node data:

```bash
zfs create $ZFS_POOL_NAME/$ZFS_DATASET_NAME
```

**Step 6: Enable Compression**

To optimize storage, enable `zstd-3` compression on the dataset:

```bash
zfs set compression=zstd-3 $ZFS_POOL_NAME/$ZFS_DATASET_NAME
```

This ensures data is compressed on the fly to save disk space.

**Step 7: Mount the Dataset**

Now, mount the dataset to your Celestia bridge data folder. Instead of using a custom path, we will mount it directly to `/home/ubuntu/.celestia-bridge-mocha-4`:

```bash
zfs set mountpoint=/home/ubuntu/.celestia-bridge-mocha-4 $ZFS_POOL_NAME/$ZFS_DATASET_NAME
```

This will make your dataset available in the specified directory, and you won’t need to modify the node store path in your Celestia commands.

***

#### **Monitoring Compression Efficiency**

Once the setup is complete, you can check how well ZFS compression is working by viewing the compression ratio:

```bash
zfs get compressratio $ZFS_POOL_NAME
```

This command will show how much data is being compressed. For example:

```bash
NAME              PROPERTY       VALUE  SOURCE
mypool            compressratio  2.05x  -
```

***

#### **Important Considerations**

* **High-End CPU Required**: Since ZFS compression can be CPU-intensive, especially with `zstd-3`, ensure your server has a high-performance CPU to handle the compression without affecting the performance of your Celestia node.
* **Real-Time Compression**: ZFS will compress data as it is written to disk, allowing for efficient storage management without requiring manual intervention.

## ZFS Optimizations for fast sync&#x20;

1.  **ZFS Compression (zstd-3):**

    Enabled and improved storage efficiency without significantly impacting performance.

    **Command:**

    ```bash
    zfs set compression=zstd-3 $ZFS_POOL_NAME/$ZFS_DATASET_NAME
    ```
2.  **Manual Trimming:**\
    **Disable Auto-Trim**: To disable ZFS auto-trim, run:

    ```bash
    sudo zpool set autotrim=off mypool
    ```

    This prevents automatic trimming, allowing manual control over trim operations.

    \
    **Manual Trim Command**: To manually trim ZFS and release unused blocks back to the SSD:

    ```bash
    sudo zpool trim mypool
    ```

    _This manually triggers a trim on the `mypool`, optimizing SSD performance._

    _You can monitor the trim process by checking the pool status:_

    ```bash
    zpool status
    ```
3.  **Sync Disabled:**

    Disabling sync improved performance by reducing the backlog to 1-7 seconds from higher values, leading to faster operations.

    **Command:**

    ```bash
    zfs set sync=disabled $ZFS_POOL_NAME/$ZFS_DATASET_NAME
    ```
4.  **Prefetch Tuning:**

    Keeping `zfs_prefetch_disable` set to 1 (disable)&#x20;

    \
    **Command to check prefetch status:**

    ```bash
    cat /sys/module/zfs/parameters/zfs_prefetch_disable
    ```

    \
    **To disable prefetch (set to 1):**

    ```bash
    echo 1 | sudo tee /sys/module/zfs/parameters/zfs_prefetch_disable
    ```

