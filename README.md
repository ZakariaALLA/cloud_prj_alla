<h1>Cloud Project</h1>

Link to my `dockerhub` [zakariaalla](https://dockerhub.com/u/zakariaalla)

## Contents
- [Part 1 How To Build a Nodejs Application with Docker](#part-1-how-to-build-a-nodejs-application-with-docker)
    - [Step 1 - Installing our Application Dependencies](#step-1---installing-our-application-dependencies)
    - [Step 2 - Creating the Application File](#step-2---creating-the-application-file)
    - [Step 3 - Writing the Dockerfile](#step-1---installing-our-application-dependencies)
    - [Step 4 - Using a Repository to Work with Image](#step-4---using-a-repository-to-work-with-image)

- [Part 2 Containerizing a Nodejs Application for Development With Docker Compose](#part-2-containerizing-a-nodejs-application-for-development-with-docker-compose)
    - [Step 1 - Cloning the Project and Modifying Dependencies](#Step-1---cloning-the-project-and-modifying-dependencies)
    - [Step 2 - Configuring our Application to Work with Containers](#step-2---onfiguring-our-application-to-work-with-containers)
    - [Step 3 - Modifying Database Connection Settings](#step-3---modifying-catabase-connection-settings)
    - [Step 4 - Defining Services with Docker Compose](#step-4---defining-services-with-docker-compose)
    - [Step 5 - Testing the Application](#step-5---testing-the-application)

- [Part 3 How To Migrate a Docker Compose Workflow to Kubernetes](#part-3-how-to-migrate-a-docker-compose-workflow-to-kubernetes)
    - [Step 1 - Installing kompose](#step-1---installing-kompose)
    - [Step 2 - Cloning and Packaging the Application](#step-2---cloning-and-packaging-the-application)
    - [Step 3 - Translating Compose Services to Kubernetes Objects with kompose](#step-3---translating-compose-services-to-kubernetes-objects-with-kompose)
    - [Step 4 - Creating Kubernetes Secrets](#step-4---creating-kubernetes-secrets)
    - [Step 5 - Creating the Database Service and an Application Init Container](#step-5---creating-the-database-service-and-an-application-init-container)
    - [Step 6 - Modifying the PersistentVolumeClaim and Exposing the Application Frontend](#step-6---modifying-the-persistentvolumeclaim-and-exposing-the-application-frontend)
    - [Step 7 - Starting and Accessing the Application](#step-7---starting-and-accessing-the-application)

- [Part 4 How To Automate Deployments to Kubernetes with CircleCI](#part-4-how-to-automate-deployments-to-kubernetes-with-circleci)
    - [Step 1 - Creating the Local Git Repository](#step-1---creating-the-local-git-repository)
    - [Step 2 - Creating a Service Account](#step-2---creating-a-service-account)
    - [Step 3 - Creating the Role and the Role Binding](#step-3---creating-the-role-and-the-role-binding)
    - [Step 4 - Creating our Sample Application](#step-4---creating-our-sample-application)
    - [Step 5 - Creating the Kubernetes Deployment and Service](#step-5---creating-the-kubernetes-deployment-and-service)
    - [Step 6 - Configuring CircleCI](#step-6---configuring-circleci)
    - [Step 7 - Updating the Deployment on the Kubernetes Cluster](#step-7---updating-the-deployment-on-the-kubernetes-cluster)

- [Part 5 How to Set Up Kubernetes Cluster Monitoring with Helm and Prometheus Operator](#part-5-how-to-set-up-kubernetes-cluster-monitoring-with-helm-and-prometheus-operator)
    - [Step 1 - Creating a Custom Values File](#step-1--creating-a-custom-values-file)
    - [Step 2 - Installing the prometheus-operator Chart](#step-2---installing-the-prometheus-operator-chart)
    - [Step 3 - Accessing Grafana and Exploring Metrics Data](#step-3---accessing-grafana-and-exploring-metrics-data)
    - [Step 4 - Accessing Prometheus and Alertmanager](#step-4---accessing-prometheus-and-alertmanager)


## Part 1 How To Build a Nodejs Application with Docker
### Step 1 - Installing our Application Dependencies
I first need to make the application files, which I can then copy to my container. These files will include the application’s static content, code, and dependencies.

### Step 2 - Creating the Application File
This is the structure of the project.

<p align="center">
  <img src="img/1.PNG" >
</p>

### Step 3 - Writing the Dockerfile
My Dockerfile specifies what will be included in the application container when it is executed. Using a Dockerfile allows me to define my container environment and avoid discrepancies with dependencies or runtime versions.

<p align="center">
  <img src="img/2.PNG" >
</p>

### Step 4 - Using a Repository to Work with Image
By pushing the application image to my DockerHub registry, I make it available for subsequent use as I build and scale the containers.

<p align="center">
  <img src="img/3.PNG" >
</p>

## Part 2 Containerizing a Nodejs Application for Development With Docker Compose
### Step 1 - Cloning the Project and Modifying Dependencies
First, I clone the nodejs-mongo-mongoose repository. This repository includes the code from the setup described in How To Integrate MongoDB with my Node Application, which explains how to integrate a MongoDB database with an existing Node application using Mongoose.

<p align="center">
  <img src="img/4.PNG" >
</p>

### Step 2 - Configuring our Application to Work with Containers
In this step I will refactor and make some changes to the code.

<p align="center">
  <img src="img/5.PNG" >
</p>

### Step 3 - Modifying Database Connection Settings
In the next step I make our database connection method more robust by adding code that handles cases where our application fails to connect to our database.

<p align="center">
  <img src="img/6.PNG" >
</p>

### Step 4 - Defining Services with Docker Compose
Now I am ready to write the docker-compose.yml file with the service definitions.

<p align="center">
  <img src="img/7.png" >
</p>

### Step 5 - Testing the Application
After building the container images and create the services by running `docker compose  up`

<p align="center">
  <img src="img/8.PNG">
</p>

## Part 3 How To Migrate a Docker Compose Workflow to Kubernetes
### Step 1 - Installing kompose
The first step is to install kompose.

<p align="center">
  <img src="img/9.png">
</p>

### Step 2 - Cloning and Packaging the Application
To use the application with Kubernetes, I need to clone the project code and package the application so that the kubelet service can pull the image.

<p align="center">
  <img src="img/10.png">
</p>

### Step 3 - Translating Compose Services to Kubernetes Objects with kompose
Convert our   service definitions to yaml files with the following command : `kompose convert`

<p align="center">
  <img src="img/11.png">
</p>

### Step 4 - Creating Kubernetes Secrets
I need to make a few modifications to the files that kompose has created.

* `secret.yaml`
* `nodejs-deployment.yaml`
* `db-deployment.yaml`


### Step 5 - Creating the Database Service and an Application Init Container
We can move on to creating the database Service and an Init Container that will poll this Service to ensure that our application only attempts to connect to the database once the database startup tasks.

<p align="center">
  <img src="img/12.png">
</p>

### Step 6 - Modifying the PersistentVolumeClaim and Exposing the Application Frontend
Before running the application, I have to make two final changes to ensure that the database storage will be provisioned properly and that I can expose our application frontend using a LoadBalancer.<br>
We should check what is the right `storage` class by typing: `kubectl get storageclass`.<br>

<p align="center">
  <img src="img/13.png">
</p>

### Step 7 - Starting and Accessing the Application
The final step is to create our Kubernetes objects and test that the application is working as expected.

<p align="center">
  <img src="img/14.png">
</p>


<p align="center">
  <img src="img/15.jpg">
</p>

## Part 4 How To Automate Deployments to Kubernetes with CircleCI
### Step 1 - Creating the Local Git Repository
The first step is to create a new Git repository locally that I  will push to GitHub later. Create two folder `do-sample-app`, `kube-general`.

<p align="center">
  <img src="img/15.png">
</p>

### Step 2 - Creating a Service Account
I create the Service Account on the cluster by running `kubectl apply`, like the following: `kubectl apply -f ~/kube-general/`.<br>
We will recieve output similar to the following:

<p align="center">
  <img src="img/16.png">
</p>

### Step 3 - Creating the Role and the Role Binding
Create the file `~/kube-general/cicd-role.yml`.

<p align="center">
  <img src="img/17.png">
</p>

### Step 4 - Creating our   Sample Application
create a new `index.html` `Dockerfile` and build the image.

<p align="center">
  <img src="img/18.png">
</p>

### Step 5 - Creating the Kubernetes Deployment and Service
Create	the	YAML	deployment	file `~/do-sample-app/kube/do-sample- deployment.yml`

<p align="center">
  <img src="img/19.png">
</p>

### Step 6 - Configuring CircleCI
Access to `CircleCI` and create an account, configure it with our `github` account.

<p align="center">
  <img src="img/20.png">
</p>

### Step 7 - Updating the Deployment on the Kubernetes Cluster
Change the deployment manifest file, then create the image and push all.

<p align="center">
  <img src="img/21.png">
</p>

## Part 5 How to Set Up Kubernetes Cluster Monitoring with Helm and Prometheus Operator
### Step 1 - Creating a Custom Values File
I have to create a custom values file that will override some of the chart’s defaults with specific configuration parameters.

<p align="center">
  <img src="img/22.png">
</p>

### Step 2 - Installing the prometheus-operator Chart
On my local machine, I have to install the `prometheus-operator` Helm chart and passing in the custom values file.

<p align="center">
  <img src="img/23.png">
</p>

### Step 3 - Accessing Grafana and Exploring Metrics Data
The `prometheus-operator` Helm chart exposes Grafana as a `ClusterIP` Service, which means that it’s only accessible via a `cluster-internal IP address`. 

<p align="center">
  <img src="img/24.png">
</p>

### Step 4 - Accessing Prometheus and Alertmanager
To connect to the `Prometheus Pods`, we have to use `kubectl port-forward` to forward a local port.

<p align="center">
  <img src="img/25.png">
</p>