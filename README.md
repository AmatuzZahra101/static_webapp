# Static Web Application POC

- This Repo can be used to deploy static website in azure. 
- It is using azure storage account and CDN service to host static website
- It is having CI CD Azure pipeline file to create/deploy the infrastructure and application code.

# Repo Structure
```
├───Readme.md
│
├───pipelines
│       static_webapp-CD.json # azure pipline CD code for application deployment
│       static_webapp-CI.yml # azure pipline CI code for application code
│       static_webapp-infra.yml # azure pipline code to deploy infrastucture
│
├───src
│       error.html # sample error.html file
│       index.html # sample index.html file
│
└───templates
        storage-account-cdn-deployment.json # ARM template to create required resource
```

## Prerequisite
- Azure Account with valid subscription.
- Azure resource groups for each environment i.e. dev, uat and prod
- Azure DevOps with service connection.

## Repo Creation
- Create a Azure DevOps repo and commit all the content available in this repo into main branch
- Create 3 main branches
	- develop - Create develop branch from main branch
	- uat  - Create develop branch from develop branch
	- prod - Create develop branch from uat branch

## Infrastructure Deployment

Below steps need to be perform to deploy the infrastructure into azure cloud:

1. Go to the Azure DevOps portal and sign in with your credentials.
2.  Select the **project** where you want to create the build pipeline.
3. In the left sidebar, click on **Pipelines** to access the Pipelines section.
4. Click on the **New Pipeline** button to start creating a new pipeline.
5. Choose the **repository** where your YAML file is located.     
6. Azure DevOps will automatically detect YAML files in your repository. Choose the YAML file (**static_webapp-infra.yml**) that contains your build configuration.  
7. Azure DevOps will open the YAML file in the editor.
8. Save it
9. Give your pipeline a name and **Run**
10. Verify the resource in Azure cloud once run completed

## Static web app build Pipeline

follow the same performed above and select **static_webapp-CI.yml** in step 6.

## static web app release pipeline

1. Go to the Azure DevOps portal and sign in with your credentials.
2.  Select the **project** where you want to create the build pipeline.
3. In the left sidebar, click on **Pipelines** to access the Pipelines section and then **releases**.
4. Click on **New** and then **Import release pipeline**
5. Now select the **static_webapp-CD.json** from your local and upload it, 
6. It will create a CD pipeline for you, just change the CD pipeline name and some parameters inside it which is showing error notification, generally you will error in pipeline agent, service connection or subscription etc.

## Testing

1. Update src/index.html file content and commit it into develop. 
2. it will trigger the static web app build pipeline and once succeeded then call the release pipeline.
3. Access the CDN endpoint over your browser, you should be able to access the html page that you have updated in step 1.