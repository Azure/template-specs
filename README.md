# Welcome to the Template Specs Private Preview

## Read the docs

* [Template Specs overview](https://docs.microsoft.com/azure/azure-resource-manager/templates/template-specs)
* [Quickstart: Create and deploy a template spec](https://docs.microsoft.com/azure/azure-resource-manager/templates/quickstart-create-template-specs)
* [Tutorial: Create a template spec with linked templates](https://docs.microsoft.com/azure/azure-resource-manager/templates/template-specs-create-linked)
* [Tutorial: Deploy a template spec as a linked template](https://docs.microsoft.com/azure/azure-resource-manager/templates/template-specs-deploy-linked-template)

## To install the PowerShell cmdlets

The AzTemplateSpecsPrivatePreview script(s) control the installation of the private preview cmdlets used to manage Template Specs. To install the private preview cmdlets on your machine, you can follow these steps:

1. Install the latest Az Powershell modules (see https://docs.microsoft.com/en-us/powershell/azure/install-az-ps)

1. Download the [AzTemplateSpecsPrivatePreview](https://github.com/Azure/template-specs/releases/download/v0.1.5/AzTemplateSpecsPrivatePreview.zip) zip package from the [Releases](https://github.com/Azure/template-specs/releases) page in this repo.
1. Unzip the downloaded package
1. Open a new Powershell window **as Administrator** and navigate to the unzipped directory
1. Ensure you are logged in to Azure by running `Login-AzAccount` or `Connect-AzAccount`. The installation will fail if you are not logged in to Azure.
1. Because the private preview scripts are **not signed**, you will need to setup a bypass for local signing policy. To do so, run `Set-ExecutionPolicy Bypass -Scope Process` in your Powershell window. Note: This will only enable bypass for the current powershell process/window.
1. Run `./AzTemplateSpecsPrivatePreview.ps1` installation script and follow the step-by-step prompts.
1. After installation, set the current subscription context (`Set-AzContext`) to the subscription onboarded to Private Preview and give the new Template Spec cmdlets a try! If you try to run one of the `*-AzTemplateSpec` cmdlets on a non-whitelisted subscription, you will get a `Not found` error.

## To install the CLI commands

### On Windows

#### via MSI
1. Download the latest [MSI installer]() from the [Releases](https://github.com/Azure/template-specs/releases)
1. Unzip the downloaded package
1. Run the extracted MSI
1. If a Windows Defender SmartScreen pops up:
    1. Click "More info"
    1. Click "Run anyway"
1. (Are you sure you want to install this product?) Click "Yes"
1. (Do you want to allow this app from an unknown publisher to make changes to your device?) Click "Yes"

#### via pip3

1. Download the latest artifacts from the [Releases](https://github.com/Azure/template-specs/releases)
2. Run:
```powershell
pip3 install wheel
pip3 install azure_cli_core-2.10.1-py3-none-any.whl
pip3 install azure_cli-2.10.1-py3-none-any.whl
```

### On Linux

**Prereqs**:
```bash
sudo apt-get update
sudo apt-get install python3
sudo apt-get install python3-pip
sudo pip3 install wheel
```

1. Since the repo is private, we recommend installing the latest artifacts from the the [Releases](https://github.com/Azure/template-specs/releases) page from a browser.
1. Run

```bash
# install package from releases
pip3 install azure_cli_core-2.10.1-py3-none-any.whl
pip3 install azure_cli-2.10.1-py3-none-any.whl
```

### On macOS

**Prereqs**:
```bash
brew update
brew install python3
brew install python3-pip
pip3 install wheel
```

1. Download the latest artifacts from the [Releases](https://github.com/Azure/template-specs/releases)
2. Run:
```bash
pip3 install azure_cli_core-2.10.1-py3-none-any.whl
pip3 install azure_cli-2.10.1-py3-none-any.whl
```

## Known limitations

* The relativePath property will *only* work for TemplateSpec-based deployments. If you use this property in a generic template deployment (from your local file system or from an external URI), the deployment will fail and tell you the relativePath property is not valid. During the private preview, we will enable support for this property in generic deployments.
* The Private Preview is PowerShell, CLI, and REST for now -- no good portal support. Robust portal support will come in the next 1-2 months.
  * If you are eager to get a glimpse of portal support, you can try it by using [this hidekey](https://ms.portal.azure.com/?feature.showassettypes=Microsoft_Azure_TemplateSpecs_ArmTemplateSpecsHub&Microsoft_Azure_TemplateSpecs=true&feature.canmodifyextensions=true#blade/Microsoft_Azure_TemplateSpecs/TemplateSpecsMenuBlade/TemplatesList), but keep in mind *it is a very old build that will be mostly replaced.* Key limitations include:	
    * Portal deployment of a template spec with linked templates (using `relativePath`) will fail	
    * No ability to view artifacts (linked templates) packaged with a template spec
    * No ability to view a single version of a template spec. As a workaround, you can edit a single version 


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
