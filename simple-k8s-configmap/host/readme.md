# Purpose

Demonstrate use of ConfigMap feature in a sample WebAPI is hosted into Kubernetes running using DockerDesktop.

- Shows how environment variables can be injected from yml file.
- Shows how appsettings.json file can be injected from yml file.

# Environment
- ASP.Net WebAPI on .Net 5
- Docker Desktop
- Windows 10
- Visual Studio 2019

# How to run
- Clone.
- Compile the project and make sure its running using Docker.
- Build the docker image
- Push the newly created image to docker image repository.
  - The sample uses Docker Hub for images

  ## Scenario 1 - Injecting env variable
- Apply the file k8s-docker-desktop-env-var-deploy.yml using kubectl
- Get the list of services in the deployment and get the NodePort number
- Navigate to http://localhost:<port number>/Echo

It will show the EnvVars object in the response

  ## Scenario 1 - Injecting env variable
- Apply the file k8s-docker-desktop-app-settings-deploy.yml using kubectl
- Get the list of services in the deployment and get the NodePort number
- Navigate to http://localhost:<port number>/Configurations/MyKey

It will show the injected value *MyKey: My value from appsettings.json available in source code* in the response

# Points to note
- The K8s yml files are targeted to deploy into local dev environments that run using Docker Desktop
- If it needs to be deployed to cloud such as Azure the service needs to use LoadBalancer instead of NodePort  
- The container expose 443 and 80 ports. But the K8s yaml file uses only port 80. This is on the assumption that with in K8s cluster pods/containers can communicate without http(s)
  - Enabling http(s) requires certificate and that is not in the scope of this PoC