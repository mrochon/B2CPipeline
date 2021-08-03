# Deploy B2C custom journeys using Azure pipelines
Using Azure pipelines to deploy B2C custom journeys. There is an alternative approach documented [here](https://docs.microsoft.com/en-us/azure/active-directory-b2c/deploy-custom-policies-devops). The advantages of the approach
provided below are:
1. Simpler PowerShell script (3 lines)
2. No need to enforce sequence of uploading to make sure base policies are uploaded before their dependencies. Script does that enforcement.
3. No need to update policies with correct tenant name or IEF application ids. It is done automatically by the script.

The script uses the [IefPolicies PowerShell module](https://github.com/mrochon/IEFPolicies).
## Process

1. Create a Git project
2. Add your custom journeys to the policies sub-folder (or use [New-IefPolicies](https://github.com/mrochon/IEFPolicies#new-iefpolicies) to create these from the Starter Pack)
3. Edit the policies/conf.json file to set policy prefix and any other variables that ought to be replaced in the policies
3. Create an Azure pipeline and reference your Git repo in it
4. Update the yaml file with the [one used in this project](https://github.com/mrochon/B2CPipeline/blob/main/azure-pipelines.yml)
5. Register an application in your B2C tenant (using the AAD tab), which can use client credentials (id/secret or certificate) to update your tenant. It needs to have **application** Graph permissions as specified [here](https://github.com/mrochon/IEFPolicies#connect-iefpolicies).
6. Add variables to your pipeline with the *clientId*, *clientSecret* of the above application and the *tenantName* (.onmicrosoft.com is not needed)
7. Run the pipeline

