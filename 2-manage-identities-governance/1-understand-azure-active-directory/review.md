# Microsoft Entra ID - Study Review

## Core Idea

Microsoft Entra ID is Microsoft's cloud-based identity and access management service. It manages identities, enforces access policies, and provides authentication and authorization for cloud and on-premises applications.

Microsoft Entra ID and Active Directory Domain Services both support identity management, but they are not the same product.

## Microsoft Entra ID Vs AD DS

AD DS is the traditional Windows Server-based directory service.

Key AD DS characteristics:

- Hierarchical X.500-based directory structure.
- Uses DNS to locate resources such as domain controllers.
- Uses LDAP for directory queries and management.
- Primarily uses Kerberos for authentication.
- Uses organizational units (OUs) and Group Policy Objects (GPOs).
- Includes computer objects for domain-joined machines.
- Uses trusts between domains.

Microsoft Entra ID is designed for cloud and internet-based identity.

Key Microsoft Entra ID characteristics:

- Primarily an identity solution for internet-based applications.
- Uses HTTP and HTTPS communications, mainly ports `80` and `443`.
- Multi-tenant cloud directory service.
- Users and groups are created in a flat structure.
- Does not use OUs or GPOs.
- Does not use LDAP for queries; it uses REST APIs over HTTP/HTTPS.
- Does not use Kerberos as its primary authentication model.
- Uses SAML, WS-Federation, and OpenID Connect for authentication.
- Uses OAuth for authorization.
- Includes federation capabilities.

Exam point: deploying AD DS on an Azure virtual machine is still AD DS. It does not become Microsoft Entra ID.

## Microsoft Entra ID For Cloud Apps

Microsoft Entra ID provides a shared cloud directory for Microsoft cloud services and applications.

It supports identity for services such as:

- Microsoft 365
- Azure
- Microsoft Dynamics 365
- Intune
- Azure App Service web apps

Instead of each cloud service having a separate identity store, Microsoft Entra ID can provide centralized authentication and authorization.

Microsoft Entra ID can also provide single sign-on (SSO) across Microsoft services, custom apps, and supported third-party identity providers or applications.

## Microsoft Entra ID P1

Microsoft Entra ID P1 adds capabilities beyond the Free and Office 365 editions.

Important P1 features from the module:

- Self-service group management.
- Advanced security reports and alerts.
- Multi-factor authentication for supported cloud and on-premises scenarios.
- Microsoft Identity Manager licensing for hybrid identity scenarios.
- Enterprise SLA of `99.9%`.
- Self-service password reset with password writeback.
- Cloud App Discovery.
- Conditional Access based on device, group, or location.
- Microsoft Entra Connect Health.

## Microsoft Entra ID P2

Microsoft Entra ID P2 includes P1 capabilities and adds stronger risk and privilege controls.

Important P2 features:

- Microsoft Entra ID Protection.
- Microsoft Entra Privileged Identity Management.

Use Microsoft Entra ID Protection to detect risky users, risky sign-ins, and irregular sign-in behavior.

Use Privileged Identity Management when administrative access needs extra governance, such as just-in-time or time-bound privileged role activation.

## Microsoft Entra Domain Services

Microsoft Entra Domain Services provides managed domain services for scenarios that need domain join, LDAP, Kerberos, or NTLM compatibility without managing domain controllers yourself.

Important limitation from the knowledge check:

- Microsoft Entra Domain Services should not be treated as a full replacement for on-premises AD DS in every scenario.
- One limitation is that the organizational unit structure is flat compared with traditional AD DS.

## When To Use Microsoft Entra ID

Use Microsoft Entra ID when you need to:

- Manage identities for cloud resources.
- Provide authentication and authorization for Microsoft cloud services.
- Support SSO for cloud applications.
- Apply Conditional Access policies.
- Use MFA and self-service password reset.
- Monitor identity health and sign-in risks.
- Integrate applications with a centralized identity provider.

## When AD DS Is Still Relevant

AD DS remains relevant when you need:

- Traditional domain join.
- Kerberos-based Windows authentication.
- LDAP directory queries.
- OUs and GPOs.
- Domain trusts.
- Traditional computer object management.

Microsoft Entra ID and AD DS are often used together in hybrid environments.

## Exam Triggers

- Cloud-based identity and access management: Microsoft Entra ID.
- Traditional Windows Server directory: AD DS.
- OUs and GPOs: AD DS, not Microsoft Entra ID.
- LDAP queries: AD DS, not Microsoft Entra ID.
- REST API over HTTP/HTTPS: Microsoft Entra ID.
- Kerberos primary authentication: AD DS.
- OAuth authorization: Microsoft Entra ID.
- SAML, WS-Federation, OpenID Connect: Microsoft Entra ID authentication protocols.
- Conditional Access by device, group, or location: Microsoft Entra ID P1/P2.
- Operational health monitoring: Microsoft Entra Connect Health.
- Bridge on-premises identity stores with Microsoft Entra ID: Microsoft Identity Manager.
- Detect risky or irregular sign-ins: Microsoft Entra ID Protection.
- Govern privileged administrator access: Privileged Identity Management.
- Self-service password reset: Microsoft Entra ID feature, not native AD DS.

## Knowledge Check Answers

1. Microsoft Entra ID primarily uses OAuth for authorization in internet-based application scenarios.
2. Microsoft Entra Connect Health provides operational insight and health monitoring.
3. A Microsoft Entra ID limitation compared to AD DS is lack of GPO support.
4. Microsoft Identity Manager helps bridge on-premises identity stores such as AD DS with Microsoft Entra ID.
5. Use Microsoft Entra ID Protection to identify irregular sign-in activity.
6. Self-service password reset is available in Microsoft Entra ID but not natively in AD DS.
7. Microsoft Entra Domain Services has limitations compared with AD DS, including a flat organizational unit structure.
8. Conditional Access is included in both P1 and P2 and supports access decisions based on device, group, or location.
9. OAuth is the Microsoft Entra ID authorization protocol that differs from AD DS.
