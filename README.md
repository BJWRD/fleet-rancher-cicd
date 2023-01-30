# fleet-rancher-cicd
The following project includes the deployment of a web application via a Fleet GitOps CICD solution.

## Prerequisites
* Minikube installation - [steps](https://minikube.sigs.k8s.io/docs/start/)
* Docker installation - [steps](https://docs.docker.com/desktop/install/mac-install/) 

**NOTE:** the following installation/steps were performed on MacOS.

## Minikube Cluster 

### 1. Start Minikube Cluster

      minikube start --driver=docker

## Docker Rancher Container 

### 1. Running the Rancher Container
If you are installing Rancher for learning purposes and therefore identity verification isn't a concern, run Rancher via Docker using a self-signed certificate by entering the following command -

      docker run -d --restart=unless-stopped \
      -p 80:80 -p 443:443 \
      --privileged \
      rancher/rancher:latest
      
This command will run a Rancher container on port 80 and 443.

<img width="563" alt="image" src="https://user-images.githubusercontent.com/83971386/214293091-0631c666-bdaf-4a50-9f78-52e3544cbe7c.png">

## Accessing Rancher 

### 1. Access the Rancher webpage

 To access the Rancher site, type and search your IP address followed by port 443 into your browser -
 
 Upon the first run you will be asked to enter the following command to retrieve the auto-generated bootstrap password -
 
      docker logs  container-id  2>&1 | grep "Bootstrap Password:"
 
![image](https://user-images.githubusercontent.com/83971386/214004856-0a146f17-2363-4c13-8ef2-1c783786a815.png)
 
 ### 2. Setting your own password
 You will then be prompted to set your own password for access to Rancher -
 
![image](https://user-images.githubusercontent.com/83971386/214005286-8465807a-abe0-410e-a1cd-aa90e159811e.png)
 
## Fleet Configuration

### 1. 


## List of tools/services used
* [Minikube](https://minikube.sigs.k8s.io/docs/)
* [Docker](https://docs.docker.com/get-started/overview/)
* [K8s Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
* [Rancher](https://ranchermanager.docs.rancher.com/)
* [Fleet](https://fleet.rancher.io)

## Useful Links -
* https://fleet.rancher.io
* https://ranchermanager.docs.rancher.com/v2.5/how-to-guides/new-user-guides/deploy-apps-across-clusters/fleet

