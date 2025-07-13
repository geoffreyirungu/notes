# Temporal
**Definitions**
* Temporal is a scalable and reliable runtime for durable function executions called Temporal Workflow Executions.
* Said another way, it's a platform that guarantees the Durable Execution of your application code.
* Temporal refers to a durable execution platform that allows developers to build reliable, scalable, and resilient applications.
* Temporal is a durable execution system that lets you write workflows (business logic) as code in your preferred programming language, and it ensures they complete successfully, even if components fail, restart, or crash.
* Temporal is a powerful open-source microservices orchestration platform designed to manage long-running, stateful, and reliable workflows.

It provides a framework for handling complex, long-running processes, especially those that might be prone to failures, by ensuring that they execute reliably to completion.
Your application will run reliably even if it encounters problems, such as network outages or server crashes, which would be catastrophic for a typical application. 
The Temporal Platform handles these types of problems, allowing you to focus on the business logic, instead of writing application code to detect and recover from failures.

## What is Temporal Platform
The Temporal Platform consists of a **Temporal Service** and **Worker Processes**. Together these components create a runtime for Workflow Executions.
A Temporal Service consists of the Temporal Server, written in Go, and a database.
Temporal Cloud, offers an alternative to hosting the Temporal Service yourself.


## Core concepts of temporal platform
**Durable Execution**
**Durable execution** refers to a system's ability to reliably persist and resume application execution, even after interruptions or failures.
This means that if a process is interrupted due to a system crash, network issues, or other disruptions, it can automatically resume from where it left off, without losing any previously completed work.
Durable execution in temporal is achieved through Temporal's use of an **Event History**, which records the state of a Workflow Execution at each step.
If a failure occurs, the Workflow Execution can resume from the last recorded event, ensuring that progress isn't lost.
This durability is a key feature of Temporal Workflow Executions, making them reliable and resilient.
It enables application code to execute effectively once and to completion, regardless of whether it takes seconds or years.
**Workflow**
A workflow defines the overall logic and control flow of a process that Temporal executes reliably and durably.
You write workflows in code (e.g., Go, Java, TypeScript).
It automatically resumes from the last step after crashes, redeployments, or restarts.
**Activities**
Activities are the individual, well-defined tasks/operations that a Workflow executes.
Activities are where you execute any operation that is prone to failure or access external services or systems, such as API requests, sending emails or database calls. 
Complex Temporal Applications have Workflows that invoke many Activities, using the results of one Activity to execute another.
If they fail, Temporal retries them with configurable policies.
**Client**
A client is the part of your application/code responsible for starting workflows, querying them, and sending signals to them — but not executing them. 
That execution is handled by workers.
**Workers**
A worker is a process (often a standalone service) that polls the Temporal server for tasks and execute the code for workflows and activities.
Each worker is configured with a Task Queue, which connects it to the Temporal service.
A worker is responsible for:
* polling task queues: Workers constantly listen to specific task queues for new tasks. 
* dequeuing tasks
* executing the code associated with those tasks: When a worker picks up a task, it executes the corresponding code, which can be Workflow code or Activity code. 
* reporting the results back to the Temporal service: After executing a task, the worker sends the results (or any errors) back to the Temporal service. 
Other notable features of workers:
* Deterministic Execution: Temporal workers ensure that workflow executions are deterministic, allowing them to be replayed on different machines if necessary. 
* Concurrency Control: Workers manage the concurrency of activity executions and workflow tasks. 
* Workflow Execution Cache: Workers can cache workflow executions for performance improvements. 

In essence, workers are the bridge between your code and the Temporal service, enabling the execution of your workflows and activities. 
**Task Queues**
A Task Queue is a lightweight, dynamically allocated queue that Temporal Workers poll to find work to do.
Workers, which are processes that execute your code, listen to Task Queues to find work.
The Temporal service routes different types of tasks (Workflow Tasks, Activity Tasks, and Nexus Tasks) to the appropriate Workers based on the Task Queue they are associated with. 
**Types of Task Queues:**
Temporal provides different types of Task Queues for different types of tasks:
* Workflow Task Queues: Used for routing Workflow Tasks to Workers. 
* Activity Task Queues: Used for routing Activity Tasks to Workers. 
* Nexus Task Queues: Used for routing Nexus Tasks to Workers. 

**Task queue performance tuning:** By analyzing Task Queue performance data (available through the Temporal service), you can determine the optimal number of Workers to deploy for a given Task Queue to avoid bottlenecks and ensure efficient task processing. 
**Task queue naming Best Practices:** When creating Task Queues, it's recommended to use descriptive names that are easy to understand and remember, such as `greeting-tasks` instead of `gtq`. 
**Task queue worker capability configuration:** You can configure Workers to listen to specific Task Queues based on the type of work they can handle.
For example, some Workers might be configured to run on GPU-enabled machines and handle tasks that require GPU processing, while others might be configured to run on non-GPU machines and handle other types of tasks. 
**Timers and Delays**
Temporal has built-in support for sleep, retries with delays, timeouts, and scheduled tasks — all durably recorded.
**Temporal Server**
The core component that manages Workflow Executions and ensures their durability and scalability. 
**Temporal SDKs**
Libraries that provide the tools and APIs for developers to interact with the Temporal server and build their applications. 

## What is a Temporal Application
A Temporal Application is a set of Temporal Workflow Executions. 
Each Temporal Workflow Execution has exclusive access to its local state, executes concurrently to all other Workflow Executions, and communicates with other Workflow Executions and the environment via message passing.

A Temporal Application can consist of millions to billions of Workflow Executions.
Workflow Executions are lightweight A Workflow Execution consumes few compute resources; in fact, if a Workflow Execution is suspended, such as when it is in a waiting state, the Workflow Execution consumes no compute resources at all.
**Reentrant Process:** A Temporal Workflow Execution is a Reentrant Process. 
A Reentrant Process is resumable, recoverable, and reactive.
* Resumable: Ability of a process to continue execution after execution was suspended on an awaitable.
* Recoverable: Ability of a process to continue execution after execution was suspended on a failure.
* Reactive: Ability of a process to react to external events.
Therefore, a Temporal Workflow Execution executes a Temporal Workflow Definition, (also called a Temporal Workflow Function, your application code), exactly once and to completion—whether your code executes for seconds or years, in the presence of arbitrary load and arbitrary failures.

## Terms Definitions
**Scalability**
Scalability is a system's ability to handle increasing workloads or growth, whether it's more users, more data, or more complex tasks, without a significant drop in performance.  
**Fault Tolerance**
Fault tolerance is a system's ability to continue operating correctly even when some of its components fail.
**Entry point**
An entry point is the specific location within a program where execution begins. 
**Idempotency**
Idempotency refers to an operation that can be applied multiple times without changing the result beyond the initial application.
**Back off**
Backoff refers to a deliberate delay or waiting period before retrying an operation, typically after a failure. 
It's a strategy used to reduce system load, avoid repeated failures, and give resources time to recover.
**Race conditions**
A race condition occurs when two or more threads or processes access shared data concurrently, 
and the final outcome depends on the timing or sequence of their execution. 
If proper synchronization is not used, this can lead to inconsistent or incorrect results.
**Remote Procedure Call(RPC)**
RPC is a communication protocol that allows a program on one computer(client) to execute a procedure(function or a block of code) on another computer(server) as if it were a local procedure.
RPC abstracts/hides away the complexities of network programming/communication.
In simpler terms:
> With RPC, you can call a function on another machine just like calling a local function.
**How RPC works**
* Client Stub: The client code doesn't call the remote procedure directly; it calls a "stub" (a local proxy) function that looks like the remote procedure.
* Marshalling: The client stub packs (serializes) the procedure name and arguments into a message.
* Transport: The message is sent over the network to the server.
* Server Stub: The server receives the message, unpacks it (unmarshalling), and calls the actual server-side function.
* Execution: The server executes the function and produces a result.
* Return: The result is marshalled and sent back to the client.
* Response Handling: The client stub receives the result, unmarshals it, and presents it to the client program.
**RPC Illustration**

Client Program                           Server Program
  |                                            |
  | --- call Add(5, 3) -------------------->   |
  |        (via client stub)                  |
  |                                            |
  |   ----> [Network Message: Add(5, 3)]       |
  |                                            |
  |                            ---> Receive RPC Request
  |                            ---> Unmarshal
  |                            ---> Call Add(5, 3)
  |                            <--- Result: 8
  |                                            |
  |   <---- [Network Message: 8]               |
  |                                            |
  | <-- Return 8 to client via stub            |

**Key Features of RPC:**
* Transparency: Makes remote calls look like local ones.
* Language Independence: Modern RPC frameworks (like gRPC) support many languages.
* Abstraction: Abstracts underlying communication (TCP/HTTP).
* Decoupling: Client and server can evolve independently.
**RPC is commonly used in:** 
* distributed systems
* microservices
* and client-server architectures 
where different parts of an application may reside on separate machines. 

Some common RPC frameworks include gRPC and Apache Thrift
**Real-World Example Use Cases of RPC:**
* Temporal uses gRPC internally for client-server communication.
* Google Cloud, Netflix, and Square use it for microservice communication.
* Mobile apps use gRPC for efficient backend communication (especially with gRPC-Web for browsers).



## Importance of Temporal Platform
**1. Fault Tolerance and Reliability**
Temporal's durability and fault tolerance make applications more reliable and resilient to failures.
**2. Scalability**
Temporal is designed to handle a large number of concurrent Workflow Executions, making it suitable for scalable applications. 
**3.Strong Observability & Debuggability**
* Full execution history is stored — you can replay or inspect past executions.
* Makes debugging and auditing extremely easy.
**4. Stateful Long-Running Workflows**
* Perfect for processes that span minutes, hours, or days (e.g., onboarding, payment settlements, batch jobs).
* Maintains workflow state without relying on external systems or polling.
**5. Simplified Distributed Systems and Reduced Development Time**
* Writing robust distributed code is hard — Temporal hides the complexity (retries, timeouts, parallelism).
* No need for brittle cron jobs, polling loops, or orchestration engines.
* This simplifies development and reduces the time it takes to build and deploy applications. 
**6. Language-Native Workflows**
* You write workflows in your language (Go, Java, TypeScript, PHP, Python).
* No need for YAML, JSON configs, or DSLs.
**7. Time-Aware Logic**
Built-in support for:
* Timeouts
* Retries with backoff
* Delays and timers
* Scheduled tasks (e.g., run in 7 days)

**Real-World Temporal Use Cases**
| Industry       | Use Case Example                                        |
| -------------- | ------------------------------------------------------- |
| **E-commerce** | Order processing, shipping, returns, refunds            |
| **Finance**    | Payment workflows, fraud detection, transaction retries |
| **Healthcare** | Appointment scheduling, patient onboarding              |
| **SaaS**       | User onboarding, subscription renewals, reminders       |
| **DevOps**     | CI/CD pipelines, infrastructure automation              |

**Comparisons to Other Tools**
| Tool/Platform       | Key Difference from Temporal                                                     |
| ------------------- | -------------------------------------------------------------------------------- |
| AWS Step Functions  | Temporal is language-native; Step Functions uses JSON & AWS-only                 |
| Apache Airflow      | Airflow is for batch ETL; Temporal is for stateful, fault-tolerant app workflows |
| Celery (Python)     | Celery handles background tasks; Temporal handles workflows + retries + state    |
| Kubernetes CronJobs | No built-in retry, state, or error handling                                      |

**Challenges Temporal Solves**
* No need to write your own retry logic
* No more losing state across process restarts
* No need for external databases to persist workflow state
* No brittle cron jobs or polling scripts
* Handles idempotency, timeouts, and task orchestration cleanly

**Summary: Why Temporal Matters**
| Feature                      | Value Provided                                   |
| ---------------------------- | ------------------------------------------------ |
| **Durable execution**        | Automatically resumes after failure              |
| **Workflow as code**         | Write workflows in real languages, no DSL needed |
| **Time-aware orchestration** | Built-in timers, delays, retries, timeouts       |
| **Scalable & Reliable**      | Runs at scale across distributed systems         |
| **Auditability**             | Full visibility and history for every workflow   |

## Setting up a local development environment for Temporal and Java
1. Install Java JDK
2. Add Temporal Java SDK Dependencies
Add the following dependencies to your Maven Project Object Model (POM) configuration file (pom.xml) to compile, build, test, and run a Temporal Application in Java.

  <dependencies>
    <!--
      Temporal dependencies needed to compile, build,
      test, and run Temporal's Java SDK
    -->

    <!--
      SDK
    -->
    <dependency>
      <groupId>io.temporal</groupId>
      <artifactId>temporal-sdk</artifactId>
      <version>1.24.1</version>
    </dependency>

    <dependency>
      <!--
        Testing
      -->
      <groupId>io.temporal</groupId>
      <artifactId>temporal-testing</artifactId>
      <version>1.24.1</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
3. Set up a local Temporal Service for development with Temporal CLI 
Temporal CLI is a tool for interacting with the Temporal Service from the command-line interface. 
It includes a self-contained distribution of the Temporal Service and Web UI as well which you can use for local development.
Install Temporal CLI on your local machine for your platform.

Once you've installed Temporal CLI and added it to your PATH, open a new Terminal window and run the following command:
	temporal server start-dev
This command starts a local Temporal Service. It starts the Web UI, creates the default Namespace, and uses an in-memory database.
* The Temporal Service will be available on localhost:7233.
* The Temporal Web UI will be available at http://localhost:8233.
You can stop the Temporal Service at any time by pressing CTRL+C.

To change the port for the Web UI, use the --ui-port option when starting the server:
	temporal server start-dev --ui-port 8080
The Temporal Web UI will now be available at http://localhost:8080.

The temporal server start-dev command uses an in-memory database, so stopping the server will erase all your Workflows and all your Task Queues. 
If you want to retain those between runs, start the server and specify a database filename using the --db-filename option, like this:
	temporal server start-dev --db-filename your_temporal.db
When you stop and restart the Temporal Service and specify the same filename again, your Workflows and other information will be available.

## Run your first Temporal application with the Java SDK
**Note:** None of your application code runs on the Temporal Server. Your Worker, Workflow, and Activity run on your infrastructure, along with the rest of your applications.
The following code examples come from git repo https://github.com/temporalio/money-transfer-project-java

**Workflow definition**
In the Temporal Java SDK, a Workflow Definition is marked by the `@WorkflowInterface` attribute placed above the class interface.
`@WorkflowMethod` is used to mark a method within that interface as the entry point for a workflow execution.
 
Example of Workflow Definition interface
	package moneytransferapp;

	import io.temporal.workflow.WorkflowInterface;
	import io.temporal.workflow.WorkflowMethod;

	@WorkflowInterface
	public interface MoneyTransferWorkflow {
		// The Workflow Execution that starts this method can be initiated from code or
		// from the 'temporal' CLI utility.
		@WorkflowMethod
		void transfer(TransactionDetails transaction);
	}

`TransactionDetails` class:
	package moneytransferapp;
	import com.fasterxml.jackson.databind.annotation.JsonDeserialize;

	@JsonDeserialize(as = CoreTransactionDetails.class)
	public interface TransactionDetails {
		String getSourceAccountId();
		String getDestinationAccountId();
		String getTransactionReferenceId();
		int getAmountToTransfer();
	}
	
> **Tip: ** It's a good practice to send a single object into a Workflow as its input, rather than multiple, separate arguments. 
> As your Workflows evolve, you may need to add information, and using a single argument will make it easier for you to change long-running Workflows in the future.

**Activity Definition**
In Temporal `@ActivityInterface` marks an interface as defining a set of activities.
`@ActivityMethod` marks individual methods within that interface as specific activities. 
Example of Activity interface:
	// ...
	import io.temporal.activity.ActivityInterface;
	import io.temporal.activity.ActivityMethod;

	@ActivityInterface
	public interface AccountActivity {
		// Withdraw an amount of money from the source account
		@ActivityMethod
		void withdraw(String accountId, String referenceId, int amount);

		// Deposit an amount of money into the destination account
		@ActivityMethod
		void deposit(String accountId, String referenceId, int amount);

		// Compensate a failed deposit by refunding to the original account
		@ActivityMethod
		void refund(String accountId, String referenceId, int amount);
	}

**Activity implementation**
	// ...
	import io.temporal.activity.*;

	public class AccountActivityImpl implements AccountActivity {
		// Mock up the withdrawal of an amount of money from the source account
		@Override
		public void withdraw(String accountId, String referenceId, int amount) {
			System.out.printf("\nWithdrawing $%d from account %s.\n[ReferenceId: %s]\n", amount, accountId, referenceId);
			System.out.flush();
		}

		// Mock up the deposit of an amount of money from the destination account
		@Override
		public void deposit(String accountId, String referenceId, int amount) {
			boolean activityShouldSucceed = true;

			if (!activityShouldSucceed) {
				System.out.println("Deposit failed");
				System.out.flush();
				throw Activity.wrap(new RuntimeException("Simulated Activity error during deposit of funds"));
			}

			System.out.printf("\nDepositing $%d into account %s.\n[ReferenceId: %s]\n", amount, accountId, referenceId);
			System.out.flush();
		}

		// Mock up a compensation refund to the source account
		@Override
		public void refund(String accountId, String referenceId, int amount) {
			boolean activityShouldSucceed = true;

			if (!activityShouldSucceed) {
				System.out.println("Refund failed");
				System.out.flush();
				throw Activity.wrap(new RuntimeException("Simulated Activity error during refund to source account"));
			}

			System.out.printf("\nRefunding $%d to account %s.\n[ReferenceId: %s]\n", amount, accountId, referenceId);
			System.out.flush();
	   }
	}

> **Why you use Activities**
> At first glance, you might think you can incorporate your logic into the Workflow Definition. 
> However, Temporal Workflows have certain deterministic constraints and must produce the same output each time, given the same input. 
> This means that any non-deterministic work such as interacting with the outside world, like accessing files or network resources, must be done by Activities.

> In addition, by using Activities, you can take advantage of Temporal's ability to retry Activities indefinitely.
> Use Activities for your business logic, and use Workflows to coordinate the Activities.

**Set the Retry Policy**
If an Activity fails, Temporal Workflows automatically retry the failed Activity by default. 
You can also customize how those retries happen through the Retry Policy.
By default, Temporal retries failed Activities forever, but you can specify some errors that Temporal should not attempt to retry.
Example of a retry policy:

	// ...
    private static final String WITHDRAW = "Withdraw";

    // RetryOptions specify how to automatically handle retries when Activities fail
    private final RetryOptions retryoptions = RetryOptions.newBuilder()
        .setInitialInterval(Duration.ofSeconds(1)) // Wait 1 second before first retry
        .setMaximumInterval(Duration.ofSeconds(20)) // Do not exceed 20 seconds between retries, even if the backoff keeps increasing
        .setBackoffCoefficient(2) // Wait 1 second, then 2, then 4, etc
        .setMaximumAttempts(5000) // Fail after 5000 attempts
        .build();
		
| Option               | Meaning                               |
| -------------------- | ------------------------------------- |
| `initialInterval`    | Time before first retry               |
| `maximumInterval`    | Max delay between retries             |
| `backoffCoefficient` | Factor by which retry delay increases |
| `maximumAttempts`    | Max total attempts before giving up   |

**Set the Activity Options Policy/settings**		
	// ActivityOptions specify the limits on how long an Activity can execute before
	// being interrupted by the Orchestration service
	private final ActivityOptions defaultActivityOptions = ActivityOptions.newBuilder()
		.setRetryOptions(retryoptions) // Apply the RetryOptions defined above
		.setStartToCloseTimeout(Duration.ofSeconds(2)) // Max execution time for single Activity
		.setScheduleToCloseTimeout(Duration.ofSeconds(5000)) // Entire duration from scheduling to completion including queue time
		.build();

| Timeout                  | Meaning                                                                |
| ------------------------ | ---------------------------------------------------------------------- |
| `ScheduleToStartTimeout` | Max wait time in **queue** before a worker picks up the activity       |
| `StartToCloseTimeout`    | Max time the activity is allowed to **run once it starts**             |
| `ScheduleToCloseTimeout` | Total wall-clock time from **scheduling** to **final completion**      |
| `HeartbeatTimeout`       | Max time allowed **between heartbeats** to prove the activity is alive |

Of all the Temporal timeout options, startToCloseTimeOut is the one you should always set.

**You can set per-activity method options**
Per-activity method options allows you to specify custom `ActivityOptions` per activity method name.
In the example below custom `ActivityOptions` is defined just for the "Withdraw" activity method.

	private static final String WITHDRAW = "Withdraw";

	private final Map<String, ActivityOptions> perActivityMethodOptions = new HashMap<String, ActivityOptions>() {{
		// A heartbeat time-out is a proof-of-life indicator that an activity is still working.
		// The 5 second duration used here waits for up to 5 seconds to hear a heartbeat.
		// If one is not heard, the Activity fails.
		// The `withdraw` method is hard-coded to succeed, so this never happens.
		// Use heartbeats for long-lived event-driven applications.
		put(WITHDRAW, ActivityOptions.newBuilder().setHeartbeatTimeout(Duration.ofSeconds(5)).build());
	}};

Why Use `perActivityMethodOptions`?
In most cases, your workflow uses a single ActivityOptions object for all activities. But sometimes:
* You have different types of activities that need different timeouts, retry rules, or heartbeat settings.
* You want fine-grained control per method rather than globally.

**Workflow Definition implementation**
	package moneytransferapp;

	import io.temporal.activity.ActivityOptions;
	import io.temporal.workflow.Workflow;
	import io.temporal.common.RetryOptions;

	import java.time.Duration;
	import java.util.HashMap;
	import java.util.Map;

	public class MoneyTransferWorkflowImpl implements MoneyTransferWorkflow {
		private static final String WITHDRAW = "Withdraw";

		// RetryOptions specify how to automatically handle retries when Activities fail
		private final RetryOptions retryoptions = RetryOptions.newBuilder()
			.setInitialInterval(Duration.ofSeconds(1)) // Wait 1 second before first retry
			.setMaximumInterval(Duration.ofSeconds(20)) // Do not exceed 20 seconds between retries, even if the backoff keeps increasing
			.setBackoffCoefficient(2) // Wait 1 second, then 2, then 4, etc
			.setMaximumAttempts(5000) // Fail after 5000 attempts
			.build();

		// ActivityOptions specify the limits on how long an Activity can execute before
		// being interrupted by the Orchestration service
		private final ActivityOptions defaultActivityOptions = ActivityOptions.newBuilder()
			.setRetryOptions(retryoptions) // Apply the RetryOptions defined above
			.setStartToCloseTimeout(Duration.ofSeconds(2)) // Max execution time for single Activity
			.setScheduleToCloseTimeout(Duration.ofSeconds(5000)) // Entire duration from scheduling to completion including queue time
			.build();

		private final Map<String, ActivityOptions> perActivityMethodOptions = new HashMap<String, ActivityOptions>() {{
			// A heartbeat time-out is a proof-of life indicator that an activity is still working.
			// The 5 second duration used here waits for up to 5 seconds to hear a heartbeat.
			// If one is not heard, the Activity fails.
			// The `withdraw` method is hard-coded to succeed, so this never happens.
			// Use heartbeats for long-lived event-driven applications.
			put(WITHDRAW, ActivityOptions.newBuilder().setHeartbeatTimeout(Duration.ofSeconds(5)).build());
		}};

		// ActivityStubs enable calls to methods as if the Activity object is local but actually perform an RPC invocation
		private final AccountActivity accountActivityStub = Workflow.newActivityStub(AccountActivity.class, defaultActivityOptions, perActivityMethodOptions);

		// The transfer method is the entry point to the Workflow
		// Activity method executions can be orchestrated here or from within other Activity methods
		@Override
		public void transfer(TransactionDetails transaction) {
			// Retrieve transaction information from the `transaction` instance
			String sourceAccountId = transaction.getSourceAccountId();
			String destinationAccountId = transaction.getDestinationAccountId();
			String transactionReferenceId = transaction.getTransactionReferenceId();
			int amountToTransfer = transaction.getAmountToTransfer();

			// Stage 1: Withdraw funds from source
			try {
				// Launch `withdrawal` Activity
				accountActivityStub.withdraw(sourceAccountId, transactionReferenceId, amountToTransfer);
			} catch (Exception e) {
				// If the withdrawal fails, for any exception, it's caught here
				System.out.printf("[%s] Withdrawal of $%d from account %s failed", transactionReferenceId, amountToTransfer, sourceAccountId);
				System.out.flush();

				// Transaction ends here
				return;
			}

			// Stage 2: Deposit funds to destination
			try {
				// Perform `deposit` Activity
				accountActivityStub.deposit(destinationAccountId, transactionReferenceId, amountToTransfer);

				// The `deposit` was successful
				System.out.printf("[%s] Transaction succeeded.\n", transactionReferenceId);
				System.out.flush();

				//  Transaction ends here
				return;
			} catch (Exception e) {
				// If the deposit fails, for any exception, it's caught here
				System.out.printf("[%s] Deposit of $%d to account %s failed.\n", transactionReferenceId, amountToTransfer, destinationAccountId);
				System.out.flush();
			}

			// Continue by compensating with a refund

			try {
				// Perform `refund` Activity
				System.out.printf("[%s] Refunding $%d to account %s.\n", transactionReferenceId, amountToTransfer, sourceAccountId);
				System.out.flush();

				accountActivityStub.refund(sourceAccountId, transactionReferenceId, amountToTransfer);

				// Recovery successful. Transaction ends here
				System.out.printf("[%s] Refund to originating account was successful.\n", transactionReferenceId);
				System.out.printf("[%s] Transaction is complete. No transfer made.\n", transactionReferenceId);
				return;
			} catch (Exception e) {
				// A recovery mechanism can fail too. Handle any exception here
				System.out.printf("[%s] Deposit of $%d to account %s failed. Did not compensate withdrawal.\n",
					transactionReferenceId, amountToTransfer, destinationAccountId);
				System.out.printf("[%s] Workflow failed.", transactionReferenceId);
				System.out.flush();

				// Rethrowing the exception causes a Workflow Task failure
				throw(e);
			}
		}
	}

> **Notice** that `Workflow.newActivityStub()` uses an interface of `AccountActivity` to create the activity stub, not the Activity implementation. 
> The workflow communicates with an Activity through its public interface and is not aware of its implementation.

**Start the Workflow**
To start the Workflow, run this Maven command:
	mvn compile exec:java \
		-Dexec.mainClass="moneytransferapp.TransferApp" \
		-Dorg.slf4j.simpleLogger.defaultLogLevel=warn

This command runs the `TransferApp.java` file within the project, starting the Workflow process.

To start a Workflow, you connect to the Temporal Cluster, specify the Task Queue, the Workflow should use, and Activities it expects in your code. 
In this tutorial, this is a small command-line program that starts the Workflow Execution.
In a real application, you may invoke this code when someone submits a form, presses a button, or visits a certain URL.

The Task Queue is where Temporal Workers look for Workflows and Activities to execute. You define Task Queues by assigning a name as a string. 
You'll use this Task Queue name when you start a Workflow Execution, and you'll use it again when you define your Workers.

src/main/java/moneytransfer/Shared.java

	package moneytransferapp;

	public interface Shared {
		static final String MONEY_TRANSFER_TASK_QUEUE = "MONEY_TRANSFER_TASK_QUEUE";
	}


	// @@@SNIPSTART money-transfer-java-initiate-transfer
	package moneytransferapp;

	import io.temporal.api.common.v1.WorkflowExecution;
	import io.temporal.client.WorkflowClient;
	import io.temporal.client.WorkflowOptions;
	import io.temporal.serviceclient.WorkflowServiceStubs;

	import java.security.SecureRandom;
	import java.time.Instant;
	import java.util.UUID;
	import java.util.Random;
	import java.util.stream.Collectors;
	import java.util.stream.IntStream;
	import java.util.concurrent.ThreadLocalRandom;

	public class TransferApp {
		private static final SecureRandom random;

		static {
			// Seed the random number generator with nano date
			random = new SecureRandom();
			random.setSeed(Instant.now().getNano());
		}

		public static String randomAccountIdentifier() {
			return IntStream.range(0, 9)
					.mapToObj(i -> String.valueOf(random.nextInt(10)))
					.collect(Collectors.joining());
		}

		public static void main(String[] args) throws Exception {

			// In the Java SDK, a stub represents an element that participates in
			// Temporal orchestration and communicates using gRPC.

			// A WorkflowServiceStubs communicates with the Temporal front-end service.
			WorkflowServiceStubs serviceStub = WorkflowServiceStubs.newLocalServiceStubs();

			// A WorkflowClient wraps the stub.
			// It can be used to start, signal, query, cancel, and terminate Workflows.
			WorkflowClient client = WorkflowClient.newInstance(serviceStub);

			// Workflow options configure  Workflow stubs.
			// A WorkflowId prevents duplicate instances, which are removed.
			WorkflowOptions options = WorkflowOptions.newBuilder()
					.setTaskQueue(Shared.MONEY_TRANSFER_TASK_QUEUE)
					.setWorkflowId("money-transfer-workflow")
					.build();

			// WorkflowStubs enable calls to methods as if the Workflow object is local
			// but actually perform a gRPC call to the Temporal Service.
			MoneyTransferWorkflow workflow = client.newWorkflowStub(MoneyTransferWorkflow.class, options);
			
			// Configure the details for this money transfer request
			String referenceId = UUID.randomUUID().toString().substring(0, 18);
			String fromAccount = randomAccountIdentifier();
			String toAccount = randomAccountIdentifier();
			int amountToTransfer = ThreadLocalRandom.current().nextInt(15, 75);
			TransactionDetails transaction = new CoreTransactionDetails(fromAccount, toAccount, referenceId, amountToTransfer);

			// Perform asynchronous execution.
			// This process exits after making this call and printing details.
			WorkflowExecution we = WorkflowClient.start(workflow::transfer, transaction);

			System.out.printf("\nMONEY TRANSFER PROJECT\n\n");
			System.out.printf("Initiating transfer of $%d from [Account %s] to [Account %s].\n\n",
							  amountToTransfer, fromAccount, toAccount);
			System.out.printf("[WorkflowID: %s]\n[RunID: %s]\n[Transaction Reference: %s]\n\n", we.getWorkflowId(), we.getRunId(), referenceId);
			System.exit(0);
		}
	}
	// @@@SNIPEND
	
> **Notice** that an interface of MoneyTransferWorkflow is used to create the Workflow stub, not the Workflow implementation.
> The workflow communicates with a Workflow through its public interface and is not aware of its implementation.

> **Note: ** There are two ways of starting a workflow 
* `WorkflowClient.start(...) approach`
	WorkflowClient.start(workflow::transfer, transaction);
	
	* This starts the workflow asynchronously.
	* It does not block waiting for the result.
	* The method (e.g., transfer) is passed as a lambda.
	* Useful when:
		* You want to start and return immediately.
		* You're calling from an HTTP endpoint and don't want to block.
		* You might signal later, or track the result asynchronously.
* Direct stub invocation: workflow.method(...)
	String greeting = workflow.getGreeting("World");
	
	* This starts the workflow and waits synchronously(blocks) for it to complete.
	* The method on the stub is invoked just like a regular method call.
	* This is equivalent to calling WorkflowClient.start(...) and then WorkflowStub.getResult(...) under the hood.

> **Specify a Workflow ID**
> A Workflow Id is unique in a namespace and is used for deduplication. 
> Using an identifier that reflects some business process or entity is a good practice. 
> For example, you might use a customer identifier as part of the Workflow Id if you run one Workflow per customer. 
> This would make it easier to find all of the Workflow Executions related to that customer later.

> **TIP** By default, the client connects to the `default` namespace of the Temporal Service running at `localhost` on port `7233` by using the `newLocalServiceStubs()` method. 
> If you want to connect to an external Temporal Service you would use the following code:

	WorkflowServiceStubs service =
			WorkflowServiceStubs.newServiceStubs(
				WorkflowServiceStubsOptions.newBuilder().setTarget("host:port").build());

	WorkflowClient client = 
			WorkflowClient.newInstance(
			  service, WorkflowClientOptions.newBuilder().setNamespace("YOUR_NAMESPACE").build());

> **Note:** This tutorial uses a separate program to start the Workflow, but you don't have to follow this pattern. 
> In fact, most real applications start a Workflow as part of another program. 
> For example, you might start the Workflow in response to a button press or an API call.
**Example: Real Use Case**

	@PostMapping("/transfer")
	public ResponseEntity<?> initiateTransfer(@RequestBody TransferRequest request) {
		MoneyTransferWorkflow workflow = workflowClient.newWorkflowStub(MoneyTransferWorkflow.class, options);
		WorkflowClient.start(workflow::transfer, request.toTransaction());
		return ResponseEntity.ok("Transfer started");
	}
This REST controller initiates a transfer.

**View the state of the Workflow with the Temporal Web UI**
Temporal records every execution, its progress, and application state through Temporal's Web UI. 
This provides insights into errors and app performance.

Temporal's Web UI lets you see details about the Workflow you're running. 
You can use this tool to see the results of Activities and Workflows, and also identify problems with your Workflow Execution.

1. Visit the Temporal Web UI where you will see your Workflow listed.
2. Click the Workflow ID for your Workflow.
Now you can see everything you want to know about the execution of the Workflow, including the input values it received, timeout configurations, scheduled retries, number of attempts, stack traceable errors, and more.
3. You can see the inputs and results of the Workflow Execution by clicking the Input and Results section
You started the Workflow, and the interface shows that the Workflow is running, but the Workflow hasn't executed yet. 
As you see from the Web UI, there are no Workers connected to the Task Queue.

You need at least one Worker running to execute your Workflows. You'll start the Worker next.
**Start a Worker**
A Worker is responsible for executing pieces of Workflow and Activity code. 
In this project, the MoneyTransferWorker type contains the code for the Worker within the MoneyTransferWorker project.
Run the following command to start the Worker:
	mvn compile exec:java \
		-Dexec.mainClass="moneytransferapp.MoneyTransferWorker" \
		-Dorg.slf4j.simpleLogger.defaultLogLevel=warn

In production environments, Temporal applications often operate with hundreds or thousands of Workers. 
This is because adding more Workers not only enhances your application's availability but also boosts its scalability.

One thing that people new to Temporal may find surprising is that the Temporal Cluster does not execute your code. 
The entity responsible for executing your code is known as a Worker, and it's common to run Workers on multiple servers.

A Worker:
* Can only execute Workflows and Activities registered to it.
* Knows which piece of code to execute based on the Tasks it gets from the Task Queue.
* Only listens to the Task Queue that it's registered to.

After the Worker executes code, it returns the results back to the Temporal Server. 
Note that the Worker listens to the same Task Queue you used when you started the Workflow Execution.

Like the program that started the Workflow, it connects to the Temporal Cluster and specifies the Task Queue to use. 
It also registers the Workflow and the three Activities:

src/main/java/moneytransfer/MoneyTransferWorker.java

	package moneytransferapp;

	import io.temporal.client.WorkflowClient;
	import io.temporal.serviceclient.WorkflowServiceStubs;
	import io.temporal.worker.Worker;
	import io.temporal.worker.WorkerFactory;

	public class MoneyTransferWorker {

		public static void main(String[] args) {
			// Create a stub that accesses a Temporal Service on the local development machine
			WorkflowServiceStubs serviceStub = WorkflowServiceStubs.newLocalServiceStubs();

			// The Worker uses the Client to communicate with the Temporal Service
			WorkflowClient client = WorkflowClient.newInstance(serviceStub);

			// A WorkerFactory creates Workers
			WorkerFactory factory = WorkerFactory.newInstance(client);

			// A Worker listens to one Task Queue.
			// This Worker processes both Workflows and Activities
			Worker worker = factory.newWorker(Shared.MONEY_TRANSFER_TASK_QUEUE);

			// Register a Workflow implementation with this Worker
			// The implementation must be known at runtime to dispatch Workflow tasks
			// Workflows are stateful so a type is needed to create instances.
			worker.registerWorkflowImplementationTypes(MoneyTransferWorkflowImpl.class);

			// Register Activity implementation(s) with this Worker.
			// The implementation must be known at runtime to dispatch Activity tasks
			// Activities are stateless and thread safe so a shared instance is used.
			worker.registerActivitiesImplementations(new AccountActivityImpl());

			System.out.println("Worker is running and actively polling the Task Queue.");
			System.out.println("To quit, use ^C to interrupt.");

			// Start all registered Workers. The Workers will start polling the Task Queue.
			factory.start();
		}
	}
	
This program first implements a service stub to be used when instantiating the client. 
The code first instantiates a factory and then creates a new worker that listens on a Task Queue. 
This worker will only process workflows and activities from this Task Queue. 
You register the Workflow and Activity with the Worker and then start the worker using factory.start().
	
When you start the Worker, it begins polling the Task Queue for Tasks to process. The terminal output from the Worker looks like this:

	Worker is running and actively polling the Task Queue.
	To quit, use ^C to interrupt.

	Withdrawing $62 from account 249946050.
	[ReferenceId: 1480a22d-d0fc-4361]

	Depositing $62 into account 591856595.
	[ReferenceId: 1480a22d-d0fc-4361]
	[1480a22d-d0fc-4361] Transaction succeeded.

The Worker continues running, waiting for more Tasks to execute.

Check the Temporal Web UI again. You will see one Worker registered where previously there was none, and the Workflow status shows that it completed.
Here's what happens when the Worker runs and connects to the Temporal Cluster:
* The first Task the Worker finds is the one that tells it to execute the Workflow.
* The Worker executes the Workflow which requests Activity Execution and communicates the events back to the Server.
* This causes the Server to send Activity Tasks to the Task Queue.
* The Worker then grabs each of the Activity Tasks in sequence from the Task Queue and executes each of the corresponding Activities.
Each of these steps gets recorded in the Event History. You can audit them in Temporal Web by clicking on the History tab next to Summary.
After a Workflow completes, the full history persists for a set retention period (typically 7 to 30 days) before the history is deleted.

Below is a visual summary of how the workflow is executed:

	1. Workflow Execution Started
	2. Workflow Task Scheduled → Started → Completed
		 ↳ Schedules Withdraw Activity
	3. Withdraw Scheduled → Started → Completed
	4. Workflow Task Scheduled → Started → Completed
		 ↳ Schedules Deposit Activity
	5. Deposit Scheduled → Started → Completed
	6. Workflow Task Scheduled → Started → Completed
	7. Workflow Execution Completed

Now map that to the workflow tasks(steps 2, 4 and 6):
| Workflow Task  | What Happens                                                         |
| -------------- | -------------------------------------------------------------------- |
| WT #1 (Step 2) | Executes from start → hits `withdraw(...)` and **suspends**          |
| WT #2 (Step 4) | Resumes after `withdraw(...)` → hits `deposit(...)` and **suspends** |
| WT #3 (Step 6) | Resumes after `deposit(...)` → runs to the end → completes           |


**Below is a quick Reference for Event Types:**
| Event Type                     | Description                                      |
| ------------------------------ | ------------------------------------------------ |
| `WORKFLOW_EXECUTION_STARTED`   | Workflow was initiated                           |
| `WORKFLOW_TASK_SCHEDULED`      | Temporal asks a worker to run some workflow code |
| `WORKFLOW_TASK_STARTED`        | A worker has picked up the task                  |
| `WORKFLOW_TASK_COMPLETED`      | Workflow code finished running                   |
| `ACTIVITY_TASK_SCHEDULED`      | An activity (side-effecting logic) is scheduled  |
| `ACTIVITY_TASK_STARTED`        | Worker started that activity                     |
| `ACTIVITY_TASK_COMPLETED`      | Activity finished successfully                   |
| `WORKFLOW_EXECUTION_COMPLETED` | Entire workflow run has ended                    |

Each Workflow and Activity task goes through:
1. Scheduled → Temporal enqueues the work
2. Started → A worker picks it up
3. Completed → The task finishes and returns

**Simulate failures**
Despite your best efforts, there's going to be a time when something goes wrong in your application. 
You might encounter a network glitch, a server might go offline, or you might introduce a bug into your code. 
One of Temporal's most important features is its ability to maintain the state of a Workflow when something fails. 
To demonstrate this, you will simulate some failures for your Workflow and see how Temporal responds.
* **Recover from a server crash**
Temporal automatically preserves the state of your Workflow even if the server is down. 
You can test this by stopping the local Temporal Cluster while a Workflow is running.
If the Temporal Cluster goes offline, you can pick up where you left off when it comes back online again.
* **Recover from an unknown error in an Activity**
To simulate an error on activity we introduce a bug in the deposit Activity method.
We modify the deposit method so activityShouldSucceed is set to false.
**Note**, that you must restart the Worker every time there's a change in code. 
You will see the Worker complete the `withdraw` Activity method, but it errors when it attempts the `deposit` Activity method.
The important thing to note here is that the Worker keeps retrying the `deposit` method:
	Withdrawing $32 from account 612849675.
	[ReferenceId: d3d9bcf0-a897-4326]
	Deposit failed
	Deposit failed
	Deposit failed
	Deposit failed

The Workflow keeps retrying using the RetryPolicy specified when the Workflow first executes the Activity.
You can view more information about the process in the Temporal Web UI.
Click the Workflow. You'll see more details including the state, the number of attempts run, and the next scheduled run time.
> **Note: **Traditionally, you're forced to implement timeout and retry logic within the service code itself. 
> This is repetitive and prone to errors. With Temporal, you can specify timeout configurations in the Workflow code as Activity options.
> Temporal offers multiple ways to specify timeouts, including Schedule-To-Start Timeout, Schedule-To-Close Timeout, Start-To-Close Timeout, and Heartbeat Timeout. 
> By default the code will be retried forever, unless a Schedule-To-Close Timeout or Start-To-Close Timeout is specified.

In the Workflow Definition, you can see that a StartToCloseTimeout is specified for the Activities, and a Retry Policy tells the server to retry the Activities up to 5000 times.
Your Workflow is running, but only the withdraw Activity method has succeeded. In any other application, you would likely have to abandon the entire process and perform a rollback.
With Temporal, you can debug and resolve the issue while the Workflow is running:
* Switch a`ctivityShouldSucceed` back to `true` and save your changes.
* Then restart the worker
* The Worker starts again. On the next scheduled attempt, the Worker picks up right where the Workflow was failing and successfully executes the newly compiled deposit Activity method:
	Depositing $32 into account 872878204.
	[ReferenceId: d3d9bcf0-a897-4326]
	[d3d9bcf0-a897-4326] Transaction succeeded.
* Visit the Web UI again, and you'll see the Workflow has completed.

You have just fixed a bug in a running application without losing the state of the Workflow or restarting the transaction!

## Workflow message passing
A Workflow can act like a stateful web service that receives messages: Queries, Signals, and Updates. 
The Workflow implementation defines these endpoints(called message handlers) via handler methods that can react to incoming messages and return values.
Temporal Clients use messages to read Workflow state and control execution.
In Temporal, a message handler method reacts to external messages or events sent to a workflow via signals, queries or updates. 
**Message Handlers**
Message handlers are defined as methods on the Workflow class, using one of the three annotations: `@QueryMethod`, `@SignalMethod`, and `@UpdateMethod`.
The parameters and return values of handlers and the main Workflow function must be serializable.
A single class with multiple fields is preferred over using multiple input parameters. A class allows you to add fields without changing the calling signature.

**Query handlers(`@QueryMethod`)**
A Query is a synchronous operation that retrieves state from a Workflow Execution.
A Query handler must not modify Workflow state.
You can't perform blocking operations such as executing an Activity in a Query handler.

How it looks:
	@WorkflowInterface
	public interface PaymentWorkflow {

		@WorkflowMethod
		void processPayment(double amount);

		@QueryMethod
		String getStatus();
	}
Example usage:
Workflow implementation:
	public class PaymentWorkflowImpl implements PaymentWorkflow {
		private String status = "Not Started";

		@Override
		public void processPayment(double amount) {
			status = "Processing";
			// Simulate work
			Workflow.sleep(1000);
			status = "Completed";
		}

		@Override
		public String getStatus() {
			return status;
		}
	}
Client querying workflow state:
	PaymentWorkflow workflow = client.newWorkflowStub(PaymentWorkflow.class, workflowOptions);
	// Start workflow asynchronously
    WorkflowClient.start(workflow::processPayment,20);
	String currentStatus = workflow.getStatus();  // This is a query
	System.out.println("Current workflow status: " + currentStatus);

* Sending a Query doesn’t add events to a Workflow's Event History.
* You can send Queries to closed Workflow Executions(one that is no longer running) within a Namespace's Workflow retention period(when workflow history is not deleted). 
This includes Workflows that have completed, failed, or timed out. Querying terminated Workflows is not safe and, therefore, not supported.
* A Worker must be online and polling the Task Queue to process a Query.

**Signal handlers(`@SignalMethod`)**
A Signal is an asynchronous message sent to a running Workflow Execution to change its state and control its flow.
The handler should not return a value. 
Unlike queries, signals can modify workflow state or behavior.
The response is sent immediately from the temporal server, without waiting for the Workflow to process the Signal.
Signal (and Update) handlers can be blocking. This allows you to use Activities, Child Workflows, durable `Workflow.sleep` Timers, `Workflow.await`, and more.
> **Note:** "Signals are asynchronous" but "Signal handlers can be blocking"

How it looks:
	@WorkflowInterface
	public interface PaymentWorkflow {

		@WorkflowMethod
		void processPayment(double amount);

		@SignalMethod
		void cancelPayment();
	}
Example usage:
Workflow implementation:
	public class PaymentWorkflowImpl implements PaymentWorkflow {
		private boolean canceled = false;

		@Override
		public void processPayment(double amount) {
			// Wait for cancel signal or complete normally
			Workflow.await(() -> canceled || /* processing finished condition */ false);

			if (canceled) {
				// handle cancellation logic
				return;
			}

			// normal processing continues
		}

		@Override
		public void cancelPayment() {
			canceled = true;
		}
	}
Client sends a signal:
	PaymentWorkflow workflow = client.newWorkflowStub(PaymentWorkflow.class, workflowOptions);
	// Start workflow asynchronously
    WorkflowClient.start(workflow::processPayment,20);
	workflow.cancelPayment();  // Sends a cancel signal asynchronously

* This sends a Signal from Client code by calling a Signal method on the WorkflowStub
* The WorkflowExecutionSignaled Event appears in the Workflow's Event History.

**Send a Signal from a Workflow:**
A Workflow can send a Signal to another Workflow, known as an External Signal. 
Use `Workflow.newExternalWorkflowStub` in your current Workflow to create an ExternalWorkflowStub for the other Workflow. 
Call Signal methods on the external stub to Signal the other Workflow:
	OtherWorkflow other = Workflow.newExternalWorkflowStub(OtherWorkflow.class, otherWorkflowID);
	other.mySignalMethod();
	
Illustration:
+---------------------+              Signal            +----------------------+
|  PaymentWorkflow    |  -------------------------->   |   OtherWorkflow      |
|  (sends signal)     |                                |  (receives signal)   |
+---------------------+                                +----------------------+


When an External Signal is sent:
* A SignalExternalWorkflowExecutionInitiated Event appears in the sender's Event History.
* A WorkflowExecutionSignaled Event appears in the recipient's Event History.

**Signal-With-Start:**
`signalWithStart()` allows a client to either signal a running workflow or start it if it’s not already running and immediately signal it.
Using `signalWithStart()` helps in avoiding race conditions (e.g., someone starts a workflow between your check and your signal)
To use Signal-With-Start, call signalWithStart and pass the name of your Signal with its arguments:

	@WorkflowInterface
	public interface GreetingWorkflow {
		@WorkflowMethod
		String greet(Customer customer);

		@SignalMethod
		void setCustomer(Customer customer);

		@QueryMethod
		Customer getCustomer();
	}

	public static void signalWithStart() {
		// WorkflowStub is a client-side stub to a single Workflow instance
		WorkflowStub untypedWorkflowStub = client.newUntypedWorkflowStub("GreetingWorkflow",
		WorkflowOptions.newBuilder()
				.setWorkflowId(workflowId)
				.setTaskQueue(taskQueue)
				.build());

		untypedWorkflowStub.signalWithStart(
			"setCustomer",                // signal method name
			new Object[] {customer2},     // signal args
			new Object[] {customer1}      // workflow method args
		);

		String greeting = untypedWorkflowStub.getResult(String.class);
	}
	
When using Signal-With-Start, the Signal handler (setCustomer) will be executed before the Workflow method (greet).

**Update handlers(`@UpdateMethod`) and validators(`@UpdateValidatorMethod`)**
An Update is a trackable synchronous request sent to a running Workflow Execution. 
It can change the Workflow state, control its flow, and return a result. 
The sender must wait until the Worker accepts or rejects the Update. 
The sender may wait further to receive a returned value or an exception if something goes wrong
Similar to a signal, but with 3 key differences:
* It is synchronous: the caller waits for the update method to complete.
* It modifies workflow state but also **can return a result** immediately.
* You can't send Updates to other Workflow Executions.
Why is it important?
* Use cases where you want to send a command to a workflow and wait for a response (e.g., to confirm the update succeeded).
* Combines the benefits of signals (state change) with queries (immediate response).
* Useful for workflows that require interactive, request-response style updates.

How it looks:
	@WorkflowInterface
	public interface PaymentWorkflow {

		@WorkflowMethod
		void processPayment(double amount);

		@UpdateMethod
		String updatePaymentDetails(String newDetails);
	}
Example usage:
Workflow implementation:
	public class PaymentWorkflowImpl implements PaymentWorkflow {
		private String paymentDetails = "Initial Details";

		@Override
		public void processPayment(double amount) {
			// do work
		}

		@Override
		public String updatePaymentDetails(String newDetails) {
			paymentDetails = newDetails;
			return "Updated to: " + paymentDetails;
		}
	}
Client calls update:
	PaymentWorkflow workflow = client.newWorkflowStub(PaymentWorkflow.class, workflowOptions);
	// Start workflow asynchronously
    WorkflowClient.start(workflow::processPayment,20);
	String result = workflow.updatePaymentDetails("New Details");
	System.out.println(result);  // prints: Updated to: New Details

* This sends an update from Client code by calling update method on the WorkflowStub and waiting for the Update to complete.
* `WorkflowExecutionUpdateAccepted` is added to the Event History when the Worker confirms that the Update passed validation.
* `WorkflowExecutionUpdateCompleted` is added to the Event History when the Worker confirms that the Update has finished.

Another way of sending an update is to send `startUpdate` to receive an `WorkflowUpdateHandle` as soon as the Update is accepted or rejected.
* Use this `WorkflowUpdateHandle` later to fetch your results.
* Blocking Update handlers normally perform long-running asynchronous operations.
* `startUpdate` only waits until the Worker has accepted or rejected the Update, not until all asynchronous operations are complete.
For example:
	WorkflowUpdateHandle<Language> handle =
		WorkflowStub.fromTyped(workflow)
			.startUpdate(
				"setLanguage",                    // The name of the @UpdateMethod to call
				WorkflowUpdateStage.ACCEPTED,    // Wait until the update is ACCEPTED (not necessarily completed)
				Language.class,                   // The return type of the update
				Language.ENGLISH                  // The argument passed to the update
			);
	previousLanguage = handle.getResultAsync().get();
To obtain an Update handle, you can:
* Use `startUpdate` to start an Update and return the handle, as shown in the preceding example.
* Use `getUpdateHandle` to fetch a handle for an in-progress Update using the Update ID and Workflow ID.
You can use the WorkflowUpdateHandle to obtain information about the update:
* `getExecution()`: Returns the Workflow Execution that this Update was sent to.
* `getId()`: Returns the Update's unique ID, which can be useful for deduplication when using Continue-As-New
* `getResultAsync()`: Returns a `CompletableFuture` which can be used to wait for the Update to complete.

**Update-With-Start:**
Update-with-Start lets you send an Update that checks whether an already-running Workflow with that ID exists:
* If the Workflow exists, the Update is processed.
* If the Workflow does not exist, a new Workflow Execution is started with the given ID, and the Update is processed before the main Workflow method starts to execute.
Use the `startUpdateWithStart` WorkflowClient API. 
It returns once the requested Update wait stage has been reached; or when the request times out. 
Use the `WorkflowUpdateHandle` to retrieve a result from the Update.
You will need to provide:
* WorkflowStub created from `WorkflowOptions`. 
The `WorkflowOptions` require Workflow Id Conflict Policy to be specified. 
Choose "Use Existing" and use an idempotent Update handler to ensure your code can be executed again in case of a Client failure. 
Not all `WorkflowOptions` are allowed. For example, specifying a Cron Schedule will result in an error.
* `UpdateOptions`.the update wait stage must be specified. 
For Update-with-Start, the Workflow Id is optional. When specified, the Id must match the one used in WorkflowOptions. 
Since a running Workflow Execution may not already exist, you can't set a Run Id.
* `WithStartWorkflowOperation`. Specify the workflow method. 
Note that a `WithStartWorkflowOperation` can only be used once. Re-using a previously used operation returns an error from startUpdateWithStart.
For example:

	GreetingWorkflow workflow = client.newWorkflowStub(
    GreetingWorkflow.class,
    WorkflowOptions.newBuilder()
        .setWorkflowId("greet-123")
        .setTaskQueue("greet-task-queue")
        .setWorkflowIdReusePolicy(WorkflowIdReusePolicy.WORKFLOW_ID_REUSE_POLICY_USE_EXISTING)
        .build());


	WorkflowUpdateHandle<Language> handle =
		WorkflowClient.startUpdateWithStart(
			workflow::setLanguage, // Update method reference: this is the @UpdateMethod to call
			Language.ENGLISH,      // this is the argument passed to the update handler above
			UpdateOptions.<Language>newBuilder().setWaitForStage(WorkflowUpdateStage.ACCEPTED).build(), // update wait stage must be specified: return once the update is ACCEPTED by the Workflow
			new WithStartWorkflowOperation<>(workflow::getGreetings)); //workflow method that should run if the workflow is not already running

	Language previousLanguage = handle.getResultAsync().get();
	
To obtain the update result directly, use the `executeUpdateWithStart` WorkflowClient API. 
It returns once the update result is available; or when the API call times out. 
The update wait stage on the `UpdateOptions` is optional. When specified, it must be `WorkflowUpdateStage.COMPLETED`.
For example:
	Language previousLanguage =
		WorkflowClient.executeUpdateWithStart(
			workflow::setLanguage,
			Language.ENGLISH,
			UpdateOptions.<Language>newBuilder().build(),
			new WithStartWorkflowOperation<>(workflow::getGreetings));

An **Update Validator** is an optional method you define in a workflow to check whether an incoming update request is valid, before the update handler is run.
It runs synchronously and immediately when the update is received — even before the update is written to the workflow's event history.
Use the `updateName` argument when declaring the validator to connect it to its Update. 
The validator must return void and accept the same argument types as the handler.
Accepting and rejecting Updates with validators:
* To reject an Update, throw an exception of any type in the validator.
* Without a validator, Updates are always accepted.
Validators and Event History:
* The `WorkflowExecutionUpdateAccepted` event is written into the History whether the acceptance was automatic or programmatic.
* When a Validator throws an error, the Update is rejected, the Update is not run, and `WorkflowExecutionUpdateAccepted` won't be added to the Event History. The caller receives an "Update failed" error.
Use `getCurrentUpdateInfo` to obtain information about the current Update. This includes the Update ID, which can be useful for deduplication when using Continue-As-New
How it works:
	@WorkflowInterface
	public interface PaymentWorkflow {

		@WorkflowMethod
		void processPayment(double amount);

		@UpdateMethod
		String updatePaymentDetails(String newDetails);
		
		@UpdateValidator(updateName = "updatePaymentDetails")
		void validatePaymentDetails(String newDetails)
	}
	
update validator implementation:
	public class PaymentWorkflowImpl implements PaymentWorkflow {
		//define other methods and variables
		public void validatePaymentDetails(String newDetails) {
			if (newDetails == null || newDetails.trim().isEmpty()) {
				throw new IllegalArgumentException("Payment details cannot be empty.");
			}
			if (newDetails.length() > 100) {
				throw new IllegalArgumentException("Payment details are too long.");
			}
			// You can add more validation logic here (e.g., format, characters, etc.)
		}
	}


**Message Handlers Summary Table:**
| Annotation      | Purpose                        | Sync/Async   | Can modify state? | Returns result? | Use Case                            |
| --------------- | ------------------------------ | ------------ | ----------------- | --------------- | ----------------------------------- |
| `@QueryMethod`  | Read-only state inspection     | Synchronous  | No                | Yes             | Check current workflow state/status |
| `@SignalMethod` | Event/notification to workflow | Asynchronous | Yes               | No              | Send external events, commands      |
| `@UpdateMethod` | Synchronous update with result | Synchronous  | Yes               | Yes             | Request-response state updates      |


**NON-TYPE SAFE API CALLS**
**untyped `WorkflowStub`**  is a Temporal client-side object that lets you interact with a workflow execution without needing the workflow definition.
In real-world development, sometimes you may be unable to import Workflow Definition method signatures. 
When you don't have access to the Workflow Definition or it isn't written in Java, you can use these non-type safe APIs to obtain an untyped WorkflowStub:
* `WorkflowClient.newUntypedWorkflowStub`
* `Workflow.newUntypedExternalWorkflowStub`.
Pass method names instead of method objects to:
* `WorkflowStub.query`
* `WorkflowStub.signal`
* `WorkflowStub.update`
* `WorkflowStub.startUpdateWithStart`
* `WorkflowStub.executeUpdateWithStart`

## Message handler patterns
This section covers common write operations, such as Signal and Update handlers. 
It doesn't apply to pure read operations, like Queries or Update Validators.
**Do blocking operations in handlers**
Signal and Update handlers can block. 
This allows you to use `Workflow.await`, Activities, Child Workflows, `Workflow.sleep` Timers, etc. 
This expands the possibilities for what can be done by a handler but it also means that handler executions and your main Workflow method are all running concurrently, with switching occurring between them at await calls.
In the following code the Update handler makes a blocking call to execute an Activity:

	@WorkflowInterface
	public interface PaymentWorkflow {

		@WorkflowMethod
		void processPayment();

		@UpdateMethod
		boolean updateCardAndVerify(String newCardNumber);
	}

	public interface PaymentActivities {
		@ActivityMethod
		boolean verifyCard(String cardNumber);
	}

	public class PaymentWorkflowImpl implements PaymentWorkflow {

		private PaymentActivities activities =
			Workflow.newActivityStub(PaymentActivities.class,
				ActivityOptions.newBuilder()
					.setStartToCloseTimeout(Duration.ofMinutes(1))
					.build());

		private String cardNumber;
		private boolean verified;

		@Override
		public void processPayment() {
			// wait until card is verified
			Workflow.await(() -> verified);

			// proceed with payment using verified card
			activities.chargeCard(cardNumber);  // another activity
		}

		// ⚠️ This is a blocking update handler — calls an activity
		@Override
		public boolean updateCardAndVerify(String newCardNumber) {
			this.cardNumber = newCardNumber;

			// 🧠 Blocking call: activity is a non-deterministic external operation
			this.verified = activities.verifyCard(newCardNumber);

			return this.verified;
		}
	}
	
Although a Signal handler can also make blocking calls like this, using an Update handler allows the Client to receive a result or error once the Activity completes. 
This lets your Client track the progress of asynchronous work performed by the Update's Activities, Child Workflows, etc.

**Add blocking wait conditions**
Sometimes, blocking Signal or Update handlers need to meet certain conditions before they should continue. 
You can use `Workflow.await` to prevent the code from proceeding until a condition is true, like in the previous example(but in the workflow method). 
You specify the condition by passing a function that returns `true` or `false`. 
This is an important feature that helps you control your handler logic.
Here are two important use cases for `Workflow.await`:
* Waiting in a handler until it is appropriate to continue.
* Waiting in the main Workflow until all active handlers have finished.

* **Wait for conditions in handlers**
It's common to use `Workflow.await` in a handler. 
For example, suppose your Workflow class has a `updateReadyToExecute` method that indicates whether your Update handler should be allowed to start executing. 
You can use `Workflow.await(...)` in the handler to make the handler pause until the condition is met:
	@Override
	public boolean updateCardAndVerify(String newCardNumber) {
		Workflow.await(() -> this.updateReadyToExecute(newCardNumber));
		...
	}

Remember: handlers can execute before the main Workflow method starts.
You can also use Workflow.await anywhere else in the handler to wait for a specific condition to become true. 
This allows you to write handlers that pause at multiple points, each time waiting for a required condition to become true.

* **Ensure your handlers finish before the Workflow completes**
`Workflow.await` can ensure your handler completes before a Workflow finishes. 
When your Workflow uses blocking Signal or Update handlers, your main Workflow method can return or Continue-as-New while a handler is still waiting on an async task, such as an Activity. 
The Workflow completing may interrupt the handler before it finishes crucial work and cause Client errors when trying to retrieve Update results. 
Use `Workflow.await` to wait for `Workflow.isEveryHandlerFinished` to return true to address this problem and allow your Workflow to end smoothly:

	public class MyWorkflowImpl implements MyWorkflow {
		...
		@Override
		public String run() {
			...
			
			// ⛔ Don't return until all signal/update handlers are done
			Workflow.await(() -> Workflow.isEveryHandlerFinished());
			return "workflow-result";
		}
	}
By default, your Worker will log a warning when you allow a Workflow Execution to finish with unfinished handler executions. 
You can silence these warnings on a per-handler basis by passing the `unfinishedPolicy` argument to the `@SignalMethod` / `@UpdateMethod` annotation:

	@WorkflowInterface
	public interface MyWorkflow {
		...
		@UpdateMethod(unfinishedPolicy = HandlerUnfinishedPolicy.ABANDON)
		void myUpdate();
	}

**Continue-As-New** is a way for a Workflow Execution to:
* Stop its current execution, and
* Start a new one with the same Workflow ID, but
* Without growing the execution history indefinitely
	
**Use `@WorkflowInit` to operate on Workflow input before any handler executes**
Normally, your Workflows constructor won't have any parameters. 
However, if you use the `@WorkflowInit` annotation on your constructor, you can give it the same Workflow parameters as your `@WorkflowMethod`.
The SDK will then ensure that your constructor receives the Workflow input arguments that the Client sent.
The Workflow input arguments are also passed to your `@WorkflowMethod` method -- that always happens, whether or not you use the `@WorkflowInit` annotation. 
This is useful if you have message handlers that need access to Workflow input
> **caution**
> Do not make blocking calls from within your @WorkflowInit method. 
> This could result in your Workflow being incompletely initialized at the start, meaning, for example, that Signal, Query, and Update handler registration would be delayed.

Here's an example. Notice that the constructor and `getGreeting` must have the same parameters:

	public class GreetingExample {
		@WorkflowInterface
		public interface GreetingWorkflow {
			@WorkflowMethod
			String getGreeting(String input);

			@UpdateMethod
			boolean checkTitleValidity();
		}

		public static class GreetingWorkflowImpl implements GreetingWorkflow {
			private final String nameWithTitle;
			private boolean titleHasBeenChecked;
			...
			// Note the annotation is on a public constructor
			@WorkflowInit
			public GreetingWorkflowImpl(String input) {
			  this.nameWithTitle = "Sir " + input;
			  this.titleHasBeenChecked = false;
			}

			@Override
			public String getGreeting(String input) {
			  Workflow.await(() -> titleHasBeenChecked)
			  return "Hello " + nameWithTitle;
			}

			@Override
			public boolean checkTitleValidity() {
			  // 👉 The handler is now guaranteed to see the workflow input
			  // after it has been processed by the constructor.
			  boolean isValid = activity.checkTitleValidity(nameWithTitle);
			  titleHasBeenChecked = true;
			  return isValid;
			}
		}
	}

**Use locks to prevent concurrent handler execution**
Concurrent processes can interact in unpredictable ways. 
Incorrectly written concurrent message-passing code may not work correctly when multiple handler instances run simultaneously. 
Here's an example of a pathological case:

	public class DataWorkflowImpl implements DataWorkflow {
		...
		@Override
		public void badSignalHandler() {
			Data data = activity.fetchData();
			this.x = data.x;
			// 🐛🐛 Bug!! If multiple instances of this method are executing concurrently, then
			// there may be times when the Workflow has self.x from one Activity execution and self.y from another.
			Workflow.sleep(Duration.ofSeconds(1));
			this.y = data.y;
		}
	}

Coordinating access with WorkflowLock corrects this code. 
Locking makes sure that only one handler instance can execute a specific section of code at any given time:

	public class DataWorkflowImpl implements DataWorkflow {
		WorkflowLock lock = Workflow.newWorkflowLock();
		...
		@Override
		public void safeSignalHandler() {
			try {
				lock.lock();
				Data data = activity.fetchData();
				this.x = data.x;
				// ✅ OK: the scheduler may switch now to a different handler execution,
				// or to the main workflow method, but no other execution of this handler
				// can run until this execution finishes.
				Workflow.sleep(Duration.ofSeconds(1));
				this.y = data.y;
			} finally {
				lock.unlock()
			}
		}
	}

## Message handler troubleshooting
When sending a Signal, Update, or Query to a Workflow, your Client might encounter the following errors:
* **The Client can't contact the server:** You'll receive a `WorkflowServiceException` on which the `cause` is a `StatusRuntimeException` and `status` of `UNAVAILABLE` (after some retries).
* **The Workflow does not exist:** You'll receive a `WorkflowNotFoundException`.
**Problems when sending a Signal**
When using Signal, the above `WorkflowExceptions`(connecting to the server and non-existent workflow) are the only types of exception that will result from the request.
In contrast, for Queries and Updates, the client waits for a response from the Worker. 
If an issue occurs during the handler execution by the Worker, the Client may receive an exception.
**Problems when sending an Update**
When working with Updates, you may encounter these errors:
* **No Workflow Workers are polling the Task Queue:** Your request will be retried by the SDK Client indefinitely. 
You can impose a timeout with `CompletableFuture.get()` method with a timeout parameter. 
This throws a `java.util.concurrent.TimeoutException` exception when it expires.
* **Update failed:** You'll receive a `WorkflowUpdateException` exception. There are two ways this can happen:
	* The Update was rejected by an Update validator defined in the Workflow alongside the Update handler.
	* The Update failed after having been accepted.
Update failures are like Workflow failures. 
Issues that cause a Workflow failure in the main method also cause Update failures in the Update handler. These might include:
	* A failed Child Workflow
	* A failed Activity (if the Activity retries have been set to a finite number)
	* The Workflow author throwing ApplicationFailure
	* Any error listed in getFailWorkflowExceptionTypes (empty by default)
* **The handler caused the Workflow Task to fail:** A Workflow Task Failure causes the server to retry Workflow Tasks indefinitely. 
What happens to your Update request depends on its stage:
	* If the request hasn't been accepted by the server, you receive a `FAILED_PRECONDITION` `WorkflowServiceException` exception.
	* If the request has been accepted, it is durable. Once the Workflow is healthy again after a code deploy, use an WorkflowUpdateHandle to fetch the Update result.
* **The Workflow finished while the Update handler execution was in progress:** You'll receive a `WorkflowServiceException` "workflow execution already completed"`.
This will happen if the Workflow finished while the Update handler execution was in progress, for example because
	* The Workflow was canceled or failed.
	* The Workflow completed normally or continued-as-new and the Workflow author did not wait for handlers to be finished.


