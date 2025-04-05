## Jenkins

Jenkins is an open source automation server written in Java.
Automation Server, also known as a CI/CD server or a build server, is a software tool that automates repetitive tasks involved in software development and deployment workflows such as building, testing, deploying, and delivering software.
Othere examples of automation servers: Gitlab CI/CD, Azure devops and bamboo.

## What is CI(Continuous Integration)/CD(Continuous Delivery/Deployment)
* Continuous Integration  is a software development practice where developers frequently integrate(merge/combine) their code changes into a shared version control repository where each integration is verified by running automated builds and tests to catch bugs as early as possible.
* Continuous Delivery is an extension of CI. In Continuous Delivery, code that has passed automated tests is automatically prepared for deployment to production or staging environments, but may require manual approval before final release/deployment to production. 
* In Continuous Deployment, the code that passes all automated tests is automatically deployed to production without manual approval/intervention.

## What is a build
In software development, a build refers to the process of converting source code into a functional, executable software artifact (like an application or library) that can be run on a computer. 
This typically involves compiling, linking, and packaging the code.  


## Workspace
In Jenkins, the workspace is the directory used by Jenkins during the build process to store project files, source code, logs, and build artifacts.

## Continuous Code Quality
Continuous Code Quality refers to the practice of continuously monitoring and improving the quality of the source code throughout the development lifecycle. 
It involves automated checks for static code analysis, bugs, security vulnerabilities, code style issues, unit tests, integration tests, testing coverage, and other quality metrics.
Continuous code quality is a vital part of both CI and CD, ensuring that every code change is of high quality and that the software is reliable and stable. 
However, its core is typically in CI where feedback is given during the integration phase.

## Static code analysis
Static Code Analysis refers to the process of analyzing a program's source code without executing it.
It involves examining the code for potential issues such as bugs, security vulnerabilities, code smells, violations of coding standards, and other types of quality defects.
Some of the popular static code analysis tools are Sonarqube, ESLint and CodeClimate.

## Quality Profile (SonarQube)
A quality profile defines a set of rules (that are specific to a language) to be applied during code analysis.

## Quality gate (SonarQube)
A Quality Gate is used to enforce policy in organization for static code analysis.
After analysis(using a particular quality profile), the quality gate takes the resulting metrics and compares them to its defined thresholds to determine if the code meets the requirements for release or merge.

## Integrating SonarQube with Jenkins
1. Install the SonarQube Scanner plugin in Jenkins
2. Configure SonarQube Servers in Jenkins
	1. Go to Manage Jenkins > Configure System.
	2. Scroll down to the SonarQube configuration section, click Add SonarQube, and add the values you're prompted for.
	3. The server authentication token(Generated from SonarQube) should be created as a Secret Text credential.
3. Configure the SonarQube scanner
	1. Go to Manage Jenkins > Tools.
	2. Scroll down to the SonarQube Scanner Installations section, click Add SonarQube Scanner.
	3. Check install automatically and give the SonarQube Scanner a name, then click save.
4. You can now use the SonarQube scanner by selecting Execute SonarQube Scanner in the build section of an item.

## Integrating SonarQube Quality gate plugin with Jenkins
1. Install the SonarQube quality gate plugin in Jenkins
2. Configure SonarQube Servers in Jenkins
	1. Go to Manage Jenkins > Configure System.
	2. Scroll down to the sonar quality gates section, click Add Sonar instance, and add the values you're prompted for.
3. You can now use the SonarQube quality gate by selecting quality gates sonarqube plugin in the post build actions section of an item.

## Configuring email notification for an unstable build in Jenkins
1. Go to Manage Jenkins > Configure System.
2. Scroll down to email notification section, and add the values you're prompted for. Then you an test by sending a test mail.
3. You can now send mails on build status by selecting email notification in the post build actions section of an item and entering the recipient mail. 

## Dashboard (Jenkins)
A dashboard displays an overview of all Pipeline projects configured on a Jenkins controller.

## Apache ANT(Another Neat Tool)
Apache ANT is a build automation tool that automates tasks like compiling, testing, and deploying applications, especially those written in java.
Ant can also be used effectively to build non Java applications, for instance C or C++ applications.

## Apache Maven
Apache maven is a build automation and project management, especially popular for Java projects, tool that automates tasks like source code compilation and dependency management, running automated tests, and packaging binary code.
Maven can also be used to build and manage projects written in C#, Ruby, Scala, and other languages.

## Difference between Ant and Maven
The main difference is Maven uses conventions(like where the code is located) and a lifecycle(predefined build phases), while Ant requires explicit instructions/configuration and lacks built-in dependency management. 
* ## conventions
Maven follows the "Convention over Configuration" principle. This means it comes with a standardized project structure and default behaviors. For example, in Maven: Your source code should be in src/main/java, tests in src/test/java.
Because of these conventions, developers don’t need to explicitly tell Maven where to find source code, tests, or how to generate the output. Maven assumes that your project follows these conventions. 

* ## lifecycle
Maven introduces a project lifecycle, which is a set of predefined build phases (such as compile, test, package, install, deploy, etc.). 
These phases define the sequence of steps to build a project and can be customized using plugins, but the order and overall flow are fixed.
For example, when you run the command mvn clean install, Maven will go through the following steps:
1. Clean: Removes previously compiled files (e.g., target/).
2. Validate: Validates the project’s structure and configuration.
3. Compile: Compiles the source code.
4. Test: Runs unit tests.
5. Package: Packages the compiled code into a JAR/WAR file.
6. Install: Installs the packaged JAR/WAR to your local Maven repository.
7. Deploy: Deploys the artifact to a remote repository (optional).

* ## explicit instructions
Ant is task-based, meaning you need to define each build step explicitly in its build.xml file. 
There is no predefined lifecycle or conventions—everything is controlled/defined explicitly by the user.
If you want Ant to compile your Java files, you have to tell it exactly what to do, like this:
	<target name="compile">
		<javac srcdir="src" destdir="bin" />
	</target>
You must also define the order of tasks manually, specifying what should happen first, second, etc. 
There are no default actions or life cycle phases like Maven. You have to manage the flow of tasks and ensure they happen in the right order.
This gives more control over the build process but requires more configuration work. 
You are responsible for specifying every detail of how the project is built.

* ## Lack of Built-in Dependency Management
Unlike Maven, Ant doesn't have built-in dependency management. 
If your project depends on external libraries (e.g., third-party JAR files), you need to manually download them and place them in your project’s directories.
There's no automatic way to pull dependencies from a central repository like Maven Central. 
If you want to manage dependencies in Ant, you typically have to use an additional tool like Apache Ivy to handle downloading and resolving dependencies, but this isn't built into Ant itself.

## Configuring Build Jobs in Jenkins
In Jenkins you can configure build job for any programming language by using the appropriate build tools and plugins, and by defining the build steps in a Jenkinsfile (a Groovy-based script) or through the Jenkins UI.
For instance to configure a build job for java you can use ant or maven build tool.
Generally the steps of building a job for java:
1. Configure Java and maven/ant
2. Build the job using the build tool configured

## Deploying in Jenkins
In Jenkins, you can deploy to virtually any environment, provided you configure the pipeline or job properly with the necessary tools and credentials.
Jenkins can integrate with various environments, such as cloud services(AWS Elastic BeanStalk, Azure App Services, Google Cloud), on-premise servers(Tomcat, nginx), containerized environments(Docker, Kubernetes), and more.

## Continuous Testing(CT)
Continuous Testing in software development refers to the practice of automatically and continuously testing the software at every stage of the development lifecycle, from integration to production.
It ensures quality and functionality at every stage and provides critical feedback to developers earlier so they can address any issues quickly and before they progress too far down the development pipeline. 
In continuous testing, you'll encounter various types of tests:

## 1. Functional Testing
Functional testing is a type of testing to check if core functionalities/features are working as expected according to its(functional) requirements.
Functional testing encompasses various types, including:
* **Unit Testing:** Tests individual units or components of a software system in isolation. Some of unit testing frameworks include junit and testNG (both are used for java applications)
* **Integration Testing:**  Verifies the interaction between different modules or components. 
* **System Testing:** Tests the entire system as a whole to ensure that it meets the specified requirements.
* **Acceptance Testing:** Verifies that the software meets the end-user's needs and expectations. Often done by the client or business stakeholders.
 
## 2. Performance Testing
Performance testing evaluates how a system performs in terms of responsiveness, speed, scalability, and stability under a particular workload.
Below are various types of performance testing:
* **Load Testing:** evaluates how the system behaves under normal or expected load(traffic/user activity) conditions.  The goal is to ensure that the system can handle the expected number of users or requests without degrading performance.
* **Stress Testing:**  Evaluates how the system behaves under extreme load conditions beyond the expected maximum capacity. It determines how the system recovers from failure.
* **Spike Testing:** Tests the system’s response to sudden, unexpected spikes in load (e.g., a sudden surge in users due to a viral event).
* **Scalability Testing:** evaluates how well the application can scale up or down to meet changing demands. 
* **Endurance/Soak Testing:** checks if the system can handle a normal load for an extended period of time without degrading performance.
* **Capacity Testing:** Determines the maximum load a system can handle. 

## 3. Regression Testing
Regression Testing ensures that new changes (e.g., bug fixes, new features) have not introduced any new issues or broken existing functionality in the application.
It involves re-running previously executed tests to ensure the software continues to function as expected after modifications. 
**Example:** After adding a new feature to a mobile app, regression testing would check that the existing features like login and profile update still work correctly.

## 4. UI(User Interface) Testing
UI Testing focuses on verifying the appearance, functionality, and usability of an application's interface(Can be GUI, CLI, VUI/voice user interface), ensuring it meets user requirements and functions correctly. 

## 5. Penetration Testing/Pen Test
A a pen test simulates cyber attacks to find vulnerabilities in a system/application before malicious actors can exploit them.


## Selenium
Selenium is an open-source suite of tools and libraries that is used for browser automation.
It allows testers and developers to write scripts to automatically perform actions on web applications, which is particularly useful in functional testing, regression testing, and user interface (UI) testing.
Selenium supports multiple programming languages like Java, Python, C#, Ruby, and JavaScript, enabling flexibility for different development environments.
Selenium does not come with built-in reporting features. You must integrate it with other tools like TestNG or JUnit for generating reports.

## Differences between JUnit and TestNG in Java
JUnit is primarily used for unit testing, while TestNG offers more flexibility and features, making it suitable for unit, integration and system testing, and also supports parallel testing and data-driven testing.

| Feature               | JUnit                                    | TestNG                                    |
|-----------------------|------------------------------------------|-------------------------------------------|
| **Primary Use Case**  | Unit Testing                             | Unit, Integration, and System Testing    |
| **Flexibility**       | Less flexible                           | More flexible                            |
| **Parallel Testing**  | Limited support                         | Supports parallel testing                |
| **Data-Driven Testing**| Limited support                        | Supports data-driven testing             |
| **Reporting**         | Basic reporting                          | Generates HTML reports by default        |
| **Ease of Use**       | Simple and easy to use                   | More complex but powerful                |

## Apache JMeter
Apache JMeter is a free and open-source software tool used for load testing and performance measurement of various software, including web applications, APIs, and databases. 
It allows you to simulate real-world user loads and identify performance bottlenecks. 


## Integrating testing in Jenkins
Jenkins allows you to automate the process of running tests as part of your build pipeline, ensuring that tests are run continuously whenever code changes are made or new builds are triggered.


## Upstream and Downstream job
An upstream job is a job that comes before the current job in the pipeline. It provides input or prerequisites for the downstream job.
A downstream job is a job that comes after the current job in the pipeline. It consumes the output or result of the upstream job.
eg. 
[Upstream] Build Job(for compiling or building code base) → [Downstream] Test Job(After build testing job runs) → [Downstream] Deploy Job (If tests pass deployment happens)

In this sequence:
* Build is an upstream job to both Test and Deploy jobs.
* Test is a downstream job of Build and an upstream job for Deploy.
* Deploy is a downstream job of both Build and Test.

## Domain Specific Language (DSL) and pipeline DSL
DSL refers to a programming or specification language that is designed and optimized or tailored for a specific set of tasks or a particular domain, rather than being a general-purpose programming language like Python, Java, or C++.
Examples of DSLs include SQL (for database queries), HTML (for web pages), and DSLs used in Jenkins for defining CI/CD pipelines. 

A pipeline DSL is a specialized DSL used to define and manage automated pipelines. 
It provides a way to script and automate the steps in a pipeline that are required for building, testing, and deploying software.
Examples of pipeline DSL include Jenkins Pipeline DSL, which uses Groovy syntax to define CI/CD pipelines. 
Other examples include YAML-based pipelines in tools like GitHub Actions and GitLab CI. 

## Some important jenkins terms
* **Scripted pipelines vs Declarative pipelines:** declarative pipelines are a newer, more structured approach for defining pipelines as code, using a simplified, human-readable syntax and a focus on clarity, while scripted pipelines are the older, more flexible approach based on Groovy scripting. 
**Example of Declarative Pipeline:**
	pipeline { //Wraps the entire pipeline configuration.
        agent any //Specifies the environment where the pipeline will run. any means it will run on any available agent.
		
        stages { //Contains a sequence of stage blocks.
            stage('Build') {  // represents a distinct part of the pipeline (e.g., Build, Test, Deploy).
                steps { // Defines the individual tasks within each stage (e.g., running shell commands like sh 'make build').
                    // Build steps
					sh 'make build'  // Run shell command
                }
            }
            stage('Test') {
                steps {
                    // Test steps
                }
            }
        }
		
		post { // Defines actions that run after the pipeline completes, such as success or failure notifications.
			success {
				echo 'Pipeline executed successfully!'
			}
			failure {
				echo 'Pipeline failed.'
			}
		}
    }
	
***Example of Scripted Pipeline:*
	node {//Defines the Jenkins agent (or node) where the pipeline will run.
	
		// Define environment variables
		def myVar = 'some value'

		try { // Provides error handling. If an error occurs in any of the stages, the pipeline will catch it, mark the build as failed, and ensure that post actions are run in the finally block.
			stage('Build') { // Defines a specific part of the pipeline, just like in the declarative pipeline.
				echo 'Building the application...'
				sh 'make build'  // Run shell command
			}

			stage('Test') {
				echo 'Running tests...'
				sh 'make test'  // Run shell command
			}

			stage('Deploy') {
				echo 'Deploying the application...'
				sh 'make deploy'  // Run shell command
			}

		} catch (Exception e) {
			currentBuild.result = 'FAILURE'
			throw e
		} finally {
			// Run post actions (like sending notifications)
			if (currentBuild.result == 'SUCCESS') {
				echo 'Pipeline executed successfully!'
			} else {
				echo 'Pipeline failed.'
			}
		}
	}


* **node:** A node in Jenkins refers to a machine(that is part of jenkins setup including the jenkins master and any agents) or an environment where the tasks in the pipeline will run. The following is the sample syntax:
	node{// execute the pipeline in master node} node('windows'){// execute the pipeline in node labelled as windows}

* **agent:** An agent is machine that connects to the Jenkins master and executes tasks, such as building software, running tests, or executing scripts. 
	pipeline {
		agent any  // This means any available agent will be used for execution.
	}
	
	pipeline {
		agent { label 'linux' }  // This will run the pipeline on any agent with the 'linux' label.
	}

* **Node vs Agent in Pipelines:** In Jenkins pipelines, the "agent" directive is used in declarative pipelines to specify where the pipeline or stage should run, while the "node" block is used in scripted pipelines or inside steps in a declarative pipeline to explicitly allocate a Jenkins executor (node) for executing the code within its block. 

* **stage: ** A stage in Jenkins defines a logical separate part/segment of the pipeline such as build, test or deploy.

* **Step/Build Step:** A step (or build step) refers to an individual task or action that is executed within a stage. These steps define what Jenkins should do at that point in the pipeline, such as running scripts, executing commands, or invoking other processes.

* **Promoted Builds:** In Jenkins, promoted builds are a way to mark a build as having reached a certain milestone or status in the CI/CD pipeline. This concept is useful for identifying builds that are considered stable or have passed specific quality criteria and are ready for further actions, such as deployment or release.

## Managing and Monitoring Jenkins

## Master-Agent Architecture
In a master-agent architecture, a central "master" component manages and coordinates the activities of multiple "agent" components, which execute tasks or perform specific functions, often in a distributed or networked environment. 
Examples of systems that use master-agent architecture: Jenkins, SNMP(Simple Network Management Protocol) and Multi-Agent systems in AI.

This architecture allows Jenkins to distribute workloads (build, test, deploy tasks) across multiple machines, improving scalability, resource utilization, and reliability.
The master node is responsible for managing the overall Jenkins environment, while the agent nodes handle the execution of actual tasks (like building code or running tests).

## Monitoring in Jenkins
The monitoring plugin provides monitoring for Jenkins with JavaMelody. 
It provides charts for CPU, memory, system load average, HTTP response time, and so on. 
It also provides details of HTTP sessions, errors and logs, actions for GC, heap dump, invalidate session(s), and so on.
You install the Monitoring plugin from the Jenkins dashboard.

## Backup and Restoring in Jenkins
The backup plugin allows us to take a backup of jenkins home and restore it.

## Managing disk usage in Jenkins
The disk usage plugin gives details on disk usage for the system where Jenkins is installed

## Auditing in Jenkins
The Audit Trail Plugin in Jenkins is used to track and record detailed logs of user activities and system events within Jenkins. 
This plugin is primarily aimed at auditing and monitoring changes made to Jenkins' configurations, jobs, builds, and user activities, ensuring accountability and traceability in Jenkins environments. 

## Workspace cleanup in Jenkins
The Workspace Cleanup plugin is used to delete the workspace from Jenkins before the build, or when a build is finished and artifacts saved.

## Conditional build in Jenkins
The Conditional Build Step plugin allows definition of conditions under which a particular build step is executed.

## Injecting environment variables in Jenkins
The EnvInject Plugin in Jenkins is a plugin that allows you to inject environment variables into your Jenkins builds, providing a way to set or modify environment variables during build execution. 


## What is SCM checkout in Jenkins
In Jenkins, scm checkout refers to the action of checking out (i.e., retrieving) the source code from a version control system (VCS) such as Git, Subversion, or Mercurial. 






















