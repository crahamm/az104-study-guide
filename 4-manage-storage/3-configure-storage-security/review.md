# Configure Storage Security Review

## Core Idea

Azure Storage security combines encryption, authentication, authorization, network restrictions, monitoring, and threat detection. For AZ-104, know when to use Microsoft Entra ID, SAS, access keys, encryption options, customer-managed keys, and storage monitoring tools.

## Exam Scope

- Domain: `Implement and manage storage` (15-20%).
- Objectives: configure access to storage, create and use SAS tokens, configure stored access policies, manage access keys, configure storage account encryption, and configure storage firewalls/virtual networks.

## Key Capabilities

- Azure Storage encrypts data at rest by default with Storage Service Encryption.
- Secure transfer can require encrypted in-transit access.
- Microsoft recommends Microsoft Entra ID with managed identities for blob, queue, and table data when possible.
- RBAC should be scoped as narrowly as practical, such as at the storage account or container level when supported.
- Storage Analytics and Storage Insights help monitor requests, usage, capacity, availability, and performance.
- Microsoft Defender for Storage adds proactive threat detection.

## Authorization Options

| Option | Use |
| --- | --- |
| `Microsoft Entra ID` | Preferred for fine-grained identity-based authorization with RBAC. |
| `Shared Key` | Uses primary/secondary account access keys; broad access and less flexible. |
| `SAS` | Delegates limited access to specific resources for a specific time. |
| Anonymous access | Public read access for containers/blobs; disabled by default and avoid for sensitive data. |

- Disable Shared Key authorization at the account level when you want to enforce Microsoft Entra authorization.
- Use Azure Key Vault to manage, rotate, and regenerate storage account access keys.

## Shared Access Signatures

| SAS Type | Key Detail |
| --- | --- |
| `User delegation SAS` | Secured with Microsoft Entra credentials; supported for Blob Storage and Data Lake Storage. |
| `Account SAS` | Can grant access across services and broader account-level operations. |
| `Service SAS` | Grants access to a specific resource in one storage service. |
| Stored access policy | Adds server-side control for service SAS; supports grouped restrictions and easier revocation. |

## SAS Best Practices

- Always create and distribute SAS URLs over `HTTPS`.
- Use stored access policies where possible so permissions can be revoked without regenerating account keys.
- Use short expiry times for ad hoc SAS tokens.
- Have clients renew SAS tokens before expiry.
- Avoid setting SAS start time to exactly now; omit start time or set it at least `15` minutes in the past to avoid clock skew.
- Grant minimum required permissions, such as read-only to one blob instead of read/write/delete to a container.
- Validate data written by clients through a SAS before using it.
- Don't use SAS when a middle-tier service with authentication, validation, and auditing is safer.

## SAS URI Parameters

| Parameter | Meaning |
| --- | --- |
| Resource URI | Storage endpoint and target operation/resource. |
| `sv` | Storage service version. |
| `ss` | Storage services included, such as blob or file. |
| `st` | Optional UTC start time. |
| `se` | UTC expiry time. |
| `sr` | Target resource type. |
| `sp` | Permissions, such as read/write. |
| `sip` | Allowed IP address or range. |
| `spr` | Allowed protocol, usually `https`. |
| `sig` | HMAC-SHA256 signature encoded with Base64. |

## Encryption

- Azure Storage encryption is automatic, transparent, enabled for all storage accounts, and can't be disabled.
- Data is encrypted before being written and decrypted when read.
- Azure Storage uses `256-bit AES` encryption for data at rest.
- Storage accounts have two `512-bit` access keys for Shared Key authorization and SAS signing.
- `Secure transfer required` helps enforce encryption in transit.
- Existing accounts should disallow deprecated `TLS 1.0` and `TLS 1.1`.

## Key Management

| Key Type | Description |
| --- | --- |
| Platform-managed keys | Generated, stored, and managed by Azure. Default for encryption at rest. |
| Customer-managed keys | Stored in customer-owned Key Vault or Managed HSM; customer controls lifecycle and access. |
| Infrastructure encryption | Encrypts data twice, once at service level and once at infrastructure level, using different keys and algorithms. |

- Customer-managed keys give control over create, disable, audit, rotate, and access control operations.
- Storage account and Key Vault for customer-managed keys must be in the same region, but can be in different subscriptions.
- Managed HSM provides `FIPS 140-2 Level 3` validation.

## Monitoring And Threat Detection

- Storage Insights provides metrics, logs, diagnostics, capacity, performance, availability, and usage trends.
- Use Storage Insights for monitoring, health analysis, optimization, and security auditing.
- Microsoft Defender for Storage provides active threat detection, malware scanning, sensitive data threat detection, and suspicious activity detection.
- Storage Insights is primarily passive monitoring and historical analysis; Defender for Storage is proactive threat detection.

## Lab And Portal Triggers

- A secure storage account can disable public network access, then allow selected networks and a client IP for administration.
- Lifecycle management can move base blobs to `Cool` after `30` days.
- Blob containers can use immutable storage policies with time-based retention, such as `180` days.
- A private blob URL should fail in an unauthenticated browser, but a generated Blob SAS URL should work within its allowed permissions and time window.
- Service endpoints use `Microsoft.Storage` on a VNet subnet, then the storage account network rule is limited to that subnet.

## When To Use

- Use Microsoft Entra ID and RBAC for durable identity-based access.
- Use SAS for limited, time-bound access to a specific storage resource.
- Use stored access policies when you need revocation control over service SAS tokens.
- Use customer-managed keys when compliance requires customer key ownership and rotation control.
- Use Microsoft Defender for Storage when active threat detection is required.

## When Not To Use

- Don't share account keys with users; access keys provide broad control and bypass granular permissions.
- Don't use long-lived SAS tokens unless backed by a clear policy and revocation plan.
- Don't use anonymous access for storage accounts containing sensitive data.
- Don't rely only on monitoring when you need real-time threat detection.

## Exam Triggers

- Recommended access: Microsoft Entra ID/managed identities where possible.
- Limited temporary access: `SAS`.
- Revoke grouped service SAS tokens: stored access policy.
- Manage and rotate account access keys: Azure Key Vault.
- Data at rest encryption: automatic, `256-bit AES`, can't be disabled.
- Customer-managed keys: Key Vault or Managed HSM; same region as storage account.
- SAS clock skew: omit start time or set start time `15` minutes in the past.

## Knowledge Check Answers

1. Use Azure Key Vault to manage and rotate storage account access keys.
2. Recommended authorization is Microsoft Entra ID where possible, or SAS for delegated limited access.
3. Use a Shared Access Signature for limited-time read access to image assets.
