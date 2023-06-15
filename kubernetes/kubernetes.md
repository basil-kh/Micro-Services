# Kubernetes
![Alt text](imgs-kubernetes/simplediag.png)![Alt text](imgs-kubernetes/bluegreendeployment.png)
**Kubernetes**, also known as **K8s**, is an open-source platform designed to automate deploying, scaling, and operating application containers. It was originally designed by Google and is now maintained by the Cloud Native Computing Foundation.

Key aspects of Kubernetes:

1. **Container Orchestration:** Kubernetes provides a framework to run distributed systems resiliently. It takes care of scaling and failover for your applications, provides deployment patterns, and more.

2. **Service Discovery and Load Balancing:** Kubernetes can expose a container using the DNS name or using their own IP address. If traffic to a container is high, Kubernetes can balance the load and distribute the network traffic so that the deployment is stable.

3. **Storage Orchestration:** Kubernetes allows you to automatically mount a storage system of your choice, such as local storage, public cloud providers, and more.

4. **Automated Rollouts and Rollbacks:** You can describe the desired state for your deployed containers using Kubernetes, and it can change the actual state to the desired state at a controlled rate. For example, you can automate Kubernetes to create new containers for your deployment, remove existing containers, and adopt all their resources to the new container.

5. **Self-Healing:** Kubernetes can restart containers that fail, replace containers, kill containers that don’t respond to your user-defined health check, and doesn't advertise them to clients until they are ready to serve.

6. **Secret and Configuration Management:** Kubernetes lets you store and manage sensitive information, such as passwords, OAuth tokens, and SSH keys. You can deploy and update secrets and application configuration without rebuilding your container images and without exposing secrets in your stack configuration.

In a nutshell, Kubernetes allows you to build a containerized app and deploy, scale, and manage it in a complex environment, such as a multi-cloud environment.

# Why should we use it


1. **Portability and Flexibility:** Kubernetes works with any type of container runtime and can deploy to any type of public, private, or hybrid cloud, which makes it a very flexible solution for varying infrastructure needs. 

2. **Scaling:** Kubernetes provides efficient horizontal scaling and high availability. For applications with variable workloads, Kubernetes is a good choice due to its advanced auto-scaling feature. 

3. **Load balancing:** Kubernetes can handle service discovery and incorporate advanced load balancing algorithms to ensure that services are stable and available.

4. **Self-healing:** Kubernetes constantly checks the health of nodes and containers. If it finds an unhealthy node, it takes the application running on the unhealthy node and schedules it on a healthy node.

5. **Automated rollouts and rollbacks:** Kubernetes allows for seamless update of applications with zero-downtime by maintaining multiple versions of an application through deployments.

6. **Community and pace of development:** Kubernetes has a vast community of developers and industry support. This results in a fast pace of development, with new features and tools being added regularly. It also means a large amount of documentation, tutorials, and guides.

7. **Secret management:** Kubernetes allows sensitive information like passwords and API keys to be stored and managed securely, which helps maintain the security of applications.

8. **Resource optimization:** By packing containers onto nodes and allowing for over-provisioning of resources, Kubernetes can increase hardware utilization and efficiency.

# K8 cluster

**What is a Kubernetes Cluster?**

A Kubernetes cluster is a set of node machines for running containerized applications. A cluster is comprised of two types of resources:

1. **Master Node(s):** The master node (or control plane) is responsible for managing the state of the cluster. It is the entry-point for all administrative tasks. The master node makes decisions about scheduling, orchestration, and maintains the cluster’s desired state. 

2. **Worker Node(s):** Worker nodes are the machines where your applications run. Each worker node includes a Kubelet, which is an agent responsible for communication between the master node and the worker node. Worker nodes also run the container runtime (like Docker) to handle the actual containers.

Clusters are the foundation of Kubernetes' ability to run containerized applications at scale. They provide the control plane and the compute infrastructure (nodes), enabling you to deploy, manage, and scale applications easily and efficiently.

# K8 Object

**What is a Kubernetes Object?**

In Kubernetes, an object is a "record of intent"--once you create the object, the Kubernetes system will constantly work to ensure that object exists. By creating an object, you're effectively telling the Kubernetes system what you want your cluster's workload to look like; this is your cluster's desired state.

Examples of Kubernetes objects include:

1. **Pods:** The smallest and simplest unit in the Kubernetes object model that you create or deploy. A Pod represents a running process on your cluster.

2. **Services:** An abstract way to expose an application running on a set of Pods as a network service.

3. **Volumes:** Provides persistent storage for a Pod. It enables data to survive container restarts.

4. **Namespaces:** Enables to divide cluster resources between multiple users.

Each Kubernetes object includes two nested object fields that govern the object’s configuration: the object `spec` and the object `status`. The `spec`, which you must provide, describes your desired state for the object, while the `status` describes the actual state of the object and is supplied and updated by the Kubernetes system.

# K8 service

**What is a Kubernetes Service?**

A Kubernetes Service is an abstraction which defines a logical set of Pods and a policy by which to access them. Services enable a loose coupling between dependent Pods. While the set of Pods targeted by a Service is generally determined by a `selector`, other routing methods are available through `serviceTypes`. 

Key characteristics of Kubernetes Services include:

1. **Discovery and routing:** Services are responsible for discovery and routing. They define the access rules and load balancing for your application.

2. **Abstraction:** The Service resource provides an abstracted way to expose an application running on a set of Pods as a network service.

3. **Stable network IP:** Regardless of the life cycle of the underlying Pods, a Kubernetes Service has a stable IP address. 

There are four types of Services:

- **ClusterIP**: Exposes the service on a cluster-internal IP. This type makes the service only reachable from within the cluster.
- **NodePort**: Exposes the service on each Node’s IP at a static port.
- **LoadBalancer**: Exposes the service externally using a cloud provider’s load balancer.
- **ExternalName**: Maps the service to the contents of the `externalName` field (e.g., `foo.bar.example.com`), by returning a `CNAME` record with its value.

# K8 Deployment

**What is a Kubernetes Deployment?**

A Kubernetes Deployment is a high-level object meant for deploying applications and updating them declaratively. Deployments use a `Pod` template, which contains a specification for its `ReplicaSets`.

Key characteristics of Kubernetes Deployments include:

1. **Declarative Updates for Pods and ReplicaSets:** You only need to describe the desired state in a Deployment object, and the Deployment controller changes the actual state to the desired state at a controlled rate for you.

2. **Creation of new ReplicaSets and Removal of old ones:** Deployment ensures new `ReplicaSets` are up and running smoothly before scaling down the old `ReplicaSets`.

3. **Rollbacks:** It provides the ability to rollback to a previous version of Deployment if the current version is not stable.

4. **Scaling:** Deployments can be scaled up or down manually, or even automatically, based on CPU utilization.

To implement these characteristics, a Deployment creates a ReplicaSet for each version of the application, then gradually increases the number of replicas in the new `ReplicaSet` while decreasing the number in the old `ReplicaSet`.

# Self healing with k8 

**What is Self-Healing in Kubernetes?**

Self-Healing is one of the most powerful features of Kubernetes. It refers to the system's ability to maintain the desired state of applications without human intervention, even in the event of failures or disruptions.

Key components of Kubernetes Self-Healing include:

1. **Auto-replacement and Auto-replication:** If a pod fails, Kubernetes can automatically replace it with a new, healthy pod to maintain the desired state. Similarly, if a node goes down or is deleted, Kubernetes can replicate and redistribute the pods that were running on the node to other nodes in the cluster.

2. **Readiness and Liveness Probes:** Kubernetes uses readiness and liveness probes to determine the health of an application. The readiness probe is used to know when the application is ready to serve traffic. The liveness probe is used to know when to restart the application. If an application fails these checks, Kubernetes restarts the failing containers to maintain service reliability.

3. **Replication Controllers:** They ensure that the specified number of pod replicas are running at any given time. If there are too many, it will kill off the excess. If there are too few, it will start more.

In summary, Kubernetes' self-healing capabilities help keep applications running efficiently and reliably, minimizing downtime and the need for manual intervention.

# Auto-scaling in k8

**What is Auto-Scaling in Kubernetes?**

Auto-scaling in Kubernetes is a method to adjust the computational resources allocated for applications based on the actual workloads dynamically. Kubernetes supports a few different types of auto-scaling:

1. **Horizontal Pod Autoscaler (HPA):** HPA automatically scales the number of pods in a replication controller, deployment, replica set, or stateful set based on observed CPU utilization (or, with custom metrics support, on some other application-provided metrics).

2. **Vertical Pod Autoscaler (VPA):** VPA automatically adjusts the CPU and memory reservations for your pods, increasing and decreasing as necessary.

3. **Cluster Autoscaler:** It adjusts the size of the Kubernetes cluster depending on the current needs, which means it automatically adds or removes nodes from the cluster.

These features allow Kubernetes to quickly and efficiently respond to changes in workload patterns, optimizing resource usage, and minimizing costs while maintaining application performance and reliability.

# Micro-services with k8

**Deploying Microservices with Kubernetes**

Kubernetes is an excellent platform for deploying and managing microservice-based architectures due to its built-in mechanisms for load balancing, service discovery, secret management, and resiliency.

1. **Pods:** In Kubernetes, the smallest and simplest unit is a Pod. When deploying microservices on Kubernetes, each microservice would typically run in its own Pod which can host one or more containers. 

2. **Services:** Kubernetes Service is an abstraction which defines a logical set of Pods and a policy by which to access them. Services enable loose coupling between dependent Pods.

3. **Deployments:** A Kubernetes Deployment checks on the health of Pods and restarts the Pod's Container if it terminates. Deployments are the recommended way to manage the creation and scaling of Pods. 

4. **Scaling:** Kubernetes allows horizontal scaling of microservices by allowing replication of pods based on CPU usage or custom metrics. This can be automatically managed by Kubernetes.

5. **Rolling updates and Rollbacks:** Kubernetes Deployments can update microservices to a new version without any downtime while monitoring application health to prevent outages.

6. **Namespaces:** Namespaces are a way to divide cluster resources between multiple users. In a microservices architecture, you can use namespaces to divide the different aspects of your system.

Microservices deployment on Kubernetes allows teams to work independently, choosing the technology stack that best fits their service. This contributes to increased development speed, system maintainability, and scalability.
