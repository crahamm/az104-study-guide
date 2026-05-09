# Core Architectural Components Of Azure - Study Review

## Core Idea

Azure is organized around physical infrastructure and management infrastructure.

For AZ-104, the most important parts are how Azure organizes resources for governance, access, billing, and resiliency:

- Physical infrastructure: datacenters, regions, availability zones, region pairs, and sovereign regions.
- Management infrastructure: resources, resource groups, subscriptions, and management groups.

This module supports the exam objective `Manage Azure subscriptions and governance`, especially resource groups, subscriptions, and management groups.

## Key Capabilities

- Deploy resources into Azure regions.
- Use availability zones for intra-region resiliency.
- Use region pairs for regional disaster recovery planning.
- Organize resources into resource groups.
- Use subscriptions as billing, access, and scale boundaries.
- Use management groups to apply policy and access controls across subscriptions.
- Understand sovereign regions for legal, compliance, or government requirements.

## Azure Services Overview

Azure provides cloud services for compute, networking, storage, databases, AI and machine learning, identity and security, DevOps, management, IoT, analytics, and integration.

Common workload patterns:

- Run existing applications on Azure virtual machines.
- Modernize apps with managed databases, app services, autoscaling, and event-driven services.
- Add AI, language, vision, speech, or generative AI capabilities with Azure AI services.
- Scale resources up, down, out, or in based on demand.

Exam point: Azure is more than hosted VMs. The platform includes managed services that reduce infrastructure management work.

## Azure Accounts And Subscriptions

To create Azure resources, you need an Azure subscription.

Key relationships:

- An Azure account is an identity associated with Azure access.
- A subscription provides access to Azure products and services.
- A subscription is also a billing and access control boundary.
- One account can have multiple subscriptions.
- Each subscription can contain multiple resource groups.
- Each resource group contains Azure resources.

You might create multiple subscriptions for:

- `Development`
- `Test`
- `Production`
- `Sandbox`
- Separate teams or workloads
- Separate billing or cost tracking

## Physical Infrastructure

Azure physical infrastructure starts with datacenters. You do not normally manage individual datacenters directly. Azure groups datacenters into regions and availability zones.

Hierarchy:

- Geography
- Region
- Availability zone
- Datacenter

## Regions

An Azure region is a geographic area that contains one or more nearby datacenters connected with low-latency networking.

Important points:

- Many Azure resources require you to choose a region during deployment.
- Some services and VM features are available only in specific regions.
- Some global services do not require a region selection.

Examples of global services:

- `Microsoft Entra ID`
- `Azure Traffic Manager`
- `Azure DNS`

Use regions to place workloads close to users, meet compliance requirements, and control service availability.

## Availability Zones

Availability zones are physically separate datacenters within an Azure region.

Each availability zone has independent:

- Power
- Cooling
- Networking

Availability zones are connected by high-speed private fiber networks.

Important facts:

- Availability zones are isolation boundaries.
- If one zone fails, other zones in the same region can continue operating.
- Availability zone-enabled regions have at least `three` separate availability zones.
- Not every Azure region supports availability zones.

Service categories:

- `Zonal services`: resources are pinned to a specific zone, such as VMs, managed disks, and IP addresses.
- `Zone-redundant services`: Azure replicates automatically across zones, such as zone-redundant storage or SQL Database.
- `Non-regional services`: available across Azure geographies and resilient to zone-wide and region-wide outages.

## Region Pairs

Most Azure regions are paired with another region in the same geography.

Region pair facts:

- Region pairs are generally at least `300 miles` apart.
- Planned Azure updates are rolled out to paired regions one region at a time.
- If a broad outage occurs, one region in each pair is prioritized for recovery.
- Region pairs help with disaster recovery and data-residency planning.
- Not every Azure service automatically replicates or fails over to its paired region.

Examples:

- `West US` is paired with `East US`.
- `Southeast Asia` is paired with `East Asia`.

Important exception:

- `Brazil South` is paired one-way with `South Central US`.
- Some newer regions do not use traditional region pairs and rely on availability zones and geo-redundant storage patterns.

## Sovereign Regions

Sovereign regions are isolated Azure instances used for legal, compliance, or government requirements.

Examples:

- `US Gov Virginia`
- `US Gov Arizona`
- `US DoD Central`
- `China East`
- `China North`

Important distinctions:

- Azure Government regions are physically and logically isolated for U.S. government agencies and partners.
- Azure China regions are operated through Microsoft's partnership with `21Vianet`.

## Resources And Resource Groups

An Azure resource is anything you create, provision, or deploy in Azure.

Examples:

- Virtual machines
- Virtual networks
- Storage accounts
- Databases
- Azure AI services

Resource group facts:

- Every resource must belong to exactly one resource group.
- A resource can be in only one resource group at a time.
- Some resources can be moved between resource groups.
- Resource groups cannot be nested.
- Resource groups cannot be renamed after creation.
- Deleting a resource group deletes the resources inside it.
- Access or policy applied at the resource group level affects resources in the group.

Use resource groups to organize resources by lifecycle, workload, environment, team, or administrative boundary.

## Subscriptions

Azure subscriptions are boundaries for:

- Billing
- Access control
- Management
- Scale

Subscription boundary types:

- `Billing boundary`: each subscription can have separate invoices, reports, and cost tracking.
- `Access control boundary`: role assignments and access policies can differ by subscription.

Common subscription strategies:

- Separate `dev`, `test`, and `prod`.
- Separate teams or projects.
- Separate sandbox environments from production.
- Track billing by department or workload.

## Management Groups

Management groups organize subscriptions above the subscription level.

Use management groups to:

- Apply Azure Policy across many subscriptions.
- Assign Azure RBAC permissions across many subscriptions.
- Build a hierarchy that mirrors business units or environments.
- Enforce governance at scale.

Important facts:

- Every Microsoft Entra tenant has one `Tenant Root Group`.
- All management groups and subscriptions roll up to the Tenant Root Group.
- Policies and permissions inherit downward.
- Management groups can be nested up to `six` levels deep, not counting the root or subscription level.
- A single directory supports up to `10,000` management groups.
- Each management group and subscription can have only one parent.

Example:

- Apply a policy at a `Production` management group to restrict VM locations.
- All subscriptions under that management group inherit the policy.
- Resource or subscription owners cannot override inherited policy if it is enforced from above.

## When To Use

- Use resource groups to manage resources with the same lifecycle.
- Use subscriptions to separate billing, access, environments, or workloads.
- Use management groups when governance must span multiple subscriptions.
- Use availability zones when workload components need resilience within a region.
- Use region pairs or geo-redundant designs for regional disaster recovery.
- Use sovereign regions when legal or regulatory rules require isolated Azure environments.

## When Not To Use

- Do not put unrelated resources in the same resource group if their lifecycle, access, or ownership differs.
- Do not rely on resource groups for nesting; they cannot be nested.
- Do not assume every region supports every service, VM size, or availability zones.
- Do not assume every service automatically replicates to a paired region.
- Do not use subscriptions only as billing containers when access separation is also needed.
- Do not apply policy subscription-by-subscription when a management group can enforce it consistently.

## Exam Triggers

- Basic deployable item in Azure: `resource`.
- Resource belongs to how many resource groups at once: `one`.
- Delete a resource group: deletes resources inside it.
- Resource groups nested: not supported.
- Resource group renamed after creation: not supported.
- Billing and access boundary: `subscription`.
- Apply policy across many subscriptions: `management group`.
- Top management group in each tenant: `Tenant Root Group`.
- Management group nesting limit: `six` levels, excluding root and subscription.
- Management groups per directory: up to `10,000`.
- Physically separate datacenters in a region: `availability zones`.
- Minimum availability zones in zone-enabled regions: `three`.
- Regional disaster recovery relationship: `region pair`.
- Region pairs are generally at least `300 miles` apart.
- Compliance-isolated Azure instance: `sovereign region`.
- Azure China operator: `21Vianet`.

## Knowledge Check Answers

1. A resource can be in `one` resource group at the same time.
2. A setting applied at the resource group level applies to current and future resources in that resource group.
3. `Region pairs` replicate resources across regions that are at least 300 miles away from each other.
