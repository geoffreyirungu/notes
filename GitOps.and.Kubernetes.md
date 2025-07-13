# GitOps and Kubernetes

source code: https://github.com/gitopsbook/resources

## Infrastructure Configuration and Software Deployment
Two every day tasks of managing and operating computer systems are infrastructure configuration and software deployment:

* **Infrastructure configuration** involves setting up and customizing the resources needed such as servers, networks, storage, databases, and more to run software

* **Software deployment** is the process of releasing your application to a runtime environment(on the computing infrastructure) — usually moving it from development to staging or production.


## Traditional IT Operations (ops)
In this model, development and operations teams are siloed(work in isolation): Developers write the code, pass it to QA who then pass it to IT Operations team.

## DevOps and GitOps
**DevOps** is a culture and set of practices that enable software development (dev) and IT operations (ops) teams to accelerate delivery through automation(test, build and deploy), collaboration, fast feedback, and iterative improvement.
The development side involves activities such as coding, building, testing, and deploying software applications. 
The IT Operation side focuses on the infrastructure needed to support the application, including managing servers, networks, and databases, as well as deploying, maintaining, monitoring and troubleshooting the software in a production environment. 

**GitOps** is a subset/extension of DevOps that uses Git as the single source of truth for managing infrastructure and application configuration and deployments.
Git refers to the version control system that tracks changes in files over time.
Ops refers to IT operations aspect of managing and deploying infrastructure and applications.

## Version/Revision/Source Control and Change control
**Version control** is a system for managing and tracking changes to files or directories over time.
It allows developers to keep a history of changes, revert to previous versions, and collaborate on the same codebase without conflicts.  
Git is a widely used distributed version control system, meaning that each developer has their own local copy of the repository and can work independently, making it easier to manage changes. 

**Change control** manages how changes are proposed, reviewed, approved, and applied to a system, whether it's code, configuration, or infrastructure.

## Git
* **pull request:** A pull request is a proposal to merge a set of changes from one branch into another.
* **request-pull command:** generates a summary of changes between two branches (or commits) in a way that someone else (like a project maintainer) can review and manually pull your changes.

Git isn’t just limited to managing code — it’s also used in system operations and management.
**System operations and management** is the process of ensuring that an organization's systems, including hardware and software, function reliably and efficiently.
It involves a wide range of activities, from basic system monitoring and maintenance to more complex tasks like configuring servers, managing networks and resources(such as cpu, ram and storage), automation (using scripts and tools to automate repetitive tasks) and ensuring system security.

#### Here’s how Git is used for System Operations and Management:
1. **Configuration management:** System configuration management tools like Ansible, Chef, or Puppet often use Git as a repository for configuration files.
2. **Infrastructure as Code:** Git can be used to manage infrastructure as code, where infrastructure is defined in code and tracked using Git.
3. **Automation(Deployment and CI/CD):** Git can be used to automate deployments by triggering automated processes when changes are pushed to specific branches.
Git is also a key part of CI/CD pipelines, enabling automated testing, building, and deployment of software. 
4. **Security(Auditing and Access Control):** Git provides a complete history of changes, making it possible to audit changes to configuration files or code.
Git repositories can be configured to restrict access to specific branches or files, improving security.  
5. **Backup and Disaster Recovery:** Storing backups of configurations or scripts in Git allows quick recovery of important files.


## The operational benefits of GitOps
1. **Declarative:** Declarative means that you define the desired state of your infrastructure and applications in a version-controlled file (typically YAML or JSON), and GitOps tools will automatically reconcile the system to that state.
2. **Observability:** Observability refers to the ability to monitor and understand the internal state of your systems based on external outputs such logs, metrics, and traces.
In GitOps, observability ensures you can see the status of your system, deployments, and infrastructure at any given time.
3. **Auditability and compliance:** Auditability and compliance are critical in regulated environments or industries that require strict control and documentation of changes made to infrastructure or applications.
All changes are recorded in Git, so you have an immutable audit trail of every change made to your infrastructure or applications. This includes who made the change, what was changed, and why it was changed (through commit messages).
Git repositories themselves can be configured with role-based access control (RBAC), meaning only authorized personnel can change the infrastructure or code.
4. **Disaster Recovery:** Disaster recovery refers to the ability to restore the system quickly and reliably after an unexpected failure or catastrophe.
Since your entire infrastructure and application configurations are stored in Git as code (in files like YAML), you can rebuild or redeploy your system from scratch just by checking out the Git repository and applying the configurations.


## Container and Containerization
A **container** is a packaged unit that contains an app and everything it needs to run.
**Containerization** is the process of creating and deploying apps in containers OR the process of packaging applications and their dependencies into containers.


## Container orchestration
Container orchestration is the process of automating the deployment, management, scaling, and networking of containers throughout their lifecycle.

## Kubernetes
Kubernetes is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications.
It was released in 2014. 

**NOTE** Borg is Google’s internal container cluster management system used to power online services like Google search, Gmail, and YouTube. Kubernetes
leverages Borg’s innovations and lessons learned, explaining why it is more stable and moves so much more quickly than its competitors.

**Cluster:** A group of computers (nodes) that work together as a single system.These computers (or nodes) coordinate and share resources to perform tasks collectively, often to provide high availability, scalability, or fault tolerance.
examples of clusters include kubernetes cluster, database cluster and HPC cluster.

Kubernetes was initially developed and open-sourced by Google based on a decade of experience with container orchestration using Borg, Google's proprietary cluster management system.
Because of this, Kubernetes is relatively stable and mature for a system so complex. 

Despite being started by Google, Kubernetes is not influenced by a single vendor. This makes the community open, collaborative, and innovative.

Other container orchestration platforms include Openshift(built atop kubernetes), docker swarm and Apache Mesos.

## Kubernetes Architecture
Kubernetes provides a layer of abstraction over the infrastructure.
High-level abstractions provide a simplified view, focusing on the desired state and application-level details, while low-level abstractions deal with the underlying infrastructure and details. 
The following set of basic objects represent the desired cluster state:

* **Pod:** A pod is one or more containers deployed together on the same host(node/vm/physical machine). A Pod is the smallest deployable unit in Kubernetes.
It provides a way to mount storage, set environment variables, and provide other container configuration information.

* **Service:** A service is an abstraction that defines a logical set of pods and a policy by which to access them. It provides a stable, unified endpoint for accessing a group of Pods, even if the Pods themselves are constantly being created, destroyed, or moved around by the Kubernetes scheduler.
In other words, a Service is a way of exposing an application running on a set of Pods to other Pods, users, or external systems.

* **Volume:** A volume is a directory accessible to containers running in a Pod. Unlike the container’s filesystem (which is ephemeral and lost when the container restarts), a volume provides persistent or shared storage that lives beyond the container's lifecycle — and in some cases even beyond the Pod's lifecycle.

Kubernetes architecture uses primary resources as a foundational layer for a set of higher-level resources. Example of high-level resources include

* **ReplicaSet:** A ReplicaSet is a controller that ensures a specified number of identical Pods are running at any given time. It manages the replication of Pods to maintain the desired state, meaning it will automatically create or delete Pods as necessary to match the desired number of replicas.
* **Deployment:** A Deployment manages the deployment and scaling of Pods, providing a declarative way to manage your application lifecycle.
* **Job:**  A job creates one or more Pods that run to completion. Unlike regular Pods that keep running indefinitely, a Job's Pods run to completion and then stop once they finish their task.
* **CronJob:** A CronJob is a Job that runs on a scheduled basis, similar to cron jobs in Linux. CronJobs allow you to run tasks at specific intervals, such as hourly, daily, weekly, etc.
* **Namespace:** A Namespace is a logical partition or virtual cluster within a physical Kubernetes cluster.

### Kubernetes components
A Kubernetes cluster consists of a control plane and one or more worker nodes. 

### Control plane
The Kubernetes control plane stores kubernetes objects and manages the cluster and its resources such as worker nodes and pods.
It monitors the cluster state, makes all the global decisions about the cluster (like scheduling, scaling, and responding to failures/events) and manages the overall state of the system.
To perform these duties, control plane has the below components:

* **kube-apiserver:** exposes the Kubernetes API and provides access to cluster data. The API server is the front end for the Kubernetes control plane.
All communication (from kubectl, other components, users, and services) goes through the API server.

* **kube-controller-manager:** Runs various controllers that manage cluster objects and maintain the desired state.
* **kube-scheduler:** Schedules pods on worker nodes. It does this by Looking for Pods not yet bound to a node, and assigns each Pod to a suitable node.
* **etcd:** A distributed(for high availability), consistent key-value store that stores the state(including configuration) of the cluster/cluster data. 
* **cloud-controller-manager(optional):** Integrates with underlying cloud provider(s).

## Worker node/node
In Kubernetes, a worker node, also called a node, is a physical or virtual machine within a cluster that runs the containerized applications/pods.
The worker node has the below components:
* **kubelet:**  An agent that communicates with the Kubernetes API server(kube-apiserver) and ensures pods are running as expected.
* **kube-proxy (optional):**  A network proxy(intermediary in the network traffic flow within a Kubernetes cluster, specifically between services and pods) that manages network rules and enables communication between pods and services.
* **container runtime/container engine:** Software/engine (like Docker) that pulls container images, starts/runs containers, and manages their lifecycle eg. containerd, CRI-O and docker engine. 

A **software agent** is a specialized program or software component designed to perform tasks autonomously or semi-autonomously on behalf of a user or another system. 



## Imperative vs Declarative Commands
In Kubernetes, there are two primary methods for configuring state: imperative and declarative.

* **Imperative:** explicitly instructs Kubernetes what to do, step by step, using specific/direct kubectl commands. eg.

	kubectl run nginx --image=nginx --port=80 ## create a Pod named nginx with the specified image (nginx) and open port 80.
	kubectl expose pod nginx --port=8080 --target-port=80 --name=nginx-service ## expose the Pod as a service that maps port 8080 on the service to port 80 on the Pod.

Imperative commands are useful for learning and experimentation but lack reproducibility and version control. 

* **Declarative:** specifys the desired state of the kubernetes object in a YAML/JSON file(manifest) and then using the `kubectl apply` command to apply the manifest to the cluster. After that Kubernetes figures out how to achieve that state.

Declarative approach is best for reproducible deployments and tracking changes.

## Required Fields in the Manifest(YAML/JSON file) for a Kubernetes Object
* **kind:** defines what kind of object you want to create eg. Pod, Deployment, Service and ReplicaSet
* **apiVersion:** defines which version of the Kubernetes API you're using to create this object eg. apps/v1, core/v1(or just v1), batch/v1 and networking.k8s.io/v1
The format of the apiVersion field is api_group/version.Some core resources belong to the core API group, which is special — for those, the group part is omitted, and you just write:
	apiVersion: v1
* **metadata:** data that helps identify the kubernetes resource/object. Common metadata subfields include name, namespace, labels, annotations, UID and timestamps.
* **spec:** stands for specification and describes the desired state/configuration of the object. The specific contents of the spec field vary depending on the type of Kubernetes object.
For example, in a Pod object, the spec field might include: containers, volume, restartPolicy and network policy.

Below is a manifest example of a Pod that hosts a website using NGINX:

	kind: Pod
	apiVersion: v1
	metadata:
		name: nginx
	spec:
		restartPolicy: Always ## The restartPolicy defines how Kubernetes should react when a container in a Pod exits — whether it finished successfully or crashed.
		volumes:   # Shared directory(all containers has access to it) accessible to containers
			- name: data
			emptyDir: {}
		initContainers: ## Run before the main containers, in sequence. Used for setup/initialization tasks. Here the container creates a file index.html in the shared directory/volume.
		- name: nginx-init5
		  image: docker/whalesay
		  command: [sh, -c] ## The command field specifies the executable that will run when the container starts. This overrides the container entrypoint (the program that runs when the container starts).
		  args: [echo "<pre>$(cowsay -b 'Hello Kubernetes')</pre>" > /data/index.html] ## The arguments of the command. This overrides the arguments passed to the entrypoint or command.
		  volumeMounts: ## Mounts a volume. In this case the data volume.
		  - name: data
			mountPath: /data
		containers:  ## Run the actual application, all together(concurrently) and after init containers are done.
		- name: nginx
		  image: nginx:1.11
		  volumeMounts:  ## Mounts a volume. In this case the data volume.
		  - name: data
			mountPath: /usr/share/nginx/html

#### Important notes on restartPolicy
* restartPolicy types: 
	* **Always:** Always restart the container if it exits. Used for long running services (e.g. web servers).
	* **OnFailure:** Restart only if the container exits with a non-zero (error) exit code. Used for One-time jobs (e.g. batch tasks)
	* **Never:** Never restart the container, even if it fails. Used for Debug Pods or development tasks.
* Applies only to the Pod type (kind: Pod) directly.
* For Deployments, ReplicaSets, etc., the restartPolicy is always Always (even if not shown), and you can’t change it.
* initContainers are never restarted unless the Pod itself restarts.




