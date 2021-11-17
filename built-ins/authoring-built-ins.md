> ⚠️ Built-in Template Specs are a feature in development and are currently not available for public use. This document describes the initial process required for built-in template spec authoring, but will remain incomplete (contains some placeholds) until the feature has shipped.


 **IMPORTANT:** Authoring and contribution of Built-in Template Specs is restricted to **authorized collaborators only** such as internal Microsoft teams and partners. PRs from unauthorized individuals will be rejected with no exceptions.

# Authoring and Contributing Built-in Template Specs

This documents provides general information on what built-in template specs are, and the process involved to contribute new built-in template specs for consumption by a wider population.

## What are built-ins?
Built-in template specs are [template specs](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/template-specs?tabs=azure-powershell) that deploy cloud components/settings that fulfill scenarios that are seen as useful for a wide variety of customers across Azure. Unlike private template specs which are only available to customers (tenants) who created them, built-in template specs are available to all customers in a specific cloud (such as the Public cloud, or the Chinese national cloud, etc. etc.). Essentially they are "global" template specs that any customer can deploy from any region, and they'll behave in the same way for each customer.

They share all the same schemas and properties as customer created template specs (including versions), except built-ins are read-only resources that are accessible to anyone (there is no need to manage access rights to built-in template specs).

Examples of useful built-ins include those that apply certain standards/policies (such as ISO 27001) to existing resources, or built-ins that simplify common deployment scenarios (like deploying a Windows VM).

## How do I contribute a new built-in?

Before continuing it's important to determine whether or not the scenario the underlying Azure Resource Manager template fulfills meets the guidelines for being a built-in template spec. Ask yourself:

 - Is it a scenario that will be commonly used by many customers across Azure without requiring tweaks to the template itself?
 - Is it a scenario that works well "out of the box" (i.e. without a very specific complex environment already setup)?

If the answer to both of these questions is yes, you're on your way towards contributing a built-in. For a new built-in contribution you can follow these steps:

### Step 1: Validate your template/template spec functionality 

Before submitting a built-in, you should create a private template spec (in your own subscription) that mirrors what you'd like to submit as a built-in. The purpose is to allow you to test the template spec in your own environment before packaging the template for built-in submission. If the template spec has parameters, make sure they have helpful descriptions before continuing to the next step.

### Step 2. Create a fork of the public template spec repo

If you're not a Microsoft employee, you should fork the [public template specs repo](https://github.com/Azure/template-specs/tree/master) (For more info on how to fork a repo see '[Fork a repo - GitHub Docs](https://docs.github.com/en/get-started/quickstart/fork-a-repo)').

If your a Microsoft employee with Azure source permissions you can simply create a new branch of the repo in github.

### Step 3: Add the main template/artifacts to your local enlistment

In your forked/branched repository, navigate to the built-ins/samples root directory and create a directory for your template spec version using the structure:

* /*{templateSpecId}*/versions/*{versionName}*

Keep in mind that *templateSpecId* will be the resource name customers use in the future to access your built-in template spec, and it **cannot** be changed after the template spec has been published... so be sure to choose a name that will stand the test of time.

For *versionName* you should select a version that aptly describes your initial version. For most cases, 'v1' is appropriate. However if your built-in targets a standard that is date driven, it's recommended that you include the targeted date within your version... For example for a built-in targeting targeting the 2020 version of SWIFT compliance, your version name could be "2020.v1".

After you've created the version directory. It's time to add the templates/artifacts json to the directory. If your template spec contains a template that does not leverage template spec artifacts (ie: relative paths), this process is extremely simple... Just copy your Azure Resource Manager template to:

* /*{templateSpecId}*/versions/*{versionName}*/**mainTemplate.json**

**If your template spec contains artifacts** you'll need to export the template spec using [Az Powershell](https://docs.microsoft.com/en-us/powershell/azure/new-azureps-module-az) cmdlets. That process is as follows:

* Use `Set-AzContext` to set the subscription where your template spec is located to the active context
* Run `Export-AzTemplateSpec -ResourceGroupName {rgName} -Name {templateSpecId} -Version {versionName} -OutputFolder {theRootBuiltInsDirectory}/{templateSpecId}/versions/{versionName}`
* Navigate to the output folder and rename the .json file created there (it'll be named with the format "*{templateSpecId}.{versionName}.json*") to **mainTemplate.json**

### Step 4: Add metadata for your template spec

Each built-in template spec requires additional metadata for the overall template spec, as well as each individual version. We'll start with the overall template spec metadata....

#### Metadata for overall template spec:
Create a file in your template spec directory with the name 'metadata.json' (eg: * /*{templateSpecId}*/metadata.json) and populate it with the following contents to start things off:

    {
        "displayName" : "User Friendly Built-in Name",
        "description": "Very short description of the built-in's purpose",
        "documentationUrl": "https://www.microsoft.com/myDocumentation",
        "category": "General",
    }

Replace the example values with values relevant to your built-in. The **required** properties are as follows:

* **displayName**: This will be the user friendly (it can contain spaces) name displayed to customers in the Azure Portal (*currently the built-in UI is pending implementation*). It should be as short as possible and follow normal casing.
* **description**: Very short description of the built-in's purpose. For example: "Deploys a Windows VM."
* **category**: The relevant category for your built-in. Currently the following categories are supported (they will be expanded in the near future, but additional requests can be raised under our github issue tracking):
  * *"General"* - Common catch-all category for general built-ins that do not fit any other available category
  * *"Quickstart"* - Provides a starting point for a common deployment scenario (deploying a VM for example)

Additionally the following **optional** properties can be set:

* **documentationUrl**: An absolute URL to documentation related to your built-in. Having this property/value present is strongly recommended. For built-ins contributed by non-Microsoft third parties, the URL may be strongly scrutinized for longevity/security reasons. 
* **icmPath**:  (Internal Microsoft Teams Only) This should be the path to the owning team in ICM, for example *"Your Team/Your Sub Team"*. Will be used to direct issues with the built-in to your team's ICM

#### Metadata for template spec versions:
Now we'll move on to the metadata for the template spec version. Create a file in your template spec version directory with the name 'metadata.json' (eg: * /*{templateSpecId}*/versions/*{versionName}*/metadata.json) and populate it with the following contents:

    {
        "description": "A short description of the version.",
        "supportedClouds": [
            "DF",
            "Prod"
        ]
    }

Version metadata has the following **required** properties:

* **description**: A very short description of what the version does. If this is the initial version of a built-in, it's completely fine to just re-use the description you used for the overall built-in. For version updates, you can include a brief indication of what has changed over the previous version, for example: "Adds support for Cosmos DB".
* **supportedClouds**: An array of the cloud environments your built-in supports. For most contributions, "DF" and "Prod" should be supported at a minimum. To be supported in other cloud environments, you should make sure any resource types (including api versions) you're referencing also exist in those clouds. The available cloud values to include in the array are as follows:

  * *"DF"* - This is the Microsoft internal "Dogfood" environment. It allows Microsoft employees to test Azure components prior to official public release.
  * *"Prod"* - Azure **public production cloud** (eg: https://portal.azure.com) used by most Azure customers.
  * *"MC"* - Chinese sovereign cloud (eg: https://portal.azure.cn)
  * *"FF"* - US Government cloud. Non-Microsoft employees can disregard this value.

Additionally the following **optional** properties are available:

* **supportsAirGapped**: A boolean value that indicates whether this built-in should be returned in airgapped cloud environments. Defaults to false. Expected to be set by Microsoft employees only.

### Step 5: Submit a PR to the template specs repo

> **IMPORTANT:** Authoring and contribution of Built-in Template Specs is restricted to **authorized collaborators only** such as internal Microsoft teams and partners. PRs from unauthorized individuals will be rejected with no exceptions.
 
Now that you've created all the necessary changes locally in your repo/branch, you should commit your changes and initiate a pull request to the main repo.

* For forked repos, you can see guidance for creating a PR here: [Creating a pull request from a fork - GitHub Docs](https://docs.github.com/en/github/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork)
* For branches within the template spec repo you can see guidance for creating a PR here: [Creating a pull request - GitHub Docs](https://docs.github.com/en/github/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)

Be sure to fill out the PR template that is shown with the relevant details. After your PR is received someone from Microsoft will review it and either provide feedback requesting changes, or it will be approved and rollout can be expected within 30 days. 

## How do I update an existing built-in?

All updates to existing built-ins should come as new versions, with exceptions for the following situations:
* Simple text updates (no modifications of functionality)
* Critical fixes for security purposes 

Unless your update meets one of the exception scenarios above, you should submit a new version using the same steps outlined for a new built-in starting from: [Step 1: Validate your template/template spec functionality](#step-1:-validate-your-template/template-spec-functionality) . As part of the update process, be sure to bump your version in a way that will make sense to users (for example if your previous version name was "v1", your new version may be "v2").

## I want to remove an existing built-in, what should I do?

Built-ins should never be removed (doing so will break customers referencing the built-in during their deployments). We are currently working on implementing deprecation logic for this purpose. If you need a built-in removed for a **critical security issue** please contact {to_be_determined}@microsoft.com with details.

---
_This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments._
