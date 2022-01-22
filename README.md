<h1>Cloud Project</h1>

<h2>Part 1 : How To Build a Node.js Application with Docker</h2>
<h4>Step 1 — Installing our   Application Dependencies</h4>
I first need to make the application files, which I can then copy to my container. These files will include the application’s static content, code, and dependencies.

<h4>Step 2 — Creating the Application File</h4>
This is the structure of the project.

<p align="center">
  <img src="img/1.PNG" >
</p>

<h4>Step 3 — Writing the Dockerfile</h4>
My Dockerfile specifies what will be included in the application container when it is executed. Using a Dockerfile allows me to define my container environment and avoid discrepancies with dependencies or runtime versions.

<p align="center">
  <img src="img/2.PNG" >
</p>

<h4>Step 4 — Using a Repository to Work with Image</h4>
By pushing the application image to my DockerHub registry, I make it available for subsequent use as I build and scale the containers.

<p align="center">
  <img src="img/3.PNG" >
</p>

<h2>Part 2 : Containerizing a Node.js Application for Development With Docker Compose</h2>
<h4>Step 1 — Cloning the Project and Modifying Dependencies</h4>
First, I clone the nodejs-mongo-mongoose repository. This repository includes the code from the setup described in How To Integrate MongoDB with my Node Application, which explains how to integrate a MongoDB database with an existing Node application using Mongoose.

<p align="center">
  <img src="img/4.PNG" >
</p>

<h4>Step 2 — Configuring our Application to Work with Containers</h4>
In this step I will refactor and make some changes to the code.

<p align="center">
  <img src="img/5.PNG" >
</p>

<h4>Step 3 — Modifying Database Connection Settings</h4>
In the next step I make our database connection method more robust by adding code that handles cases where our application fails to connect to our database.

<p align="center">
  <img src="img/6.PNG" >
</p>

<h4>Step 4 — Defining Services with Docker Compose</h4>
Now I am ready to write the docker-compose.yml file with the service definitions.

<p align="center">
  <img src="img/7.PNG" >
</p>

<h4>Step 5 — Testing the Application</h4>
After building the container images and create the services by running `docker compose  up`

<p align="center">
  <img src="img/8.PNG">
</p>

<h2>Part 3 : How To Migrate a Docker Compose Workflow to Kubernetes
<h4>Step 1 — Installing kompose</h4>

<h4>Step 2 — Cloning and Packaging the Application</h4>

<h4>Step 3 — Translating Compose Services to Kubernetes Objects with kompose</h4>

<h4>Step 4 — Creating Kubernetes Secrets</h4>

<h4>Step 5 — Creating the Database Service and an Application Init Container</h4>

<h4>Step 6 — Modifying the PersistentVolumeClaim and Exposing the Application Frontend</h4>

<h4>Step 7 — Starting and Accessing the Application</h4>

<h2>Part 4: How To Automate Deployments to Kubernetes with CircleCI</h2>
<h4>Step 1 — Creating the Local Git Repository</h4>

<h4>Step 2 — Creating a Service Account</h4>

<h4>Step 3 — Creating the Role and the Role Binding</h4>

<h4>Step 4 — Creating our   Sample Application</h4>

<h4>Step 5 — Creating the Kubernetes Deployment and Service</h4>

<h4>Step 6 — Configuring CircleCI</h4>

<h4>Step 7 — Updating the Deployment on the Kubernetes Cluster</h4>

<h2>Part 5: How to Set Up Kubernetes Cluster Monitoring with Helm and Prometheus Operator</h2>
<h4>Step 1 — Creating a Custom Values File</h4>

<h4>Step 2 — Installing the prometheus-operator Chart</h4>

<h4>Step 3 — Accessing Grafana and Exploring Metrics Data</h4>

<h4>Step 4 — Accessing Prometheus and Alertmanager</h4>

