<h1>Cloud Project</h1>
## Contents
- [Part 1 : How To Build a Node.js Application with Docker](#part-1-:-how-to-build-a-node.js-application-with-docker)
    - [Step 1 — Installing our   Application Dependencies](#step-1-installing-our-application-dependencies)


<h2>Part 1 : How To Build a Node.js Application with Docker</h2>
<h3>Step 1 — Installing our   Application Dependencies</h3>
I first need to make the application files, which I can then copy to my container. These files will include the application’s static content, code, and dependencies.

<h3>Step 2 — Creating the Application File</h3>
This is the structure of the project.

<p align="center">
  <img src="img/1.PNG" >
</p>

<h3>Step 3 — Writing the Dockerfile</h3>
My Dockerfile specifies what will be included in the application container when it is executed. Using a Dockerfile allows me to define my container environment and avoid discrepancies with dependencies or runtime versions.

<p align="center">
  <img src="img/2.PNG" >
</p>

<h3>Step 4 — Using a Repository to Work with Image</h3>
By pushing the application image to my DockerHub registry, I make it available for subsequent use as I build and scale the containers.

<p align="center">
  <img src="img/3.PNG" >
</p>

<h2>Part 2 : Containerizing a Node.js Application for Development With Docker Compose</h2>
<h3>Step 1 — Cloning the Project and Modifying Dependencies</h3>
First, I clone the nodejs-mongo-mongoose repository. This repository includes the code from the setup described in How To Integrate MongoDB with my Node Application, which explains how to integrate a MongoDB database with an existing Node application using Mongoose.

<p align="center">
  <img src="img/4.PNG" >
</p>

<h3>Step 2 — Configuring our Application to Work with Containers</h3>
In this step I will refactor and make some changes to the code.

<p align="center">
  <img src="img/5.PNG" >
</p>

<h3>Step 3 — Modifying Database Connection Settings</h3>
In the next step I make our database connection method more robust by adding code that handles cases where our application fails to connect to our database.

<p align="center">
  <img src="img/6.PNG" >
</p>

<h3>Step 4 — Defining Services with Docker Compose</h3>
Now I am ready to write the docker-compose.yml file with the service definitions.

<p align="center">
  <img src="img/7.png" >
</p>

<h3>Step 5 — Testing the Application</h3>
After building the container images and create the services by running `docker compose  up`

<p align="center">
  <img src="img/8.PNG">
</p>

<h2>Part 3 : How To Migrate a Docker Compose Workflow to Kubernetes
<h3>Step 1 — Installing kompose</h3>
The first step is to install kompose.

<p align="center">
  <img src="img/9.png">
</p>

<h3>Step 2 — Cloning and Packaging the Application</h3>
To use the application with Kubernetes, I need to clone the project code and package the application so that the kubelet service can pull the image.

<p align="center">
  <img src="img/10.png">
</p>

<h3>Step 3 — Translating Compose Services to Kubernetes Objects with kompose</h3>
Convert our   service definitions to yaml files with the following command : `kompose convert`

<p align="center">
  <img src="img/11.png">
</p>

<h3>Step 4 — Creating Kubernetes Secrets</h3>
I need to make a few modifications to the files that kompose has created.

* `secret.yaml`
* `nodejs-deployment.yaml`
* `db-deployment.yaml`


<h3>Step 5 — Creating the Database Service and an Application Init Container</h3>
We can move on to creating the database Service and an Init Container that will poll this Service to ensure that our application only attempts to connect to the database once the database startup tasks.

<p align="center">
  <img src="img/12.png">
</p>

<h3>Step 6 — Modifying the PersistentVolumeClaim and Exposing the Application Frontend</h3>
Before running the application, I have to make two final changes to ensure that the database storage will be provisioned properly and that I can expose our application frontend using a LoadBalancer.<br>
We should check what is the right `storage` class by typing: `kubectl get storageclass`.<br>

<p align="center">
  <img src="img/13.png">
</p>

<h3>Step 7 — Starting and Accessing the Application</h3>
The final step is to create our Kubernetes objects and test that the application is working as expected.

<p align="center">
  <img src="img/14.png">
</p>


<p align="center">
  <img src="img/15.jpg">
</p>

<h2>Part 4: How To Automate Deployments to Kubernetes with CircleCI</h2>
<h3>Step 1 — Creating the Local Git Repository</h3>
The first step is to create a new Git repository locally that I  will push to GitHub later. Create two folder `do-sample-app`, `kube-general`.

<p align="center">
  <img src="img/15.png">
</p>

<h3>Step 2 — Creating a Service Account</h3>
I create the Service Account on the cluster by running `kubectl apply`, like the following: `kubectl apply -f ~/kube-general/`.<br>
We will recieve output similar to the following:

<p align="center">
  <img src="img/16.png">
</p>

<h3>Step 3 — Creating the Role and the Role Binding</h3>
Create the file `~/kube-general/cicd-role.yml`.

<p align="center">
  <img src="img/17.png">
</p>

<h3>Step 4 — Creating our   Sample Application</h3>
create a new `index.html` `Dockerfile` and build the image.

<p align="center">
  <img src="img/18.png">
</p>

<h3>Step 5 — Creating the Kubernetes Deployment and Service</h3>
Create	the	YAML	deployment	file `~/do-sample-app/kube/do-sample- deployment.yml`

<p align="center">
  <img src="img/19.png">
</p>

<h3>Step 6 — Configuring CircleCI</h3>
Access to `CircleCI` and create an account, configure it with our `github` account.

<p align="center">
  <img src="img/20.png">
</p>

<h3>Step 7 — Updating the Deployment on the Kubernetes Cluster</h3>
Change the deployment manifest file, then create the image and push all.

<p align="center">
  <img src="img/21.png">
</p>

<h2>Part 5: How to Set Up Kubernetes Cluster Monitoring with Helm and Prometheus Operator</h2>
<h3>Step 1 — Creating a Custom Values File</h3>
I have to create a custom values file that will override some of the chart’s defaults with specific configuration parameters.

<p align="center">
  <img src="img/22.png">
</p>

<h3>Step 2 — Installing the prometheus-operator Chart</h3>
On my local machine, I have to install the `prometheus-operator` Helm chart and passing in the custom values file.

<p align="center">
  <img src="img/23.png">
</p>

<h3>Step 3 — Accessing Grafana and Exploring Metrics Data</h3>
The `prometheus-operator` Helm chart exposes Grafana as a `ClusterIP` Service, which means that it’s only accessible via a `cluster-internal IP address`. 

<p align="center">
  <img src="img/24.png">
</p>

<h3>Step 4 — Accessing Prometheus and Alertmanager</h3>
To connect to the `Prometheus Pods`, we have to use `kubectl port-forward` to forward a local port.

<p align="center">
  <img src="img/25.png">
</p>