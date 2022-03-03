# Sample AKS Deployment Strategies with Github Actions

- Fork this repo and clone into your local env
- In order to initialize your demo environment (Azure resourses and Workflows) execute the init-demo-env.sh file in your command line (require Azure CLI access with "az")
- Push your local repo to GitHub
- Workflow will be fail beacuse of missing secrets
- Create the below secrets;
  - ACR_URL ((az acr list --query "[?contains(resourceGroup, 'github-cd-poc')].loginServer" -o table))
  - ACR_USERNAME (az acr credential show --name <ACR_NAME> --query "username" -o table)
  - ACR_PASSWORD (az acr credential show --name <ACR_NAME> --query "passwords[0].value" -o table)
  - AZURE_CREDENTIALS (az ad sp create-for-rbac --role Contributor --sdk-auth)
  - DNS_NAME (az aks show -g {resource-group-name} -n {aks-cluster-name} -o tsv --query addonProfiles.httpApplicationRouting.config.HTTPApplicationRoutingZoneName)
- Trigger the workflow to observe it's effects on your AKS cluster