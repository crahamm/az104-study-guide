# Configure Blob Storage Review

## Core Idea

Azure Blob Storage stores unstructured object data at scale. For AZ-104, know how to organize blobs in containers, choose access tiers, configure lifecycle management, enable protection features, and use object replication.

## Exam Scope

- Domain: `Implement and manage storage` (15-20%).
- Objectives: create and configure blob containers, configure storage tiers, configure blob lifecycle management, configure soft delete, configure blob versioning, configure object replication, and manage data with Storage Explorer or `AzCopy`.

## Key Capabilities

- Blob Storage stores text and binary data, including documents, images, videos, installers, backups, and archives.
- Blob Storage resources are organized as storage account -> container -> blob.
- A blob must exist in a container; containers can hold an unlimited number of blobs.
- A storage account can contain an unlimited number of containers.
- Public access is private by default and anonymous access should remain disabled unless content is intentionally public.

## Container Settings

| Setting | Key Detail |
| --- | --- |
| Name | Unique within the storage account; lowercase letters, numbers, and hyphens only. |
| Length | `3` to `63` characters. |
| `Private` | No anonymous access to container or blobs. |
| `Blob` | Anonymous read access to blobs only. |
| `Container` | Anonymous read and list access to the container and blobs. |

- `Blob` and `Container` public access levels only work if account-level `Allow Blob anonymous access` is enabled.

## Blob Types

| Blob Type | Use |
| --- | --- |
| `Block blob` | Default type; files, images, videos, text, and binary objects. |
| `Append blob` | Append-optimized workloads such as logging. |
| `Page blob` | Frequent random read/write workloads; VM OS and data disks; up to `8 TB`. |

- After a blob is created, its blob type can't be changed.

## Access Tiers

| Tier | Best For | Minimum Duration | Latency | Cost Pattern |
| --- | --- | --- | --- | --- |
| `Hot` | Frequently read/written data. | None | Milliseconds | Highest storage, lowest access. |
| `Cool` | Infrequently accessed online data. | `30` days | Milliseconds | Lower storage, higher access. |
| `Cold` | Rarely accessed online data. | `90` days | Milliseconds | Lower storage, higher access than Cool. |
| `Archive` | Offline long-term retention. | `180` days | Hours | Lowest storage, highest access/retrieval. |

- Archive blobs must be rehydrated to `Hot`, `Cool`, or `Cold` before reading.
- Rehydrate by `Copy Blob` to an online tier or `Set Blob Tier` in place.
- Archive rehydration supports `Standard` priority up to `15` hours and `High` priority within `1` hour for objects under `10 GB`, at higher cost.

## Lifecycle Management

- Lifecycle rules are available for `GPv2`, Premium block blob, and legacy Blob Storage accounts.
- Rules use `If` conditions and `Then` actions based on age, access, or modification dates.
- Actions include move to `Cool`, move to `Cold`, move to `Archive`, or delete the blob.
- Rules can apply to the whole account, selected containers, name prefixes, or blob index tags.
- Lifecycle management can delete current versions, previous versions, and snapshots.
- Rules can automatically move blobs from `Cool` back to `Hot` when accessed.

## Object Replication

- Object replication asynchronously copies blobs between containers based on replication policies.
- Replication includes blob content, metadata, properties, and versions.
- Blob versioning must be enabled on both source and destination accounts.
- Blob snapshots are not replicated.
- Source and destination accounts can use `Hot`, `Cool`, or `Cold` tiers and don't need to be in the same tier.
- A replication policy contains one or more rules that map source containers to destination containers.

## Data Protection

- Blob soft delete protects blobs, snapshots, and versions from accidental deletion or overwrite during the configured retention period.
- Blob versioning maintains previous blob versions so earlier versions can be restored.
- Common lab setting: configure blob soft delete for `21` days and enable blob versioning for website content recovery.

## Management Tools

- Use the Azure portal for a small number of uploads or manual configuration.
- Use Azure Storage Explorer to upload, download, preview, edit, and manage blobs, files, queues, tables, Data Lake Storage entities, and managed disks.
- Use `AzCopy` for command-line copy operations to and from Blob Storage, across containers, or across accounts.
- Use Azure Data Box Disk for large on-premises data transfers when network upload is impractical.

## Pricing Triggers

- Blob costs depend on data volume, operations, data transfer, and redundancy.
- Cooler tiers reduce per-GB storage cost but increase read, transaction, and retrieval charges.
- Geo-replication adds per-GB replication transfer charges.
- Outbound data transfer is billed as bandwidth usage.
- Moving account data from `Cool` to `Hot` is billed like reading all data; moving from `Hot` to `Cool` is billed like writing all data to Cool.

## When To Use

- Use `Hot` for active datasets and frequent reads/writes.
- Use `Cool` for short-term backup, disaster recovery data, and older media that must remain immediately available.
- Use `Cold` for rarely accessed data that still needs online millisecond access.
- Use `Archive` for compliance data, raw originals, secondary backups, and data that tolerates hours of retrieval latency.
- Use object replication to reduce read latency, distribute data for regional compute, or improve failover patterns.
- Use lifecycle management when access decreases predictably as data ages.

## When Not To Use

- Don't use `Archive` for data that must be read immediately.
- Don't rely on object replication for snapshots; snapshots are unsupported.
- Don't configure public container access unless both account-level anonymous access and container-level public access are intentionally enabled.
- Don't manually manage tier transitions for large data sets when lifecycle rules can automate them.

## Exam Triggers

- `Hot`, `Cool`, `Cold`, `Archive` are primarily cost/access pattern decisions.
- `Archive` is offline and has hours of retrieval latency.
- `Cool` minimum duration is `30` days, `Cold` is `90` days, and `Archive` is `180` days.
- Object replication requires blob versioning on source and destination.
- Object replication does not replicate snapshots.
- `AzCopy` is the CLI transfer tool; Storage Explorer is the GUI tool.
- Public blob access requires account-level anonymous access plus container access level.

## Knowledge Check Answers

1. Move a Cool-tier blob to `Archive` after 90 days if lifecycle policy indicates further cost reduction.
2. Lifecycle policy balances data accessibility with cost savings over time.
3. Use object replication for consistent blob availability across regions for compute workloads.
4. Move data to `Archive` when it is rarely accessed after a month.
5. Move blobs not accessed for over 365 days to `Archive` for long-term cost savings.
6. Container naming conventions ensure uniqueness within the account and help organize data.
7. Snapshots are not replicated because object replication doesn't support snapshot replication.
8. Lifecycle rules transition data by conditions such as age and access frequency.
9. Missing blob versioning on source or destination can prevent object replication.
