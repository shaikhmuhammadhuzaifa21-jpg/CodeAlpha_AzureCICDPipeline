# CodeAlpha_DevOps_Task1 - CI/CD Pipeline using Azure

Simple Node.js app deployed via an automated Azure Pipelines CI/CD pipeline
(build → Docker image → Azure Container Registry → Azure App Service).

## Local run

```
npm install
npm start
```
Visit http://localhost:8080

## Docker build (local test)

```
docker build -t codealpha-devops-app .
docker run -p 8080:8080 codealpha-devops-app
```

## Azure Setup Steps

1. Create a **Resource Group** in Azure Portal.
2. Create an **Azure Container Registry (ACR)** inside that resource group.
3. Create an **Azure App Service** (Web App for Containers, Linux) in the same resource group.
4. In Azure DevOps:
   - Create a new Project.
   - Go to Project Settings → Service connections → create:
     - A Docker Registry connection to your ACR.
     - An Azure Resource Manager connection to your subscription.
   - Go to Pipelines → New Pipeline → connect your GitHub repo → use existing `azure-pipelines.yml`.
   - Replace the placeholders in `azure-pipelines.yml`:
     - `<YOUR_ACR_SERVICE_CONNECTION_NAME>`
     - `<YOUR_ACR_NAME>`
     - `<YOUR_AZURE_WEBAPP_NAME>`
     - `<YOUR_AZURE_SERVICE_CONNECTION_NAME>`
5. Run the pipeline. It will build the Docker image, push it to ACR, then deploy to App Service.
6. Visit your App Service URL to confirm it's live.
