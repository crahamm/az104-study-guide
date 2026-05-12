# Configure Network Security Groups - Study Review

## Core Idea

Network security groups (NSGs) control inbound and outbound traffic to Azure resources. They contain security rules that allow or deny traffic based on source, destination, port, protocol, direction, and priority.

This module maps to `Configure secure access to virtual networks`, especially creating NSGs and application security groups, evaluating effective security rules, and restricting network access.

## Key Capabilities

- Associate an NSG with a subnet or network interface.
- Create inbound and outbound allow or deny rules.
- Use priorities to control rule order.
- Evaluate effective security rules when multiple NSGs apply.
- Use application security groups (ASGs) to group VMs by workload.
- Reduce rule count with augmented security rules.

## How NSGs Work

An NSG can be associated with:

- A `subnet`
- A `network interface`

Association limits:

- Each subnet can have zero or one NSG.
- Each network interface can have zero or one NSG.
- The same NSG can be associated with multiple subnets or NICs.

Subnet-level NSGs apply to all resources in the subnet. NIC-level NSGs apply to traffic through a specific network interface.

## Security Rules

NSG rules filter traffic by conditions such as:

- `Source`
- `Source port ranges`
- `Destination`
- `Destination port ranges`
- `Protocol`
- `Direction`
- `Action`
- `Priority`

Protocol options include `TCP`, `UDP`, `ICMP`, `ESP`, `AH`, or `Any`. `ESP` and `AH` are available through JSON templates and PowerShell.

Priority is critical:

- Priority values range from `100` to `4096`.
- Lower numbers are processed first.
- Each priority must be unique within the NSG.
- Leave gaps, such as `100`, `200`, and `300`, so you can insert future rules.

Default rules:

- Azure creates default inbound and outbound rules for every NSG.
- Default inbound rules deny all inbound traffic except traffic from the virtual network and Azure load balancers.
- Default outbound rules allow outbound traffic to the virtual network and internet.
- Default rules can't be deleted.
- You can override a default rule by creating a higher-priority custom rule.

## Effective Security Rules

If an NSG is applied to both a subnet and a NIC, both NSGs are evaluated independently.

Inbound evaluation order:

- Subnet NSG first.
- NIC NSG second.

Outbound evaluation order:

- NIC NSG first.
- Subnet NSG second.

Traffic must be allowed by each NSG in the path. If one layer does not allow the traffic, the traffic is denied.

Important exam point: when using NSGs at both subnet and NIC levels, you need matching allow rules at both levels for intended traffic.

Use `Effective security rules` in the Azure portal or Network Watcher tools to troubleshoot which rules apply to a VM, subnet, or NIC.

## Application Security Groups

Application security groups (ASGs) let you group virtual machines by workload or application tier instead of IP address.

ASGs are used as the source or destination in NSG rules.

Typical pattern:

- Create an ASG for web servers.
- Create an ASG for application or database servers.
- Assign VM NICs to the appropriate ASG.
- Create NSG rules that allow traffic between ASGs.

Example:

- Allow internet traffic to web servers on `80` and `443`.
- Allow web servers to reach application/database servers on `1433`.
- Deny direct HTTP/HTTPS access to application/database servers.

ASGs are useful because:

- Rules follow workload membership instead of static IP addresses.
- New VMs inherit the right rules when added to the ASG.
- You can avoid creating separate rules for each VM.
- Security design is easier to understand by application tier.

## Augmented Security Rules

Augmented security rules let one NSG rule include multiple values, such as:

- Multiple IP addresses.
- Multiple port ranges.
- Service tags.
- Application security groups.

Use augmented rules to reduce rule sprawl. For example, one rule can allow ports `80`, `443`, `8080`, and `8090` instead of four separate rules.

## When To Use

- Use NSGs to restrict traffic to subnets or VM NICs.
- Use subnet-level NSGs for broad protection of all resources in a subnet.
- Use NIC-level NSGs for more specific control on a single VM.
- Use ASGs when security rules should follow workloads instead of IP addresses.
- Use `Effective security rules` when troubleshooting traffic that should be allowed or denied.
- Use a deny rule with higher priority than a default allow rule when you need to block internet or VNet traffic.

## When Not To Use

- Do not rely only on default NSG rules for sensitive workloads.
- Do not create broad inbound rules such as `Any` to management ports unless required and controlled.
- Do not assume a NIC-level allow rule is enough if a subnet-level NSG also applies.
- Do not manage workload security with individual IP addresses when ASGs would be simpler.
- Do not try to delete default NSG rules; override them with custom rules.

## Exam Triggers

- Restrict traffic flow to VNet resources: use an `NSG`.
- Secure a subnet as a DMZ: associate an NSG with the subnet.
- Allow only HTTPS inbound: create an inbound allow rule for port `443`; all other inbound traffic is denied by default or explicit deny.
- New rule has a higher numeric priority value: it is processed later.
- Lower priority number: higher precedence.
- Need workload-based grouping: use `Application Security Groups`.
- Need to check applied rules: use `Effective security rules`.
- Inbound path with subnet and NIC NSGs: subnet then NIC.
- Outbound path with subnet and NIC NSGs: NIC then subnet.
- Default outbound internet access exists as `AllowInternetOutbound`; override it with a higher-priority deny rule if required.

## Knowledge Check Answers

1. To allow inbound traffic, set the source to `Any` or a specific IP range and set the action to `Allow`.
2. A rule with a higher numeric priority value is processed after rules with lower priority values.
3. Use NSGs when you need to restrict traffic flow to resources in a virtual network with specific security rules.
4. To allow only HTTPS inbound, create an NSG rule allowing inbound port `443` and deny all other inbound traffic.
5. Use `Application Security Groups` to manage security for different workloads with less complexity.
6. Use `Application Security Groups` when VMs should be organized by workload for simpler security rule management.
7. A key ASG benefit is defining network security based on application logic rather than IP addresses.
8. Use `Application Security Groups` to group VMs by function and apply specific security rules.
9. A DMZ acts as a buffer between internal resources and external traffic.
