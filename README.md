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

 To access the Rancher site, type and search your IP address followed by port 443 into your browser 
 
 Upon the first run you will be asked to enter the following command to retrieve the auto-generated bootstrap password -
 
      docker logs  container-id  2>&1 | grep "Bootstrap Password:"
 
![image](https://user-images.githubusercontent.com/83971386/214004856-0a146f17-2363-4c13-8ef2-1c783786a815.png)
 
 ### 2. Setting your own password
 You will then be prompted to set your own password for access to Rancher -
 
![image](https://user-images.githubusercontent.com/83971386/214005286-8465807a-abe0-410e-a1cd-aa90e159811e.png)

## Cluster Importation

### 1. Importing the Cluster 
Once logged in, you will be presented with the following screen -

![image](https://user-images.githubusercontent.com/83971386/214011251-c7cbcff6-c921-4e8c-8a3d-edfd1f1f4c5a.png)

You will need to select the 'Import Existing' button, followed by 'Custom'.

![image](https://user-images.githubusercontent.com/83971386/214011626-7192889e-bb16-482f-b0ad-90ed60230f1f.png)

Enter the name of the cluster and description, then select the 'Create' button.

**NOTE:** There is also the option of entering environment variables and assigning a label/annotation.

<img width="506" alt="image" src="https://user-images.githubusercontent.com/83971386/214292910-67bd8975-40c6-4896-9eb5-15c3c196b9a3.png">

### 2. Register the Cluster into Rancher
Now it's time to register the Cluster into Rancher. This can be done by following the instructions within the screenshot below -

![image](https://user-images.githubusercontent.com/83971386/214012981-ba7d4cd9-7c02-4cfb-8a44-202aa4783b2a.png)

These commands will need to be entered within the running Minikube Cluster -

      kubectl apply -f https://localhost/v3/import/7lzggvls7m2cdhr8ptl87nflwktjdgjn5cpr99kwb7tvsjvm8zvkvr_c-m-5ql2dkvx.yaml
      curl --insecure -sfL https://localhost/v3/import/7lzggvls7m2cdhr8ptl87nflwktjdgjn5cpr99kwb7tvsjvm8zvkvr_c-m-5ql2dkvx.yaml | kubectl apply -f -
      kubectl create clusterrolebinding cluster-admin-binding --clusterrole cluster-admin --user <your username from your kubeconfig>

**NOTE:** Your kubeconfig username can be found within the following file - `~/.kube/config`

### 3. Cluster Rancher Verification
Now just wait a few minutes so that your cluster’s State changes from Pending to Active. Once changed, click on your Cluster’s Name and you will see this screen -

<img width="596" alt="image" src="https://user-images.githubusercontent.com/83971386/214292634-fed0144d-98fc-4a46-95ae-4951cbe0c325.png">

This verifies that the Minikube Cluster has been successfully imported within your Rancher setup.

## KubeConfig Setup Verification

### 1. Download the Cluster KubeConfig file
Access the newly imported cluster and select the following buttons to download the Clusters kubeConfig file -

<img width="511" alt="image" src="https://user-images.githubusercontent.com/83971386/214250194-0ee79f96-1c1b-43a1-b2f8-7ae044575017.png">

### 2. Access the downloaded KubeConfig file
Using an IDE of your choice, open the downloaded cluster.yaml file, to view your cluster contents -

<img width="439" alt="image" src="https://user-images.githubusercontent.com/83971386/214250672-c882c6a5-cb69-4838-a05f-9805ca980628.png">

### 3. Test Cluster access via Kubectl/KubeConfig

      kubectl get node --kubeconfig=/pathofkubeconfigfile/test.yaml

<img width="284" alt="image" src="https://user-images.githubusercontent.com/83971386/214279744-14dfd4d9-9de6-4c99-9702-d4528e5471e7.png">
 
## Fleet Configuration

### 1. Creating a Cluster Group 
Create the Cluster Group 

Assign the Cluster Group to the imported Cluster using the key and value also. 

### 1. Adding your Git Repository

Select the three vertical lines in the top-left of the dashboard, followed by the `Continous Delivery` option.

<img width="229" alt="image" src="https://user-images.githubusercontent.com/83971386/216150978-83815d53-0b89-49ce-9cbe-cfad9308abcf.png">

By default your current Workspace will be set to `fleet-default'.

Click on `Gitrepos` on the navigation bar 
<img width="756" alt="image" src="https://user-images.githubusercontent.com/83971386/216155301-bf24de39-7d09-4907-8978-0c3c80c3a42a.png">

Define the following `Step 1:`repository details -

<img width="632" alt="image" src="https://user-images.githubusercontent.com/83971386/216156323-940b610d-b3a8-4694-8638-20f9920583b4.png">

Then, define these `Step 2:` repository details -

<img width="635" alt="image" src="https://user-images.githubusercontent.com/83971386/216443563-c450b417-0b13-4015-9e30-348725a7e592.png">

### 2. CICD Pipeline 


## List of tools/services used
* [Minikube](https://minikube.sigs.k8s.io/docs/)
* [Docker](https://docs.docker.com/get-started/overview/)
* [K8s Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
* [Rancher](https://ranchermanager.docs.rancher.com/)
* [Fleet](https://fleet.rancher.io)

## Useful Links -
* https://fleet.rancher.io
* https://ranchermanager.docs.rancher.com/v2.5/how-to-guides/new-user-guides/deploy-apps-across-clusters/fleet
* https://github.com/rancher/fleet-examples/tree/master/single-cluster/helm
* https://www.youtube.com/watch?v=lNeX_PxnzLM

