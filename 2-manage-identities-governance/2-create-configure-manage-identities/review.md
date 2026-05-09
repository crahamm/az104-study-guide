# Create, Configure, and Manage Identities - Study Review

## Core Idea

Microsoft Entra ID centralizes identity management for Azure and Microsoft cloud services. For AZ-104, this module is mainly about creating users and groups, managing group membership, assigning licenses, and choosing the right device identity model.

This module maps to the exam objective `Manage Microsoft Entra users and groups` under `Manage Azure identities and governance (20-25%)`.

## Key Capabilities

- Create and manage Microsoft Entra users.
- Distinguish `cloud identities`, `directory-synchronized identities`, and `guest users`.
- Create and manage `security groups` and `Microsoft 365 groups`.
- Use `assigned`, `dynamic user`, and `dynamic device` group membership.
- Assign licenses directly or through groups.
- Troubleshoot group-based license assignment errors.
- Configure device identity with registered, joined, or hybrid joined devices.
- Use custom security attributes for business-specific metadata and access decisions.
- Use provisioning automation with `SCIM 2.0` or API-driven inbound provisioning.

## Users

Every user who needs access to Azure or Microsoft cloud resources needs a Microsoft Entra user account. After authentication, Microsoft Entra ID issues an access token that is used to authorize what the user can access and do.

User identity types:

- `Cloud identities`: exist only in Microsoft Entra ID. Common for cloud-only users and administrator accounts.
- `Directory-synchronized identities`: originate in on-premises `Windows Server AD` and sync to Microsoft Entra ID.
- `Guest users`: external users invited into the tenant, such as vendors or contractors.

Important deletion behavior:

- Deleted users remain restorable for `30 days`.
- After permanent deletion, the account cannot be restored.
- Roles that can restore or permanently delete users include `Global administrator` and `User administrator`.

## Groups

Groups reduce repetitive access management by applying permissions or services to a collection of users, devices, or service principals.

Group types:

- `Security groups`: used to manage access to resources and assign permissions.
- `Microsoft 365 groups`: used for collaboration features such as a shared mailbox, calendar, files, and SharePoint site.

Membership types:

- `Assigned`: members are added and maintained manually.
- `Dynamic User`: users are added or removed automatically based on user attributes such as department, job title, or location.
- `Dynamic Device`: devices are added or removed automatically based on device attributes. This applies to security groups only.

Important exam points:

- Dynamic membership requires `Microsoft Entra ID P1`.
- Microsoft 365 groups support dynamic users, but not dynamic devices.
- If the requirement is collaboration, think `Microsoft 365 group`.
- If the requirement is permission assignment, think `security group`.

## Licenses

Microsoft paid cloud services such as Microsoft 365, Enterprise Mobility + Security, and Dynamics 365 require user licenses. License management is performed in the `Microsoft 365 admin center`, while Microsoft Entra ID tracks license assignment state.

Group-based licensing:

- Assigns one or more product licenses to a security group.
- Automatically assigns licenses to new group members.
- Removes inherited licenses when users leave the group.
- Can disable one or more service plans within a product license.
- Usually applies membership changes within minutes.
- Consumes only one license if the same license reaches a user from multiple sources.

Requirements:

- Group-based licensing requires `Microsoft Entra ID Premium P1` or higher, or `Office 365 Enterprise E3` or higher.
- You need enough licenses for each unique member of licensed groups.
- Set the user's `usage location` before assigning licenses, especially for multi-region tenants.
- If a user has no usage location during group-based assignment, the user inherits the directory location.

## License Errors

Group-based license assignment happens in the background, so errors are recorded on the user object and shown in the admin portal.

Common license errors:

- `CountViolation`: not enough available licenses. Buy more licenses or free unused ones.
- `MutuallyExclusiveViolation`: conflicting service plans. Remove or disable the conflicting plan or license.
- `DependencyViolation`: a service plan being removed is required by another product. Reassign the prerequisite or disable the dependent service first.
- `ProhibitedInUsageLocationViolation`: the service is not available for the user's usage location.
- Duplicate proxy address: Exchange Online cannot assign the license because another object already uses the proxy address.

Operational details:

- If a license issue is fixed, you may need to select `Reprocess` on the group or user license page.
- Before deleting a licensed group, remove the licenses from the group.
- For add-on products, keep the prerequisite service plan and add-on in the same group when using group-based licensing.
- When migrating from direct licenses to group licenses, verify users have equivalent inherited licenses before gradually removing direct assignments.

## Device Identity

Microsoft Entra ID supports device identities so organizations can control access from user devices and apply Conditional Access or device compliance rules.

### Microsoft Entra Registered

Use `Microsoft Entra registered` for BYOD and personal-device scenarios.

Key points:

- Device is registered with Microsoft Entra ID.
- The user does not need to sign in to the device with an organization account.
- Common for personal Windows, macOS, iOS, Android, or Linux devices.
- Supports SSO to cloud resources and Conditional Access when integrated with Intune or app protection policies.

### Microsoft Entra Joined

Use `Microsoft Entra joined` for cloud-first or cloud-only organization-owned devices.

Key points:

- Device is joined only to Microsoft Entra ID.
- User signs in to the device with an organizational account.
- Intended for work-owned Windows devices and cloud-based management.
- Supports SSO to cloud and on-premises resources, Conditional Access, SSPR, and Windows Hello PIN reset.

### Hybrid Microsoft Entra Joined

Use `Hybrid Microsoft Entra joined` when an organization still depends on on-premises Active Directory.

Key points:

- Device is joined to on-premises AD and registered with Microsoft Entra ID.
- Best for hybrid environments with existing AD, Group Policy, imaging, or AD-dependent Win32 apps.
- Supports management with Group Policy, Configuration Manager, or co-management with Intune.

Important exam point:

- `Device writeback` is no longer supported or recommended.
- New hybrid identity deployments should use `Cloud Kerberos Trust` instead.

## Custom Security Attributes

Custom security attributes are tenant-wide business-specific key-value pairs assigned to Microsoft Entra objects.

Use them to:

- Extend user or application metadata.
- Categorize users, applications, or service principals.
- Support filtering, auditing, and fine-grained access control.
- Store values as `Boolean`, `integer`, or `string`.
- Use single-value or multi-value attributes.

Limitations:

- Not supported in `Microsoft Entra Domain Services`.
- Not supported in `SAML` token claims.
- Not supported in `JWT` claims.

## Automatic Provisioning

`SCIM 2.0` automates user and group provisioning between identity systems and target applications.

Core components:

- `HCM system`: HR source system for employee lifecycle data.
- `Microsoft Entra Provisioning Service`: connects to the application SCIM endpoint.
- `Microsoft Entra ID`: identity repository.
- `Target system`: application or system that receives provisioned users and groups.

Use automatic provisioning to create, update, or remove users based on source-system changes. This reduces the risk of stale accounts when users leave or change roles.

If the source system does not expose a SCIM endpoint, use `API-driven inbound provisioning` to send workforce data to the Microsoft Entra provisioning API.

## When To Use

- Use `cloud identities` for accounts managed only in Microsoft Entra ID.
- Use `directory-synchronized identities` when on-premises AD remains the source of authority.
- Use `guest users` for external vendors, contractors, or partners.
- Use `security groups` for access management and license assignment.
- Use `Microsoft 365 groups` for collaboration workloads.
- Use `dynamic groups` when membership should follow attributes automatically.
- Use group-based licensing for large teams or departments.
- Use `Microsoft Entra registered` for BYOD.
- Use `Microsoft Entra joined` for cloud-managed corporate devices.
- Use `Hybrid Microsoft Entra joined` for devices that still need on-prem AD integration.

## When Not To Use

- Do not use `Microsoft 365 groups` when the only requirement is resource permission management.
- Do not use direct per-user licensing at scale when group-based licensing fits.
- Do not expect dynamic device membership in Microsoft 365 groups.
- Do not remove direct licenses during migration until inherited group licenses are verified.
- Do not rely on `device writeback` for new hybrid designs.
- Do not expect custom security attributes to appear in `SAML` or `JWT` claims.

## Exam Triggers

- Shared mailbox, calendar, files, or SharePoint site: `Microsoft 365 group`.
- Access control or permission assignment: `security group`.
- Rule-based membership by department or job title: `dynamic user`.
- Rule-based device membership: `dynamic device` security group.
- Dynamic group requirement: `Microsoft Entra ID P1`.
- External vendor access: `guest user`.
- Deleted user recovery: `30 days`.
- Large team licensing: assign licenses to a group.
- Not enough licenses: `CountViolation`.
- Conflicting license plans: `MutuallyExclusiveViolation`.
- Dependent service plan problem: `DependencyViolation`.
- Service blocked by region: check `usage location`.
- Personal device with work account attached: `Microsoft Entra registered`.
- Organization-owned cloud device: `Microsoft Entra joined`.
- On-prem AD joined plus Microsoft Entra registration: `Hybrid Microsoft Entra joined`.
- Business-specific key-value metadata: `custom security attributes`.
- Automatic provisioning standard: `SCIM 2.0`.
- HR/custom source without SCIM endpoint: `API-driven inbound provisioning`.

## Knowledge Check Answers

1. For `MutuallyExclusiveViolation`, remove conflicting licenses or service plans from the user.
2. Custom security attributes define business-specific information that can categorize users and enforce access policies.
3. For shared mailbox, calendar, and files, create a `Microsoft 365 group`.
4. Custom security attributes add metadata that can be used to categorize and filter access logs.
5. For `CountViolation`, increase available licenses or free unused licenses.
6. For `DependencyViolation`, ensure dependent service plans are reassigned before removing the license.
7. `Security groups` manage permissions; `Microsoft 365 groups` provide collaboration features.
8. Certification-specific custom security attributes can be used in access policies to restrict access.
9. For a large team, assign licenses through a security group.
