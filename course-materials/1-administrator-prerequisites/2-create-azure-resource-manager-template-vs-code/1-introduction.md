Introduction
============

JSON Azure Resource Manager templates (ARM templates) allow you to specify your project's infrastructure in a declarative and reusable way. You can version and save the templates in the same source control as your development project.

Suppose you're managing a software team that's developing an inventory system for your partner companies. You plan to deploy this product to Azure, and let each partner company have its own solution. You plan to implement different policies for each deployment through different Azure storage accounts. You decide to use the practice of *infrastructure as code* by using ARM templates. This approach lets you track the different versions and ensure that your infrastructure deployments for each environment are consistent and flexible.

In this module, we introduce you to ARM template structure and let you practice creating and deploying an ARM template to Azure.

**Note:**
Bicep is a language for defining your Azure resources. It has a simpler authoring experience than JSON, along with other features that help improve the quality of your infrastructure as code. We recommend that anyone new to infrastructure as code on Azure use Bicep instead of JSON. To learn about Bicep, see the [Fundamentals of Bicep](https://learn.microsoft.com/en-us/training/paths/fundamentals-bicep/) learning path.

Learning objectives
-------------------

In this module, you will:

-   Implement a JSON ARM template by using Visual Studio Code.
-   Declare resources and add flexibility to your template by adding parameters and outputs.

Prerequisites
-------------

-   Familiarity with Azure, including the Azure portal, subscriptions, resource groups, and resource definitions.
-   An Azure account. You can get a free account [here](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn_5f57c3df-9c14-af73-f8f8-da2369315010).
-   [Visual Studio Code](https://code.visualstudio.com/) installed locally.
-   Either:
    -   The latest [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli) tools installed locally.
    -   The latest [Azure PowerShell](https://learn.microsoft.com/en-us/powershell/azure/install-az-ps) installed locally.