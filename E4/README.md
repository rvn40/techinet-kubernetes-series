# Kubernetes: Understanding Container Orchestration

The primary responsibility of Kubernetes is container orchestration. Kubernetes, often abbreviated as K8s, is a powerful open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications. Kubernetes provides a robust and standardized framework for container orchestration in both on-premises and cloud environments. It's provides many capabilities and key features include automated load balancing, self-healing, and rolling updates, allowing developers and operators to efficiently manage and scale applications without manual intervention. 

As the results, kubernetes abstracts away the complexities of infrastructure, enabling seamless deployment and orchestration of microservices and applications, making it a cornerstone technology for modern, cloud-native development, however, that also means the containers must be packed efficiently following the constraints of the deployment environment and the cluster configuration. 


## Traditional vs Modern Ways

### Virtualization: Physical machines, Virtual machines, and Containers

The evolution of internet technology has witnessed a transformative journey in the way we deploy and manage applications, moving from physical machines to virtual machines and, most recently, to containers.

1. **Physical Machines (Pre-2000s):** In the early days of the internet, applications were primarily deployed on physical machines, each dedicated to a specific task. While this approach provided isolation and dedicated resources, it often led to inefficient utilization, with machines running at partial capacity.

2. **Virtual Machines (2000s):** The advent of virtualization technology marked a significant shift. Virtual machines (VMs) allowed multiple operating systems to run on a single physical machine. This enabled better resource utilization, flexibility, and isolation. Technologies like VMware emerged as pioneers in the virtualization space, providing a way to abstract the underlying hardware and run multiple VMs on a single physical host.

3. **Containers (2010s - Present):** As applications became more modular and scalable, the need for lightweight and portable solutions became apparent. Containers, as popularized by Docker, emerged as a game-changer. Containers encapsulate an application and its dependencies, providing consistency across different environments. They are lightweight, start up quickly, and share the host OS kernel, making them highly efficient. Kubernetes, an open-source container orchestration platform, further streamlined container management, enabling automated deployment, scaling, and management of containerized applications.

This journey reflects a constant drive for efficiency, scalability, and agility in deploying applications. While physical machines, virtual machines, and containers each have their place, containers, with their portability and efficiency, have become a cornerstone in modern application development and deployment, especially in the context of microservices architecture and cloud-native environments. Therefore, virtualization continues to be a fundamental technology in IT infrastructure, supporting diverse workloads, from traditional applications to modern, containerized microservices. The journey underscores the ongoing quest for efficient resource utilization, scalability, and agility in computing environments.

### Culture: Cattle vs Pets

The "cattle vs pets" analogy in the context of IT infrastructure and systems management reflects a shift in how companies perceive and treat their servers and infrastructure components. The analogy is commonly associated with cloud computing and the principles of scalable, automated, and ephemeral infrastructure.

1. **Pet Culture (Traditional Approach - Pre-Cloud Era):** In the early days of IT, servers were treated like pets. Each server had a unique identity, often given names, and administrators invested time and effort in nurturing and maintaining them. If a server failed, it would be painstakingly repaired to its original state. This approach was resource-intensive, time-consuming, and not scalable, especially as companies faced growing infrastructure demands.

2. **Cattle Culture (Cloud and DevOps Era):** The advent of cloud computing and the rise of DevOps practices brought about a paradigm shift. In the "cattle" approach, servers are treated as interchangeable and expendable resources. They are provisioned and managed in a standardized and automated fashion. If a server fails, it is replaced rather than repaired. This approach aligns with the principles of scalability, resilience, and rapid deployment, allowing companies to respond dynamically to changing workloads.

The shift to a "cattle" culture is closely tied to the adoption of cloud-native technologies, containerization, and orchestration tools. Services like AWS, Azure, and Google Cloud provide infrastructure at scale, encouraging the mindset that servers are disposable entities that can be easily replaced.

This cultural shift has several benefits:
- **Scalability:** The ability to scale infrastructure up or down rapidly to meet demand.
- **Automation:** Automated provisioning and configuration management reduce manual intervention.
- **Resilience:** Designing for failure by replacing failed components rather than repairing them.

The "cattle vs pets" metaphor captures the essence of this cultural change, illustrating how modern IT practices prioritize efficiency, scalability, and automation over the traditional, more labor-intensive methods of managing individual servers. It has become a guiding principle in the era of cloud computing, enabling companies to build and manage large, dynamic, and resilient infrastructures.






## Basic Concepts

In Kubernetes, several key terms describe fundamental concepts within the system. These terms are fundamental to understanding the architecture and functioning of Kubernetes and the basis for discussions, documentation, and interactions within the Kubernetes ecosystem. In this section, I'll briefly introduce many important Kubernetes concepts and give you some context.

### Cluster
In Kubernetes, a cluster refers to a cohesive set of computing resources, both physical and virtual, that collectively form the foundation for deploying, managing, and scaling containerized applications. The cluster consists of two primary components: master nodes and worker nodes. Master nodes host the control plane components, including the API server, scheduler, controller manager, and etcd, which collectively manage the state and configuration of the entire cluster. Worker nodes, on the other hand, execute the actual workloads by running containers within encapsulated units called pods. The concept of a Kubernetes cluster embodies the collaborative orchestration of resources to provide a scalable, resilient, and efficient environment for deploying and managing applications in a containerized ecosystem.

### Node
Node is an individual computing unit, which can be either a physical machine or a virtual instance, that is part of a larger cluster. Nodes serve as the operational foundation for deploying and running containerized applications. Within the Kubernetes architecture, nodes are categorized as either master or worker nodes. Master nodes host the control plane components, managing the overall state and orchestration of the cluster, while worker nodes execute the actual workloads. Each worker node runs a kubelet, which ensures the creation and management of containers within encapsulated units called pods. Nodes collaborate to provide the necessary resources and runtime environment for containerized applications, making them the fundamental building blocks of a Kubernetes cluster.

### Master
In the realm of Kubernetes, a master node represents the control plane component responsible for managing and orchestrating the overall state of the entire cluster. Comprising essential components such as the API server, scheduler, controller manager, and etcd (a distributed key-value store), the master node is the central brain that governs the deployment, scaling, and maintenance of containerized applications within the cluster. The API server acts as the entry point for cluster management, receiving and processing requests, while the scheduler assigns workloads to worker nodes. The controller manager ensures that the desired state of the system is maintained, and etcd stores configuration data crucial for cluster coordination. As the authoritative entity, the master node plays a pivotal role in the smooth operation of a Kubernetes environment, providing the necessary intelligence and coordination to maintain the desired configuration and health of the entire cluster.

### Namespace
In Kubernetes, a namespace is a virtual cluster within a physical or virtual cluster, serving as a way to partition resources and create isolated environments. It provides a scope for naming and organizing objects within the cluster, such as pods, services, and replication controllers. By employing namespaces, Kubernetes enables multiple users or teams to share the same cluster while maintaining segregation of resources. This abstraction facilitates the organization and management of objects, preventing naming conflicts and allowing for more efficient resource allocation. Namespace usage is particularly advantageous in multi-tenant environments or scenarios where different projects, departments, or applications coexist within the same Kubernetes cluster, offering a means to logically separate and govern the diverse components running in the system.

### Pod
In Kubernetes, a pod represents the smallest and simplest deployable unit that encapsulates one or more closely related containers and their shared resources, such as storage and network, on a single node within a cluster. Containers within a pod share the same network namespace, enabling them to communicate with each other using localhost, and can also share storage volumes. Pods are fundamental to the Kubernetes architecture, forming the basic building blocks for deploying and managing containerized applications. They are designed to be ephemeral and scalable, with Kubernetes managing their lifecycle, ensuring high availability, and enabling seamless rolling updates. The concept of a pod emphasizes the co-location of containers that need to work together, promoting efficient resource utilization and providing a cohesive and manageable unit for container orchestration within the Kubernetes ecosystem.

### Name
In Kubernetes, the term "name" is a fundamental attribute associated with various objects within the cluster, such as pods, services, and deployments. It serves as a unique identifier, helping to distinguish and reference individual instances of these resources. The name is crucial for addressing and interacting with Kubernetes objects, enabling users to manage, query, and update specific entities within the cluster. Naming conventions typically follow guidelines to ensure clarity, consistency, and avoid conflicts. A well-defined naming strategy is essential for maintaining order and facilitating effective communication within the Kubernetes environment, where various components and configurations coexist. The name attribute is a key element in the overall organizational structure and accessibility of resources within a Kubernetes cluster.

### Label
In Kubernetes, a "label" is a key-value pair associated with objects such as pods, nodes, or services, allowing users to attach custom metadata for the purpose of organizational categorization and resource selection. Labels are versatile and serve multiple functions, providing a flexible mechanism for grouping and filtering resources based on specific criteria. They are commonly employed to denote characteristics such as environment, application version, or role, enabling users to organize and identify resources more effectively. Labels play a pivotal role in Kubernetes operations, facilitating the dynamic selection of resources for tasks such as scaling, deployment, and service routing. The adoption of a consistent and meaningful labeling strategy enhances the manageability and visibility of objects within the cluster, contributing to a more organized and efficient Kubernetes environment.

### Annotation
In the context of Kubernetes, "annotations" refer to additional metadata attached to objects, providing supplementary information beyond what labels offer. Unlike labels, annotations are not used for selecting or organizing resources; rather, they serve as a space to add arbitrary key-value pairs for documentation, tooling, or tracking purposes. Annotations are valuable for storing non-identifying information about resources, such as build details, release notes, or any data that might aid in the management, monitoring, or understanding of objects within the Kubernetes cluster. Their flexibility and non-prescriptive nature make annotations a useful tool for extending the information associated with various resources, offering a way to enrich the context and documentation associated with objects without impacting the core functionality of the Kubernetes system.

### Label Selector
In Kubernetes, a "label selector" is a mechanism used to filter and select resources within the cluster based on their associated labels. It allows users to define specific criteria, such as matching labels with certain values or using logical operators, to identify and group related resources. Label selectors are integral to various Kubernetes operations, including the dynamic assignment of pods to nodes, scaling applications, and managing services. They enable precise targeting of resources, facilitating streamlined interactions and operations within the cluster. Whether used in deploying applications or orchestrating scaling events, label selectors provide a powerful and flexible means for users to effectively manage and organize resources based on their assigned labels.

### Replication Controller & Replication Set
In Kubernetes, a "Replication Controller" and a "Replica Set" are both abstractions designed to ensure the desired number of identical pod replicas are running within the cluster. A Replication Controller, an earlier concept, is responsible for maintaining a specified number of pod replicas, restarting any that fail, and scaling the number of replicas up or down based on the defined configuration. On the other hand, a Replica Set is an evolution of the Replication Controller, offering more expressive label-based selectors for identifying and managing sets of pods. While Replication Controllers are still functional, Replica Sets provide a more advanced and flexible mechanism for managing pod replicas. Both components play a vital role in achieving high availability and scalability in Kubernetes by ensuring the consistent deployment and operation of pod instances based on user-defined configurations and policies.

### Service
In Kubernetes, a "Service" is an abstraction that provides a stable endpoint and network identity for a set of pods, allowing them to communicate with other services within the cluster. Services enable the decoupling of application components by offering a consistent way to access the dynamic set of pods that make up a workload. They can operate at the transport layer (TCP/UDP) or application layer (HTTP), and are defined by labels, allowing them to dynamically discover and load balance traffic across the underlying pods. Services play a pivotal role in facilitating the development of microservices-based architectures within Kubernetes, providing a level of abstraction that shields applications from the underlying infrastructure changes. They contribute to the scalability and reliability of applications by offering a stable endpoint that clients can reliably connect to, even as the set of pods backing the service evolves over time.

### Volume
In Kubernetes, a "Volume" is a directory or a file in a container that exists beyond the container’s lifetime and can be shared among multiple containers in the same pod. Volumes provide a means for persistent data storage and communication between containers within a pod. They abstract the underlying storage details and enable decoupling of data from the container's lifecycle, allowing for data persistence and sharing even if the container restarts or moves to another node. Kubernetes supports various types of volumes, including local storage, network-attached storage, and cloud-based storage solutions, offering flexibility to match different application requirements. Volumes play a crucial role in handling stateful applications, databases, and other scenarios where data persistence is essential, contributing to the overall reliability and flexibility of containerized applications within Kubernetes.

### Petset
In Kubernetes, a "PetSet" is a higher-level abstraction designed for managing stateful applications, particularly those that require unique identities and stable network identities. Formerly known as StatefulSet, PetSet extends the capabilities of ReplicaSets to handle stateful workloads by providing ordered and unique naming conventions for pods. PetSets are particularly useful for applications like databases, where maintaining identity, stable network addresses, and data persistence is crucial. Unlike other controllers that manage stateless pods, PetSets offer a degree of predictability and stability in the deployment and scaling of stateful applications, making them a valuable tool for scenarios where pod identity and order are significant considerations in the Kubernetes ecosystem.

### Secret
In Kubernetes, a "Secret" is an object that allows the secure storage and management of sensitive information, such as passwords, API keys, and tokens, within the cluster. Secrets are crucial for decoupling sensitive data from application code and configuration files, enhancing security practices by restricting access to confidential information. They can be used by pods to access secure credentials or configuration data during runtime. Kubernetes provides various types of secrets, including generic secrets, TLS secrets for storing certificates, and Docker registry secrets for pulling private images. By centralizing the management of sensitive information, Secrets contribute to maintaining a more secure and modular architecture within Kubernetes, ensuring that confidential data is handled with the appropriate level of protection and access controls.


## Basic Components
Kubernetes components can be broadly classified into two main categories: control plane components and node components. In Kubernetes, the terms "master node components" and "control plane components" are often used interchangeably, but they refer to the same set of critical components that collectively manage and orchestrate the overall state of the cluster. You need those essential components that work together to facilitate container orchestration, management, and communication. Here are the key components required for a basic Kubernetes cluster:

![Kubernetes Components](https://avinetworks.com/wp-content/uploads/2021/01/kubernetes-architecture-diagram-1.png "Kubernetes Components from avinetworks.com")

### Master Components
The master components in Kubernetes form the control plane, serving as the brain of the cluster and orchestrating its operations. The key master components include the kube-apiserver, which exposes the Kubernetes API and acts as the central entry point for communication; etcd, a distributed key-value store ensuring consistent storage of cluster configuration data; kube-controller-manager, responsible for overseeing various controllers that regulate the state of the system; and kube-scheduler, which assigns workloads to nodes based on resource requirements. Together, these components collaborate to manage the entire lifecycle of containerized applications, from deployment to scaling and maintenance. The master components play a pivotal role in achieving the desired state of the cluster, ensuring high availability, and facilitating seamless interactions within the Kubernetes ecosystem. They embody the intelligence and coordination required to maintain the cluster's integrity and responsiveness to the dynamic demands of modern, cloud-native environments.

#### API server
The kube API server exposes the Kubernetes REST API. It can easily scale horizontally as it is stateless and stores all the data in the etcd cluster. The API server is the embodiment of the Kubernetes control plane.

#### Etcd
Etcd is a highly reliable distributed data store. Kubernetes uses it to store the entire cluster state. In small, transient cluster a single instance of etcd can run on the same node with all the other master components. But, for more substantial clusters it is typical to have a 3-node or even 5-node etcd cluster for redundancy and high availability.

#### Controller manager
The controller manager is a collection of various managers rolled up into one binary. It contains the replication controller, the pod controller, the services controller, the endpoints controller, and others. All these managers watch over the state of the cluster via the API and their job is to steer the cluster into the desired state.

#### Scheduler
The kube-scheduler is responsible for scheduling pods into nodes. This is a very complicated task as it needs to consider multiple interacting factors, such as the following:
  • Resource requirements
  • Service requirements
  • Hardware/software policy constraints
  • Affinity and anti-affinity specifications
  • Data locality
  • Deadlines

#### DNS
Starting with Kubernetes 1.3, a DNS service is part of the standard Kubernetes cluster. It is scheduled as a regular pod. Every service (except headless services) receives a DNS name. Pods can receive a DNS name too. This is very useful for automatic discovery.

### Node Components
In the Kubernetes ecosystem, node components are fundamental to the actual execution and operation of containerized workloads. The primary node components include the kubelet, which acts as the node-level supervisor responsible for managing and maintaining individual pods, ensuring they adhere to the desired state; kube-proxy, which manages network connectivity by maintaining network rules and facilitating communication between pods; and the container runtime, which is the software responsible for running containers within pods. Together, these components collaborate to execute and manage containers on each node, responding to commands from the control plane. The node components play a critical role in ensuring the operational integrity and performance of the workloads, contributing to the scalability and efficiency of the overall Kubernetes cluster. They bridge the gap between the high-level orchestration directives from the control plane and the actual execution of containerized applications on the individual nodes, forming the operational backbone of a distributed and dynamic container environment.

#### Proxy
The kube proxy does low-level network housekeeping on each node. It reflects the Kubernetes services locally and can do TCP and UDP forwarding. It finds cluster IPs via environment variables or DNS.

#### Kubelet
The kubelet is the Kubernetes representative on the node. It oversees communicating with the master components and manage the running pods. That includes the following:
  • Download pod secrets from the API server
  • Mount volumes
  • Run the pod's container (Docker or Rkt)
  • Report the status of the node and each pod
  • Run container liveness probes

In this section, we dug into the guts of Kubernetes and explored its architecture from a very high level of vision and supported design patterns, through its APIs and the components used to control and manage the cluster. In the next section, we will take a quick look at the various runtimes that Kubernetes supports.


### Kubernetes API
If you want to understand the capabilities of a system and what it provides, you must pay a lot of attention to its API. The API (Application Programming Interface) has become a crucial aspect in modern technology for several key reasons, such as: Interoperability and Integration, Microservices Architecture, Third-Party Development, Cloud Computing and Serverless Architectures, Mobile App Development, Data Access and Sharing, Automation and DevOps, and Rapid Innovation and Prototyping. In short, the API provides a comprehensive view of what you can do with the system as a user. Kubernetes exposes several sets of REST APIs for different purposes and audiences. You can access the API through the kubectl cli, via client libraries, or directly through REST API calls.

The Kubernetes API uses a RESTful design, and its endpoints are organized in a hierarchical structure, reflecting the various resources and operations available in a Kubernetes cluster. The typical formation of a Kubernetes API endpoint follows this pattern:

```
https://<kubernetes-master>/api/<version>/<resource>/<resource-name>
```

- `<kubernetes-master>`: This is the address of the Kubernetes API server, which is the entry point for all API requests.
- `<version>`: Specifies the API version. Kubernetes supports multiple API versions to allow for backward compatibility. For example, v1 is a common version used in many API endpoints.
- `<resource>`: Represents the Kubernetes resource type, such as pods, services, deployments, etc. This denotes the object type that the API operation will act upon.
- `<resource-name>`: Refers to the specific instance or name of the resource. This part is optional for some operations.

Example API Usages:

1. List all Pods:
```
GET https://<kubernetes-master>/api/v1/pods
```
2. Get details of a specific Pod:
```
GET https://<kubernetes-master>/api/v1/namespaces/default/pods/<pod-name>
```
3. Create a Deployment:
```
POST https://<kubernetes-master>/apis/apps/v1/namespaces/default/deployments
```
4. Scale a Deployment:
```
PUT https://<kubernetes-master>/apis/apps/v1/namespaces/default/deployments/<deployment-name>/scale
```
5. Delete a Service:
```
DELETE https://<kubernetes-master>/api/v1/namespaces/default/services/<service-name>
```

### API Scopes/Groups

In Kubernetes, there are several types of APIs that serve different purposes and are organized into API groups. The two main categories are the Core API and Custom Resources (Extended API). Each category contains various API groups and versions.

1. **Core API:**
   - **v1:** The core API group includes the stable and commonly used resources. Examples include pods, services, namespaces, replication controllers, and more.

2. **Extensions API:**
   - **apps/v1:** This API group includes resources related to deploying and managing applications, such as Deployments, DaemonSets, ReplicaSets, etc.
   - **batch/v1:** Resources related to batch processing, like Jobs and CronJobs.
   - **autoscaling/v1:** Resources related to horizontal pod autoscaling.
   - **storage.k8s.io/v1:** Resources related to storage, such as StorageClasses and PersistentVolumeClaims.
   - **networking.k8s.io/v1:** Resources related to networking, including NetworkPolicies.
   - **rbac.authorization.k8s.io/v1:** Resources related to role-based access control (RBAC).
   - **policy/v1beta1:** Resources like PodSecurityPolicy for security policies.
   - **apiextensions.k8s.io/v1:** Resources for managing custom resources, including CustomResourceDefinitions (CRDs).

3. **Custom Resources (Extended API):**
   - **CustomResourceDefinitions (CRDs):** Kubernetes allows users to define their custom resources, extending the API with domain-specific objects. CRDs are part of the `apiextensions.k8s.io/v1` group.

4. **Other API Groups:**
   - Apart from the above, there are other API groups that are more specialized and used for specific purposes, such as `events.k8s.io`, `scheduling.k8s.io`, etc.

Each API group can have multiple versions, and it's common for new versions to be introduced as Kubernetes evolves. When interacting with the API, users specify the API group and version to target the desired resource.

Understanding the structure of these API as well as the different API groups and versions is essential for working with Kubernetes, especially when dealing with custom resources and extensions beyond the core set of objects. Developers and administrators use tools like kubectl or build custom scripts and applications that make HTTP requests to these endpoints to manage and orchestrate containerized workloads within a Kubernetes cluster.

