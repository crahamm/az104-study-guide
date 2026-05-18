Determine storage account types
===============================

General purpose Azure storage accounts have two basic [types](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-overview?toc=%2Fazure%2Fstorage%2Fblobs%2Ftoc.json#types-of-storage-accounts): Standard and Premium.

### Things to know about storage account types

**Standard** storage accounts are backed by magnetic hard disk drives (HDD). A standard storage account provides the lowest cost per GB. You can use Standard storage for applications that require bulk storage or where data is infrequently accessed.

**Premium** storage accounts are backed by solid-state drives (SSD) and offer consistent low-latency performance. You can use Premium storage for Azure virtual machine disks with I/O-intensive applications like databases.

> **Note:** You can't convert a Standard storage account to a Premium storage account or vice versa. You must create a new storage account with the desired type and copy data, if applicable, to a new storage account. All storage account types are encrypted by using Storage Service Encryption (SSE) for data at rest.

| Storage account | Supported services | Redundancy options | Recommended usage |
| --- |  --- |  --- |  --- |
| [**Standard****general-purpose v2**](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-upgrade) | Blob Storage (including Data Lake Storage), Queue Storage, Table Storage, and Azure Files | LRS, GRS, RA-GRS, ZRS, GZRS, RA-GZRS | Standard storage account for most scenarios, including blobs, file shares, queues, tables, and disks (page blobs). |
| --- |  --- |  --- |  --- |
| [**Premium** **block blobs**](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blob-block-blob-premium) | Blob Storage (including Data Lake Storage) | LRS, ZRS | Premium storage account for block blobs and append blobs. Recommended for applications with high transaction rates. Use Premium block blobs if you work with smaller objects or require consistently low storage latency. This storage is designed to scale with your applications. |
| [**Premium** **file shares**](https://learn.microsoft.com/en-us/azure/storage/files/storage-how-to-create-file-share) | Azure Files | LRS, ZRS | Premium storage account for file shares only. Recommended for enterprise or high-performance scale applications. Use Premium file shares if you require support for both Server Message Block (SMB) and NFS file shares. |
| [**Premium** **page blobs**](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blob-pageblob-overview) | Page blobs only | LRS only | Premium high-performance storage account for page blobs only. Page blobs are ideal for storing index-based and sparse data structures, such as operating systems, data disks for virtual machines, and databases. |

> **Note:** Administrators managing existing Azure subscriptions may encounter legacy storage account types such as General-purpose v1 (GPv1) and legacy BlobStorage accounts. Microsoft recommends upgrading legacy accounts to General-purpose v2 for access to all current capabilities. Upgrades are supported in-place via the Azure portal, Azure CLI, or PowerShell.

> **Tip:** Before continuing, consider working through the [*Create a storage account*](https://learn.microsoft.com/en-us/training/modules/create-azure-storage-account/) training module.
