# Sample Node.js app for Endava Azure DevOps Challenge

[![Build Status](https://dev.azure.com/ivazure/uKo-Endava/_apis/build/status/uKo12.node-express-azure?branchName=master)](https://dev.azure.com/ivazure/uKo-Endava/_build/latest?definitionId=1&branchName=master)

Simple Node.js app deployed with Azure DevOps. 

- Project name: uKo-Endava

- Pipeline with two stages - DEV -> PROD. PROD is with implemented Pre-deployment approval.

- azure-pipelines.yml:

```
trigger:
- master

pool:
  vmImage: 'Ubuntu-16.04'

steps:
- task: NodeTool@0
  inputs:
    versionSpec: '8.x'
  displayName: 'Install Node.js'

- script: |
    npm install
  displayName: 'npm install'

- script: |
    npm test
  displayName: 'npm test'

- task: ArchiveFiles@2
  displayName: 'Archive files'
  inputs:
    rootFolderOrFile: '$(System.DefaultWorkingDirectory)'
    includeRootFolder: false

- task: PublishBuildArtifacts@1
  displayName: 'Publish artifacts: drop'
```

- Made some modification in the code (text change) and modification in one of the tests (index_test.js) since is monitoring for the text on the Index page.

- Deployed on Azure App service on Linux with Staging slot (DEV).

- Manual test created in the DevOps portal for testing the access to the web page - https://ukoendava.azurewebsites.net.

- Monitoring (Alert rule) implemented in the Azure portal monitoring for HTTP 5xx and 403 requests.

- App service URL:

  - DEV slot: https://ukoendava-dev.azurewebsites.net
  - PROD: https://ukoendava.azurewebsites.net/

- Credentials for the Azure portal and Azure DevOps portal will be send in the email.

