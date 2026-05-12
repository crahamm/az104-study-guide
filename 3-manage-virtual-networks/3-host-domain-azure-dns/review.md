# Host A Domain On Azure DNS - Study Review

## Core Idea

Azure DNS hosts DNS zones and records on Azure infrastructure. It lets you manage public and private DNS records with the same Azure credentials, APIs, tools, billing, RBAC, activity logs, and resource management model as other Azure services.

This module maps to `Configure name resolution and load balancing`, especially configuring Azure DNS and understanding public/private DNS zones.

## Key Capabilities

- Host DNS records for a registered domain.
- Create public DNS zones.
- Delegate a domain from a registrar to Azure DNS name servers.
- Create record sets such as `A`, `AAAA`, `CNAME`, `MX`, and `TXT`.
- Create private DNS zones for name resolution inside virtual networks.
- Use alias record sets to point DNS names to Azure resources.

## How DNS Works

DNS translates human-readable names such as `www.contoso.com` into IP addresses.

DNS servers commonly:

- Cache recently resolved names.
- Store authoritative records for domains they manage.
- Forward lookup requests to other DNS servers when they do not have an answer.

Common record types:

- `A`: maps a host name to an IPv4 address.
- `AAAA`: maps a host name to an IPv6 address.
- `CNAME`: creates an alias from one name to another.
- `MX`: maps mail delivery to mail servers.
- `TXT`: stores text strings, often for ownership verification.
- `NS`: identifies name servers for the zone.
- `SOA`: identifies the start of authority for the zone.

Azure automatically creates `NS` and `SOA` records when you create a DNS zone.

## Public DNS Zones

A public DNS zone hosts records for an internet domain, such as `contoso.com`.

Basic workflow:

1. Register the domain with a third-party domain registrar.
2. Create a DNS zone in Azure DNS with the domain name.
3. Copy the Azure DNS name servers from the zone's `NS` record.
4. Update the domain registrar to use all four Azure DNS name servers.
5. Verify delegation by querying the `SOA` record.
6. Add records such as `A`, `AAAA`, `CNAME`, `MX`, or `TXT`.

Important terms:

- `DNS zone`: container for DNS records for a domain.
- `Domain delegation`: changing registrar name server settings so Azure DNS is authoritative.
- `TTL`: time-to-live, or how long a DNS answer can be cached.
- `Record set`: multiple records with the same name and type, such as one `A` record set with multiple IP addresses.

Exam point: Azure DNS hosts and manages DNS for registered domains, but domain registration still happens with a domain registrar.

## Private DNS Zones

Private DNS zones provide name resolution inside virtual networks without exposing records to the internet.

Use private DNS zones to:

- Resolve VM names inside a VNet.
- Resolve names across linked VNets.
- Use custom private domain names instead of Azure-provided names.
- Support split-horizon DNS, where the same domain name can exist in public and private zones and resolve differently depending on where the query starts.

Basic workflow:

1. Create a private DNS zone, such as `private.contoso.com`.
2. Identify the virtual networks that need private name resolution.
3. Create virtual network links from the private zone to those VNets.
4. Add records for resources that need private DNS names.

Private DNS zones do not require domain registrar delegation because they are not internet-visible.

## Alias Record Sets

Alias records link DNS records to Azure resources instead of hardcoding an IP address or external DNS name.

Alias records can point to:

- Traffic Manager profiles.
- Azure Content Delivery Network endpoints.
- Public IP resources.
- Azure Front Door profiles.

Alias record sets are supported for:

- `A`
- `AAAA`
- `CNAME`

Why alias records matter:

- They reduce dangling DNS records when a target Azure resource changes or is deleted.
- They automatically track target resource IP changes.
- They support load-balanced apps at the zone apex.
- They can point the zone apex to Azure resources where a normal `CNAME` is not allowed.

The zone apex is the root of the DNS zone, such as `contoso.com`. In Azure DNS, the `@` symbol often represents the apex.

## When To Use

- Use Azure DNS when you want Azure to host DNS records for a registered domain.
- Use public DNS zones for internet-facing domain records.
- Use private DNS zones for internal VNet name resolution.
- Use `A` or `AAAA` records to map a host name to IP addresses.
- Use `CNAME` records when one name should alias another DNS name.
- Use `TXT` records for domain ownership verification scenarios.
- Use alias records when DNS should target an Azure resource and follow that resource over time.
- Use `nslookup` to verify name resolution and delegation.

## When Not To Use

- Do not expect Azure DNS to register a domain name; use a domain registrar first.
- Do not use a public DNS zone for records that should only resolve inside VNets.
- Do not use `CNAME` at the zone apex; use alias records where supported.
- Do not manually hardcode resource IPs when an alias record can track an Azure public IP or Traffic Manager target.
- Do not forget to update the registrar with all four Azure DNS name servers during delegation.

## Exam Triggers

- Host DNS records for a registered domain: use `Azure DNS`.
- Create domain records in Azure: create a `DNS zone`.
- Point registrar to Azure DNS: update `NS` records at the registrar with Azure DNS name servers.
- Verify delegation: query the `SOA` record with `nslookup`.
- Map a host to IPv4: create an `A` record.
- Map a host to IPv6: create an `AAAA` record.
- Alias one DNS name to another: create a `CNAME`.
- Verify Microsoft 365 or domain ownership: create a `TXT` record.
- Private VNet-only name resolution: create a `Private DNS zone` and virtual network link.
- Apex domain points to Azure public IP or Traffic Manager: use an alias record.
- Avoid dangling DNS records: use alias record sets.

## Knowledge Check Answers

1. Azure DNS lets you manage and host your registered domain and associated records.
2. Azure DNS security integrates with Azure Resource Manager features such as RBAC, activity logs, and resource locking.
3. Use an `A` or `AAAA` record to map one or more IP addresses to a single domain.
