# Secure Azure Resources With RBAC - Study Review

## Core Idea

Azure role-based access control (Azure RBAC) is the authorization system for Azure resources. It controls who can access Azure resources, what they can do, and where the access applies.

This module maps to `Manage access to Azure resources`, especially built-in roles, role assignments at scopes, and interpreting access assignments.

## Key Capabilities

- Verify access for yourself and others.
- Assign built-in roles at the correct scope.
- Remove access by deleting role assignments.
- Use least privilege when choosing roles and scopes.
- View Azure RBAC changes in the Azure Activity Log.
- Create custom roles when built-in roles do not fit.

## How Azure RBAC Works

Azure RBAC grants access through a role assignment. A role assignment combines:

- `Security principal`: who gets access.
- `Role definition`: what permissions are granted.
- `Scope`: where the access applies.

Security principals can be:

- Users
- Groups
- Service principals
- Managed identities

Scope inheritance order:

- Management group
- Subscription
- Resource group
- Resource

Access assigned at a parent scope is inherited by child scopes. For example, `Contributor` at subscription scope applies to all resource groups and resources in that subscription.

## Built-In Roles

Important built-in roles:

- `Owner`: full access to resources and can delegate access to others.
- `Contributor`: can create and manage Azure resources but cannot grant access to others.
- `Reader`: can view existing resources.
- `User Access Administrator`: can manage user access to Azure resources.
- `Virtual Machine Contributor`: can manage virtual machines but not the virtual networks or storage accounts they connect to unless separately permitted.

Azure has many built-in roles. Use custom roles only when built-in roles are too broad or too narrow.

## Allow Model

Azure RBAC is an allow model.

- A role assignment grants allowed actions.
- Multiple role assignments are additive.
- If one assignment grants read and another grants write at the same scope, the effective permission includes both read and write.

Role definitions can include:

- `Actions`: allowed control-plane operations.
- `NotActions`: operations subtracted from `Actions`.
- `DataActions`: allowed data-plane operations.
- `NotDataActions`: data-plane operations subtracted from `DataActions`.

Exam point: `NotActions` is not a deny rule. It subtracts permissions from a role definition.

## Check Access

Use `Access control (IAM)` to review and troubleshoot Azure RBAC.

Common tasks:

- Use `My permissions` from the Azure portal profile menu to see your own assignments.
- Open a resource group or resource and select `Access control (IAM)` to view assignments.
- Use the `Role assignments` tab to see who has access.
- Use `Check access` to verify a specific user's access.
- Look for assignments marked as inherited from parent scopes.

## Grant Access

To grant access in the portal:

- Open the target scope, such as a resource group.
- Select `Access control (IAM)`.
- Select `Add` > `Add role assignment`.
- Choose the role.
- Choose the user, group, service principal, or managed identity.
- Review and assign.

You need a role such as `Owner` or `User Access Administrator` to create role assignments.

Use least privilege:

- Assign only the permissions required.
- Assign at the narrowest practical scope.
- Prefer groups over individual users for repeatable access management.

## Remove Access

To remove access, delete the role assignment. Removing a user from a group can also remove access that was inherited through that group.

Be careful to check inherited assignments. If access comes from a parent scope, removing a role assignment at a child scope will not remove the inherited access.

## Activity Logs

Azure RBAC changes are recorded in the Azure Activity Log.

For audit reports, search for `Activity log` and filter by operations such as:

- `Create role assignment (roleAssignments)`
- `Delete role assignment (roleAssignments)`
- `Create or update custom role definition (roleDefinitions)`
- `Delete custom role definition (roleDefinitions)`

You can set a time range, such as the last week or last month, and export the results as CSV.

## When To Use

- Use `Reader` when users only need visibility.
- Use `Contributor` when users need to create and manage resources but must not grant access.
- Use `Owner` only when the user must manage resources and delegate access.
- Use `User Access Administrator` when the user should manage access without full resource ownership.
- Assign access at resource scope when a user needs access to only one resource.
- Assign access at resource group scope when a user needs access to all resources in that group.
- Assign access at subscription or management group scope only for broad administrative responsibilities.

## When Not To Use

- Do not use Microsoft Entra admin roles to manage Azure resource permissions; use Azure RBAC.
- Do not assign `Owner` when `Contributor` or a narrower role is enough.
- Do not assign broad subscription access when resource or resource group scope is enough.
- Do not expect Azure RBAC to enforce configuration standards; use Azure Policy for that.
- Do not treat `NotActions` as an explicit deny.

## Exam Triggers

- Who, what, where: security principal, role definition, scope.
- Can manage resources but not grant access: `Contributor`.
- Full access and can delegate access: `Owner`.
- View-only access: `Reader`.
- Manage access assignments: `User Access Administrator`.
- User needs access only to one VM: assign role at `resource` scope.
- Developer needs full access to a resource group: assign at `resource group` scope.
- Check a user's access: `Access control (IAM)` > `Check access`.
- Review role assignment history: `Activity log`.
- Filter RBAC report: `roleAssignments` and `roleDefinitions`.
- Access inherited from parent scope: shown as `Inherited` in IAM.
- Role assignment disabled in portal: current user lacks permission to assign roles.

## Knowledge Check Answers

1. A role definition is a named collection of permissions assignable to a user, group, or application.
2. Use `Contributor` when a user must create and manage Azure resources but cannot grant access to others.
3. Scope inheritance order is management group, subscription, resource group, resource.
4. To check a team member's access to a resource group, open the resource group and select `Access control (IAM)` > `Check access`.
5. To grant access to just one virtual machine, assign the appropriate role at the resource scope.
6. For least privilege when a developer needs full access to a resource group, assign the role at resource group scope.
7. To report role assignments for the last week, use `Activity log` and filter for `Create role assignment (roleAssignments)`.
