## OpenShift

OpenShift is built atop two open source keystones: application containers and the Kubernetes container orchestrator.

## Application Containers
Application containers refer to lightweight, portable, and self-sufficient environments that bundle an application and its dependencies (such as libraries, configurations, and runtime). 
Containers provide a consistent environment, ensuring that an application behaves the same way across different environments, whether it's on a developer's laptop, in a testing environment, or in production.

## Kubernetes container orchestrator
Kubernetes is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications. 
Kubernetes helps manage large numbers of containers, ensuring that the desired state of the application (e.g., the number of running instances) is maintained, handling network communication, load balancing, and more.
OpenShift uses Kubernetes to orchestrate these containers. It ensures that the desired state (e.g., a certain number of running instances of an application) is maintained. 
OpenShift also adds features like continuous deployment, automated scaling, integrated CI/CD pipelines, and more on top of Kubernetes.

## Some of OpenShift features
1. Web Console
	The OpenShift Web Console is a graphical view of the cluster and your applications.
2. Curated Software Catalogs(OpenShift app store)
	The Web Console also aggregates software catalogs, from application templates to Kubernetes Operators. The OperatorHub inside the Web Console, for
	example, is like an app store for Kubernetes applications.
3. CI/CD: Pipelines
4. Networking and service mesh
5. Integrated prometheus metrics, monitoring and alerts
	OpenShift constructs its features for monitoring cluster resources atop the opensource Prometheus project.
	The Web Console presents graphs showing CPU, memory, and network usage for the whole cluster, a project, a deployment, or all
    the way down to a running container.
	
## OpenShift Concepts

## Namespace

In Kubernetes, a namespace is a logical partitioning of cluster resources, allowing for the organization of resources and the isolation of environments within a single cluster. 


## OpenShift Project

In OpenShift, a project is an extension of the concept of a namespace in Kubernetes. While it provides the same basic functionality for resource isolation and organization, it also includes additional features tailored for enterprise environments.

## Manifest yaml
"manifest" or "manifest YAML" is usually a YAML file(configuration file) that describes or defines resources(like pods, deployments etc) and their desired state of a system or application, typically in a structured format like YAML or JSON.


## Pods

A pod is the smallest deployable unit in Kubernetes. It encapsulates one or more containers that share storage and network resources. 
Pods are designed to run a single instance of a given application, and they provide a way to manage containers that need to work together.

## ReplicaSet

A ReplicaSet is an object used to maintain a stable set of replicated pods running within a cluster at any given time.
 
## Deployment

A Deployment in Kubernetes (and OpenShift) is a higher-level abstraction that manages the lifecycle(deployment and scaling) of a set of pods. 
It ensures that a specified number of replicas of a pod are running at all times(automatically manages ReplicaSets) and provides mechanisms for updating and scaling applications seamlessly.

## Event Listener

An EventListener is a component that listens for external events (like GitHub webhooks, GitLab pushes, container image pushes or other trigger events) and responds by triggering a trigger such as a pipeline run.

 
## services

A service is an abstraction that defines a logical set of pods and a policy by which to access them. 
Services enable stable networking for pods, which can change over time as they are created or destroyed.

## OpenShift Image Stream
An Image Stream is a concept specific to OpenShift (which is built on top of Kubernetes) that provides a way to manage and track container images in a more flexible and integrated way. 
An Image Stream is essentially a way to track a specific image, regardless of where it's stored (locally in the OpenShift cluster, or externally in Docker Hub or another container registry).
 
## OpenShift Routes

In OpenShift, a route is an object that exposes a service to the outside world, allowing external traffic to reach applications running inside the OpenShift cluster. 
Routes provide a way to manage external access to services based on hostnames or paths.

## OpenShift BuildConfig(Build Configuration)

BuildConfig defines how a container image is built from source code.
It specifies the steps to take, the source from where the code comes (e.g., a Git repository, a Docker image), and the destination where the resulting image will be stored (e.g., an OpenShift internal registry or an external registry like Docker Hub).

## Controller
A controller continuously monitors the state of cluster resources and ensures that the actual state of resources matches the desired state, as specified by users through declarative configuration.

## Operator
A kubernetes operator is a specialized piece of software that acts as a controller, automatically managing the lifecycle and configuration of complex applications within the cluster, by extending the functionality of kubernetes API.
OR
A Kubernetes operator is a method of packaging, deploying, and managing an application by extending the functionality of the Kubernetes API.
It introduces new object types beyond the default resources (like Pods, Deployments, etc.) through Custom Resource Definitions, an extension mechanism in Kubernetes.

## CatalogSource
A CatalogSource represents a store of metadata that OLM(Operator Lifecycle Manager) can query to discover and install operators and their dependencies.

## OperatorSource
An OperatorSource is a Kubernetes/OpenShift resource that defines the location or source from where an operator is retrieved, allowing the system to download and install the operator on the cluster.
It is part of the broader Operator framework and plays a crucial role in making Operators available to Kubernetes clusters.

## Difference between OperatorSource and CatalogSource
"OperatorSource" is a more general term referring to the source of an operator, while "CatalogSource" specifically represents a repository or location where metadata about operators is stored, allowing the Operator Lifecycle Manager (OLM) to discover and install operators from that source. 

## Operator subscription
An Operator Subscription in Kubernetes/OpenShift is a way to declare the installation and lifecycle management of an Operator in a cluster. 

## Operator Lifecycle Manager (OLM)
OLM manages the installation and life cycle of Operators on a cluster in accordance with the cluster’s subscriptions.


## Interacting with OpenShift
To interact with OpenShift you use the openshift web console or the oc command line tool



## OpenShift Pipelines

OpenShift Pipelines is a powerful, cloud-native CI/CD (Continuous Integration/Continuous Deployment) framework built on top of Tekton, an open-source project that provides Kubernetes-native automation for CI/CD workloads.

## OpenShift Pipelines Operator
The OpenShift Pipelines Operator installs and manages Pipelines components and services.


## OpenShift pipeline resources

Command/Script: Actions or scripts executed in a step.
Step: An individual unit of work within a task (e.g., a script or command).
Task: A set of steps to perform a specific job (e.g., build, deploy). Tasks execute steps in serial order, starting each step on the completion of the one
		before it. 
Pipeline: A sequence of tasks that together define a complete CI/CD process. Unlike the steps within them, all of a pipeline’s Tasks run at once in parallel unless a Task is configured to wait
			on another. 
PipelineRun: An instantiation of a pipeline, representing a single execution of the pipeline.


##  Service Binding Operator (SBO)
The Service Binding Operator (SBO) is a Kubernetes operator that enables the automatic and dynamic binding of services(backing services such as databases and queues) to applications in a Kubernetes or OpenShift environment.
It binds by automatically managing the necessary configuration details, eliminating the need for manual configuration and providing a consistent way to access services across different environments; 

## Postgres Operator
The Postgres operator manages PostgreSQL clusters on Kubernetes (K8s)

## Role and Role binding
A role defines a set of permissions to perform actions on resources within a namespace.
A role binding associates a Role with a subject (such as a user, service account, or group).

## Finalizer
A finalizer is a special kind of metadata attached to a Kubernetes or OpenShift resource that ensures specific cleanup operations or final steps are performed before the resource is fully deleted. 
It allows for custom logic to be executed before the resource is actually removed from the cluster.
eg. A ServiceBinding might have a finalizer that ensures associated secrets or database connections are properly cleaned up before the binding itself is deleted.

## Scaling
Scaling refers to adjusting the number of instances (replicas) of a pod or application running in a Kubernetes or OpenShift cluster. 
The goal of scaling is to handle changes in application load, ensuring the system remains responsive, efficient, and resilient. 
Scaling can be done either vertically(resources such as cpu and memory) or horizontally(pods).

You can configure your application’s scale using the OpenShift CLI by executing(Manual scaling)
```
oc scale <resourcetype eg. deployment>/<deployment name> --replicas <desired replica count>
```
eg.
```
oc scale  deployment/quarkus-backend --replicas 3
```

## Horizontal Pod Autoscaler(HPA)
The Horizontal Pod Autoscaler (HPA) is one of the automatic scaling mechanisms built into OpenShift that will automatically scale your application
deployment based on a CPU and memory threshold that you define. These
metrics are captured using Prometheus, an open source monitoring solution that
is included with the OpenShift Container Platform. 

## Health-Checking Probes
Health-checking probes provide the polling(checking the status repeatedly) functionality to guarantee that your application is up, healthy, and responding as expected. 
There are three common health checks that you can configure when deploying your application on OpenShift: Readiness, Liveness, and Startup.

1. ## Readiness probe
A readiness probe determines whether a container is ready to accept service requests. 
If the readiness probe fails for a container, it will be removed from the list of available service endpoints(connection point(IP and port) where a pod can be accessed). 
After a failure, the probe continues to poll the pod. If it becomes available, OpenShift will add the pod to the list of available service endpoints.

2. ## Liveness probe
A liveness probe determines whether a container is still running.
If the liveness probe fails, Kubernetes will consider the container to be unhealthy and will restart the container to bring it back to a healthy state.

3. ## Startup probe
A startup probe indicates whether the application within a container is started.
All other probes are disabled until the startup succeeds. If the startup probe does not succeed within a specified period, OpenShift will kill the container, usually
restarting it immediately after.

## Deployment Strategies
A Deployment Strategy allows you to determine how your application is rolled out (gradual updating or deployment of application) in the event of an update, creation, updated scale(scaling), or if a pod was
killed for some other reason.

## Deployment Strategies on OpenShift
1. ## Rolling Update(Default Strategy in OpenShift)
In this strategy, Kubernetes/OpenShift gradually replaces old pods with new ones, ensuring that the application remains available during the update(No downtime).

2. ## Canary Deployment
A canary deployment tests a new version of an application before rolling it out to the entire user base of that app.
In fact, in OpenShift, all rolling deployments are canary deployments. The canary version, or the new version in a deployment update, is tested before all the old
instances of that deployment are replaced. If the canary crashes immediately or if a configured readiness check never succeeds, the canary will be removed and
the deployment will be automatically rolled back to the previously known working deployment.

3. ## Recreate
The Recreate strategy stops all the old pods before creating the new ones. 
This strategy can cause downtime during the transition, as no pods are running while the update happens.
This strategy is useful for applications where downtime is acceptable and it is necessary to completely replace the old version with the new one.
It can also be used when you want your deployment to use a persistent volume with strict writing requirements that specify that only one pod can mount the volume at a time.

4. ## Custom Deployment Strategy
Custom deployment strategy is a user-defined approach for deploying and updating applications, which goes beyond the standard deployment strategies (like Rolling Update, Recreate, or Canary) offered by default. 
This type of deployment strategy allows you to run custom commands for each rollout, and you are able to base your deployment rollout on the specific needs of a given
application as well.

## Serverless(there are still servers but the cloud provider manages them)
Serverless refers to a cloud computing model where developers can build and run applications without having to manage the underlying infrastructure.
In a serverless environment, cloud providers manage the infrastructure, scaling, and execution of code, and developers focus purely on writing and deploying their application code.

## Rollback
In Kubernetes and OpenShift, rollback refers to the process of reverting a deployment or resource to a previous, stable version after a failure or undesirable change in the application.

To view rollout history of a deployment run:
```
oc rollout history deployment/<deployment-name>
```

To perform a rollback to the previous revision run:
```
oc rollout undo deployment/<deployment-name>
```

To perform a rollback to the specific revison specify the revision number:
```
oc rollout undo deployment/<deployment-name> --to-revision=<revision-number>
```

You can validate a rollback by listing the history again.

## Listing and Detailing resources
The oc tool is the simplest form of monitoring OpenShift resources. 
There is a general pattern for addressing a resource in an oc command line. You specify
the action you want to do, the kind of object you want to do it to, and the name
of that specific object: 

``` 
oc <verb> <kind> <name>
```

Specifying a kind but not a name refers to all the objects of that kind.
eg. oc get pods   (lists all the pods running in the current project)

## Using labels to filter listed resources
Labels are key-value pairs that are used to organize and categorize resources in Kubernetes/OpenShift.
They are attached to various resources like pods, services, deployments, and more. 
Labels allow you to identify, group, and select objects based on their characteristics or use cases. 
You can select only those resources with a given label by passing a --selector or -l argument to oc get naming the label and value you want:
```
oc get pods --selector app=noted-app (get pods labeled with app=noted-app)
oc get pods -l app=noted-app
```

## Logs and Events
Logs are records of output generated by the application running inside the container or the container runtime eg.docker or containerd.
A container runtime, also known as container engine, is a software component that can run containers on a host operating system.
You can retrieve logs for a resource with the logs verb:
```
oc logs caddy-5bf94cc5b6-qfhh2
```
Events in Kubernetes/OpenShift are timestamped records of significant occurrences within the cluster, generated by the Kubernetes system, controllers, and operators.
You can view events:
```
oc get events
```
## Debugging an application in its container
## oc rsh
The oc rsh(remote shell) command in OpenShift is used to open a remote shell (a.k.a. remote SSH) session directly into a running container inside a pod. 
It allows you to access the container's environment and execute commands interactively. 
The container image must include an interactive shell.
By default, rsh picks the first container in the pod. You can specify another container in the pod by passing its name to rsh’s -c argument:
```
oc rsh <pod-name> [-c <container-name>]
```
or
```
oc rsh deployment/<deployment-name>
```
If the pod is located in a different namespace, you can specify the namespace using the -n flag:
```
oc rsh -n <namespace> <pod-name>
```
If the pod has only one container, the argument -c is not necessary.

## oc exec
The oc exec command in OpenShift is used to execute a command inside a running container within a pod.
Unlike rsh which keeps the shell open exec runs the command and exits.
You can exec where you can’t rsh; exec can directly invoke an executable without needing a shell like with oc rsh. 
Like rsh, exec connects to the pod’s first container by default, or to the container named in a -c argument:
```
oc exec <pod-name> [-c <container-name>] -- <command> [args...]
```
or
```
oc rsh deployment/<deployment-name>  -- <command> [args...]
```
eg.
```
$ oc exec caddy-5bf94cc5b6-qfhh2 -- /bin/caddy --version
v1.11
```

## oc debug
The oc debug command starts a debug pod to troubleshoot and debug a running pod or deployment.
It creates the new debug pod alongside the target pod unlike rsh which provides the shell directly in the target pod:
```
oc debug deployment/<deployment-name>
```
## OpenShift Monitoring
OpenShift monitoring is a feature built atop the open source Prometheus project that help track and observe the health, performance, and behavior of applications, containers, and clusters.
It provides real-time monitoring, logging, and alerting, helping administrators and developers to ensure the smooth operation of their OpenShift clusters and the applications running within them.
Prometheus is an open-source monitoring and alerting tool that collects metrics data and stores that data in a time series database. 

## Deleting Resources, Applications, and Projects
oc delete is used to delete resources.
To delete a project and all the resources in it:
```
oc delete project <project-name>
```
To delete a subset of resources with a particular label(eg. app=noted-app):
```
oc delete all -l app=noted-app
```
or
```
oc delete all --selector app=noted-app
```

## Templates
A template is a way to define a set of resources that can be used to create or deploy applications.
The set of objects/resources can be parameterized and the parameter values provided during the template instantiation.
When we talk about "parameterized" templates, we are referring to templates that include placeholders or variables (called parameters) that can be substituted with actual values at runtime or when the template is instantiated.

To view or inspect templates(eg. on openshift namespace) use the get verb like any other resource:
```
oc get templates -n openshift
```
## oc process
The oc process command in OpenShift is used to process a template and generate a list of resources (like Pods, Services, Deployments, etc.) on the standard output based on the template and its parameters.
Processing here means substituting parameters (placeholders) within the template with actual values to produce a final resource definition that can be used to create OpenShift resources.
If a template has been uploaded to your cluster, you can refer to it by its namespace and name: eg.
```
oc process -n openshift nginx-example  (No parameters passed so the template is outputted with default values or the placeholders)
```
```
oc process -n openshift nginx-example -p NAME=nginx-two  (parameters passed using -p followed by name and value of the parameter)
```

If the template is not on the cluster you specify the file path(-f): eg.
```
oc process -f my-template.yaml -p APP_NAME=my-new-app -p REPLICAS=3 -p IMAGE=nginx:latest
```
You can list the configurable parameters of a template:
```
oc process --parameters -n openshift nginx-example (--parameters lists the parameters of nginx-example template)
```
## oc create
The oc create command in OpenShift is used to create resources (like Pods, Services, Deployments, etc.) in the cluster from a given resource definition (YAML or JSON file):
```
oc create -f <resource-file>
```
```
oc create -f my-deployment.yaml (This would create the resources defined in the my-deployment.yaml file in the OpenShift cluster)
```
You can also run oc process and check the output. Once it’s correct, run process again, piping the output to oc create to actually create the objects:
```
oc process -n openshift nginx-example -p NAME=nginx-two | oc create -f -
```
Notice the trailing dash ( “-”) in the invocation of oc create -f -. It indicates that oc should read from the standard input.
If the resource that is supposed to be created already exists, you will get an error, and it will not modify the resource.


## oc new-app
The oc new-app command in OpenShift is used to create a new application by automatically generating and deploying resources such as a Deployment, Service, Route, BuildConfig, or ImageStream, depending on the input provided.

## Common usages of oc new-app
1. Create an application from a Git repository
```
oc new-app https://github.com/openshift/ruby-hello-world.git   (creates the build config, deployment config, service and route)
```

2. Create an application from a pre-built image
3. Create an application from an OpenShift template:
```
oc new-app -p HOST=el-event-listener-499pkk -p PORT=8080 -p TOKEN=2qnVM9Zhw3PCmvh766PMlk5LKRx_4EYx9m31ucQLmv5trBd9G -f C:/Users/gkairu/OC/templates/ngrok4.yml
```
4. Create an application from an existing Docker image or registry

## oc apply
The oc apply command in OpenShift (and Kubernetes) is used to create, update, or modify resources such as Pods, Deployments, Services, and ConfigMaps within the cluster:
```
oc apply -f <filename> [options]
```
```
oc apply -f C:/Users/gkairu/OC/roleAndRolebindings/service-binding-operator-role.yml
```
You can also apply multiple files by specifying a directory:
```
oc apply -f /path/to/directory/
```
Create or update from standard input:
```
echo -e "apiVersion: apps/v1\nkind: Deployment\nmetadata:\n  name: nginx\nspec:\n  replicas: 3\n" | oc apply -f -
```
If a resource already exists, oc apply will apply only the changes defined(merges changes) in the provided configuration without overwriting the entire resource. 
When you use oc apply, OpenShift stores the resource configurations as "previous versions" in its internal management system. This allows for easy rollback if needed (via oc rollout undo).

## oc replace
The oc replace command in OpenShift (and its Kubernetes counterpart kubectl replace) is used to replace an existing resource with a new one.
It overwrites/replaces the existing resource:
```
oc replace -f <resource_file>
```
If the resource does not exist, it will return an error (resource not found).
With oc replace, there is no merging of configuration or tracking of history. This is different from oc apply, which attempts to merge changes and only applies the differences.

## oc run
The oc run command in OpenShift is used to create and run a pod or deployment in OpenShift, typically for debugging, testing, or running one-off tasks:
```
oc run NAME --image=IMAGE [flags]
```
```
oc run -i --tty --image=image-registry.openshift-image-registry.svc:5000/openshift/java:openjdk-17-ubi8 --rm debug -- /bin/sh
```
## oc adm
The oc adm (OpenShift Cluster Administration)command in OpenShift is a command-line tool that provides administrative functions and operations for managing OpenShift clusters.

An example of oc adm command:
```
oc adm policy add-scc-to-user anyuid -z default -n o4d-noted
```
This command is adding the anyuid Security Context Constraint (SCC) to the default service account in the o4d-noted namespace.


## OpenShift Security Context Constraints (SCCs)

Security Context Constraints (SCCs) are mechanisms to control permissions for pods(and their containers). 
These permissions determine the actions that a pod can perform and what resources it can access.
Security context constraints allow an administrator to control:

1. Whether a pod can run privileged containers with the allowPrivilegedContainer flag

2. Whether a pod is constrained with the allowPrivilegeEscalation flag

3. The capabilities that a container can request

4. The use of host directories as volumes

5. The SELinux context of the container

6. The container user ID

7. The use of host namespaces and networking

8. The allocation of an FSGroup that owns the pod volumes

9. The configuration of allowable supplemental groups

10. Whether a container requires write access to its root file system

11. The usage of volume types

12. The configuration of allowable seccomp profiles

Some of default SCCs are anyuid, hostaccess, hostmount-anyuid, hostnetwork, hostnetwork-v2, restricted, restricted-v2(default) etc.





















