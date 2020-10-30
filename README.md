# Welcome to the Template Specs Private Preview

## Read the docs

* [Template Specs overview](https://docs.microsoft.com/azure/azure-resource-manager/templates/template-specs)
* [Quickstart: Create and deploy a template spec](https://docs.microsoft.com/azure/azure-resource-manager/templates/quickstart-create-template-specs)
* [Tutorial: Create a template spec with linked templates](https://docs.microsoft.com/azure/azure-resource-manager/templates/template-specs-create-linked)
* [Tutorial: Deploy a template spec as a linked template](https://docs.microsoft.com/azure/azure-resource-manager/templates/template-specs-deploy-linked-template)

## To install the PowerShell cmdlets
Install the latest version of [Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-az-ps?view=azps-5.0.0)

## To install the CLI commands
Install the latest version of the [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli)

## To manage template specs in the Azure Portal
The work here is not *quite* done, but you can play with what's currently complete at https://aka.ms/gettemplates

## Known limitations

* The relativePath property will *only* work for TemplateSpec-based deployments. If you use this property in a generic template deployment (from your local file system or from an external URI), the deployment will fail and tell you the relativePath property is not valid. During the private preview, we will enable support for this property in generic deployments.
* The portal experience for template specs is only available through a hidekey. Navigate to https://aka.ms/gettemplates to use the portal experience.

For a full list of issues, or to file a new one, look at the [issues tab](https://github.com/azure/template-specs/issues).

## Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
