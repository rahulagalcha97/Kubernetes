1.	Kubernetes

What Is Kubernetes?
Kubernetes is an open-source container management (orchestration) tool. Its container management responsibilities include container deployment, scaling & descaling of containers & container load balancing.

-	Written on Golang it has a huge community because it was first developed by Google & later donated to CNCF
Note: Kubernetes is not a containerization platform. It is a multi-container management solution.

Why Use Kubernetes?

Companies out there maybe using Docker or Rocket or maybe simply Linux containers for containerizing their applications. But, whatever it is, they use it on a massive scale. They don’t stop at using 1 or 2 containers in Prod. But rather, 10’s or 100’s of containers for load balancing the traffic and ensuring high availability.
Keep in mind that, as the traffic increases, they even have to scale up the number of containers to service the ‘n’ no of requests that come in every second. And, they have to also scale down the containers when the demand is less. Can all this be done natively?
Well to be honest, I’m not sure it can be done. Even if it can be done, it is only then it’s only after loads of manual effort for managing those containers. So, the real question is, is it really worth it? Won’t automated intervention make life easier? Absolutely it will!
That is why; the need for container management tools is imminent. Both “Docker Swarm” and “Kubernetes” are popular tools for Container management and orchestration. But, Kubernetes is the undisputed market leader. Partly because it is Google’s brainchild and partly because of its better functionality.




Features of Kubernetes
 



1. Automatic Binpacking
 Kubernetes automatically packages your application and schedules the containers based on their requirements and available resources while not sacrificing availability. To ensure complete utilization and save unused resources, Kubernetes balances between critical and best-effort workloads.

2. Service Discovery & Load balancing
 With Kubernetes, there is no need to worry about networking and communication because Kubernetes will automatically assign IP addresses to containers and a single DNS name for a set of containers that can load-balance traffic inside the cluster. 

3. Storage Orchestration
 With Kubernetes, you can mount the storage system of your choice. You can either opt for local storage, or choose a public cloud provider such as GCP or AWS, or perhaps use a shared network storage system such as NFS, iSCSI, etc.

4. Self-Healing
 Personally, this is my favourite feature. Kubernetes can automatically restart containers that fail during execution and kill those containers that don’t respond to user-defined health checks. But if nodes itself die, and then it replaces and reschedules those failed containers on other available nodes.

5. Secret & Configuration Management
 Kubernetes can help you deploy and update secrets and application configuration without rebuilding your image and without exposing secrets in your stack configuration.

6. Batch Execution 
 In addition to managing services, Kubernetes can also manage your batch and CI workloads, thus replacing containers that fail, if desired.

7. Horizontal Scaling
 Kubernetes needs only 1 command to scale up the containers, or to scale them down when using the CLI. Else, scaling can also be done via the Dashboard (kubernetes UI).

8. Automatic Rollbacks & Rollouts
 Kubernetes progressively rolls out changes and updates to your application or its configuration, by ensuring that not all instances are worked at the same instance. Even if something goes wrong, Kubernetes will rollback the change for you.
These were some of the notable features of Kubernetes.


Kubernetes Architecture:

Since Kubernetes implements a cluster computing background, everything works from inside a Kubernetes Cluster. This cluster is hosted by one node acting as the ‘master’ of the cluster, and other nodes as ‘nodes’ which do the actual ‘containerization‘. Below is a diagram showing the same.
Master controls the cluster, and the nodes in it. It ensures the execution only happens in nodes and coordinates the act. Nodes host the containers; in-fact these Containers are grouped logically to form Pods. Each node can run multiple such Pods, which are a group of containers that interact with each other, for a deployment. 

 

Replication Controller is Master’s resource to ensure that the requested no. of pods is always running on nodes. Service is an object on Master that provides load balancing across a replicated group of Pods.

So, that’s the Kubernetes architecture in simple fashion.

Understanding Kubernetes Architecture
Kubernetes architecture and the moving parts of Kubernetes and also what are the key elements, what are the roles and responsibilities of them in Kubernetes architecture.


 
Kubernetes Architecture has the following main components:
•	Master nodes
•	Worker/Slave nodes
•	Distributed key-value store (etcd.)
Master Node: - It is the entry point for all administrative tasks which is responsible for managing the Kubernetes cluster. There can be more than one master node in the cluster to check for fault tolerance. More than one master node puts the system in a High Availability mode, in which one of them will be the main node which we perform all the tasks.
For managing the cluster state, it uses etcd in which all the master nodes connect to it.
Let us discuss the components of a master node. As you can see in the diagram it consists of 4 components:
API server: 
•	Performs all the administrative tasks through the API server within the master node.
•	In this REST commands are sent to the API server which validates and processes the requests.
•	After requesting, the resulting state of the cluster is stored in the distributed key-value store.

Scheduler: 
•	The scheduler schedules the tasks to slave nodes. It stores the resource usage information for each slave node.
•	It schedules the work in the form of Pods and Services.
•	Before scheduling the task, the scheduler also takes into account the quality of the service requirements, data locality, affinity, anti-affinity, etc. 

Controller manager: 
•	Also known as controllers.
•	It is a daemon which regulates the Kubernetes cluster which manages the different non-terminating control loops.
•	It also performs lifecycle functions such as namespace creation and lifecycle, event garbage collection, terminated-pod garbage collection, cascading-deletion garbage collection, node garbage collection, etc.
•	Basically, a controller watches the desired state of the objects it manages and watches their current state through the API server. If the current state of the objects it manages does not meet the desired state, then the control loop takes corrective steps to make sure that the current state is the same as the desired state.


What is the ETCD?
Etcd is a crucial component for Kubernetes as it stores the entire state of the cluster: its configuration, specifications, and the statuses of the running workloads.




Worker Node (formerly minions)

It is a physical server or you can say a VM which runs the applications using Pods (a pod scheduling unit) which is controlled by the master node. On a physical server (worker/slave node), pods are scheduled. For accessing the applications from the external world, we connect to nodes.
 


Container runtime: 
•	To run and manage a container’s lifecycle, we need a container runtime on the worker node. 
•	Sometimes, Docker is also referred to as a container runtime, but to be precise, Docker is a platform which uses containers as a container runtime. 
Kubelet: 
•	It is an agent which communicates with the Master node and executes on nodes or the worker nodes. It gets the Pod specifications through the API server and executes the containers associated with the Pod and ensures that the containers described in those Pods are running and healthy.


Kube-proxy: 
•	Kube-proxy runs on each node to deal with individual host sub-netting and ensure that the services are available to external parties.
•	It serves as a network proxy and a load balancer for a service on a single worker node and manages the network routing for TCP and UDP packets.
•	It is the network proxy which runs on each worker node and listens to the API server for each Service endpoint creation/deletion.
•	For each Service endpoint, kube-proxy sets up the routes so that it can reach to it.
Pods:
A pod is one or more containers that logically go together. Pods run on nodes. Pods run together as a logical unit. So they have the same shared content. They all share the same IP address but can reach other Pods via localhost, as well as shared storage. Pods don’t need to all run on the same machine as containers can span more than one machine. One node can run multiple pods.

Kubernetes / Docker Swarm Difference 
 


Kubernetes - Master and Node Structure
 






Summary of Master& Nodes: 

                      

Etcd: This is the Key-Value store for the cluster. When an object is created, that object’s state is stored here.
API Server: This is the Frontend for the Kubernetes Control panel. All API calls are sent to this server and the server sends commands to other services.
Scheduler: When a new pod is created, the scheduler determines which node the pod will run on.
The decision is based on many factors including hardware, workloads etc.







Kube-Controller Manager:  
 

Nodes Component:

Kube-Proxy: Kube-proxy runs on each worker node as the network proxy. It listens to the API server for each service point creation or deletion. For each service point, kube-proxy sets the routes so that it can reach to it.
Kubelet: It is an agent which communicates with the Master node and executes on nodes or the worker nodes. It gets the Pod specifications through the API server and executes the containers associated with the Pod and ensures that the containers described in those Pods are running and healthy.
Container Runtime: The container runtime is basically used to run and manage a continuous life cycle on the worker node. Some examples of container runtimes that I can give you are the containers rkt, lxc, etc. It is often observed that Docker is also referred to as container runtime, but to be precise, let me tell you that Docker is a platform that uses containers as the container runtime.

PODs:
 

