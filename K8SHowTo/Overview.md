# Kubernetes

## Introduction

From [Kubernetes website](https://kubernetes.io/) :  Kubernetes (K8S) is an open-source system for automating deployment, scaling, and management of
containerized applications.

* Why do I need Kubernetes and what can it do?

    At a minimum, Kubernetes can schedule and run application containers on clusters of physical or virtual machines. However, Kubernetes also allows 
    developers to ‘cut the cord’ to physical and virtual machines, moving from a host-centric infrastructure to a container-centric infrastructure, 
    which provides the full advantages and benefits inherent to containers. Kubernetes provides the infrastructure to build a truly container-centric
    development environment.

    Kubernetes satisfies a number of common needs of applications running in production, such as checking application health, replicating application 
    instances, horizontal autoscaling, balancing loads, rolling updates, providing authentication and authorization etc .

## Overview and Tutorial

A good overview  post on K8S can be found  [here](https://deis.com/blog/2016/kubernetes-overview-pt-1/). 

You can also test drive K8S in a temporory environment on Kubernetes playground at [https://kubernetes.io/docs/tutorials/kubernetes-basics/](https://kubernetes.io/docs/tutorials/kubernetes-basics/).

Kubectl needs a config file to interact with the cluster components. By default it looks for the config file in `~/.kube/config`. Copy the file available at `/scratch/services/kubernetes/config/config` to your `~/.kube` directory. 

    First few commands : 

    `$ kubectl get nodes` - to list the nodes available in the cluster.
    
    `$ kubectl get pods` - to list the current pods running on the cluster.

    `$ kubectl get deployments` - to list current deployments

    `$ kubectl get services` - to list the services and the port on which they are running

### How to run your containers/services on Kubernetes

* Create a container image and push it to lab container registry  
* Run a sanity check  to test if the container image is visible to other hosts on the cluster
* deploy the image on the cluster
* expose the service to lab network
* scale the service to required number of instances
* Kuberentes Dashboard

### Kubernetes Volumes

Since the files stored in containers are ephemeral (they are lost when a container is shutdown) volumes is way to link files on server and container so that there is no data loss when containers are killed. This is especially important because Kubenetes automatically restarts containers that are killed/stopped and it is important that kubernetes knows how to restore Data onto containers.

Also, in many cases you would want multiple containers/pods to share information. This is very easily achieved by using K8S volumes.

* Kubernetes Volumes is the solution to the above described problems. There are several ways of using Volumes and detailed information about all of them can be found at [https://kubernetes.io/docs/concepts/storage/volumes/](https://kubernetes.io/docs/concepts/storage/volumes/)

* The easiest (but not the best) way of setting up volumes is to link a path in the container (say /data/globalshareddata (path on container) to a path on disk like /scratchd/adityaas/kubernetes/globarshareddata/ (path on one of the servers)). This will make sure that any modification to files in either the container or host is reflected in the other. **You have to be careful not to delete the file on server by mistake though** 

### Kubernetes DNS (To be expanded)
[https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)


Assign CPU and Memory Resources to Containers and Pods
    - https://kubernetes.io/docs/tasks/configure-pod-container/assign-cpu-resource/
    - https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/
Storage Management

Assign Pods to Nodes
    - https://kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes/

