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

## Developer benefits of GitOps
1. **Infrastructure as Code(IaC):** Defining and managing infrastructure using machine-readable code instead of manual configuration.
In simpler terms:
> You write code to create and configure servers, networks, and cloud resources, and that code can be versioned, reviewed, and reused—just like application code.
2. **Self service:** Developers can make changes to infrastructure or applications directly through Git, without needing to manually touch clusters or wait for operations teams.
3. **Code reviews:** Code review is a software development practice in which code changes are proactively examined for errors or omissions by a second pair of eyes, leading to fewer preventable outages. 
When GitOps is used with Kubernetes, the “code” being reviewed may be primarily Kubernetes YAML manifests or other declarative configuration files, not traditional
code written in a programming language.
4. **Pull request:** a mechanism in which proposed changes can be committed to a branch or fork and then merged with the main branch through a pull request.

## The operational benefits of GitOps
1. **Declarative:** Declarative means that you define the desired state of your infrastructure and applications in a version-controlled file (typically YAML or JSON), and GitOps tools will automatically reconcile the system to that state.
2. **Observability:** Observability refers to the ability to monitor and understand the internal state of your systems based on external outputs such logs, metrics, and traces.
In GitOps, observability ensures you can see the status of your system, deployments, and infrastructure at any given time.
It enables operators to compare the actual running state with the desired state held in source control at any point in time to verify that the states match.
3. **Auditability and compliance:** Auditability and compliance are critical in regulated environments or industries that require strict control and documentation of changes made to infrastructure or applications.
All changes are recorded in Git, so you have an immutable audit trail of every change made to your infrastructure or applications. This includes who made the change, what was changed, and why it was changed (through commit messages).
Git repositories themselves can be configured with role-based access control (RBAC), meaning only authorized personnel can change the infrastructure or code.
**Compliance** refers to an organization’s information system conforming to industry standards and internal security policies regarding customer data and access controls.
**Auditability** is the capability of a system to be examined and proven to conform to those standards and policies.
Auditability means being able to prove who changed what, when, and why.
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

Since late 2016, Kubernetes has become recognized as the dominant de facto industry standard container orchestration system in much the same way that Docker has become
the standard for containers.

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

* **ReplicaSet:** A ReplicaSet is a controller that ensures a specified number of identical Pods are running at any given time. 
It manages the replication of Pods to maintain the desired state, meaning it will automatically create or delete Pods as necessary to match the desired number of replicas.
* **Deployment:** declaratively manages a set of identical Pods and keeps them running in the desired state.
* **Job:**  A job creates one or more Pods that run to completion. Unlike regular Pods that keep running indefinitely, a Job's Pods run to completion and then stop once they finish their task.
* **CronJob:** A CronJob is a Job that runs on a scheduled basis, similar to cron jobs in Linux. CronJobs allow you to run tasks at specific intervals, such as hourly, daily, weekly, etc.
* **Namespace:** A Namespace is a logical partition or virtual cluster within a physical Kubernetes cluster.

### Kubernetes components
A Kubernetes cluster consists of a **control plane** and one or more **worker nodes**. 

### Control plane
The Kubernetes control plane monitors the cluster state, makes all the global decisions about the cluster (like scheduling, scaling, and responding to failures/events) and manages the overall state of the system.
To perform these duties, control plane has the below components:

* **kube-apiserver:** exposes the Kubernetes API and provides access to cluster data. The API server is the front end for the Kubernetes control plane.
All communication (from kubectl, other components, users, and services) goes through the API server.

* **kube-controller-manager:** Runs various controllers that manage cluster objects and maintain the desired state.
* **kube-scheduler:** Schedules pods on worker nodes. It does this by Looking for Pods not yet bound to a node, and assigns each Pod to a suitable node.
* **etcd:** A distributed(for high availability), consistent key-value store that stores the state(including configuration) of the cluster/cluster data. 
* **cloud-controller-manager(optional):** Integrates with underlying cloud provider(s).

### Worker node/node
In Kubernetes, a worker node, also called a node, is a physical or virtual machine within a cluster that runs the containerized applications/pods and is managed by the control plane.
The worker node has the below components:
* **kubelet:**  An agent that communicates with the control plane via Kubernetes API server(kube-apiserver) and ensures pods are running as expected.
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

**Reproducibility** is the ability to rerun a computational experiment and get the same results.

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

## `kubectl`
`kubectl` stands for: Kubernetes Control.  
It is the command-line tool to control Kubernetes resources/objects in a cluster.

**What it’s used for**  
kubectl lets you:  
* Deploy applications (`kubectl apply`, `kubectl create`)
* Inspect cluster state (`kubectl get`, `kubectl describe`)
* Debug workloads (`kubectl logs`, `kubectl exec`)
* Manage resources (`kubectl delete`, `kubectl scale`)

It supports imperative commands, imperative object configuration, and declarative object configuration.

**`kubectl create` vs `kubectl apply`**
A `kubectl create` will fail if the resource already exists. 
The `kubectl apply` command first detects whether the resource exists and performs a create operation if the object doesn’t exist or an update if it already exists. 

| Aspect (starting with the big difference) | `kubectl create`                  | `kubectl apply`                                   |
| ----------------------------------------- | --------------------------------- | ------------------------------------------------- |
| **Core intent (big difference)**          | Create a resource **once**        | Declare and **continuously manage desired state** |
| **If resource already exists**            | ❌ Fails with “already exists”     | ✅ Updates existing resource                       |
| **Idempotent (safe to re-run)**           | ❌ No                              | ✅ Yes                                             |
| **State tracking**                        | ❌ No record of previous config    | ✅ Stores last-applied configuration               |
| **Merge behavior**                        | Full object create only           | 3-way merge (live, last-applied, new)             |
| **Field ownership**                       | None                              | Tracks field ownership (who owns what)            |
| **Risk of overwriting changes**           | High (manual replaces needed)     | Low (preserves other actors’ fields)              |
| **Declarative workflow**                  | ❌ Imperative                      | ✅ Declarative-first                               |
| **GitOps / CI-CD friendly**               | ❌ No                              | ✅ Yes                                             |
| **Typical usage**                         | Bootstrapping, quick experiments  | Production workloads, Git-managed configs         |
| **Generates YAML**                        | ✅ Excellent (`--dry-run -o yaml`) | ⚠️ Not its purpose                                |
| **Controllers reconciliation fit**        | Weak                              | Native                                            |
| **Recommended for production**            | ❌ No                              | ✅ Yes                                             |

**`kubectl diff`**  
The `kubectl diff` command compares the current state of a resource in the cluster with the desired state defined in a local manifest file (YAML).   
It shows the differences between these two states.  
**Example of its usage**  
	kubectl diff -f deployment.yaml

It’s especially useful for GitOps, CI/CD, and pre-deployment checks.  
It provides visibility into changes and reduces risk by showing you exactly what will change before applying it.  

**3-way merge**  
A three-way merge is a merge algorithm that combines changes from two different versions of a file by comparing them to a common ancestor (base) version.  
This process is a fundamental component of modern version control systems like Git and also it is also performed by `kubectl apply`.  

When you run `kubectl apply -f <resource>.yaml`, Kubernetes performs a 3-way merge between:
* **The Base:** The last applied configuration (stored as annotations in the resource).
* **The Current:** The live configuration (what's currently running in the cluster).
* **The New:** The configuration you're applying (the file you’re giving with kubectl apply).  

**All merge possibilities (well-explained table)**  
Assume we are merging one field (e.g. `replicas`).
| Case | Base | Current | New     | What happened                        | Result             | Conflict?           |
| ---- | ---- | ------- | ------- | ------------------------------------ | ------------------ | ------------------- |
| 1    | A    | A       | A       | Nothing changed anywhere             | Keep A             | ❌ No                |
| 2    | A    | A       | B       | Only *you* changed it                | Apply B            | ❌ No                |
| 3    | A    | B       | A       | Someone else changed it, you didn’t  | Keep B             | ❌ No                |
| 4    | A    | B       | B       | Both changed it to the same value    | Keep B             | ❌ No                |
| 5    | A    | B       | C       | Both changed it differently          | **Ambiguous**      | ✅ **YES**           |
| 6    | A    | A       | removed | You removed it                       | Remove             | ❌ No                |
| 7    | A    | removed | A       | Someone removed it, you want it back | Restore A          | ❌ No                |
| 8    | A    | removed | B       | Someone removed it, you changed it   | **Intent unclear** | ⚠️ Usually conflict |


You typically should not mix imperative commands, such as `kubectl edit` or `kubectl scale`, with declarative resource management.   
This will make the current state not match the last-applied-configuration annotation and will defeat the merge algorithm kubectl uses to determine deleted fields.  
`kubectl apply` deletes fields only if it previously applied them.  
The `kubectl replace` command similarly ignores the last-applied-configuration annotation and removes that annotation altogether after applying the changes.  
So if you make any changes imperatively, you should be ready to undo the changes using imperative commands before continuing with declarative configuration.  

To stop managing a field, remove it from the YAML and re-apply the manifest so `kubectl apply` can update the last-applied annotation automatically.  
Client-side apply(`kubectl apply`) can cause disruption by resetting managed fields (like replicas) to default values if you remove them from the manifest.  
Server-side apply(`kubectl apply --server-side`) avoids this issue by allowing Kubernetes to remove ownership of the field without resetting it, enabling other controllers (like HPA) to continue managing it.  

## Controller
A controller is a Kubernetes component that implements control loops to continuously reconcile the actual state of cluster resources with their desired state.  
A control loop is the reconciliation pattern; a controller is the software that executes that pattern in Kubernetes.  
**Examples of Controllers**  
| Controller                    | Resource Watched                | What it Actually Reconciles                                         |
| ----------------------------- | ------------------------------- | ------------------------------------------------------------------- |
| **Deployment Controller**     | Deployments                     | Manages ReplicaSets and rollout strategy (create, update, rollback) |
| **ReplicaSet Controller**     | ReplicaSets                     | Ensures the desired number of Pods are running                      |
| **StatefulSet Controller**    | StatefulSets                    | Manages ordered, stable Pods with persistent identity               |
| **DaemonSet Controller**      | DaemonSets                      | Ensures one Pod per node (or selected nodes)                        |
| **Job Controller**            | Jobs                            | Ensures Pods run to successful completion                           |
| **CronJob Controller**        | CronJobs                        | Creates Jobs on a time-based schedule                               |
| **Horizontal Pod Autoscaler** | Deployments / RS / StatefulSets | Adjusts replica count based on metrics                              |

**API Object**
An API object is a Kubernetes resource stored in the API server that declaratively defines desired state and is reconciled by controllers.  
**Common Kubernetes API objects**  
| Category       | Examples                                      |
| -------------- | --------------------------------------------- |
| Workloads      | Pod, ReplicaSet, Deployment, StatefulSet, Job |
| Networking     | Service, Ingress                              |
| Storage        | PersistentVolume, PersistentVolumeClaim       |
| Config         | ConfigMap, Secret                             |
| Access control | Role, RoleBinding, ServiceAccount             |
| Extensions     | Custom Resources (CRDs)                       |

**Kind vs API Object vs Resource**  
A **Kind** defines what type of object something is.  
Examples: `Pod`, `Deployment`, `Service`, `ConfigMap`  
Defined in YAML as `kind:`  
Describes the schema and behavior  
Think of it as a class in programming  
	kind: Deployment

An **API object** is a specific instance of a kind, stored in the API server. 
Examples: A Deployment named `nginx-deployment`, A Pod named `nginx-abc123`  
Has `metadata.name`, `spec`, `status`  
Represents desired state  
Reconciled by controllers  
	apiVersion: apps/v1
	kind: Deployment
	metadata:
	  name: nginx-deployment


A **resource** is the REST API endpoint exposed by the Kubernetes API server.  
Examples: `pods`, `deployments`, `services`, `configmaps`  
Always plural  
What you interact with via `kubectl`  
Maps to URLs like: 
 
	/api/v1/pods
	/apis/apps/v1/deployments  

	kubectl get deployments

| Concept        | What it is           | Example            | Analogy         |
| -------------- | -------------------- | ------------------ | --------------- |
| **Kind**       | Object type / schema | `Deployment`       | Class           |
| **Resource**   | API endpoint         | `deployments`      | REST collection |
| **API Object** | Concrete instance    | `nginx-deployment` | Object          |


### Controller delegation
Controller delegation in Kubernetes is a pattern where a controller fulfills its responsibility by creating or updating API objects that are then reconciled by other, more specialized controllers.  
**Canonical example: Deployment → ReplicaSet → Pods**  
> A Deployment controller does not create or manage Pods directly.  
> Instead, it delegates Pod replication to a ReplicaSet controller by creating or updating ReplicaSet objects.  
> The ReplicaSet controller then creates and maintains the required Pods.  

Controller delegation is a design pattern that enhances modularity, extensibility, and scalability within the Kubernetes architecture.  

* **Modularity**
Each controller has a single, focused responsibility (Deployment = rollout logic, ReplicaSet = pod count, etc.).  
* **Extensibility**
New behavior can be added by introducing new controllers (e.g., Operators, HPAs) without changing existing ones.
* **Scalability**
Controllers operate independently and reconcile state via the API, allowing the control plane to scale safely and reliably.

### Controller pattern
The controller pattern in Kubernetes is a design pattern that uses control loops to continuously monitor the cluster's actual state and takes actions to reconcile it with the desired state specified by the user, via API objects.  

**How the Controller Pattern Works**
The pattern is based on a continuous reconciliation loop: 
* **Desired State (Spec):** A user defines the desired state of a resource (e.g., in a YAML file) in the spec field of a Kubernetes object. This is what the user wants the system to look like.
* **Actual State (Status):** The Kubernetes system and its components constantly report the current, actual state of the resources in the cluster, which is stored in the object's status field.
* **The Control Loop:** The controller runs in a non-terminating loop, constantly comparing the actual state with the desired state.
* **Reconciliation:** If a discrepancy is detected, the controller takes action to reconcile the two states. For example, if a user specifies 3 replicas of an application but only 2 pods are running, the controller will create a new pod.  

## Controllers vs operators
Controllers are core Kubernetes components that implement the control loop pattern for built-in resources.  
An operator is a specific type of custom controller that uses domain-specific knowledge and API extensions (Custom Resource Definitions or CRDs) to manage complex applications.  
| Feature       | Controller                                      | Operator                                            |
| ------------- | ----------------------------------------------- | --------------------------------------------------- |
| Resource type | Built-in Kubernetes resources                   | Custom resources (CRDs) or apps                     |
| Complexity    | Simple, generic logic                           | Complex, application-specific logic                 |
| Purpose       | Maintain cluster state                          | Automate operational tasks for apps                 |
| Example       | ReplicaSet, Deployment, StatefulSet controllers | MySQL operator, Prometheus operator, Kafka operator |
| Extensibility | Static, core Kubernetes                         | Highly extensible via CRDs                          |

All operators use the controller pattern, but not all controllers are operators.

## Kubernetes Watch API
The Kubernetes Watch API allows clients to continuously receive a stream of events when Kubernetes resources are created, updated, or deleted, instead of repeatedly polling the API server.  
**Who uses the Watch API**  
| Component   | Usage                             |
| ----------- | --------------------------------- |
| Controllers | Reconcile resource state          |
| Operators   | React to resource changes         |
| kubelet     | Track assigned Pods               |
| kubectl     | Display live updates (`--watch`)  |
| Informers   | Cached, scalable watch management |

**Watch API vs Polling**
| Polling               | Watch API                 |
| --------------------- | ------------------------- |
| Repeated requests     | Single open connection    |
| Higher API load       | More efficient            |
| Slower updates        | Near real-time events     |
| Simple implementation | Event-driven architecture |


The `kubectl` utility allows watching for resource changes using the get command with the `--watch` flag:  

	kubectl get pods --watch

This Lists existing pods, then keeps streaming changes:

	kubectl get pods --watch
	NAME                               READY   STATUS    RESTARTS   AGE
	nginx-imperative-bdbc5c75b-wt5d5   0/1     Pending   0          0s
	nginx-imperative-bdbc5c75b-wt5d5   0/1     Pending   0          0s
	nginx-imperative-bdbc5c75b-wt5d5   0/1     ContainerCreating   0          0s
	nginx-imperative-bdbc5c75b-d6c8z   0/1     Pending             0          0s
	nginx-imperative-bdbc5c75b-g88w2   0/1     Pending             0          0s
	nginx-imperative-bdbc5c75b-d6c8z   0/1     Pending             0          0s
	nginx-imperative-bdbc5c75b-g88w2   0/1     Pending             0          0s

The `--output-watch-events` command instructs `kubectl` to output the change type, which takes one of the following values: `ADDED`, `MODIFIED`, or `DELETED`:

	kubectl get pods --watch --output-watch-events
	EVENT      NAME                               READY   STATUS    RESTARTS   AGE
	ADDED      nginx-imperative-bdbc5c75b-d6c8z   1/1     Running   0          5m55s
	ADDED      nginx-imperative-bdbc5c75b-g88w2   1/1     Running   0          5m55s
	ADDED      nginx-imperative-bdbc5c75b-wt5d5   1/1     Running   0          6m3s
	...
	MODIFIED   nginx-imperative-bdbc5c75b-d6c8z   0/1     Completed     0          6m27s
	DELETED    nginx-imperative-bdbc5c75b-d6c8z   0/1     Completed     0          6m27s

## How you can create an custom nginx controller
The NGINX operator watches ConfigMaps and reconciles them into NGINX Deployments, delegating pod management to Kubernetes controllers.  
* Operator = custom Kubernetes controller
* Desired state stored in ConfigMaps
* One ConfigMap represents one NGINX server
* ConfigMap data contains static website content
* Operator watches ConfigMaps and the respective events using Watch API
* Operator runs an infinite reconciliation loop
* On ADDED → create Deployment
* On MODIFIED → update Deployment
* On DELETED → delete Deployment
* Operator delegates runtime to Deployment controller
* NGINX pods mount ConfigMap as static content
* No direct Pod management by operator
* Can be implemented as a Bash script using `kubectl --watch` or any other language including Java, C++ or even JavaScript
* Below is a sample configmap yaml and the respective controller implemented as a bash script:  

	apiVersion: v1
	kind: ConfigMap
	metadata:
	  name: sample
	data:
	  index.html: hello world


	#!/usr/bin/env bash

	kubectl get --watch --output-watch-events configmap \
	-o=custom-columns=type:type,name:object.metadata.name \
	--no-headers | \
	while read next; do                                        #B

		NAME=$(echo $next | cut -d' ' -f2)                     #C
		EVENT=$(echo $next | cut -d' ' -f1)

		case $EVENT in
			ADDED|MODIFIED)                                    #D
				kubectl apply -f - << EOF
	apiVersion: apps/v1
	kind: Deployment
	metadata: { name: $NAME }
	spec:
	  selector:
		matchLabels: { app: $NAME }
	  template:
		metadata:
		  labels: { app: $NAME }
		  annotations: { kubectl.kubernetes.io/restartedAt: $(date) }
		spec:
		  containers:
		  - image: nginx
			name: $NAME
			ports:
			- containerPort: 80
			volumeMounts:
			- { name: data, mountPath: /usr/share/nginx/html }
		  volumes:
		  - name: data
			configMap:
			  name: $NAME
	EOF
				;;
			DELETED)                                            #E
				kubectl delete deploy $NAME
				;;
		esac
	done




















