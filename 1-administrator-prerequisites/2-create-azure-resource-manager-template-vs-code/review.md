# ARM Templates In Visual Studio Code - Study Review

## Core Idea

Azure Resource Manager templates, or ARM templates, are JSON files that define Azure infrastructure and configuration as code. They use declarative syntax: you describe the desired resources and properties, and Azure Resource Manager handles the deployment steps.

ARM templates support infrastructure as code because they can be versioned, reviewed, reused, and stored with application source code.

## Key Capabilities

- Define Azure infrastructure in JSON.
- Deploy consistent environments repeatedly.
- Store infrastructure definitions in source control.
- Use parameters to make deployments flexible.
- Use outputs to return values after deployment.
- Validate templates before deployment starts.
- Let Azure Resource Manager orchestrate dependencies and create resources in the correct order.
- Deploy resources in parallel when possible.
- Integrate deployments into CI/CD tools such as Azure Pipelines or GitHub Actions.

## ARM Template Structure

Common ARM template sections:

- `$schema`: Required. Points to the JSON schema for the deployment scope.
- `contentVersion`: Required. Documents the template version, such as `1.0.0.0`.
- `apiProfile`: Optional. Defines a collection of API versions for resource types.
- `parameters`: Optional. Values supplied during deployment.
- `variables`: Optional. Reusable values that simplify expressions.
- `functions`: Optional. User-defined functions for repeated expressions.
- `resources`: Required. The Azure resources to deploy or update.
- `outputs`: Optional. Values returned after deployment.

Exam point: `idempotent` is not a template section. It is a behavior of ARM template deployments.

## Infrastructure As Code Benefits

Infrastructure as code provides:

- Consistent configurations.
- Improved scalability.
- Faster deployments.
- Better traceability.

ARM templates are idempotent. If you redeploy the same template with no changes, Azure Resource Manager does not make changes to existing resources. If the template changes, Resource Manager applies only the required changes.

## Resource Definitions

Resources are declared in the `resources` section.

Each resource needs a resource provider and resource type in the form:

```text
{resource-provider}/{resource-type}
```

Example:

```text
Microsoft.Storage/storageAccounts
```

Important storage account naming rule from the module: storage account names must be globally unique, 3 to 24 characters, and use only lowercase letters, numbers, and hyphens.

## Deploying Templates

Common local deployment flow:

1. Sign in to Azure:

```bash
az login
```

2. Create a resource group:

```bash
az group create --name <resource-group-name> --location <location>
```

3. Optionally set a default resource group:

```bash
az configure --defaults group="<resource-group-name>"
```

4. Deploy a template at resource group scope:

```bash
az deployment group create \
  --name <deployment-name> \
  --template-file azuredeploy.json
```

Exam point: prefer `az deployment group create`. The older `az group deployment create` command is deprecated.

## Parameters

Parameters let you provide deployment-specific values at runtime. Use parameters for values that vary between environments, such as names, SKUs, sizes, capacity, and secrets.

Important limits and types:

- A template can have up to 256 parameters.
- Common parameter types include `string`, `secureString`, `int`, `bool`, `object`, `secureObject`, and `array`.
- Use `allowedValues` to restrict acceptable inputs.
- Use `minLength`, `maxLength`, `minValue`, and `maxValue` to validate parameter values.
- Use `metadata.description` to document what a parameter is for.

Security rule: never hardcode usernames, passwords, or secrets. Use parameters, and use `secureString` or `secureObject` for sensitive values.

Reference a parameter in a template with:

```json
"[parameters('storageName')]"
```

Pass parameter values during deployment with:

```bash
az deployment group create \
  --name <deployment-name> \
  --template-file azuredeploy.json \
  --parameters storageSKU=Standard_LRS storageName=<unique-name>
```

## Outputs

Outputs return values after a successful deployment. They are useful when a later task needs deployment-generated information, such as endpoints.

Example output pattern:

```json
"outputs": {
  "storageEndpoint": {
    "type": "object",
    "value": "[reference(parameters('storageName')).primaryEndpoints]"
  }
}
```

The `reference()` function retrieves runtime state for a deployed resource.

## When To Use ARM Templates

Use ARM templates when you need to:

- Define Azure infrastructure as code.
- Reuse the same infrastructure definition across environments.
- Deploy repeatable, consistent resources.
- Track infrastructure changes in source control.
- Parameterize deployments for development, test, and production.
- Integrate Azure deployments into CI/CD.

## Exam Triggers

- JSON file defining Azure infrastructure: ARM template.
- Declarative deployment syntax: ARM template.
- Same template can run repeatedly without unwanted changes: idempotent.
- Values supplied at deployment time: parameters.
- Sensitive values in a template: `secureString` or `secureObject`.
- Restrict allowed deployment values: `allowedValues`.
- Return deployment values after success: outputs.
- Get runtime state of a resource: `reference()`.
- Resource group deployment command: `az deployment group create`.
- Actual Azure resources to deploy: `resources` section.

## Knowledge Check Answers

1. An ARM template is a JSON file that defines the infrastructure and configuration for a deployment.
2. `idempotent` is not an ARM template element.
3. If an unchanged idempotent template is deployed again, Azure Resource Manager does not change the deployed resources.
