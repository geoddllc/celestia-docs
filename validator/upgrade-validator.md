---
icon: arrow-up-from-line
---

# Upgrade Validator

When a new release is announced (such as in the Celestia Discord channel), you must update your validator to the specified version. This is handled efficiently by modifying the **app\_version** variable in the Ansible playbook.

#### **Key Variable: `app_version`**

**`app_version`**: This variable specifies the version of the Celestia app you want to upgrade to. Always check for the latest version announcement on the Celestia Discord channel and update the playbook accordingly.

Example of updating the version:

```yaml
app_version: "v2.1.2"
```

When a new version is released (e.g., `"v2.1.3"`), you must change the `app_version` variable in the playbook to reflect this new version before running the upgrade.

***

#### **Steps to Upgrade Validator Node Using Ansible**

1.  **Update the Playbook with the Latest Version:**

    Edit the `upgrade_validator.yml` playbook and modify the `app_version` variable to the latest release from Celestia:

    ```yaml
    app_version: "v2.1.3"  # Update this to the latest version as per Discord announcement
    ```
2.  **Run the Upgrade Playbook:**

    After updating the version, execute the playbook to upgrade your validator:

    ```bash
    ansible-playbook -i hosts.ini playbooks/upgrade-validator.yml -l <target-host>
    ```

    \

3.  **Upgrading Multiple Nodes:**

    To upgrade multiple validator nodes simultaneously, update your `hosts.ini` file to include all the validators you want to upgrade. For example:

    ```ini
    [validators]
    validator1 ansible_host=192.168.0.101
    validator2 ansible_host=192.168.0.102
    ```

    Then run the playbook for all validators:

    ```bash
    ansible-playbook -i hosts.ini playbooks/upgrade_validator.yml -l validators
    ```
4.  **Confirm the Upgrade:** Once the playbook completes, verify the upgrade by checking the status of the validator service:

    ```bash
    sudo systemctl status celestia-appd
    ```

    Additionally, confirm the running version of the Celestia app:

    ```bash
    bashCopy codecelestia-appd version
    ```

    The version should match the one specified in the `app_version` variable.
