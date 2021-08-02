# Deploy B2C custom journeys using Azure pipelines
Using Azure pipelines to deploy B2C custom journeys

## Process

1. Create a Git project
2. Add your custom journeys to the policies sub-folder (or use New-IefPolicies to create these from the Starter Pack)
3. Edit the policies/conf.json file to set policy prefix and any other variables that ought to be replaced in the policies
3. Create an Azure pipeline and reference your Git repo in it
4. Update the yaml file with contents provided in this project
5. Register an application in your B2C tenant (using the AAD tab), which can use client credentials (id/secret or certificate) to update your tenant. It needs to have **application** Graph permissions as specified [here](https://github.com/mrochon/IEFPolicies#connect-iefpolicies).
6. Add variables to your pipeline with the clientId, secret of the above application and the tenant name (.onmicrosoft.com is not needed)
7. Run the pipeline

