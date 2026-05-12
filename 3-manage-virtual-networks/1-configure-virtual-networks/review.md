# Configure Virtual Networks - Study Review

## Core Idea

Azure Virtual Network provides private network isolation in Azure. It lets Azure resources communicate securely with each other, the internet, and on-premises networks.

This module maps to `Implement and manage virtual networking`, especially creating and configuring virtual networks and subnets, configuring public IP addresses, and understanding private IP addressing.

## Key Capabilities

- Create a logical network boundary for Azure resources.
- Segment address space into subnets.
- Connect Azure networks to on-premises networks with VPN or ExpressRoute.
- Use public IP addresses for internet-facing access.
- Use private IP addresses for VNet and hybrid communication.
- Plan non-overlapping CIDR ranges for cloud and on-premises networks.

## How It Works

An Azure virtual network is a logical representation of a network in Azure. Each virtual network has its own CIDR address space and one or more subnets.

Core components:

- `Virtual network`: isolated network boundary in Azure.
- `Address space`: CIDR block assigned to the VNet, such as `10.1.0.0/16`.
- `Subnet`: smaller range inside the VNet address space, such as `10.1.0.0/24`.
- `Private IP address`: used for communication inside a VNet or across private hybrid connectivity.
- `Public IP address`: used when a resource must communicate with the internet or public-facing Azure services.

Azure routes traffic between subnets in the same virtual network by default. You can change that behavior with route tables, network virtual appliances, or security rules.

## Subnets

Subnets divide a virtual network into logical segments for security, performance, and management.

Subnet rules:

- A subnet address range must be inside the VNet address space.
- Subnet ranges in the same VNet can't overlap.
- Subnet ranges use CIDR notation.
- Some Azure services require a dedicated subnet, such as `AzureFirewallSubnet` for Azure Firewall or a gateway subnet for VPN Gateway.
- A subnet can have zero or one associated network security group.

Azure reserves five IP addresses in every subnet:

- First address: network address.
- Second address: default gateway.
- Third and fourth addresses: Azure DNS mapping.
- Last address: broadcast address.

Example for `192.168.1.0/24`:

- `192.168.1.0`
- `192.168.1.1`
- `192.168.1.2`
- `192.168.1.3`
- `192.168.1.255`

## IP Addressing

Azure resources can use private or public IP addresses.

Private IP addresses:

- Used for VNet, subnet, and on-premises communication.
- Assigned from the subnet address range.
- Can be dynamic or static.
- Dynamic assignment is the default.

Public IP addresses:

- Used for internet-facing access.
- Can be associated with VM NICs, internet-facing load balancers, VPN gateways, application gateways, NAT gateways, Azure Firewall, Azure Bastion, Route Server, and API Management front ends.
- Standard SKU public IP addresses are static and secure by default.
- Public IP SKU must match the load balancer SKU when used with a load balancer.
- Public IP tier must match the load balancer tier.

Use static IP addresses when the IP must remain stable, such as:

- DNS servers.
- Domain controllers.
- Firewall rules based on IP address.
- IP-based security models.
- TLS/SSL certificate bindings tied to an IP address.
- DNS records that would break if the address changed.

## When To Use

- Use a virtual network when Azure resources need private communication.
- Use subnets to separate tiers, such as web, app, database, and firewall.
- Use private IP addresses for communication inside a VNet or over VPN/ExpressRoute.
- Use public IP addresses for resources that must be reachable from the internet.
- Use site-to-site VPN to securely extend an on-premises datacenter into Azure.
- Use non-overlapping address ranges when connecting VNets or on-premises networks.

## When Not To Use

- Do not overlap VNet address space with another connected VNet or on-premises network.
- Do not put every workload in one flat subnet when isolation or policy boundaries are needed.
- Do not use dynamic public IP addresses for workloads that require stable DNS or firewall references.
- Do not expose resources with public IPs when private connectivity is enough.
- Do not forget service-specific subnet requirements, such as VPN Gateway or Azure Firewall.

## Exam Triggers

- Private cloud-only network: create an Azure virtual network.
- Securely connect on-premises to Azure: use site-to-site VPN or ExpressRoute.
- Logical divisions inside a VNet: use `subnets`.
- Avoid address conflicts: use unique, non-overlapping CIDR ranges.
- VM needs on-premises communication without internet exposure: use a private IP address.
- Resource needs internet/public Azure service access: use a public IP address.
- VM loses internet connectivity after restart: dynamic public IP might have changed.
- DNS server or domain controller: use a static IP address.
- Public IP with load balancer: SKU and tier must match.
- Azure reserves five IP addresses per subnet.

## Knowledge Check Answers

1. Use a `public IP address` for an Azure resource that needs to connect with Azure public-facing services.
2. `Logical isolation` lets Azure Virtual Network create a virtual representation of your network in the cloud.
3. Subnet ranges can't overlap with other subnet IP address ranges in the same virtual network.
4. A restarted VM might lose internet connectivity if it uses a dynamic public IP address.
5. Use `subnets` to create logical divisions for security and performance.
6. Use `Site-to-Site VPN` to connect an on-premises network to an Azure virtual network securely.
7. Use a static IP address for a DNS server.
8. When planning address space, make sure it is unique and does not overlap with on-premises networks.
9. Use a `private IP address` when an Azure VM needs to communicate with an on-premises server without internet exposure.
