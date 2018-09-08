---
layout: post
title:  "Kubernetes"
date:   2018-09-04 
categories: other
---

Source: Introduction to Kubernetes course offered by edX

### Key Concepts & Terms

<b>Container image</b>: bundle consisting of application and its dependencies  
<b>Containers</b>: deployed image which is platform agnostic  
<b>Container orchestrators</b>: are tools that group hosts together to create a cluster  
<b>Advantages of using container orchestrators</b>:  
  (1) Can connect multiple hosts together to form a cluster   
  (2) Schedule containers to run on different hosts  
  (3) Help containers running on one host reach oout to containers running on other hosts in the cluster  
  (4) Bind containers and storage  
  (5) Keep resource usage in-check, and optimize it when necessary  
  (6) Allow secure acces to applications running inside containers  
  while we could do all of these things manually, container orchestrators make it easier for the operator    
<b>Examples of well-known container orchestrators</b>: Docker Swarm, Kubernetes, Amazon EC2 Container Service, and more  

### Kubernetes Architecture - Overview
<b>Kubernetes</b>: "Kubernetes is an open-source system for automating the deployment, scaling, and management of containerized applications"  
<b>Kubernetes architecture</b>: it is made up of master nodes, worker nodes, etcd (distributed key-value store used to manage the cluster state)  
<b>Role of Master Node</b>: responsible for managing the Kubernetes cluster and is the entry point for all administrative tasks. we can communicate with the master node via the CLI, the GUI, or via APIs.  
<b>Role of Worker Node</b>: Responsible fo running the applications using Pods (one or more collection which are always scheduled together) and is controlled by the master node.  
<b>Components of the master node</b>:  
  (1) API Server: Used to perform adminstrative tasks. After executing the requests, the resulting state of the cluster is stored in the distributed key-value store.  
  (2) Scheduler: Schedules work to different worker nodes.  
  (3) Controller Manager: Manages control loop???  
  (4) etcd: Distributed key-value store which is used to store the cluster state, configuration details such as subnets, ConfigMaps, etc.  
<b>Components of the worker node</b>:  
  (1) Container runtime: Used to run and manage a container's lifecyle (examples include: containerd, rkt)  
  (2) kubelet:  
    * Agent which runs on each worker node and communicates with the master node  
    * Runs containers associated with the Pod  
    * Ensures containers which are part of the Pods are healthy at all times  
  (3) kube-proxy: runs on each worker node and listens to the API server for each Service endpoint creation/deletion  
<b>Requirements for a functional Kubernetes Cluster</b>:  
    * A unique IP is assigned to each Pod  
    * Containers in a Pod can communicate with each other   
    * The Pod is able to communicate with other Pods in the cluster  
    * The application deployed inside a Pod is accessible from the external world  
<b>Container-to-Container communication inside a Pod</b>: Inside a Pod, containers share the network namespaces, so that theye can reach to each other via localhost  
<b>Pod-to-Pod communication across nodes</b>:  There isn't any network address translation that occurs
<b>Pot-to-External-World</b>: Services are exposed through kube-proxy  
<b>kubectl</b>: Used to access Minikube via CLI
   
### Kubernetes Object Model
<b>Object model</b>: Used to represent different persistent entities in the Kubernetes cluster. The entities describe: what containerized applications we are running and on which node, application resource consumption, different policies attached to applications, like restart/upgrade policies, fault tolerence, etc.  
<b>Examples of Kubernetes objects</b>: Pods, ReplicaSets, Deployments, Namespace, etc.  
<b>Spec field</b>: To create an object, we need to provide the spec field to the Kubernetes API server.  
<b>Pod</b>: Is the smallest and simplest Kubernetes object. It represents a single instance of the application. It is a logical collection of one or more containers, which: are scheduled together on the same host, share the same network namespace, mount the same external storage. Controllers are responsible for a Pod's replication, fault tolerance, self-heal, etc.  
<b>Labels</b>: Labels are used to organize and select a subset of objects.  
<b>ReplicationController</b>: It's a part of the master node's controller manager. It's jobs is to ensure the specified number of replicas for a Pod is running at any given point in time.  
<b>ReplicaSets</b>: Is the next-generation ReplicationController.  
<b>DeploymentController</b>: The DeploymentController is part of thjjj1e master node's controller manager, and it makes sure that the current state always matches the desired state.  
<b>Namespaces</b>: If we have numerous users whom we would like to organize into teams/projects, we can partition the Kubernetes cluster into sub-clusters using Namespaces. The names of the resources/objects created inside a Namespace are unique, but not accross Namespaces.  

### Authentication, Authorization, Admission Control
<b>Normal Users</b>: They are managed outside of the Kubernetes cluster via independent services like Google accounts, etc.
<b>Service Accounts</b>: The Service Account users are tied to a given Namespace
