Collect client performance counters by using VM insights
========================================================

Besides monitoring your VM host's health, utilization, and performance, you need to monitor the software and processes running on your VM. These are called the VM guest or client. In this unit, you enable the Azure Monitor VM insights feature, which offers a quick way to start monitoring the VM client.

The VM client includes the operating system and other workloads and applications. To monitor the software running on your VM, you install the Azure Monitor Agent, which collects data from inside the VM. VM insights:

-   Installs Azure Monitor Agent on your VM.
-   Creates a DCR that collects and sends a predefined set of client performance data to a Log Analytics workspace.
-   Presents the data in curated workbooks.

Although you don't need to use VM insights to install Azure Monitor Agent, create DCRs, or set up workbooks, VM insights makes setting up VM client monitoring easy. VM insights provides you with a basis for monitoring the performance of your VM client and mapping the processes running on your machine.

Enable VM insights
------------------

1.  In the Azure portal, on your VM's **Overview** page, select **Insights** from the left navigation menu under **Monitoring**.

2.  On the **Insights** page, select **Enable**.

3.  Under **Data collection rule**, note the properties of the DCR that VM insights creates. In the DCR description, **Processes and dependencies (Map)** is set to **Disabled**, which you can change to **Enabled** or review [this article on how-to](https://learn.microsoft.com/en-us/azure/azure-monitor/vm/vminsights-maps) if greyed out. Also a default **Log Analytics workspace** is created or assigned.

4.  Select **Configure**.

    [![Screenshot that shows enabling and configuring VM insights.](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/enable-insights.png)](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/enable-insights.png#lightbox)

    Configuration of the workspace and the agent installation typically takes 5 to 10 minutes. It can take another 5 to 10 minutes for data to become available to view in the portal.

5.  When the deployment finishes, confirm that the Azure Monitor Agent is installed by looking on the **Properties** tab of the VM's **Overview** page under **Extensions + applications**.

    On the **Monitoring** tab of the **Overview** page, under **Performance and utilization**, you can see that **Guest OS metrics** are now being collected.

    [![Screenshot that shows Guest OS metrics on the VM's Monitoring tab.](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/guest-os-metrics.png)](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/guest-os-metrics.png#lightbox)

View VM insights
----------------

VM insights creates a DCR that sends client VM performance counters to Azure Monitor Logs. Because the DCR sends its metrics to Azure Monitor Logs, you don't use Metrics Explorer to view the metrics data that VM insights collects.

To view the VM insights performance graphs and maps:

1.  Select **Insights** from the VM's left navigation menu under **Monitoring**.

2.  Near the top of the **Insights** page, select the **Performance** tab. The prebuilt VM insights Performance workbook shows charts and graphs with performance-related data for the current VM.

    [![Screenshot that shows the prebuilt VM insights Performance workbook.](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/vm-insights-performance.png)](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/vm-insights-performance.png#lightbox)

        -   You can customize the view by specifying a different **Time range** at the top of the page and different aggregations at the top of each graph.

        -   Select **View Workbooks** to select from other available prebuilt VM insights workbooks. Select **Go To Gallery** to select from a gallery of other VM insights workbooks and workbook templates, or to edit and create your own workbooks.

3.  If enabled earlier, select the **Map** tab on the **Insights** page to see the workbook for the Map feature. The map visualizes the VM's dependencies by discovering running process groups and processes that have active network connections over a specified time range.

    [![Screenshot that shows a dependency map on the Map tab of VM insights.](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/dependency-map.png)](https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/media/dependency-map.png#lightbox)

Check your knowledge
--------------------

1. What capabilities does enabling VM insights provide?

- Prebuilt client performance workbooks and guest OS metrics.

  - Enable VM insights with the Azure Monitor Agent to collect guest OS metrics and use prebuilt workbooks to visualize VM client performance.

2. What's a quick way to install the Azure Monitor Agent to collect guest OS metrics?

- Select the **Azure Monitor Agent** when you enable VM insights.

  - Select the Azure Monitor Agent instead of the legacy Log Analytics Agent when you enable VM insights.
