# Azure Deployment

## Overview
- The Decentralize Nzuri web application can be deployed on Azure using Docker containers.
- The deployment includes three main services:
    1. **Streamlit**: The frontend web interface for Honda and Nissan applications.
    2. **Flask API**: Handles user authentication and session tracking.
    3. **InfluxDB**: Stores time-series data for user login/logout events.

## Azure Container Registry (ACR)
1. **Create ACR**:
```bash
az acr create --resource-group <resource-group> --name <acr-name> --sku Basic
```
2. **Login to ACR**:
```bash
az acr login --name <acr-name>
```
3. **Tag Images**:
```bash
docker tag streamlit <acr-name>.azurecr.io/streamlit:latest
docker tag flask <acr-name>.azurecr.io/flask:latest
docker tag influxdb <acr-name>.azurecr.io/influxdb:latest
```
4. **Push Images to ACR**:
```bash
docker push <acr-name>.azurecr.io/streamlit:latest
docker push <acr-name>.azurecr.io/flask:latest
docker push <acr-name>.azurecr.io/influxdb:latest
```

## Azure Container Instance (ACI)
A container group that houses all the three services is created and then deployed using a deployment.yaml file that mirrors the docker-compose.yaml file that was used to build the container locally.

First, a deploment.yml file is created.
The `deployment.yml` file is used to deploy the application to an Azure Container Group (ACI):
```yaml
apiVersion: 2021-09-01
location: eastus
name: <dns-name-label>
properties:
  containers:
  - name: streamlit
    properties:
      image: <acr-name>.azurecr.io/streamlit:latest
      ports:
      - port: 80
      - port: 443
  - name: flask
    properties:
      image: <acr-name>.azurecr.io/flask:latest
      ports:
      - port: 5000
  - name: influxdb
    properties:
      image: <acr-name>.azurecr.io/influxdb:latest
      ports:
      - port: 8086
  osType: Linux
  ipAddress:
    type: Public
    ports:
    - protocol: tcp
      port: 80
    - protocol: tcp
      port: 443
    - protocol: tcp
      port: 5000
    - protocol: tcp
      port: 8086
  restartPolicy: Always
tags: null
type: Microsoft.ContainerInstance/containerGroups
```

## Running the Application
1. Deploy the application using the YAML file:
```bash
az container create --resource-group <resource-group> --file deployment.yml
```
2. Access the application at `http://<dns-name-label>.eastus.azurecontainer.io`

## Error Handling
- The application includes basic error handling for:
    - Docker build errors
    - Container startup failures
    - SSL certificate generation errors

## Output
- The application runs in Docker containers on Azure, accessible via your web browser.

## Limitations
- Requires proper configuration of Azure resources.