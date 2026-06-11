You have an Azure subscription that contains a virtual network named VNet1.

You plan to deploy a virtual machine named VM1 to be used as a network inspection appliance.

You need to ensure that all network traffic passes through VM1.

What should you do?

Select only one answer.

- Configure a user-defined route.

**This answer is correct.**

> Azure automatically creates a route table for each subnet on an Azure virtual network and adds system default routes to the table. You can override some of the Azure system routes with custom user-defined routes and add more custom routes to route tables. Azure routes outbound traffic from a subnet based on the routes on a subnet's route table.
>
> [Azure virtual network traffic routing | Microsoft Learn](https://learn.microsoft.com/azure/virtual-network/virtual-networks-udr-overview)

---

You have an Azure subscription that contains the following virtual networks:

-   VNet1 has an IP address range of 192.168.0.0/24.
-   VNet2 has an IP address range of 10.10.0.0/24.
-   VNet3 has an IP address range of 192.168.0.0/16.

You need configure virtual network peering.

Which two peerings can you create? Each correct answer presents complete solution.

Select all answers that apply.

- VNet1 can be peered with VNet2.

**This answer is correct.**

- VNet2 can be peered with VNet3.

**This answer is correct.**

> VNet1 and VNet2 have non-overlapping IP addresses. For virtual network peering, both virtual networks must have non-overlapping IP addresses.
>
> [Azure Virtual Network peering | Microsoft Learn](https://learn.microsoft.com/azure/virtual-network/virtual-network-peering-overview)
>
> [Configure virtual network peering - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/configure-vnet-peering/)

---

You have two Azure subscriptions named Sub1 and Sub2.

Sub1 contains a virtual network named VNet1 and a VPN gateway. Sub2 contains a virtual network named VNet2.

You have an on-premises device named Device1 that runs Windows and has a Point-to-Site (P2S) VPN client installed.

You configure network peering between VNet1 and VNet2.

You need to ensure that Device1 can access VNet2 when a VPN connection is established.

What should you do?

Select only one answer.

- Download and reinstall the P2S VPN client on Device1.

**This answer is correct.**

> Point-to-Site (P2S) VPN clients must be downloaded and reinstalled again after virtual network peering is successfully configured to ensure that the new routes are downloaded to the client.
>
> A private endpoint and Azure Front Door are not required nor used to be able to access VNet2 from VNet1.
>
> Device1 already has a digital certificate when you install the P2S VPN client, so you do not need to create new certificate manually.
>
> [Create, change, or delete an Azure virtual network peering | Microsoft Learn](https://learn.microsoft.com/azure/virtual-network/virtual-network-manage-peering?tabs=peering-portal#requirements-and-constraints)

---

You have an Azure subscription that contains network security groups (NSGs).

Which two resources can be associated with a NSG? Each correct answer presents a complete solution.

Select all answers that apply.

- Network interfaces

**This answer is correct.**

- Subnets

**This answer is correct.**

> You can use a network security group (NSG) to be assigned to a network interface. NSGs can be associated with subnets or individual virtual machine instances within that subnet. When an NSG is associated with a subnet, the access control list (ACL) rules apply to all virtual machine instances of that subnet.
>
> [Azure network security groups overview | Microsoft Learn](https://learn.microsoft.com/azure/virtual-network/network-security-groups-overview)
>
> [Configure network security groups - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/configure-network-security-groups/)

---

Question 5 of 50

You have a virtual machine named VM1 that is assigned to a network security group (NSG) named NSG1.

NSG1 has the following outbound security rules:

Rule1:

-   Priority: 900
-   Name: BlockInternet
-   Port: 80
-   Protocol: TCP
-   Source: Any
-   Destination: Any
-   Action: Block

Rule2:

-   Priority: 1000
-   Name: AllowInternet
-   Port: 80
-   Protocol: TCP
-   Source: Any
-   Destination: Any
-   Action: Allow

You need to ensure that internet access to VM1 on port 80 is allowed.

What should you do?

Select only one answer.

- Change the priority of Rule2.

**This answer is correct.**

> Rule1 has higher priority, so the action will be blocked. You can increase the priority of Rule2, decrease the priority of Rule1, or change the action of Rule1 to achieve the goal.
>
> [Azure network security groups overview | Microsoft Learn](https://learn.microsoft.com/azure/virtual-network/network-security-groups-overview)
>
> [Configure network security groups - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/configure-network-security-groups/)

---

Question 6 of 50

You create several Azure virtual machines that run Windows Server.

You need to connect to the virtual machines without exposing RDP ports over the internet.

Which Azure service should you deploy?

Select only one answer.

- Azure Bastion

**This answer is correct.**

> Azure Bastion is a service that lets you connect to a virtual machine by using a browser, without exposing RDP and SSH ports. Azure Monitor helps you maximize the availability and performance of applications and services. Azure Network Watcher provides tools to monitor, diagnose, view metrics, and enable or disable logs for resources in an Azure virtual network. Remote Desktop is a feature of the operating system, which exposes the RDP port to connect to a server from the internet.
>
> [About Azure Bastion | Microsoft Learn](https://learn.microsoft.com/azure/bastion/bastion-overview)
>
> [Configure virtual networks - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/configure-virtual-networks/)

---

You need to create an Azure Storage account that supports the Azure Data Lake Storage Gen2 capabilities.

Which two types of storage accounts can you use? Each correct answer presents a complete solution.

Select all answers that apply.

- Premium block blobs

**This answer is correct.**

- Standard general-purpose v2

**This answer is correct.**

> To support Data Lake Storage, the storage account must support blob storage, which is available as standard general-purpose v2 and premium block blobs. Additionally, when you create the storage account, you must enable the hierarchical namespace.
>
> [Create a storage account for Azure Data Lake Storage Gen2 - Azure Storage | Microsoft Learn](https://learn.microsoft.com/azure/storage/blobs/create-data-lake-storage-account)
>
> [Determine storage account types - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/configure-storage-accounts/4-determine-storage-account-kinds)

---

You have two premium block blob Azure Storage accounts named storage1 and storage2.

You need to configure object replication from storage1 to storage2.

Which three features should be enabled before configuring object replication? Each correct answer presents part of the solution.

Select all answers that apply.

- Blob versioning for storage1

**This answer is correct.**

- Blob versioning for storage2

**This answer is correct.**

- Change feed for storage1

**This answer is correct.**

---

