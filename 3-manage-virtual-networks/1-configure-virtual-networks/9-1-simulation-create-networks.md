Exercise: Create and configure virtual networks
===============================================

Exercise scenario
-----------------

Your organization is migrating a web-based application to Azure. Your first task is to put in place the virtual networks and subnets. You also need to securely peer the virtual networks. You identify these requirements.

-   Two virtual networks are required, app-vnet and hub-vnet. The virtual networks simulate a hub and spoke network architecture.
-   The app-vnet hosts the application. The app-vnet virtual network requires two subnets. The frontend subnet hosts the web servers. The backend subnet hosts the database servers.
-   The hub-vnet only requires a subnet for the firewall.
-   The two virtual networks must be able to communicate with each other securely and privately through virtual network peering.
-   Both virtual networks should be in the same region.

Architecture diagram
--------------------

![Diagram of the architecture as explained in the objectives.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-virtual-networks/media/create-network-architecture.png)

Job skills
----------

-   Create a virtual network.
-   Create a subnet.
-   Configure virtual network peering (optional).

 Note

Estimated time: 30 minutes. To complete this exercise, you need an [Azure subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn_79c01a4f-9410-6cbc-5a75-ef6ab0a7152d).

Launch the exercise, and follow the instructions. When finished, be sure to return to this page so you can continue learning.

[![Button to launch exercise.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-virtual-networks/media/launch-exercise.png)](https://microsoftlearning.github.io/Configure-secure-access-to-workloads-with-Azure-virtual-networking-services/Instructions/Labs/LAB_01_virtual_networks.html)