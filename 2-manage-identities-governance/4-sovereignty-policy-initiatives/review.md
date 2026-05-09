# Sovereignty And Policy Initiatives - Study Review

## Core Idea

Azure Policy is the main Azure governance tool for enforcing organizational standards and assessing compliance at scale. It works with the Cloud Adoption Framework governance model to balance control, compliance, and productivity.

This module maps to `Manage Azure subscriptions and governance`, especially `Implement and manage Azure Policy`.

## Key Capabilities

- Enforce allowed regions, VM sizes, tags, security settings, and diagnostic requirements.
- Assess current and future resources for compliance.
- Group policies into initiatives for larger governance or regulatory goals.
- Assign policies at management group, subscription, or resource group scope.
- Use exemptions, attestations, and remediation tasks.
- Test policies safely with `enforcementMode`.
- React to policy state changes with Azure Event Grid.

## Cloud Governance

The Cloud Adoption Framework `Govern` methodology treats governance as a continuous process:

- Build a governance team.
- Assess cloud risks.
- Document governance policies.
- Enforce governance policies.
- Monitor governance.

Iterate on risk assessment, documentation, enforcement, and monitoring as requirements change.

The five core governance disciplines are:

- `Cost management`
- `Security baseline`
- `Resource consistency`
- `Identity baseline`
- `Deployment acceleration`

## Governance Hierarchy

Azure governance scope follows the management hierarchy:

- Management group
- Subscription
- Resource group
- Resource

Settings applied at higher scopes are inherited by lower scopes. A policy assigned at a management group can affect all subscriptions below it. A policy assigned at a resource group affects only that resource group and its resources.

## Azure Resource Manager

Azure Resource Manager is the deployment and management layer for Azure. It handles create, update, and delete operations for Azure resources.

Key exam distinction:

- `Control plane`: management operations such as creating resources, assigning RBAC, deploying templates, auditing, monitoring, tagging, and policy evaluation.
- `Data plane`: service-specific data operations, such as reading Key Vault secrets, querying SQL data, or uploading files to a storage account.

Azure Policy is integrated with Azure Resource Manager and primarily evaluates control-plane operations. Some services support data-plane policy modes, such as `Microsoft.Kubernetes.Data`, `Microsoft.KeyVault.Data`, `Microsoft.Network.Data`, `Microsoft.ManagedHSM.Data`, `Microsoft.DataFactory.Data`, and `Microsoft.MachineLearningServices.v2.Data`.

## Greenfield And Brownfield

`Greenfield` means policy exists before a resource is created or updated.

- RBAC is checked before Azure Policy.
- If the caller lacks permission, policy is not evaluated.
- If the caller has permission, Azure Policy evaluates the requested target state.
- For updates, Azure Policy combines the submitted delta with the current resource state before evaluation.

`Brownfield` means resources already exist before the policy is assigned.

- Existing resources are evaluated by a compliance scan.
- The automatic full scan runs every `24 hours`.
- You can manually trigger a scan with `az policy state trigger-scan`.
- Existing noncompliant resources are flagged; they are not automatically deleted just because a new deny policy is assigned.

## Policy Resources

Main Azure Policy resource concepts:

- `Definitions`: describe conditions and effects.
- `Initiatives`: group multiple policy definitions into a single assignable policy set.
- `Assignments`: apply a definition or initiative to a scope.
- `Exemptions`: exclude a resource hierarchy or resource from evaluation while still counting it in compliance.
- `Attestations`: manually set compliance state for manual policies.
- `Remediations`: bring noncompliant resources into compliance for supported effects.

Built-in policies are provided by Microsoft. Custom policies are created when built-ins do not meet the requirement.

## Policy Definitions

A policy definition has two main parts:

- `condition`: compares resource fields or values to required criteria.
- `effect`: determines what happens when the condition matches.

Important JSON elements:

- `displayName`
- `description`
- `policyType`
- `mode`
- `metadata`
- `parameters`
- `policyRule`

The `policyRule` uses:

- `if`: conditions such as `allOf`, `anyOf`, or `not`.
- `then`: the effect to apply.

Use `parameters` to reuse one definition with different assignment values, such as allowed locations.

## Effects

Common Azure Policy effects:

- `disabled`: policy rule is not evaluated.
- `append`: adds fields to a request; mostly replaced by `modify`.
- `modify`: adds, updates, or removes properties or tags during create or update.
- `deny`: blocks a noncompliant request.
- `denyAction`: blocks a specific action at scale; currently supports `DELETE`.
- `audit`: logs a warning event but does not block the request.
- `auditIfNotExists`: audits related-resource conditions.
- `deployIfNotExists`: deploys a related resource when the condition is met.
- `manual`: requires self-attestation.

Layered policy assignments are cumulative and most restrictive.

## Enforcement Mode

`enforcementMode` is an assignment property used to test a policy without enforcing its effect.

Values:

- `Default`: policy effect is enforced.
- `DoNotEnforce`: policy evaluates compliance but does not enforce the effect or create Activity Log entries for the blocked action.

Exam distinction:

- `disabled` effect means the policy does not evaluate.
- `enforcementMode: DoNotEnforce` means the policy evaluates, but the effect does not happen.

## Safe Deployment

Recommended safe policy deployment:

- Start new assignments with `enforcementMode` disabled.
- Review compliance results before enforcing deny or modify behavior.
- Deploy policies through rings.
- Start with test and development scopes.
- Expand gradually to production.
- Treat policy as code and keep definitions in source control.

## When To Use

- Use Azure Policy to enforce standards across subscriptions and resource groups.
- Use initiatives for regulatory frameworks or multi-policy governance goals.
- Use `audit` to observe noncompliance without blocking work.
- Use `deny` to prevent noncompliant deployments.
- Use `modify` or `deployIfNotExists` when supported remediation is required.
- Use exemptions for approved exceptions.
- Use Event Grid when applications need to react to policy state changes.

## When Not To Use

- Do not use Azure Policy as a replacement for RBAC; RBAC controls who can act, Policy controls whether allowed actions comply.
- Do not assign broad deny policies directly to production without testing.
- Do not expect a new brownfield deny policy to delete existing noncompliant resources.
- Do not use `disabled` when you still need compliance evaluation; use `enforcementMode`.

## Exam Triggers

- Enforce allowed regions, VM sizes, tags, MFA, diagnostics, or replication rules: `Azure Policy`.
- Group many policy definitions: `initiative`.
- Apply policy to many subscriptions: assign at `management group` scope.
- Existing resources after new assignment: `Brownfield` compliance scan.
- Policy exists before resource deployment: `Greenfield`.
- Test policy without enforcement: `enforcementMode` set to `DoNotEnforce`.
- Disable policy evaluation entirely: `disabled` effect.
- Block noncompliant creation: `deny`.
- Log without blocking: `audit`.
- Add or update tags automatically: `modify`.
- Deploy missing related configuration: `deployIfNotExists`.
- Temporary approved exception: `waiver` exemption.
- Policy intent met another way: `mitigated` exemption.
- Manual compliance statement: `attestation`.
- Policy state event routing: Azure Policy events through `Azure Event Grid`.

## Knowledge Check Answers

1. Azure Policy assesses compliance at scale and enforces organizational and regulatory standards.
2. Deploy policies safely by starting with `enforcementMode` disabled and then using deployment rings.
3. `enforcementMode` lets you test policy outcomes without initiating the policy effect.
4. Azure Resource Manager is the Azure deployment and management service for creating, updating, and deleting resources.
5. Azure Policy can be assigned at management group, subscription, and resource group scopes.
