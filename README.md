# azure-policies

This repo keeps Azure Policies set and up to date depending on what is on the main branch. The Policies and Policy Sets are based on an export of the Policies from the outputs of the [Microsoft CAF module](https://github.com/Azure/terraform-azurerm-caf-enterprise-scale)

The policies/ folder contains a sub folder for each policy. Inside each subfolder is a policy.json file describing the policy.
The initiatives/ folder contains a sub folder for each policy set. Inside each subfolder is a policy.json file describing the policy set.

The workflow for this repo can keep any or all of the policies up-to-date if properly set to track the changes to each in main.

To run this as an action, you will need to create a service principal with the Resource Policy Contributor role on your root management group.
This action can be set to run on all commits to main by changing the workflow file.

## Setup

1. `az ad sp create-for-rbac --name "GitHubAzurePoliciesAction" --sdk-auth`

2. Capture the entire json object that is output from this command, and use that to populate your Azure Secret called AZURE_CREDENTIALS.

3. Then, you will need to go into the Root Management Group in the Azure portal, and grant this SP the Resource Plicy Contributor role on that scope.

4. You will need to also create a secret called MANAGEMENT_GROUP_ID with your root Management Group's UUID.

### For more info, you can reference these pages:

**The [azure/login](https://github.com/Azure/login) GitHub action:**

**The [manage-azure-policy action README](https://github.com/marketplace/actions/manage-azure-policy) (as of 1-Apr-2022 some of the commands listed in this README do not work)**
