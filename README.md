# Welcome to the Template Specs Private Preview

## To install the PowerShell cmdlets
The AzTemplateSpecsPrivatePreview script(s) control the installation of the private preview cmdlets used to manage Template Specs. To install the private preview cmdlets on your machine, you can follow these steps:

1. Install the latest Az Powershell modules (see https://docs.microsoft.com/en-us/powershell/azure/install-az-ps)
1. Download the [AzTemplateSpecsPrivatePreview](https://github.com/Azure/template-specs/releases/download/v0.1/AzTemplateSpecsPrivatePreview.zip) zip package from the Releases page in this repo.
1. Open a new Powershell window as Administrator.
1. Because the private preview scripts are not signed, you will need to setup a bypass for local signing policy. To do so, run "Set-ExecutionPolicy Bypass -Scope Process" in your Powershell window. Note: This will only enable bypass for the current powershell process/window.
1. Unzip the downloaded package and execute AzTemplateSpecsPrivatePreview.ps1 and follow the step-by-step prompts.
1. After installation, set the current subscription context (Set-AzContext) to the subscription onboarded to Private Preview and give the new Template Spec cmdlets a try!

## Caveats/Things to be aware of
* The Private Preview is PowerShell and REST for now. CLI support is 2-4 weeks out. Portal support will come in the next 1-2 months.
* The relativePath property will *only* work for TemplateSpec-based deployments. If you use this property in a generic template deployment (from your local file system, for example), the deployment will fail and tell you the relativePath property is not valid. During the private preview, we will enable support for this property in generic deployments.
* ...

# Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.