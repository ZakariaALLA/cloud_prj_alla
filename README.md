# Cloud Project

## Part 1 : How To Build a Node.js Application with Docker
### Step 1 — Installing our   Application Dependencies
I first need to make the application files, which I can then copy to my container. These files will include the application’s static content, code, and dependencies.

### Step 2 — Creating the Application File
This is the structure of the project.
![](img/1.PNG?raw=true)

### Step 3 — Writing the Dockerfile
My Dockerfile specifies what will be included in the application container when it is executed. Using a Dockerfile allows me to define my container environment and avoid discrepancies with dependencies or runtime versions.
![](img/2.PNG?raw=true)

### Step 4 — Using a Repository to Work with Image
By pushing the application image to my DockerHub registry, I make it available for subsequent use as I build and scale the containers.
![](img/3.PNG?raw=true)

## Part 2 : Containerizing a Node.js Application for Development With Docker Compose
### Step 1 — Cloning the Project and Modifying Dependencies
First, I clone the nodejs-mongo-mongoose repository. This repository includes the code from the setup described in How To Integrate MongoDB with my Node Application, which explains how to integrate a MongoDB database with an existing Node application using Mongoose.
![](img/4.PNG?raw=true)

### Step 2 — Configuring our Application to Work with Containers
In this step I will refactor and make some changes to the code.
![](img/5.PNG?raw=true)

### Step 3 — Modifying Database Connection Settings
In the next step I make our database connection method more robust by adding code that handles cases where our application fails to connect to our database.
![](img/6.PNG?raw=true)

### Step 4 — Defining Services with Docker Compose

### Step 5 — Testing the Application

## Part 3 : How To Migrate a Docker Compose Workflow to Kubernetes
### Step 1 — Installing kompose

### Step 2 — Cloning and Packaging the Application

### Step 3 — Translating Compose Services to Kubernetes Objects with kompose

### Step 4 — Creating Kubernetes Secrets

### Step 5 — Creating the Database Service and an Application Init Container

### Step 6 — Modifying the PersistentVolumeClaim and Exposing the Application Frontend

### Step 7 — Starting and Accessing the Application

## Part 4: How To Automate Deployments to Kubernetes with CircleCI
### Step 1 — Creating the Local Git Repository

### Step 2 — Creating a Service Account

### Step 3 — Creating the Role and the Role Binding

### Step 4 — Creating our   Sample Application

### Step 5 — Creating the Kubernetes Deployment and Service

### Step 6 — Configuring CircleCI

### Step 7 — Updating the Deployment on the Kubernetes Cluster

## Part 5: How to Set Up Kubernetes Cluster Monitoring with Helm and Prometheus Operator
### Step 1 — Creating a Custom Values File

### Step 2 — Installing the prometheus-operator Chart

### Step 3 — Accessing Grafana and Exploring Metrics Data

### Step 4 — Accessing Prometheus and Alertmanager

