# Configure VNet Peering - Study Review

## Core Idea

Azure Virtual Network peering connects two Azure virtual networks so resources can communicate privately over the Microsoft backbone network. After peering, the VNets behave like one network for connectivity, while each VNet remains a separate Azure resource.

This module maps to `Implement and manage virtual networking`, especially creating and configuring virtual network peering, user-defined routes, and troubleshooting connectivity.

## Key Capabilities

- Connect VNets in the same region with regional peering.
- Connect VNets in different regions with global peering.
- Keep traffic private on the Azure backbone.
- Share a VPN Gateway or Route Server through gateway transit.
- Support hub-and-spoke network designs.
- Extend peering with user-defined routes and service chaining.
- Test connectivity with Network Watcher and PowerShell tools.

## How It Works

VNet peering creates private connectivity between two virtual networks.

Key characteristics:

- Peered VNets can communicate without public IP addresses.
- Traffic stays on the Microsoft backbone network.
- No VPN gateway or public internet path is required for basic peering traffic.
- VNets can be peered across subscriptions and tenants.
- Peering does not cause downtime for resources in either VNet.
- Each VNet remains independently managed after peering.

Peering types:

- `Regional peering`: connects VNets in the same Azure region.
- `Global peering`: connects VNets in different Azure regions.

Requirements and limitations:

- Peered VNets must have non-overlapping address spaces.
- To change a peered VNet address range, remove peering first, change the address space, then recreate peering.
- Azure built-in name resolution does not work across peered VNets; use Azure Private DNS zones or custom DNS servers for cross-VNet name resolution.
- Use Standard Load Balancer for cross-region peered scenarios that need internal load balancer communication.
- Global peering across different Azure Government cloud regions is not permitted.

## Peering Settings

The Azure portal exposes key peering options:

- `Traffic to remote virtual network`: allows or blocks direct traffic to the remote VNet.
- `Traffic forwarded from remote virtual network`: allows or blocks forwarded traffic from the remote VNet.
- `Virtual network gateway or Route Server`: lets this VNet's gateway or Route Server be used by the peered VNet.
- `Remote virtual network gateway or Route Server`: lets this VNet use the remote VNet's gateway or Route Server.

Peering status:

- `Initiated`: one side of the peering has been created.
- `Connected`: both sides are configured and the peering is active.

Exam point: peering is not successfully established until both virtual networks show `Connected`.

## Gateway Transit

Gateway transit lets peered VNets use a VPN Gateway or Route Server in another VNet, often a hub VNet.

Use gateway transit when:

- A hub VNet has a VPN Gateway.
- Spoke VNets need access to on-premises resources through the hub.
- You want to avoid deploying a separate VPN Gateway in each spoke VNet.

Important details:

- A VNet can have only one VPN Gateway.
- Gateway transit is supported for regional and global peering.
- The hub side allows gateway transit.
- The spoke side uses the remote gateway.
- NSGs can still allow or block traffic between peered VNets or subnets.

Gateway transit can support:

- Site-to-site VPN.
- VNet-to-VNet connections.
- Point-to-site VPN client access.

## Nontransitive Peering

VNet peering is nontransitive.

If VNet A is peered with VNet B, and VNet B is peered with VNet C, VNet A does not automatically communicate with VNet C.

To connect A and C, use another mechanism such as:

- Direct VNet peering between A and C.
- Hub-and-spoke design with routing through a hub.
- User-defined routes through a network virtual appliance.
- Gateway transit where appropriate.

## User-Defined Routes And Service Chaining

User-defined routes (UDRs) override or add to Azure system routes.

Service chaining directs traffic through a virtual appliance or gateway. In a hub-and-spoke architecture, traffic from spoke VNets can be sent through a hub network virtual appliance (NVA), Azure Firewall, or VPN Gateway.

Common pattern:

- Hub VNet hosts shared services, VPN Gateway, Azure Firewall, or an NVA.
- Spoke VNets peer with the hub.
- UDRs send traffic to a next hop in the hub.
- Peering settings allow forwarded traffic when traffic must pass through the hub.

## When To Use

- Use VNet peering when Azure resources in separate VNets need private connectivity.
- Use global peering when VNets are in different Azure regions.
- Use hub-and-spoke peering for shared services and centralized inspection.
- Use gateway transit to let spoke VNets share a hub VPN Gateway.
- Use UDRs and service chaining when traffic must flow through an NVA, Azure Firewall, or gateway.
- Use Network Watcher connection troubleshooting before and after peering to validate connectivity.

## When Not To Use

- Do not peer VNets with overlapping address spaces.
- Do not assume peering is transitive.
- Do not expect Azure built-in DNS to resolve names across peered VNets without Private DNS or custom DNS.
- Do not create a VPN Gateway in every spoke when gateway transit can meet the requirement.
- Do not forget forwarded traffic settings when routing through a hub appliance.
- Do not treat peering as a security boundary replacement; still use NSGs, routes, and firewall controls.

## Exam Triggers

- Connect two VNets privately: use `virtual network peering`.
- Same-region VNet connection: `regional peering`.
- Different-region VNet connection: `global peering`.
- Traffic path for peered VNets: Microsoft backbone network, not public internet.
- Successful peering status: `Connected` on both sides.
- Peering needs two VNets and non-overlapping address spaces.
- Peered VNets need shared VPN Gateway access: use `gateway transit`.
- VNet can have only one VPN Gateway.
- A-B and B-C peering does not allow A-C automatically: peering is nontransitive.
- Route through firewall/NVA in hub: use UDRs and service chaining.
- Cross-VNet DNS resolution: use Azure Private DNS zones or custom DNS.

## Knowledge Check Answers

1. When virtual networks are successfully peered, both virtual networks show a peering status of `Connected`.
2. `Gateway transit` lets peered virtual networks share the gateway and access external resources.
3. Azure Virtual Network peering keeps traffic between virtual networks on the Microsoft backbone network.
