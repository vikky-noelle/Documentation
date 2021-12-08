# Kubernetes

## Introduction

### What is Kubernetes

Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.

## Kubernetes components

When you deploy Kubernetes, you get a cluster.

A Kubernetes cluster consists of a set of worker machines, called nodes, that run containerized applications. Every cluster has at least one worker node.

The worker node(s) host the Pods that are the components of the application workload. The control plane manages the worker nodes and the Pods in the cluster. In production environments, the control plane usually runs across multiple computers and a cluster usually runs multiple nodes, providing fault-tolerance and high availability.

This document outlines the various components you need to have for a complete and working Kubernetes cluster.

![Components of Kubernetes](https://d33wubrfki0l68.cloudfront.net/2475489eaf20163ec0f54ddc1d92aa8d4c87c96b/e7c81/images/docs/components-of-kubernetes.svg)

### Control Plane

The control plane's components make global decisions about the cluster (for example, scheduling), as well as detecting and responding to cluster events (for example, starting up a new pod when a deployment's replicas field is unsatisfied).

Control plane components can be run on any machine in the cluster. However, for simplicity, set up scripts typically start all control plane components on the same machine, and do not run user containers on this machine.

### kube-apiserver

The API server is a component of the Kubernetes control plane that exposes the Kubernetes API. The API server is the front end for the Kubernetes control plane.

The main implementation of a Kubernetes API server is kube-apiserver. kube-apiserver is designed to scale horizontally—that is, it scales by deploying more instances. You can run several instances of kube-apiserver and balance traffic between those instances.

### etcd

Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data.

If your Kubernetes cluster uses etcd as its backing store, make sure you have a back up plan for those data.

You can find in-depth information about etcd in the official documentation.

### kube-scheduler

Control plane component that watches for newly created Pods with no assigned node, and selects a node for them to run on.

Factors taken into account for scheduling decisions include: individual and collective resource requirements, hardware/software/policy constraints, affinity and anti-affinity specifications, data locality, inter-workload interference, and deadlines.

### kube-controller-manager

Control plane component that runs controller processes.

Logically, each controller is a separate process, but to reduce complexity, they are all compiled into a single binary and run in a single process.

Some types of these controllers are:

- Node controller: Responsible for noticing and responding when nodes go down.
- Job controller: Watches for Job objects that represent one-off tasks, then creates Pods to run those tasks to completion.
- Endpoints controller: Populates the Endpoints object (that is, joins Services & Pods).
- Service Account & Token controllers: Create default accounts and API access tokens for new namespaces.

### cloud-controller-manager

A Kubernetes control plane component that embeds cloud-specific control logic. The cloud controller manager lets you link your cluster into your cloud provider's API, and separates out the components that interact with that cloud platform from components that only interact with your cluster.

The cloud-controller-manager only runs controllers that are specific to your cloud provider. If you are running Kubernetes on your own premises, or in a learning environment inside your own PC, the cluster does not have a cloud controller manager.

As with the kube-controller-manager, the cloud-controller-manager combines several logically independent control loops into a single binary that you run as a single process. You can scale horizontally (run more than one copy) to improve performance or to help tolerate failures.

The following controllers can have cloud provider dependencies:

- Node controller: For checking the cloud provider to determine if a node has been deleted in the cloud after it stops responding
- Route controller: For setting up routes in the underlying cloud infrastructure
- Service controller: For creating, updating and deleting cloud provider load balancers

### Node Components

Node components run on every node, maintaining running pods and providing the Kubernetes runtime environment.

#### kubelet

An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod.

The kubelet takes a set of PodSpecs that are provided through various mechanisms and ensures that the containers described in those PodSpecs are running and healthy. The kubelet doesn't manage containers which were not created by Kubernetes.

#### kube-proxy

kube-proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept.

kube-proxy maintains network rules on nodes. These network rules allow network communication to your Pods from network sessions inside or outside of your cluster.

kube-proxy uses the operating system packet filtering layer if there is one and it's available. Otherwise, kube-proxy forwards the traffic itself.

#### Container runtime

The container runtime is the software that is responsible for running containers.

Kubernetes supports several container runtimes: Docker, containerd, CRI-O, and any implementation of the Kubernetes CRI (Container Runtime Interface).

## Kubernetes Object

When you create an object in Kubernetes, you must provide the object spec that describes its desired state, as well as some basic information about the object (such as a name). When you use the Kubernetes API to create the object (either directly or via kubectl), that API request must include that information as JSON in the request body. Most often, you provide the information to `kubectl` in a `.yaml` file. kubectl converts the information to JSON when making the API request.

<pre>
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # tells deployment to run 2 pods matching the template
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
</pre>

## Difference between replication controller and replication set

### Replication Controller

Replication controller, also termed as rc in short, is a wrapper on pod. The replication controller provides an additional functionality to the pods which is providing replicas.

The replication controller monitors pods and automatically restarts them if they fail. Also, if the whole node fails, the replication controller respawn all the pods of that node on some different node whereas in case of pods, once they dies, they won’t be spawn again unless and until they are wrapped around replication controller or replica set.

The scope of replication controller is decided by the label-selectors. Whichever pod matches its label with the provided selector, that will be managed by the replication controller.

A replication controller continuously monitors the list of running pods by running a reconciliation loop and ensures that the specified number of replicas are always running. It maintains the replicas in two ways:

- By creating new replicas if the actual replicas are less than the desired replicas, and
- By removing extra replicas if the actual replicas are more than the desired replicas. This can be possible if,

A pod is created of the same type manually.
A label of an existing pod’s changes to a value which is same as the replication controller label-selector.
Someone decreases the desired number of pods.
Replication Controller manifest
Just as pod, the replication controller also has a spec file which, in addition to podSpecs defines the required number of replicas as shown below:

  <pre>
  ---
  apiVersion: v1
  kind: ReplicationController
  metadata: 
    name: nginx-rc
  spec:
    replicas: 3
    selector:
      app: nginx
      tier: dev
    template: 
      metadata:
        name: nginx
        labels: 
          app: nginx
          tier: dev
      spec:
        containers:
        - name: nginx-container
          image: nginx
          ports:
          - containerPort: 80
  </pre>

The manifest file of replication file consist of the following fields:
- apiVersion: This field specifies the version of kubernetes Api to which the object belongs. ReplicationController belongs to v1 apiVersion.
- kind: This field specify the type of object for which the manifest belongs to. Here, it is ReplicationController.
- metadata: This field includes the metadata for the object. It mainly includes two fields: name and labels of replication controller.
- spec: This field specifies the label selector to be used to select the pods, number of replicas of the pod to be run and the container or list of containers which the pod will run. In the above example, we are running 3 replicas of nginx container.

The replication controller ensures that the actual pods always match the desired pods, we can verify the same by deleting a running pod controlled by replication controller manually and the replication controller will automatically spawn a new pod to meet the desired state. Here’s an example:

- Get the pod replicas:
`kubectl get pods`
- Delete any pod in replication controller fetched from previous cmd:
`kubectl delete pod nginx-rc-haShCoDe`
- Get the pod replicas again:
`kubectl get pods`

Also, inside the spec, if we didn’t put the selector, the replication controller will automatically configure it with the labels of pod, as the pod labels must be same as the replication controller selectors, otherwise the pods will move out of the scope of replication controller.

**kubectl commands for replication controller**

- Create a ReplicationController:
`kubectl create -f nginx-rc.yml`

- Get the ReplicationController:
  ```
  kubectl get rc/nginx-rc
  kubectl get rc/nginx-rc -o wide
  kubectl get rc/nginx-rc -o yaml
  kubectl get rc/nginx-rc -o json
  ```
- Describe the ReplicationController:
`kubectl describe rc/nginx-rc`
- To scale up the replicas:
`kubectl scale rc nginx-rc --replicas=5`
- To delete the ReplicationController:
  ```
  1. kubectl delete rc nginx-rc
  2. kubectl delete -f nginx-rc.yml
  ``` 

### Replica Set

Replica set, also termed as rs in short, is almost same as the replication controller is, only with a single difference. The replica set are also known as next generation replication controller. The only difference between replica set and replication controller is the selector types.

The replication controller supports equality based selectors whereas the replica set supports equality based as well as set based selectors.

**Equality based Selectors**

Equality based selectors allow filtering by label keys and values. Matching objects must satisfy all of the specified label constraints, though they may have additional labels as well. 

Three operators used in set based equality based selectors are = , == , !=. The first two represent equality (and are simply synonyms), while the latter represents inequality. 

For example, if we provide the following selectors:
`env = prod`
`tier != frontend`

Here, we’ll select all resources with key equal to environment and value equal to production. The latter selects all resources with key equal to tier and value distinct from frontend, and all resources with no labels with the tier key.

One usage scenario for equality-based label requirement is for Pods to specify node selection criteria.

**Set Based Selectors**

Unlike Equality based, Set-based label selectors allow filtering keys according to a set of values.

Three kinds of operators used in set-based selectors are in , notin, exists(only the key identifier).

For example, if we provide the following selectors:
`env in (prod, qa)`
`tier notin (frontend, backend)`
`partition`

Here, in the first selector will selects all resources with key equal to environment and value equal to production or qa.
The second example selects all resources with key equal to tier and values other than frontend and backend, and all resources with no labels with the tier key. The third example selects all resources including a label with key partition; no values are checked.

The set-based label selector is a general form of equality since environment=production is equivalent to environment in (production). Similarly for != and notin.

**Replica Set manifest**

Just as replication controller, the replica set has a same spec file with the difference in the as shown below:
  <pre>
  ---
  apiVersion: apps/v1
  kind: ReplicaSet
  metadata: 
    name: nginx-rs
  spec:
    replicas: 3
    selector:
      matchLabels:
        env: prod
      matchExpressions:
      - { key: tier, operator: In, values: [frontend] }
    template:
      metadata:
        name: nginx
        labels: 
          env: prod
          tier: frontend
      spec:
        containers:
        - name: nginx-container
          image: nginx
          ports:
          - containerPort: 80
  </pre>

In the above spec file, under the selector, I’ve used matchLabels and matchExpression to specify the key value pair. The matchLabel works exactly same as the equality based selector, and the matchExpression is used to specify the set based selectors.
Also, the apiVersion of replicaSet is apps/v1. It weren’t there in the initial apiVersion and the kind is ReplicaSet.
Rest all is same as the replication controller.

**kubectl commands for replication set**
- Create a ReplicaSet:
`kubectl create -f nginx-rs.yml`
- Get the ReplicaSet:
  ```
  kubectl get rs/nginx-rs
  kubectl get rs/nginx-rs -o wide
  kubectl get rs/nginx-rs -o yaml
  kubectl get rs/nginx-rs -o json
  ```
- Describe the ReplicaSet:
`kubectl describe rs/nginx-rs`
- To scale up the replicas:
`kubectl scale rs nginx-rs --replicas=5`
- To delete the ReplicaSet:
  ```
  1. kubectl delete rs nginx-rs
  2. kubectl delete -f nginx-rs.yml 
  ```

## Difference between Deployment and Replica Set

Deployment works one level above ReplicaSet object. Deployment is recommended for application services.

With deployment you should be able to do rolling upgrade or rollback. You can update image from v1 to v2.

With ReplicaSet you define number of replicas you want to run. For a particular service. You would have those many replicas running.

[Kubernetes rollout and upgrades example](https://learnk8s.io/kubernetes-rollbacks)

## Services

### Cluster IP

A service that helps with communication between pods irrespective of what their IP address is, is called cluster IP

  <pre>
  apiVersion: v1
  kind: Service
  metaData:
    name: back-end
  spec:
    type: ClusterIP
    ports:
      - targetPort: 80 //basically the port where the container is exposed
        ports: 80 //basically the port where the service will be exposed
    selector:
      app: myApp
      type: back-end
  </pre>