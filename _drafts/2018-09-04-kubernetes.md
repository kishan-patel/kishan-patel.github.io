---
layout: post
title:  "Kubernetes"
date:   2018-09-04 
categories: other
---
<b>Kubernetes Control Plane</b>:
- Responsible for ensuring the cluster's current state matches the desired state (it can ensure this through (re)start of containers, scaling the number of replicas, etc.)
- Consists of a collection of processes running on the master and worker nodes. The proceses running on the master nodes are: kube-apiserver, kube-controller-manager, kube-scheduler. The processes runing on the worker node are kubelet and kube-proxy.
- Responsible for maintaining a record of all Kubernetes Objects in the system and runs continuous control loops to manage those object's state.  

<b>Kubernetes Objects</b>: 
- Are abstractions used to represent the state of the system
- The basic Kubernetes objects include: Pod, Service, Volume, Namespace, ReplicaSet, Deployment, StatefulSet, DaemonSet, etc.

<b>Kubernetes Master</b>:
- Responsible for maintaining the desired state of the cluster. 
- Allows user to interact via cluster through the processing of kubectl commands

<b>Kubernetes Nodes</b>:
- Responsbile for running the applications.
- Controlled by the master node; Users rarely interact with the worker nodes.

<b>kube-apiserver (master component)</b>:  
- Responsible for exposing the Kubernetes API
- Can be thought of as the front-end for the Kubernetes control plane

<b>etcd (master component)</b>:
- Key value store used to store cluster data

<b>kube-scheduler (master component)</b>:
- Reponsible for monitoring newly created pods and assigning a node for them to run on

<b>kube-controller-manager (master component)</b>:
- Component on the master node that runs controllers
- Examples of controllers are: node controller (responsible for monitoring nodes), replication controller (responsible for maintaining the correct number of pods for every replication controller object in the system), etc.

<b>kublet (node component)</b>: 
- Agent that runs on each node in teh cluster and responsible for making fsure that containers are running in the pod
- Takes a set of PodSpecs and ensure that the containers are running as described in those PodSpecs

<b>kube-proxy (node component)</b>:
- Responsible for maintaining network rules on teh host and performing connection forwarding.

<b>container runtime (node component)</b>:
- Software that is responsible for running containers. 
- The following runtimes are supported by Kubernetes: Docker, rkt, runc, etc.

<b>Namespaces</b>:
- Kubernetes supports multiple virtual clusters backed by the same physical cluster. These virtual clusters are called namespaces.
- Namespaces are intended for use in environments with many users spread across multiple teams, or projects. For clusters with a fwe to tens of users, you should not need to create or think about namespaces at all.
- It is not necessary to use multiple namespaces just to separate slightly different resources, such as different versions of the same software: use labels to distinguish resources within the same namespace.
- There are three namespaces: default (the default namespace for objects with no other namespace), kube-system (the namespace for objects created by the Kubernetes system), kube-public (the namespace that is created automatically and is readable by all users)

<b>commands</b>:
<code>
</code>