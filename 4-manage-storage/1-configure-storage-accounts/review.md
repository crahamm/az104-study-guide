# Configure Storage Accounts Review

## Core Idea

Azure Storage accounts provide a durable, scalable namespace for Azure Storage services. For AZ-104, focus on choosing the right account type, service, redundancy option, endpoint access pattern, and network security configuration.

## Exam Scope

- Domain: `Implement and manage storage` (15-20%).
- Objectives: create and configure storage accounts, configure redundancy, configure firewalls and virtual networks, configure encryption, and manage data by using Azure Storage tools.

## Key Capabilities

- Azure Storage supports virtual machine data, unstructured data, and structured data.
- Main data services are `Blob Storage`, `Azure Files`, `Queue Storage`, and `Table Storage`.
- Storage account endpoints use the storage account name as the subdomain, such as `<account>.blob.core.windows.net` or `<account>.file.core.windows.net`.
- Blob data can use a custom domain by mapping a DNS `CNAME` record to the Blob endpoint.
- Blob Storage supports `SFTP` when hierarchical namespace is enabled.
- Blob Storage can support `NFSv3` for Linux file workload migration scenarios.
- The portal setting `Default to Microsoft Entra authorization` makes Microsoft Entra/RBAC the preferred authorization path over shared keys.

## Storage Services

| Service | Use When |
| --- | --- |
| `Blob Storage` | Massive unstructured object data, browser delivery, streaming, backups, archive, analytics input. |
| `Azure Files` | Managed SMB/NFS file shares, lift-and-shift apps, shared tools/configuration/logs. |
| `Queue Storage` | Asynchronous message processing; messages can be up to `64 KB`. |
| `Table Storage` | Structured NoSQL key/attribute data with a schemaless design. |

## Storage Account Types

| Account Type | Backing Storage | Key Use |
| --- | --- | --- |
| `Standard general-purpose v2` | HDD | Default choice for most blobs, files, queues, and tables. |
| `Premium block blobs` | SSD | High transaction rates and consistently low storage latency for block/append blobs. |
| `Premium file shares` | SSD | High-performance Azure Files workloads with SMB and NFS support. |
| `Premium page blobs` | SSD | Page blobs only, including VM disks and sparse/index-based data. |

- You can't convert `Standard` to `Premium` or `Premium` to `Standard`; create a new account and copy data.
- Legacy `GPv1` and `BlobStorage` accounts should generally be upgraded to `GPv2`.
- Storage Service Encryption is enabled for all account types.

## Redundancy

| Option | Protection Scope | Read Access During Regional Outage |
| --- | --- | --- |
| `LRS` | Three copies within one datacenter/storage scale unit. | No |
| `ZRS` | Synchronous copies across three availability zones in one region. | No |
| `GRS` | LRS in primary, async replication to paired secondary region. | Only after Microsoft failover |
| `RA-GRS` | Same as GRS, plus secondary read endpoint. | Yes |
| `GZRS` | ZRS in primary, plus async regional replication. | Only after failover |
| `RA-GZRS` | Same as GZRS, plus secondary read endpoint. | Yes |

## How It Works

- `LRS` is cheapest and suitable when data can be recreated, changes constantly, or must stay in one location for governance.
- `ZRS` protects against zone failure and keeps low-latency access inside one region, but isn't available everywhere.
- `GRS` and `RA-GRS` protect against regional outage with asynchronous replication to a secondary region.
- `GZRS` and `RA-GZRS` combine zone resilience in the primary region with geo-replication.
- Microsoft recommends `GZRS` for workloads needing consistency, durability, high availability, performance, and disaster recovery resilience.

## Secure Endpoint Access

- Use `Firewalls and virtual networks` to restrict storage account access to selected public IP ranges, virtual networks, and subnets.
- Service endpoints keep the storage account public endpoint but restrict access to selected subnets.
- Private endpoints assign a private IP from a VNet to the storage account and route traffic over the Microsoft backbone.
- Private endpoints are preferred for production workloads requiring strong network isolation or compliance.
- Virtual networks/subnets used for storage service endpoint restrictions must be in the same Azure region or region pair as the storage account.

## When To Use

- Use `Standard GPv2` for most storage account requirements.
- Use `Premium` options only when workload latency, throughput, or IOPS justify the cost.
- Use `RA-GRS` or `RA-GZRS` when users or apps must read from the secondary region during primary-region failure.
- Use private endpoints for production private connectivity to Azure Storage.
- Use custom domains when users need a friendly DNS name for Blob-hosted content.

## When Not To Use

- Don't use `LRS` for data that must survive datacenter or regional disasters unless another recovery mechanism exists.
- Don't expose storage broadly with public network access when only selected networks need access.
- Don't assume a container access level makes blobs public if account-level anonymous access is disabled.
- Don't choose `Premium` storage solely for capacity; choose it for performance.

## Exam Triggers

- `GRS` protects from regional outage; `RA-GRS` allows reads from secondary before failover.
- `GZRS` gives zone resilience plus geo-redundancy; `RA-GZRS` adds secondary read access.
- `Private endpoint` means private IP in VNet and no public internet exposure.
- `Service endpoint` means public endpoint remains, but access is restricted to selected VNets/subnets.
- `Firewalls and virtual networks` is the storage account portal area for network restrictions.
- Custom domain for Blob Storage uses `CNAME` mapping.
- Storage endpoints are service-specific: `.blob`, `.file`, `.queue`, and `.table.core.windows.net`.

## Knowledge Check Answers

1. `GRS` replicates data to a secondary geographic region to protect against regional outages.
2. Azure Private Endpoints assign a private IP from a VNet to the storage account.
3. Use Azure Custom Domain to map a custom domain to Blob Storage.
4. Use `Firewalls and virtual networks` to restrict access to specific subnets.
5. Use `HTTPS` for secure Blob access through a custom domain.
6. Not verifying domain ownership before mapping can cause custom domain access issues.
7. Use `GRS` when data must remain accessible after regional failover and immediate consistency isn't required.
8. `RA-GRS` improves on `GRS` by allowing read access to the secondary region.
