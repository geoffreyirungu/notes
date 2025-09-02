# Migration

## Delta
In computing, "delta" generally refers to the difference or change between two values or states.
It maybe changes made between two versions of a file, dataset, or system.

## Changelog
A changelog/change log is a record of all changes made to a system/project.
It provides a chronological history/tracks modifications, including bug fixes, new features, and other updates, helping users, developers, and stakeholders understand the project's evolution. 

## Data Migration
Data migration is the process of moving/transferring data from one location to another such as from on-premises to a cloud platform, one format to another, or one application to another.
Some reasons for data migration involve:
* Replacing, upgrading, or expanding storage systems or upgrading servers
* Installing software upgrades
* Migrating applications or databases
* Moving on-premises infrastructure to cloud-based services
* Merging/consolidating websites
* Performing infrastructure maintenance
* Combining/consolidating data from multiple sources into a single system
* Data center relocation

The data migration process requires organizations to prepare, extract and transform data and to follow a specified set plan -- which differs by organization and migration.

### Types of Data Migration
* **Database Migration:** Database migration refers to the process of transferring data, schema, or both from one database to another.
It can also refer to the act of changing the structure/schema of a database over time, while preserving or transferring the existing data.
examples of database migration tools include liquibase and flyway.
* **Storage Migration:** Moving data from one storage medium to another, like moving from hard drives to SSDs or to cloud storage.
* **Application Migration:** moves an application or program from one environment/platform to another. 
* **Cloud Migration:** moves data or applications or both from an on-premises location to the cloud or from one cloud service to another. 
* **Business Process Migration:** moves business applications and related data and processes to a new environment.

## Liquibase
Liquibase is an open-source database schema change management tool. 
It helps developers and database administrators track, version, and deploy database changes in a structured and automated way.
**How Liquibase Works — Overview**
* **Changelogs**
Database changes (like creating tables, adding columns) are written in changelog files. Changelog files can be in XML, YAML, JSON, or SQL formats.
The changes are called **changesets**.
There are two types of changelogs: 
	* primary changelog: This changelog file directly contains changesets that modify the database schema. eg:
		databaseChangeLog:
		- changeSet:
			id: 1749722559558-3
			author: javanoyugi
			changes:
			- dropForeignKeyConstraint:
				baseTableName: subprocess_role
				constraintName: fka3h8f9t6lowvldj5i0iiiav3w
	* Master/parent changelog: This changelog does not have changesets itself, but uses include or includeAll directives to reference other changelog files.
		databaseChangeLog:
		  - include:
			  file: db/changelog/changes/20250603142527.yaml
		  - include:
			  file: db/changelog/changes/20250604215838.yaml
	
| Type                    | Contains             | Use case                       |
| ----------------------- | -------------------- | ------------------------------ |
| Primary Changelog       | Changesets           | Small projects, simple setup   |
| Master/Parent Changelog | `include` directives | Large projects, modularization |


* **Changesets**
Each changeset represents a single database operation, such as creating a table, adding a column, or modifying data.
Each changeset has:
	* A unique id (per author and file)
	* An author (who made the change)
	* The actual changes (e.g., createTable, addColumn, insert)
Each changeset is uniquely identified by an id and author and changelog file path.
The unique identification ensures every change is tracked individually and also ensuring the same changes are never applied twice.

Here’s an example of a changelog with changesets in yaml format:

	databaseChangeLog:
	- changeSet:
		id: 1749722559558-3
		author: javanoyugi (generated)
		changes:
		- dropForeignKeyConstraint:
			baseTableName: subprocess_role
			constraintName: fka3h8f9t6lowvldj5i0iiiav3w
	- changeSet:
		id: 1749722559558-1
		author: javanoyugi (generated)
		changes:
		- addColumn:
			columns:
			- column:
				name: crq_number
				type: VARCHAR(255)
			tableName: subprocess

* **DATABASECHANGELOG and DATABASECHANGELOGLOCK Tables**
**DATABASECHANGELOG** table is used by liquibase to track which changesets have been run. This tracks which changes are already applied.
**DATABASECHANGELOGLOCK** is a lock table that Liquibase uses to ensure only one instance of Liquibase applies changesets at a time on a database.
	* When Liquibase starts applying changes, it tries to acquire a lock by inserting a row or setting a flag in this table.
	* If another Liquibase process tries to run concurrently, it will wait or fail because the lock is held.
	* This prevents race conditions like two processes trying to update the same schema simultaneously, which could corrupt the database state.
	
The **DATABASECHANGELOGLOCK** table usually contains:
| ID | LOCKED | LOCKGRANTED         | LOCKEDBY                        |
| -- | ------ | ------------------- | ------------------------------- |
| 1  | true   | 2025-06-26 12:34:56 | myhost/12345/liquibase\_version |

	* LOCKED is true or false
	* LOCKGRANTED timestamp when lock was acquired
	* LOCKEDBY describes who/what holds the lock (hostname, process, etc.)

Liquibase releases this lock once all changesets have been applied.

Below is the structure of the **DATABASECHANGELOG**:
| Column Name    | Data Type | Description                                                                      |
|----------------|-----------|----------------------------------------------------------------------------------|
| ID             | VARCHAR   | Unique identifier for each changeset.                                            |
| AUTHOR         | VARCHAR   | Name or username of the changeset author.                                        |
| FILENAME       | VARCHAR   | Name of the XML file containing the changeset.                                   |
| DATEEXECUTED   | TIMESTAMP | Timestamp indicating when the changeset was executed.                            |
| ORDEREXECUTED  | INT       | Integer representing the order of changeset execution.                           |
| EXECTYPE       | VARCHAR   | Execution type of the changeset (e.g., "EXECUTED").                              |
| MD5SU          | VARCHAR   | Checksum value generated from the changeset content.                             |
| DESCRIPTION    | VARCHAR   | Brief description of the changeset.                                              |
| COMMENTS       | VARCHAR   | Additional comments or notes related to the changeset.                           |
| TAG            | VARCHAR   | Indicates if the changeset is associated with a specific tag.                    |
| LIQUIBASE      | VARCHAR   | Version of Liquibase that executed the changeset.                                |
| CONTEXTS       | VARCHAR   | Contexts in which the changeset should be executed.                              |
| LABELS         | VARCHAR   | Labels used to group changesets based on common characteristics.                 |
| DEPLOYMENT_ID  | VARCHAR   | Identifier representing a specific deployment, useful in multi-node environments.|

* **Applying Changes**
Liquibase compares the changesets in your changelog file with entries in DATABASECHANGELOG and applies only the changes that haven’t run yet.

* **Rollback**
Liquibase supports rollbacks, letting you undo changesets if needed.
**Note:** liquibase cannot auto-generate rollback SQL from raw SQL files. It only auto-generates rollback for YAML / XML / JSON.

**Illustration of the Liquibase Workflow**
| Step                         | Description                                                 |
| ---------------------------- | ----------------------------------------------------------- |
| 1. Write changelog           | Create changelog file with changesets describing DB changes |
| 2. Run Liquibase update      | Liquibase checks DATABASECHANGELOG, applies new changesets  |
| 3. DATABASECHANGELOG updated | Marks changesets as executed                                |
| 4. Use in CI/CD(Optional)    | Liquibase runs as part of deployment pipeline               |
| 5. Rollback if needed        | Rollback commands revert changesets to a previous state     |

**Example: Using Liquibase with XML Changelog**
**Step 1: Install liquibase**
Install liquibase from https://www.liquibase.com/download-oss
**Step 2: Database Configuration**
Configure your database connection details (URL, username, password) in a liquibase.properties file.
	url=jdbc:postgresql://localhost:3306/mydatabase?currentSchema=my_schema
	username=myuser
	password=mypassword

**Step 3: Create a changelog XML file (db.changelog.xml)**
	<?xml version="1.0" encoding="UTF-8"?>
	<databaseChangeLog
			xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
			xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
			xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog
			 http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.1.xsd">

		<changeSet id="1" author="alice">
			<createTable tableName="employee">
				<column name="id" type="int" autoIncrement="true" >
					<constraints primaryKey="true" nullable="false"/>
				</column>
				<column name="first_name" type="varchar(50)"/>
				<column name="last_name" type="varchar(50)"/>
				<column name="email" type="varchar(100)"/>
			</createTable>
		</changeSet>

		<changeSet id="2" author="alice">
			<addColumn tableName="employee">
				<column name="date_of_birth" type="date"/>
			</addColumn>
		</changeSet>

	</databaseChangeLog>

**Step 4: Run Liquibase command to update database**
	liquibase --changeLogFile=db.changelog.xml update

Liquibase connects to your database.
* It checks the DATABASECHANGELOG table.
* Finds which changesets haven’t run yet.
* Runs them in order (id=1 then id=2).
* Records each applied changeset in DATABASECHANGELOG.

**Step 5: DATABASECHANGELOG table (auto-created)**
| ID | AUTHOR | FILENAME         | DATEEXECUTED        | ORDEREXECUTED | EXECTYPE |
| -- | ------ | ---------------- | ------------------- | ------------- | -------- |
| 1  | alice  | db.changelog.xml | 2025-06-27 12:00:00 | 1             | EXECUTED |
| 2  | alice  | db.changelog.xml | 2025-06-27 12:01:00 | 2             | EXECUTED |

**Step 6: Rollback Example**
If you want to undo changeset 2 (adding the date_of_birth column):
	liquibase --changeLogFile=db.changelog.xml rollbackCount 1
Liquibase will drop the date_of_birth column and remove the record from DATABASECHANGELOG(undoes the last 1 applied changeset from the changelog file).

| Command           | Meaning                                           |
| ----------------- | ------------------------------------------------- |
| `rollbackCount 1` | Undo last 1 applied changeset                     |
| `rollbackCount 2` | Undo last 2 applied changesets (in reverse order) |
| `rollbackCount N` | Undo last **N** changesets from the changelog     |

**Writing Changelogs in SQL**
**Example: SQL Changelog (db.changelog.sql)**
	--liquibase formatted sql

	--changeset alice:1
	CREATE TABLE employee (
		id INT PRIMARY KEY AUTO_INCREMENT,
		first_name VARCHAR(50),
		last_name VARCHAR(50),
		email VARCHAR(100)
	);

	--changeset alice:2
	ALTER TABLE employee ADD COLUMN date_of_birth DATE;

Breakdown:
* `--liquibase formatted sql`: Tells Liquibase that this is a formatted SQL changelog.
* `--changeset author:id`: Marks the beginning of a new changeset. Must be unique within the changelog.
* SQL statements: Your native DDL or DML statements (like CREATE TABLE, ALTER TABLE).

**How to Run It**
	liquibase --changeLogFile=db.changelog.sql update

**⚠️ Limitations of SQL Changelogs**
While SQL changelogs are straightforward, be aware:
| Limitation                     | Description                                                                       |
| ------------------------------ | --------------------------------------------------------------------------------- |
| 🔁 Rollbacks need to be manual | You must define rollback statements explicitly.                                   |
| 📂 Portability may vary        | Native SQL syntax may not work across different DB types (e.g., Oracle vs MySQL). |
| 📄 Less validation             | You lose schema validation provided by structured formats (XML/YAML/JSON).        |

**Example with Rollback**
	--liquibase formatted sql

	--changeset alice:3
	INSERT INTO employee (first_name, last_name, email) VALUES ('Jane', 'Doe', 'jane@example.com');

	--rollback DELETE FROM employee WHERE email = 'jane@example.com';
	
During a rollback, Liquibase will run the custom rollback statement if defined.

**Generating Database Schema using Liquibase**
The `generateChangeLog` command in Liquibase is used to generate a changelog file from an existing database schema.
It connects to your database, inspects the schema (tables, columns, indexes, constraints, etc.), 
and outputs a changelog file (in YAML, XML, JSON, or formatted SQL) that represents the current state of the database schema.

Before running the `generateChangeLog` command make sure liquibase has been configured or pass the configs in the command eg:

	url=jdbc:postgresql://localhost:5432/mydb
	username=dbuser
	password=dbpass
	driver=org.postgresql.Driver
	changeLogFile=db/changelog/generated/changelog.yaml

**Run the command**
	liquibase generateChangeLog

This generates a changelog file (`changelog.yaml`:specified in the configuration) containing all the tables, constraints, views, sequences, etc. found in the target database.
**Important Notes**
| Aspect            | Detail                                                                      |
| ----------------- | --------------------------------------------------------------------------- |
| 🔄 One-time Use   | Usually used once at project start to capture existing DB                   |
| ⚠️ Not idempotent | Re-running it generates a full schema again — not changes                   |
| 🧾 Output Format  | Based on the extension of `--changeLogFile` (e.g., `.yaml`, `.xml`, `.sql`) |
| 📂 Output Path    | The path to `--changeLogFile` must exist or Liquibase will fail             |

**Advanced: Output Formats**
You can choose other formats:

	liquibase --changeLogFile=changelog.sql generateChangeLog
	liquibase --changeLogFile=changelog.xml generateChangeLog

**Obtaining Schema Differences in Liquibase**
The `liquibase diff` command compares two databases and shows the differences as a report in the console.
It's one of Liquibase's most powerful tools for database synchronization, auditing, and validation.

As usual before running the `diff` command make sure liquibase has been configured or pass the configs in the command eg:

	referenceUrl=jdbc:postgresql://localhost:5432/source_db
	referenceUsername=user
	referencePassword=password
	url=jdbc:postgresql://localhost:5432/target_db
	username=dbuser
	password=dbpass
	driver=org.postgresql.Driver
	changeLogFile=db/changelog/generated/changelog.yaml
	
**Run the `liquibase diff` command(Basic Syntax)**
	liquibase diff

**Example Output(schema differences between the referenceUrl (source) and url (target))**
The command will print a list of differences, like:
	Missing Table: public.employee
	Changed Column: public.user.email type changed from VARCHAR(100) to VARCHAR(255)
	Unexpected Index: public.orders.idx_created_at
	
The output is schema differences between the referenceUrl (source) and url (target).
It does not modify the database — just shows differences.

The `diffChangeLog` command compares two databases and generates a Liquibase changelog file(YAML/XML/SQL) that would transform one into the other.
This creates a changelog you can apply with update.

As usual before running the `diffChangeLog` command make sure liquibase has been configured or pass the configs in the command.

**Run the `liquibase diffChangeLog` command(Basic Syntax)**
	liquibase diffChangeLog

The output changelog will contain changesets representing schema objects missing in the target database.

**Additional Options for the liquibase differences commands**
* `--diffTypes`: to limit what to compare (tables, views, columns, etc.)
* Output format can be controlled via `--changeLogFile`
* Liquibase diff isn't limited to comparing two live databases — it can also compare the current database schema to a Java-based model (via JPA/Hibernate), effectively detecting differences between your Java entities and the database.

**✅ Liquibase Command Summary with Usage Examples**
| Command                 | Purpose                                                                 | When to Use                                           | How to Run (Example)                                                                    |
| ----------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `update`                | Applies changesets from the changelog to the database                   | Deploy schema changes                                 | `liquibase --changeLogFile=db.changelog-master.yaml update`                             |
| `updateSQL`             | Outputs the SQL Liquibase would run (doesn't apply)                     | Preview changes without modifying DB                  | `liquibase --changeLogFile=db.changelog-master.yaml updateSQL > changes.sql`            |
| `rollbackCount N`       | Rolls back the last **N** applied changesets                            | Undo recent changes (manual or during testing)        | `liquibase --changeLogFile=db.changelog-master.yaml rollbackCount 2`                    |
| `validate`              | Validates the changelog structure and syntax                            | Check for issues before applying                      | `liquibase --changeLogFile=db.changelog-master.yaml validate`                           |
| `status`                | Shows unexecuted changesets (differences between changelog and DB)      | Detect what's pending                                 | `liquibase --changeLogFile=db.changelog-master.yaml status`                             |
| `generateChangeLog`     | Generates a full changelog by reverse-engineering the current DB schema | Bootstrap Liquibase for an existing DB                | `liquibase --outputChangeLogFile=full-schema.yaml generateChangeLog`                    |
| `diff`                  | Compares two schemas (DB vs DB, DB vs entities, etc.)                   | Detect schema differences                             | `liquibase --referenceUrl=... --url=... diff`                                           |
| `diffChangeLog`         | Outputs a changelog describing differences between two schemas          | Auto-generate migration file based on differences     | `liquibase --referenceUrl=... --url=... --changeLogFile=changes.yaml diffChangeLog` 	  |
| `snapshot`              | Saves the structure of a DB into a snapshot file                        | Track schema at a point in time                       | `liquibase --url=... --outputFile=schema.json snapshot`                                 |
| `rollbackToDate`        | Rolls back to a specific date/time                                      | Time-based rollback of changesets                     | `liquibase --changeLogFile=db.changelog-master.yaml rollbackToDate 2024-01-01`          |
| `changelogSync`         | Marks all changesets as already applied (no actual changes made)        | Sync DB state with changelog without applying changes | `liquibase --changeLogFile=db.changelog-master.yaml changelogSync`                      |
| `clearCheckSums`        | Removes checksums from `DATABASECHANGELOG` to force revalidation        | When checksums mismatch due to file edits             | `liquibase clearCheckSums`                                                              |
| `updateTestingRollback` | Applies all changesets, then rolls them back (in-memory test)           | Validate changesets are reversible                    | `liquibase --changeLogFile=db.changelog-master.yaml updateTestingRollback`              |


**Summary of Benefits of Liquibase**
* Version control friendly: Changelogs are text files that live in your source control.
* Automated Schema Updates: automatically apply new changesets (units of database changes) to your database, making deployments smoother and less error-prone.
* Track changes: Avoids running the same changes twice.
* Rollback support: Safely undo mistakes.
* Cross-platform: Works with many relational DB engines.
* Automation-friendly: Integrates with CI/CD pipelines.

**Common Liquibase Use Cases:**
* Automating database updates as part of the deployment process
* Managing schema migrations across different environments
* Ensuring database changes are repeatable and auditable
* Coordinating schema updates between multiple developers or teams

## `pg_dump` in PostgreSQL
pg_dump is a utility for backing up a PostgreSQL database. 
It makes consistent backups even if the database is being used concurrently. pg_dump does not block other users accessing the database (readers or writers).
pg_dump only dumps a single database. To back up an entire cluster, or to back up global objects that are common to all databases in a cluster (such as roles and tablespaces), use pg_dumpall.

**✅ Why is pg_dump Important?**
* Database Backups: Regular backups for disaster recovery.
* Migration: Move data between PostgreSQL instances or environments (e.g., dev → prod).
* Version Control: Store schema snapshots as part of release pipelines.
* Replication: Clone data from one environment to another.

**Common pg_dump Options**
| Option          | Description                                                                                                              |
| --------------- | ------------------------------------------------------------------------------------------------------------------------ |
| `-U`            | Username                                                                                                                 |
| `-W`            | Prompt for password                                                                                                      |
| `-h`            | Hostname                                                                                                                 |
| `-p`            | Port                                                                                                                     |
| `-F`            | Format (`c` for custom, `t` for tar, `p` for plain SQL)                                                                  |
| `-f`            | Output file                                                                                                              |
| `-d`            | Database name                                                                                                            |
| `--schema-only` | Dump only the schema (DDL, no data)                                                                                      |
| `--data-only`   | Dump only the data (no DDL)                                                                                              |
| `--schema`      | Dump only objects in the specified schema (e.g. `--schema=public`)                                                       |
| `-t`            | Dump only the specified table (e.g. `-t users` or `-t public.users`). Can be used multiple times to dump several tables. |

Instead of passing creds and other configs you can store them as envrionment variables:

	PGHOST=10.197.30.73
	PGPORT=5475
	PGDATABASE=testdb
	PGUSER=user
	PGPASSWORD=password
	PGOPTIONS='--search_path=my_schema' # sets the runtime schema lookup path for queries
	
`PGOPTIONS` allows passing additional runtime options to the PostgreSQL server. In the example above it sets the runtime schema lookup path for queries.
Other environment variables may include:
* PG_COLOR: Controls color usage in diagnostic messages. The available options are always (always use color), auto (use color only if outputting to a terminal), never (disable color).

**Example Usages**
**Backup Entire Database (SQL format)**
	pg_dump -U postgres -h localhost -d mydb -f mydb_backup.sql
✅ This creates a plain .sql file you can run in psql to restore.

**Backup Schema only from enterprise_process_tracker schema in the db (SQL format)**
	pg_dump --schema-only -f schema.sql --schema=enterprise_process_tracker
	
**Backup data only from enterprise_process_tracker schema in the db (SQL format)**
	pg_dump --data-only -f data.sql --schema=enterprise_process_tracker
	
**Backup schema and data from enterprise_process_tracker schema in the db (SQL format)**
	pg_dump -f schema_data.sql --schema=enterprise_process_tracker
	
**Backup data only from enterprise_process_tracker schema from databasechangelog table (SQL format)**
	pg_dump --data-only -t enterprise_process_tracker.databasechangelog -f databasechangelog_data.sql --schema=enterprise_process_tracker
	
**Custom Format for Flexibility**
	pg_dump -U postgres -F c -f mydb_backup.dump mydb
* -F c → Custom format
* Use pg_restore to restore it (see below)

**Compressed Dump with Password Prompt**
	pg_dump -U postgres -W -F c -f secure_backup.dump mydb
You'll be prompted for the password for better security.

**Restoring a Backup**
**From Plain SQL:**
	psql -U postgres -d newdb -f mydb_backup.sql
**From Custom Format:**
	pg_restore -U postgres -d newdb mydb_backup.dump
Or with options:
	pg_restore -U postgres --create --dbname=postgres mydb_backup.dump
	
**Running an sql command using psql**
psql -c "SELECT * FROM nept_user;"


**Summary**
| Task              | Tool                               |
| ----------------- | ---------------------------------- |
| Full backup (SQL) | `pg_dump -f backup.sql mydb`       |
| Compressed backup | `pg_dump -F c -f backup.dump mydb` |
| Schema only       | `pg_dump --schema-only`            |
| Data only         | `pg_dump --data-only`              |
| Restore SQL       | `psql -f backup.sql`               |
| Restore dump      | `pg_restore -d mydb backup.dump`   |













