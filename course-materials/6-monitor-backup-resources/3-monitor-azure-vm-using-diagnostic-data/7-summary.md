Summary
=======

Azure Monitor helps you collect, analyze, and alert on various types of host and client monitoring data from your Azure VMs.

-   Azure Monitor provides a set of VM host logs and performance and usage metrics for all Azure VMs.
-   You can enable recommended alert rules when you create VMs or afterwards to alert on important VM host metrics.
-   Azure Monitor Metrics Explorer lets you graph and analyze metrics for Azure VMs and other resources.
-   VM insights provides a simple way to monitor important VM client performance counters and processes running on your VM.
-   You can create data collection rules to collect other metrics and logs from your VM client.
-   You can use Log Analytics to query and analyze log data.

Now that you understand these tools, you're confident that Azure Monitor can effectively monitor your Azure VMs and help you keep your website running effectively.

Clean up resources
------------------

In this module, you created a VM in your Azure subscription. To prevent further charges for this VM, you can delete it or the resource group that contains it.

To delete the resource group that contains the VM and its resources:

1.  Select the **Resource group** link at the top of the **Essentials** section on the VM's **Overview** page.
2.  At the top of the resource group page, select **Delete resource group**.
3.  On the delete screen, select the checkbox next to **Apply force delete for selected virtual machines and virtual machine scale sets**. Enter the resource group name in the field, and then select **Delete**.

Learn more
----------

To learn more about monitoring your VMs with Azure Monitor, see the following resources:

-   [Azure Monitor documentation](https://learn.microsoft.com/en-us/azure/azure-monitor)
-   [Monitor virtual machines with Azure Monitor](https://learn.microsoft.com/en-us/azure/azure-monitor/vm/monitor-virtual-machine)
-   [Supported metrics with Azure Monitor](https://learn.microsoft.com/en-us/azure/azure-monitor/reference/supported-metrics/metrics-index)
-   [Send Azure Monitor Activity log data](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/activity-log)
-   [Supported metrics for Microsoft.Compute/virtualMachines](https://learn.microsoft.com/en-us/azure/azure-monitor/reference/supported-metrics/microsoft-compute-virtualmachines-metrics)
-   [Overview of VM insights](https://learn.microsoft.com/en-us/azure/azure-monitor/vm/vminsights-overview)
-   [Create interactive reports with VM insights workbooks](https://learn.microsoft.com/en-us/azure/azure-monitor/vm/vminsights-workbooks)
-   [Use the Map feature of VM insights to understand application components](https://learn.microsoft.com/en-us/azure/azure-monitor/vm/vminsights-maps)
-   [Azure Monitor Agent overview](https://learn.microsoft.com/en-us/azure/azure-monitor/agents/azure-monitor-agent-overview)
-   [Collect data with Azure Monitor Agent](https://learn.microsoft.com/en-us/azure/azure-monitor/agents/azure-monitor-agent-data-collection)
-   [Tutorial: Collect guest logs and metrics from an Azure virtual machine](https://learn.microsoft.com/en-us/azure/azure-monitor/vm/tutorial-monitor-vm-guest)
