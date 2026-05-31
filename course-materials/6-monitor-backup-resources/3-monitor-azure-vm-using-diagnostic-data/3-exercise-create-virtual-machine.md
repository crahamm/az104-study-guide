Monitor VM host data
====================

You want to monitor the VMs that host your website, so you decide to quickly create a VM in the Azure portal and evaluate its built-in monitoring capabilities. In this unit, you use the Azure portal to create a Linux VM with recommended alerts and boot diagnostics enabled. As soon as the VM starts up, Azure automatically begins collecting basic metrics and activity logs. You can then view built-in metrics graphs, activity logs, and boot diagnostics.

Create a VM and enable recommended alerts
-----------------------------------------

1.  Sign in to the [Azure portal](https://portal.azure.com/), and in the Search field, enter *virtual machines*.

2.  On the **Virtual machines** page, select **Create**, and then select **Azure virtual machine**.

3.  On the **Basics** tab of the **Create a virtual machine** page:

        -   In the **Subscription** field, select the correct subscription if not already selected.
        -   Under **Resource group**:
                    1.  Select **Create new**.
                    2.  Under **Name**, enter *learn-monitor-vm-rg*.
                    3.  Select **OK**.
        -   For **Virtual machine name**, enter *monitored-linux-vm*.
        -   For **Image**, select **Ubuntu Server 20.04 LTS - x64 Gen2**.
4.  Leave the other settings at their current values, and select the **Monitoring** tab.

    [![Screenshot that shows the Basics tab of the Create a virtual machine page.](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/create-vm-basic.png)](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/create-vm-basic.png#lightbox)

5.  On the **Monitoring** tab, select the checkbox next to **Enable recommended alert rules**.

6.  On the **Set up recommended alert rules** screen:

        1.  Select all the listed alert rules if not already selected, and adjust the values if desired.
        2.  Under **Notify me by**, select the checkbox next to **Email**, and enter an email address to receive alert notifications.
        3.  Select **Save**.
7.  Under **Diagnostics**, for **Boot diagnostics**, ensure that **Enable with managed storage account (recommended)** is selected.

     Note

    Don't select **Enable OS guest diagnostics**. The Linux Diagnostics Agent (LAD) is deprecated, and you can enable OS guest and client monitoring later.

8.  Select **Review + create** at the bottom of the page, and when validation passes, select **Create**.

    [![Screenshot that shows the Monitoring tab and alert rule configuration screen of the Create a virtual machine page.](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/create-vm-monitoring.png)](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/create-vm-monitoring.png#lightbox)

9.  On the **Generate new key pair** popup dialog box, select **Download private key and create resource**.

It can take a few minutes to create the VM. When you get the notification that the VM is created, select **Go to resource** to see basic metrics data.

View built-in metrics graphs
----------------------------

Once your VM is created, Azure starts collecting basic metrics data automatically. Built-in metrics graphs, along with the recommended alerts you enabled, can help you monitor whether and when your VM encounters health or performance issues. You can then use more advanced monitoring and analytics capabilities to investigate issue causes and remediation.

1.  To view basic metrics graphs, on the VMs **Overview** page, select the **Monitoring** tab.

    [![Screenshot that shows Monitoring tab on a VMs Overview screen.](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/select-monitoring.png)](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/select-monitoring.png#lightbox)

2.  Under **Performance and utilization** \> **Platform metrics**, review the following metrics graphs related to the VMs performance and utilization. Select **Show more metrics** if all the graphs don't appear immediately.

        -   **VM Availability**
        -   **CPU (average)**
        -   **Disk bytes (total)**
        -   **Network (total)**
        -   **Disk operations/sec (average)**

    [![Screenshot that shows the platform metrics graphics on the VM Overview page.](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/platform-metrics.png)](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/platform-metrics.png#lightbox)

3.  Under **Guest OS metrics**, notice that guest OS metrics aren't being collected yet. In the next units, you configure VM insights and data collection rules to collect guest OS metrics.

View the activity log
---------------------

You can view the VMs activity log by selecting **Activity log** from the VMs left navigation menu. You can also retrieve entries by using PowerShell or the Azure CLI.

[![Screenshot of the activity log for a VM.](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/activity-log.png)](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/activity-log.png#lightbox)

View boot diagnostics
---------------------

You enabled boot diagnostics when you created the VM. You can view boot diagnostics to view boot data and troubleshoot startup issues.

1.  In the left navigation menu for the VM, select **Boot diagnostics** under **Help**.

2.  On the **Boot diagnostics** page, select **Screenshot** to see a startup screenshot from the VMs hypervisor. Select **Serial log** to view log messages created when the VM started.

    [![Screenshot that shows the boot diagnostic image captured.](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/3-boot-diagnostics.png)](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/3-boot-diagnostics.png#lightbox)

Check your knowledge
--------------------

1. What do you need to do to enable recommended alert rules when you create a VM?

- Select **Enable recommended alert rules** on the **Monitoring** tab.

  - You can easily enable recommended alerts at VM creation by selecting **Enable** and configuring the alert parameters on the **Monitoring** tab.

2. Which metrics graph isn't available by default on the **Monitoring** tab when you create a VM?

- Guest OS Available Memory

  - Guest OS metrics charts aren't available until you enable the Azure Monitor Agent to collect client VM metrics.
