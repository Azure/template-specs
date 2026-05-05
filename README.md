# Welcome to the Template Specs on GitHub

[Template Specs](https://learn.microsoft.com/azure/azure-resource-manager/templates/template-specs) let you store an Azure Resource Manager (ARM) or Bicep template as a resource type in Azure, version it, share it via Azure RBAC, and deploy it directly without first uploading the template to a storage account or repo.

## Read the docs

* [Template Specs overview](https://learn.microsoft.com/azure/azure-resource-manager/templates/template-specs)
* [Quickstart: Create and deploy a template spec](https://learn.microsoft.com/azure/azure-resource-manager/templates/quickstart-create-template-specs)
* [Tutorial: Create a template spec with linked templates](https://learn.microsoft.com/azure/azure-resource-manager/templates/template-specs-create-linked)
* [Tutorial: Deploy a template spec as a linked template](https://learn.microsoft.com/azure/azure-resource-manager/templates/template-specs-deploy-linked-template)
* [Author template specs with Bicep](https://learn.microsoft.com/azure/azure-resource-manager/bicep/template-specs)

## Install the tooling

* **Azure PowerShell** — install the latest [Az module](https://learn.microsoft.com/powershell/azure/install-azure-powershell). Template Spec cmdlets live in the `Az.Resources` module.
* **Azure CLI** — install the latest [Azure CLI](https://learn.microsoft.com/cli/azure/install-azure-cli). See [`az ts`](https://learn.microsoft.com/cli/azure/ts) for the Template Spec commands.
* **Bicep CLI** — install [Bicep](https://learn.microsoft.com/azure/azure-resource-manager/bicep/install) to author and publish template specs from `.bicep` files using `bicep publish`.

## Manage template specs in the Azure portal

Template Specs are generally available in the Azure portal. Search for **Template specs** in the portal, or go directly to [https://portal.azure.com](https://portal.azure.com/#view/HubsExtension/BrowseResource/resourceType/Microsoft.Resources%2FtemplateSpecs) to create, version, view, and deploy them.

## Known limitations

* The `relativePath` property in a `Microsoft.Resources/deployments` resource only works for template-spec–based deployments. If you use it in a generic template deployment (from a local file or external URI), the deployment will fail with a validation error stating that `relativePath` isn't valid.

For a full list of issues, or to file a new one, see the [issues tab](https://github.com/Azure/template-specs/issues).

## Contributing

This project welcomes contributions and suggestions. Most contributions require you to agree to a Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
