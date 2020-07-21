# Welcome to the Template Specs Private Preview

## Read the docs

* [Template Specs overview](https://docs.microsoft.com/azure/azure-resource-manager/templates/template-specs)
* [Quickstart: Create and deploy a template spec](https://docs.microsoft.com/azure/azure-resource-manager/templates/quickstart-create-template-specs)
* [Tutorial: Create a template spec with linked templates](https://docs.microsoft.com/azure/azure-resource-manager/templates/template-specs-create-linked)
* [Tutorial: Deploy a template spec as a linked template](https://docs.microsoft.com/azure/azure-resource-manager/templates/template-specs-deploy-linked-template)

## To install the PowerShell cmdlets

The AzTemplateSpecsPrivatePreview script(s) control the installation of the private preview cmdlets used to manage Template Specs. To install the private preview cmdlets on your machine, you can follow these steps:

1. Install the latest Az Powershell modules (see https://docs.microsoft.com/en-us/powershell/azure/install-az-ps)

1. Download the [AzTemplateSpecsPrivatePreview](https://github.com/Azure/template-specs/releases/download/v0.1/AzTemplateSpecsPrivatePreview.zip) zip package from the Releases page in this repo.
1. Unzip the downloaded package
1. Open a new Powershell window **as Administrator** and navigate to the unzipped directory
1. Ensure you are logged in to Azure by running `Login-AzAccount` or `Connect-AzAccount`. The installation will fail if you are not logged in to Azure.
1. Because the private preview scripts are **not signed**, you will need to setup a bypass for local signing policy. To do so, run `Set-ExecutionPolicy Bypass -Scope Process` in your Powershell window. Note: This will only enable bypass for the current powershell process/window.
1. Run `./AzTemplateSpecsPrivatePreview.ps1` installation script and follow the step-by-step prompts.
1. After installation, set the current subscription context (`Set-AzContext`) to the subscription onboarded to Private Preview and give the new Template Spec cmdlets a try! If you try to run one of the `*-AzTemplateSpec` cmdlets on a non-whitelisted subscription, you will get a `Not found` error.

## Known limitations

* The Private Preview is PowerShell and REST for now. CLI support is 2-4 weeks out. Robust portal support will come in the next 1-2 months.
* The relativePath property will *only* work for TemplateSpec-based deployments. If you use this property in a generic template deployment (from your local file system or from an external URI), the deployment will fail and tell you the relativePath property is not valid. During the private preview, we will enable support for this property in generic deployments.
* System wide install support for Linux and macOS is currently disabled due to a bug. We are looking to get this resolved by 7/24.
* Template Specs with a description will fail to deploy. The fix for this issue has already been checked in and will be fully deployed by 7/28. ([Link to issue](https://github.com/Azure/template-specs/issues/13))
* Passing parameters using dynamic parameters (e.g. `New-AzResourceGroupDeployment ... -myTemplateParam` is not currently working. ([Link to issue](https://github.com/Azure/template-specs/issues/9))

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
