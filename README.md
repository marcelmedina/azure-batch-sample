# azure-batch-sample

To publish the .NET app as a container, use the following command:
```
dotnet publish --os linux --arch x64 /t:PublishContainer
```

After the image is pushed to your local registry, push it to Azure Container Registry:
```
az acr login --name myregistry.azurecr.io
docker tag batch:1.0.0 myregistry.azurecr.io/batch:1.0.0
docker push myregistry.azurecr.io/batch:1.0.0
```

When creating a Job on Azure Batch, configure the run options with:
```
Image name: myregistry.azurecr.io/batch:1.0.0
Container run options: --rm --workdir /app
Container registry: Default (as this was already specified during the Azure Batch creation)
```