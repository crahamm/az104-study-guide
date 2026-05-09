# ARM Templates In Visual Studio Code - Study Review

## Core Idea

Azure Resource Manager templates, or ARM templates, are JSON files that define Azure infrastructure and configuration declaratively. They support infrastructure as code by letting you store, version, validate, and redeploy infrastructure definitions consistently.

This module supports the AZ-104 objective `Automate deployment of resources by using Azure Resource Manager (ARM) templates or Bicep files`.

## Key Capabilities

- Define Azure resources in JSON.
- Deploy infrastructure consistently with declarative syntax.
- Use templates as infrastructure as code.
- Version templates in source control.
- Deploy templates with Azure CLI or Azure PowerShell.
- Add flexibility with parameters.
- Return deployment values with outputs.
- Use Visual Studio Code and ARM template tooling for authoring.

## ARM Template Structure

Common ARM template sections:

- `$schema`: required. Points to the JSON schema for the template.
- `contentVersion`: required. Tracks the version of the template.
- `apiProfile`: optional. Defines API versions for resource types.
- `parameters`: optional. Values supplied at deployment time.
- `variables`: optional. Values used to simplify expressions.
- `functions`: optional. User-defined functions.
- `resources`: required. Azure resources to deploy or update.
- `outputs`: optional. Values returned after deployment.

Exam point: `idempotent` is an ARM template behavior, not a template section.

## Infrastructure As Code

Infrastructure as code means infrastructure is described in code and managed like application code.

Benefits:

- Consistent configurations.
- Improved scalability.
- Faster deployments.
- Better traceability.
- Source control and versioning.
- CI/CD integration with tools such as Azure Pipelines or GitHub Actions.

ARM templates are declarative. You define the desired end state, and Azure Resource Manager handles the deployment sequence.

## Deployment Behavior

ARM templates are `idempotent`.

This means:

- Running the same unchanged template again does not recreate or unnecessarily modify resources.
- Azure Resource Manager creates missing resources.
- Azure Resource Manager updates resources only when template changes require it.

Azure Resource Manager also:

- Validates the template before deployment.
- Orchestrates dependencies.
- Creates resources in parallel when possible.
- Records deployment history in the Azure portal.

## Deployment Commands

Common Azure CLI commands:

- Sign in: `az login`
- List locations: `az account list-locations`
- Create a resource group: `az group create`
- Set defaults: `az configure --defaults`
- Deploy to a resource group: `az deployment group create`

Use `az deployment group create`, not the older `az group deployment create`.

Example:

```bash
az deployment group create \
  --name addstorage \
  --resource-group myResourceGroup \
  --template-file azuredeploy.json
```

PowerShell equivalent:

```powershell
New-AzResourceGroupDeployment
```

## Resources

Resources are defined with a resource provider and resource type.

Example:

- Provider: `Microsoft.Storage`
- Resource type: `storageAccounts`
- Full type: `Microsoft.Storage/storageAccounts`

Resource definitions commonly include:

- `type`
- `apiVersion`
- `name`
- `location`
- `sku`
- `kind`
- `properties`

Storage account exam detail:

- Storage account names must be globally unique.
- Names must be `3` to `24` characters.
- Names must use lowercase letters, numbers, and hyphens.

## Parameters

Use parameters for values that vary between deployments.

Good parameter candidates:

- Resource names.
- SKU.
- Size.
- Capacity.
- Environment-specific settings.
- Usernames and secrets.

Parameter facts:

- Templates support up to `256` parameters.
- Use `allowedValues` to restrict acceptable values.
- Use `defaultValue` when a safe default exists.
- Use `metadata.description` to document parameters.
- Use `secureString` for passwords or secrets.
- Use `secureObject` for sensitive JSON object data.

Do not hardcode usernames, passwords, or secrets in templates.

## Outputs

Use `outputs` to return values after deployment.

Examples:

- Storage account endpoints.
- Resource IDs.
- Connection information needed by another deployment step.

The `reference()` function can read runtime state, such as a storage account's `primaryEndpoints`.

## When To Use

Use ARM templates when you need to:

- Deploy Azure resources consistently.
- Repeat deployments across environments.
- Store infrastructure definitions in source control.
- Track deployment history.
- Validate infrastructure before deployment.
- Integrate infrastructure deployment into CI/CD.
- Break complex deployments into linked or nested templates.

## When Not To Use

Do not use hardcoded templates when the value should vary per environment. Use parameters instead.

Do not use plain `string` or default values for secrets. Use `secureString` or `secureObject`.

For new infrastructure as code authoring, Microsoft recommends `Bicep` for a simpler authoring experience, though AZ-104 still expects ARM template literacy.

## Exam Triggers

- JSON infrastructure definition: ARM template.
- Desired state rather than step-by-step commands: declarative syntax.
- Same deployment run again with no changes: no resource changes because templates are `idempotent`.
- Required resource section: `resources`.
- Required schema section: `$schema`.
- Required version section: `contentVersion`.
- Values supplied at deployment time: `parameters`.
- Values returned after deployment: `outputs`.
- Sensitive value parameter type: `secureString`.
- Deploy template to resource group with Azure CLI: `az deployment group create`.
- Old deployment command to avoid: `az group deployment create`.
- Storage account provider/type: `Microsoft.Storage/storageAccounts`.

## Knowledge Check Answers

1. An ARM template is a JSON file that defines the infrastructure and configuration for a deployment.
2. `idempotent` is not an ARM template element.
3. If an unchanged template is run again, Azure Resource Manager does not make changes to the deployed resources.
