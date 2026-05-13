# Configure Azure Files And Azure File Sync Review

## Core Idea

Azure Files provides fully managed cloud file shares over standard protocols, and Azure File Sync caches Azure file shares on Windows Server. For AZ-104, focus on Azure Files use cases, protocols, tiers, authentication, snapshots, soft delete, Storage Explorer, and File Sync components.

## Exam Scope

- Domain: `Implement and manage storage` (15-20%).
- Objectives: create and configure Azure file shares, configure snapshots and soft delete for Azure Files, configure identity-based access for Azure Files, and manage data with Azure Storage Explorer.

## Key Capabilities

- Azure Files is a PaaS file share service; no VMs, operating system management, or server patching required.
- Azure file shares can be accessed by `SMB`, `NFS`, and `HTTP`.
- Clients can connect from Windows, Linux, and macOS.
- A single Azure file share can store up to `100 TiB`; an individual file can be up to `4 TiB`.
- Data is encrypted at rest and in transit.
- Azure file shares integrate with Microsoft Entra identities or AD DS identities synced to Microsoft Entra ID.
- Azure File Sync caches Azure Files shares on on-premises Windows Server or cloud VMs.

## Azure Files vs Blob Storage

| Azure Files | Blob Storage |
| --- | --- |
| True directory objects and file shares. | Flat object namespace in containers. |
| Access through SMB, NFS, REST, and client libraries. | Access through REST and client libraries at massive object scale. |
| Best for lift-and-shift apps that expect native file system APIs. | Best for unstructured object data, streaming, browser access, and random-access object scenarios. |
| Good for shared tools, configs, logs, and diagnostic data across VMs. | Good for images, video, backups, archives, and distributed object access. |

## File Share Tiers

| Tier | Account Type | Performance | Redundancy | Billing | Use Case |
| --- | --- | --- | --- | --- | --- |
| `Premium` | `FileStorage` | SSD, low latency | `LRS`, `ZRS` | Provisioned | High-performance workloads. |
| `Transaction Optimized` | `GPv2` | Standard HDD | `LRS`, `GRS`, `RA-GRS`, `ZRS`, `GZRS`, `RA-GZRS` | Pay-as-you-go | High-transaction workloads. |
| `Hot` | `GPv2` | Standard HDD | `LRS`, `GRS`, `RA-GRS`, `ZRS`, `GZRS`, `RA-GZRS` | Pay-as-you-go | General-purpose team shares. |
| `Cool` | `GPv2` | Standard HDD | `LRS`, `GRS`, `RA-GRS`, `ZRS`, `GZRS`, `RA-GZRS` | Pay-as-you-go | Cost-efficient online archive and backup. |

- `Premium` uses provisioned billing; Standard tiers use pay-as-you-go billing.
- A single Azure file share doesn't support both SMB and NFS, but one storage account can contain SMB and NFS shares.
- SMB uses port `445`; many ISPs block outbound `445`, which commonly breaks on-premises mounting.

## Authentication

| Method | Key Detail |
| --- | --- |
| Identity-based SMB authentication | Supports on-premises AD DS, Microsoft Entra Domain Services, and Microsoft Entra Kerberos. Assign RBAC after selecting the identity source. |
| Access key | Older, static, full-control option; avoid sharing because it bypasses access controls. |
| SAS token | Restricted URI-based access; for Azure Files, used for REST API access from code. |

## File Share Snapshots

- Snapshots are incremental, read-only, point-in-time copies at the share level.
- Snapshots capture only changes since the last snapshot to reduce time and cost.
- Same snapshot experience applies for SMB and NFS shares in Azure public regions.
- A snapshot adds a unique timestamp to the share URI.
- Snapshots use the file share's redundancy settings.
- Azure Files supports up to `200` snapshots per file share.
- Snapshots persist until deleted; deleting the share deletes all snapshots.
- Azure Backup can lease snapshots to help prevent accidental deletion.
- You can restore a file, folder, or full share; full restore requires only the latest snapshot.

## Soft Delete

- Soft delete for Azure Files is enabled at the storage account level.
- Deleted file shares transition to a soft-deleted state instead of being permanently erased.
- Retention can be configured from `1` to `365` days.
- Soft delete can be enabled for new or existing file shares.
- Use soft delete for accidental deletion recovery, failed upgrade rollback, ransomware recovery, retention requirements, and business continuity.

## Azure Storage Explorer

- Azure Storage Explorer is a standalone app for Windows, macOS, and Linux.
- It can connect to storage accounts in subscriptions, shared/external storage accounts, national clouds, local emulator storage, or services attached by SAS.
- Full access requires both Azure Resource Manager management permissions and data-plane permissions through Microsoft Entra ID.
- Access keys allow broad access to the entire storage account; rotate regularly and secure them carefully.
- Two access keys are provided so one key can remain in use while the other is regenerated.

## Azure File Sync Components

| Component | Role |
| --- | --- |
| `Storage Sync Service` | Azure resource that manages synchronization; supports up to `100` sync groups and `99` registered Windows Servers. |
| `Sync group` | Sync relationship containing one cloud endpoint and up to `50` server endpoints. |
| `Cloud endpoint` | Azure file share in the sync group; only one per sync group. |
| `Server endpoint` | NTFS path on a registered Windows Server; can't be system volume. |
| `Azure File Sync Agent` | Background Windows service installed on each Windows Server. |

- Azure File Sync turns Windows Server into a local cache of Azure file shares.
- Local users can access cached data through protocols available on Windows Server, such as SMB, NFS, and FTPS.
- Azure File Sync supports branch office caching, hybrid application access, backup/disaster recovery, and cloud tiering.
- Cloud tiering keeps recently accessed data local and moves older data to Azure Files.

## When To Use

- Use Azure Files when applications require file shares, true directories, or native file system APIs.
- Use Azure Files for shared diagnostic logs, configuration files, tools, and utilities across VMs.
- Use `Premium` Azure Files for high-performance low-latency workloads.
- Use snapshots for point-in-time recovery from bad deployments, corruption, or accidental changes.
- Use soft delete when deleted shares must be recoverable for a retention period.
- Use Azure File Sync for branch office caching and hybrid file server modernization.

## When Not To Use

- Don't use Azure Files when object storage semantics and massive unstructured scale are the primary requirement; use Blob Storage.
- Don't use access keys as a normal user access model when identity-based authentication is available.
- Don't expect one share to support both SMB and NFS protocols.
- Don't forget port `445` requirements for SMB access from on-premises networks.
- Don't delete a file share unless you understand its snapshots are deleted with it.

## Exam Triggers

- Azure Files = SMB/NFS file shares and true directories.
- Blob Storage = unstructured object data in containers.
- Soft delete recovery retention: `1` to `365` days.
- File share snapshots: incremental, read-only, share-level, up to `200` per share.
- Storage Explorer requires management and data-plane permissions.
- Azure File Sync sync group: one cloud endpoint and up to `50` server endpoints.
- Storage Sync Service: up to `100` sync groups and `99` registered Windows Servers.
- SMB connectivity issue from on-premises often means outbound port `445` is blocked.

## Knowledge Check Answers

1. Use Azure Files for diagnostic logs and metrics shared across multiple VMs.
2. Configure soft delete to recover deleted Azure file shares.
3. Azure Storage Explorer requires Microsoft Entra ID permissions plus appropriate data access.
4. File share snapshots capture point-in-time, read-only copies.
5. Incremental snapshots reduce cost by saving only changes since the previous snapshot.
6. Enable soft delete by configuring the retention period in the Azure portal.
7. Use Azure Files to replace on-premises file servers with cloud SMB/NFS shares.
8. Azure Files provides true directory objects, unlike Blob Storage.
9. Set the soft delete retention period to match organizational retention requirements.
