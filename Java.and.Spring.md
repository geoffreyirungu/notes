## Java And Spring


## Java SE (Standard Edition) and Java/Jakarta EE(Enterprise Edition)
**Java SE (Standard Edition)** is the foundational/core Java platform that provides essential libraries and APIs for general-purpose programming.
It forms the basis for other Java platforms, including Java EE and Java ME.
Java SE includes database access, networking, GUI development, and security libraries.
It is used for desktop applications, command-line tools, and basic backend development.

**Java EE (Enterprise Edition)**, now known as **Jakarta EE**, extends Java SE by providing additional features necessary for developing enterprise-level applications. 
It is designed for large-scale, distributed, multi-tier, scalable, secure applications — typically web and enterprise applications.
It includes specifications for building web applications, microservices, and business applications that can handle high transaction volumes and many concurrent users.
**Some key Features of Java EE:**
* Servlets and JSP: Used for building web applications.
* Enterprise JavaBeans (EJB): A framework for developing scalable and secure enterprise-level applications.
* JPA (Java Persistence API): Simplifies database interactions using Object-Relational Mapping (ORM).
* JMS (Java Messaging Service): Supports asynchronous messaging for enterprise systems.
* Web Services: Provides support for RESTful and SOAP-based web services.
**Some common Use Cases of Java EE:**
* E-commerce websites
* Banking applications
* Enterprise Resource Planning (ERP) systems
* Customer Relationship Management (CRM) systems
* Complex distributed systems requiring scalability, security, and transaction management

**Difference Between Java SE and Java EE**
| **Characteristic**      | **Java SE (Standard Edition)**                  | **Java EE (Enterprise Edition)**                              |
| ----------------------- | ----------------------------------------------- | ------------------------------------------------------------- |
| **Purpose**             | General-purpose programming                     | Enterprise-level and large-scale applications                 |
| **APIs**                | Basic APIs for standard applications            | Includes APIs for web, enterprise, and cloud applications     |
| **GUI Framework**       | Provides Swing and AWT for desktop GUIs         | Not used for GUIs; focused on web and enterprise apps         |
| **Web Development**     | No direct support for web development           | Supports Servlets, JSP, and web services                      |
| **Database Access**     | Uses JDBC for direct database access            | Uses JPA for ORM-based database interactions                  |
| **Enterprise Features** | Lacks enterprise-specific features              | Supports EJB, JMS, distributed transactions, etc.             |
| **Scalability**         | Suitable for small to medium applications       | Designed for large, scalable, distributed applications        |
| **Security**            | Basic security features (e.g., `java.security`) | Advanced security (e.g., role-based access, declarative auth) |

Other Java platforms include:
* Java ME(Micro Edition) - For embedded systems and mobile devices with limited resources. Not commonly used anymore — replaced in many cases by Android or IoT-specific platforms.
* JavaFX - used to create rich client applications with graphical user interfaces (GUIs). 


## What is Java Specification Request(JSR)
Java Specification Request (JSR) is a formal document that describes proposed specifications and technologies for the Java platform.
It’s a formal proposal for a new feature, API, or standard in the Java ecosystem.
It is created and managed through the Java Community Process (JCP), which is the mechanism that allows the Java community to develop and revise Java technologies collaboratively. 
These specifications can address various aspects of the Java ecosystem, including new technologies or improvements to existing ones, and they go through a review and approval process within the JCP. 
Each JSR includes:
	* A detailed specification of the technology.
	* A reference implementation.
	* A Technology Compatibility Kit (TCK) to ensure compliance.

**Why are JSRs important?**
	* They define new capabilities or improvements for Java.
	* They help maintain compatibility and standardization across different Java implementations.
	* They are developed and reviewed by the Java community, including vendors, developers, and users.
	
**Example:** A JSR might define a new API for working with a specific type of data, or it could propose a new way to handle concurrency in Java. 

**Examples of famous JSRs:**
* JSR 14 – Java language changes in Java 1.4
* JSR 299 – Contexts and Dependency Injection (CDI)
* JSR 376 – Java Platform Module System (introduced in Java 9)
* JSR 250 - also known as "Common Annotations for the Java Platform," is a JSR that defines a set of standard annotations.
	**Key JSR 250 annotations include:**
		* @Resource — for dependency injection (alternative to Spring's @Autowired or @Inject)
		* @PostConstruct — marks a method to be called after dependency injection is done, typically for initialization
		* @PreDestroy — marks a method to be called before the bean is removed, for cleanup
		* @RolesAllowed — declarative security annotation to specify allowed roles for methods or classes
		* @DeclareRoles — declares security roles for the application

**In short:**
A JSR is like a blueprint or a proposal document that explains how a new feature or standard should be added to the Java platform, and it goes through community review before becoming part of Java.


## What is Serializable in java
In Java, Serializable is a marker interface (an interface with no methods or fields) that indicates(tells JVM) that an object can be converted into a byte stream, a process known as serialization, and vice versa/deserialization(from byte stream to object). 
To make a class Serializable, it must implement the java.io.Serializable interface. When an object of a Serializable class is serialized, all its non-transient fields are also serialized. 
The transient keyword can be used to exclude fields from the serialization process.

Serialization is useful for: Persisting objects to storage, Transferring objects across a network, Caching objects, and Inter-process communication.

A serialVersionUID is often associated with Serializable classes. It is a unique identifier used during deserialization to ensure that the sender and receiver of a serialized object have compatible class definitions.
If the serialVersionUID values do not match, an InvalidClassException is thrown.
If it is not defined Java generates one automatically at runtime based on class details (fields, methods, etc.) and any changes to the class (even minor ones like renaming a method) can cause the generated ID to change. This may break deserialization across versions of the class
**Best practice:** Always explicitly define it when implementing Serializable.


	
## What is a record in java
A record in Java is a special type of class, introduced in Java 14 (preview) and officially in Java 16, that simplfies the process of creating immutable data classes.
It automatically generates essential methods like constructors(with all fields as parameters), accessors, equals(), hashCode(), and toString() based on the record's components, reducing boilerplate code.
Records are implicitly final and their components/fields are also final, ensuring immutability.	
This makes them suitable for representing data transfer objects (DTOs) or data structures where the state should not change after creation.

This record:
	public record Person(String name, int age) {}	
	
Is equivalent to writing:

	public final class Person {
		private final String name;
		private final int age;

		public Person(String name, int age) {
			this.name = name;
			this.age = age;
		}

		public String name() { return name; }
		public int age() { return age; }

		// plus equals(), hashCode(), and toString()
	}
	
## What is Optional in java
Optional<T> is a container object introduced in Java 8 that may or may not contain a non-null value.
It is used to represent the presence or absence of a value, providing a way to handle null values more gracefully and avoid NullPointerException.
**Creating Optional instances:**
* `Optional.of(value)`: Creates an Optional with the specified non-null value. Throws NullPointerException if value is null.
* `Optional.ofNullable(value)`: Creates an Optional with the specified value, which can be null. If the value is null, it creates an empty Optional.
* `Optional.empty()`: Creates an empty Optional.

	
## What is Hibernate in java
Hibernate is a Java-based ORM (Object-Relational Mapping) framework. 
It allows developers to map Java objects (classes) to database tables and vice versa, enabling interaction with the database using high-level Java code instead of writing raw SQL.

**NB:** Object-Relational Mapping (ORM) is a programming technique that simplifies interaction between object-oriented programming languages (like Java, Python, C#) and relational databases (like MySQL, PostgreSQL). 
It allows developers to interact with data in a more natural way, using objects and their properties instead of writing SQL queries directly. 

While Hibernate is a powerful Object-Relational Mapping (ORM) framework, it is not primarily a database migration tool in the same way as specialized tools like Flyway or Liquibase. 
Hibernate offers features for schema generation and update, which can be helpful during development and testing.
However, these features are not designed for managing complex, versioned database migrations in production environments. 

## What is JPA and Spring JPA/Spring Data JPA
### JPA (Java Persistence API)
JPA is a Java specification for accessing, persisting, and managing data between Java objects and relational databases.
JPA itself doesn't do anything; it requires an implementation like Hibernate or EclipseLink to function.

### Spring Data JPA
Spring Data JPA is a higher-level abstraction built on top of JPA.
Spring Data JPA offers features like automatic repository implementation, query derivation from method names, and pagination support, making database interactions more efficient and less verbose. 



## What is @MappedSuperClass in JPA
@MappedSuperclass is a JPA annotation used to define base entity classes that share common fields (like id, createdAt, updatedAt, etc.) with other entity classes. 
However, unlike @Entity classes, @MappedSuperclass itself is not recognized as an entity and does not have its own database table.
When a class is annotated with @MappedSuperclass, its persistent fields and mapping information are copied into the entity classes that extend it.
This avoids code duplication and promotes a more organized and maintainable structure for entities with common attributes.

Example:

	@MappedSuperclass
	public abstract class BaseEntity {
		@Id
		@GeneratedValue(strategy = GenerationType.IDENTITY)
		private Long id;

		@Column(name = "created_at")
		private LocalDateTime createdAt;

		// Getters and setters
	}

	@Entity
	public class Product extends BaseEntity {
		private String name;
		private double price;

		// Getters and setters
	}


In this example, BaseEntity is a @MappedSuperclass containing the common id and createdAt fields. 
Product entity extends BaseEntity, will inherit these fields(id and createdAt) and their mappings.
The product entity table will now contain id, createdAt, name and price. No table will be created for BaseEntity.

## JPA @Version
In JPA, the `@Version` annotation is used for optimistic locking, a strategy to prevent concurrent updates to the same record in a database. 
It is applied to a field in an entity class, typically an integer or a timestamp, which represents the version of the entity.
It ensures that if multiple transactions attempt to update the same entity simultaneously, only the first transaction to commit its changes will succeed. Subsequent transactions will fail, preventing data corruption due to lost updates(concurrency control).
Example

	@Entity
	public class Product {

		@Id
		private Long id;

		private String name;

		private double price;

		@Version
		private int version;

		// Getters and setters
	}
In this example, the version field is annotated with `@Version`. When a Product entity is updated, JPA will automatically increment the version field. If another transaction has updated the same Product entity in the meantime, the update will fail, and a javax.persistence.OptimisticLockException will be thrown. 

## JPA @Temporal
In JPA, `@Temporal` is used to specify the temporal precision of java.util.Date or java.util.Calendar fields when they are mapped to database columns.
**Why it's used:** Java's Date and Calendar types contain both date and time information, but relational databases often store these with different column types (e.g., DATE, TIME, TIMESTAMP). The `@Temporal` annotation tells JPA how to interpret and persist that data.
`@Temporal` annotation accepts a `TemporalType` enum, which can be one of the following:
* **DATE**: only the date part is stored (year, month, day), discarding the time component.
* **TIME**: only the time part is stored (hour, minute, second), discarding the date component.
* **TIMESTAMP**: stores both date and time (full precision).

If `@Temporal` is not specified for a java.util.Date or java.util.Calendar field, the default behavior is to map it as a TIMESTAMP. 

Example

	import javax.persistence.Entity;
	import javax.persistence.GeneratedValue;
	import javax.persistence.GenerationType;
	import javax.persistence.Id;
	import javax.persistence.Temporal;
	import javax.persistence.TemporalType;
	import java.util.Date;

	@Entity
	public class Event {
		@Id
		@GeneratedValue(strategy = GenerationType.IDENTITY)
		private Long id;

		private String name;

		@Temporal(TemporalType.DATE)
		private Date eventDate;

		@Temporal(TemporalType.TIME)
		private Date eventTime;

		@Temporal(TemporalType.TIMESTAMP)
		private Date createdAt;

		// Getters and setters
	}

In this example, eventDate will store only the date, eventTime will store only the time, and createdAt will store both date and time.

**NB:** `@Temporal` is only used with java.util.Date or java.util.Calendar.
It is not needed (and should not be used) with Java 8+ date/time types like java.time.LocalDate, LocalDateTime, or Instant. Those types are supported natively by JPA 2.2+ and newer Hibernate versions.


## @Converter, AttributeConverter and @Convert in JPA
The `@Converter` annotation(applied to a class that implements `javax.persistence.AttributeConverter` interface) is used to define a custom converter class that can be used to convert between a Java type and a database type. 
The converter class can be marked with `@Converter(autoApply = true)` if you want it to be automatically applied to all entity attributes of the type it is converting.
The AttributeConverter interface requires implementation of two methods:
* `convertToDatabaseColumn(X attribute)`: Converts the Java attribute value (X) to the database column value (Y).
* `convertToEntityAttribute(Y dbData)`: Converts the database column value (Y) back to the Java attribute value (X).

The `@Convert` annotation is used on an entity attribute to specify which AttributeConverter should be used for that attribute.
It takes the converter attribute, which specifies the class of the AttributeConverter to use.

Example:

	@Converter
	public class BooleanToStringConverter implements AttributeConverter<Boolean, String> {

		@Override
		public String convertToDatabaseColumn(Boolean attribute) {
			return (attribute != null && attribute) ? "Y" : "N";
		}

		@Override
		public Boolean convertToEntityAttribute(String dbData) {
			return "Y".equals(dbData);
		}
	}

	@Entity
	public class MyEntity {
		@Id
		private Long id;

		@Convert(converter = BooleanToStringConverter.class)
		private Boolean active;

		// Getters and setters
	}
	
## What is @EntityListeners in JPA
In JPA, @EntityListeners is used to specify/register one or more listener classes that react to specific lifecycle events of an entity.
These events include operations such as persisting, updating, and deleting an entity.
The listener classes define methods annotated with @PrePersist, @PostPersist, @PreUpdate, @PostUpdate, @PreRemove, and @PostRemove, which are executed before or after the corresponding entity lifecycle events.
It allows custom behavior (like auditing or logging) to be executed automatically when an entity is persisted, updated, removed, etc. without cluttering the entity classes themselves.

### **Example of Custom listener:**

**Step 1: Entity Listener Class**

	public class AuditListener {

		@PrePersist
		public void beforeCreate(Object entity) {
			System.out.println("Before entity is persisted: " + entity);
		}

		@PostLoad
		public void afterLoad(Object entity) {
			System.out.println("After entity is loaded: " + entity);
		}
	}

**Step 2: Annotate Your Entity**

	@Entity
	@EntityListeners(AuditListener.class)
	public class Product {
		@Id
		private Long id;

		private String name;
	}

Now, whenever a Product is loaded or saved, those methods in AuditListener will be called.
	

## Spring Data JPA Auditing and its annotations
Auditing allows you to track and review modifications made to your data, providing a valuable history of who changed what and when.

The below annotations are part of spring data jpa and are used for auditing purposes:
1. **@CreatedBy**:  This annotation marks a field that stores the user who created the entity. It's typically used with a String or User type field.
2. **@LastModifiedBy**: This annotation marks a field that stores the user who last modified the entity. Similar to @CreatedBy, it's used with a String or User type field.
3. **@CreatedDate**: This annotation marks a field that stores the date and time when the entity was created. It's used with java.util.Date, java.time.LocalDateTime, or similar date/time types.
4. **@LastModifiedDate**: This annotation marks a field that stores the date and time when the entity was last modified. It also uses java.util.Date, java.time.LocalDateTime, or similar date/time types.
 
You should add the `@EntityListeners(AuditingEntityListener.class)` annotation on your auditable class (or its superclass) to register the AuditingEntityListener, which is the internal class that populates the fields.
Additionally, for `@CreatedBy` and `@LastModifiedBy` to work, an implementation of `AuditorAware` needs to be provided to determine the current user.
The annotations also require enabling auditing in the Spring application, typically by adding `@EnableJpaAuditing` to a configuration class.

## Hibernate Envers
Envers/Hibernate Envers is an extension to Hibernate ORM that provides an easy way to add auditing / versioning(of data/each change not the same as versioning in the strict sense of optimistic locking) for entities.

**`@Audited` annotation in Hibernate Envers**
The @Audited annotation in Hibernate Envers enables auditing for entities/fields, meaning changes to their attributes are tracked and stored in an audit table.
When applied, Hibernate Envers will automatically create audit tables and keep track of changes made to those entities or fields.
This means every time the entity is inserted, updated, or deleted, a snapshot of its state is stored in a corresponding audit table.
**Where to Use It**
* On entity classes: Audits all fields by default.
* On specific fields within an entity: Audits only those fields.
* On embeddable types (with some additional configuration).

**Basic Usage Example**
	import org.hibernate.envers.Audited;
	import jakarta.persistence.Entity;
	import jakarta.persistence.Id;

	@Entity
	@Audited
	public class Product {

		@Id
		private Long id;

		private String name;

		private Double price;

		// getters and setters
	}
**What Happens Behind the Scenes**
**1. Audit Table Creation**
For each audited entity, Envers creates a separate audit table named usually as:
	[entity_table_name]_AUD
For example, for a table `Product`, Envers creates `Product_AUD`.
**2. Audit Columns**
The audit table contains all entity columns, plus:
* `REV`: a foreign key referencing the revision info (revision metadata).
* `REVTYPE`: type of revision (0=ADD, 1=MOD, 2=DEL).
**3. Revision Info Table Creation**
Envers tracks all changes in a `REVINFO` table which stores metadata about each revision (like revision number, timestamp, user info if configured).

**Advanced @Audited Features**
* Exclude fields with `@NotAudited` to audit the entity but skip specific properties.
* Audit with modified flags: `@Audited(withModifiedFlag = true)` adds boolean flags to know which fields changed in each revision.
* Audit Embeddables: you can audit fields inside embedded types.
* Relation auditing: can audit associations such as @OneToMany, @ManyToOne.

**How to Query Audit Data**
Hibernate Envers provides an AuditReader API to query historical data. Below is a simple example:

	AuditReader reader = AuditReaderFactory.get(entityManager);

	Product oldProduct = reader.find(Product.class, 1L, 3); // entityClass, primaryKey, revisionNumber
	
What this does: Fetches the state of the Product with ID 1 at revision 3.

**Summary**
| Feature                                  | Description                                     |
| ---------------------------------------- | ----------------------------------------------- |
| `@Audited`                               | Marks an entity or field for audit/versioning.  |
| Audit Tables                             | Auto-created tables to store historical states. |
| Revision Info                            | Stores metadata about each revision.            |
| `@NotAudited`                            | Skip auditing specific fields.                  |
| Modified Flags (`withModifiedFlag=true`) | Track which fields were changed per revision.   |
| AuditReader API                          | Query audit history programmatically.           |


## What is @OnDelete in Hibernate
The Hibernate-specific annotation @OnDelete allows you to instruct Hibernate to apply database-level cascading deletes when a referenced entity is deleted.
**In other words:** When you delete a parent entity, Hibernate delegates the deletion of child rows to the database using the `SQL ON DELETE CASCADE` feature.

## @SoftDelete in hibernate
The @SoftDelete annotation in hibernate marks an entity or a collection(@ElementCollection) for soft-deletion rather than permanently removing them from the database(hard deletion).
Internally, it handles the “deletions” from a database table by setting a column in the table to indicate deletion.
By default the column name that indicates deletion is "deleted" which can store true or false.
You can customize the column name that indicates deletion:

	@SoftDelete
or
	@SoftDelete(strategy = SoftDeleteType.DELETED) ## The default naming strategy that creates the column with name ‘deleted‘.
	
	@SoftDelete(strategy=SoftDeleteType.ACTIVE) ## Creates the column with name ‘active‘.
	
	@SoftDelete(columnName = “archived”)  ## The custom naming strategy that creates the column with name ‘archived‘.
	
You can also customize how the indicator value is stored in the database:

	@SoftDelete
or 
	@SoftDelete(converter = NumericBooleanConverter.class) ## It is the default. Stores the values as boolean 0 or 1.
	
	@SoftDelete(converter = TrueFalseConverter.class) ## Stores the values as ‘F’ for false and ‘T’ for true.
	
	@SoftDelete(converter = YesNoConverter.class) ## Stores the values as ‘N’ for false and ‘Y’ for true.
	
	
## @Transactional in JPA/Spring JPA
In JPA (Java Persistence API), the @Transactional annotation is used to define the scope of a database transaction. 
`@Transactional` can be applied at both the class and method levels. When applied at the class level, it applies to all methods within the class. 
It's commonly used in service layer classes to manage transactions for business logic operations.It ensures that a series of operations are treated as a single unit of work, meaning that either all operations succeed, or if any operation fails, all changes are rolled back, maintaining data consistency.

	import org.springframework.transaction.annotation.Transactional;

	@Service
	public class MyService {

		@Autowired
		private MyRepository myRepository;

		@Transactional
		public void performDatabaseOperations(MyEntity entity1, MyEntity entity2) {
			myRepository.save(entity1);
			myRepository.save(entity2);
			// If any exception occurs here, both saves will be rolled back
		}
	}
	
## What is flush in JPA, commit and lazy loading
* `flush()` means pushing changes from the persistence context (memory) to the database, without committing the transaction.

* `commit()` means finalizing a transaction: all flushed changes are persisted permanently in the database.
In Spring, you don't call commit() manually — it's handled by the transaction manager.

* Lazy loading means related entities (like @OneToMany or @ManyToOne) are not loaded from the database immediately. They’re fetched only when accessed — and require an open transaction.	
Fetching of lazy loaded fields will fail if accessed outside a transaction since Hibernate can’t fetch the field data because the underlying JDBC connection is already closed.

## @Entity and @Table in JPA
**@Entity**: This annotation is mandatory for any class that you want to persist in the database(Marks a Java class as a JPA entity).
It also allows you to specify a custom name for the entity by giving the name attribute.
**NB:** The name of the entity is used for referencing the entity in JPQL (Java Persistence Query Language) and other JPA operations and is not the same as table name.
**@Table**: This annotation is optional and specifies the name of the table (and other metadata like schema, unique constraints) the entity maps to.
if omitted, JPA uses the class name as the table name (case-sensitive, depending on DB).

Example:

	@Entity
	@Table(name = "app_user")
	public class User {
		@Id
		private Long id;

		private String username;
	}

Now, the User entity maps to a table named app_user, instead of user.

Example:

	@Entity(name = "UserEntity")  // Custom name for the entity
	@Table(name = "users")        // Custom name for the table
	public class User {
		@Id
		private Long id;
		private String username;
	}
	
`@Entity(name = "UserEntity")`: You’re giving the JPA entity the name UserEntity. This is useful when you need to reference the entity in JPQL queries.
If you hadn't specified the name attribute in @Entity, the default entity name would be the class name (User).


## @Lob in JPA
The @Lob annotation in JPA is used to indicate that a field should be persisted as a Large OBject (LOB).
This is typically used for fields that store large amounts of data such as binary data (images, videos, etc.) or large text data (such as a document, a description, or an HTML file).
In JPA, there are two types of LOBs:
* **BLOB (Binary Large Object):** Used to store binary data like images, PDFs, etc.
* **CLOB (Character Large Object):** Used to store large amounts of text data.

The @Lob annotation allows JPA to choose the appropriate data type for that field in the underlying database: BLOB OR CLOB.
It can be used on fields of types String (as CLOB), byte[] (as BLOB), char[] (as CLOB), and other types supported by your JPA provider.
You don't have to explicitly use @Column with columnDefinition when using @Lob because JPA will automatically choose the appropriate column type (like BLOB for byte[] or CLOB for String).
If you specify @Column with columnDefinition, you are explicitly overriding JPA's default behavior and telling it to use the BLOB/CLOB column type for the field.


Example:

	@Entity
	public class Product {
		
		@Id
		private Long id;
		
		private String name;

		@Lob
		@Column(name = "image_data")
		private byte[] image;  // This will be stored as BLOB
	}
	
	@Entity
	public class Article {

		@Id
		private Long id;

		private String title;

		@Lob
		@Column(name = "content")
		private String content;  // This will be stored as CLOB
	}


Searching on @Lob fields directly is not efficient and may not be supported by all databases.
The best approach is to store searchable metadata in smaller, indexed columns and use those for efficient searches eg. The title field in the Article Entity.

## What is UUID
A Universally Unique Identifier (UUID) is a 128-bit/16 bytes value/label used to uniquely identify objects in computer systems.
The term Globally Unique Identifier (GUID) is also used, mostly in Microsoft systems.
In theory the IDs may not be globally unique, but the probability of duplicates is vanishingly small.
UUIDs are widely used in various applications, including databases, distributed systems, and web applications, for tasks like identifying data records, tracking user sessions, and ensuring data integrity. 
UUID is usually represented as a 36-character string (including hyphens), consisting of 5 segments: 8-4-4-4-12 hexadecimal digits eg.

	550e8400-e29b-41d4-a716-446655440000
	
	xxxxxxxx-xxxx-Mxxx-Nxxx-xxxxxxxxxxxx
	
In a UUID M indecates the UUID version and N is the UUID variant(structure/layout/encoding rules)

There are several versions of UUIDs, each with different generation strategies. Below are some of them:
* **Version 1:** Generated using the timestamp and MAC address of the host machine.
* **Version 3 and 5:** Generated by hashing a namespace identifier and a name, using different hashing algorithms (MD5 and SHA-1).
* **Version 4:** Completely random UUIDs.
* **Version 7:** Generated by combining a high-precision timestamp (in milliseconds) with random bits(random entropy) to generate chronologically ordered IDs. 
Generally, Version 7 UUIDs have better entropy (i.e. randomness) than Version 1 UUIDs.

## What is ULID(Universally Unique Lexicographically Sortable Identifier)
A ULID (Universally Unique Lexicographically Sortable Identifier) is a 128-bit identifier that is both unique and sortable.
It is encoded as a 26-character string, unlike the 36-character UUID. 
It is split into two main parts: timestamp(48 bits) in milliseconds since Unix epoch and randomness(80 bits).
ULIDs are encoded in Base32 (using Crockford’s Base32 alphabet) and case insensitive.

Here’s an example of a ULID:

	01HZX1D6FM5T1P8QF7BJZK1WB4

* **Timestamp part (48 bits):** 01HZX1D6FM
* **Random part (80 bits):** 5T1P8QF7BJZK1WB4

## When to use ULID over UUID v7 
* **Human-friendly:** The Base32 encoding is more compact(smaller) and easier to read and debug than the standard UUID format (which uses hexadecimal and is 36 characters long).
* **Better for logs and URLs:** The short and readable format is ideal for using ULIDs in public-facing systems, URLs, or logs.
* **Storage as strings:** When storing the IDs as strings

## When to use UUID v7 over ULID
* You want compatibility with UUID systems
* You need time-ordered UUIDs to avoid index fragmentation in the DB.
* You store IDs as native UUID or BINARY(16) in your DB for performance.
* You want to follow a standardized format (UUIDv7 is part of the upcoming official RFC).


## @UuidGenerator in hibernate
The @UuidGenerator annotation in hibernate is employed to automatically generate UUID (Universally Unique Identifier) values for entity primary keys. 
Hibernate is capable of creating UUIDs of two versions — 1 and 4. 
By default, Hibernate generates Version 4 UUIDs.

	@Entity
	class Sale {

		@Id
		@UuidGenerator
		private UUID id;

		private boolean completed;

		// getters and setters 
	}

Furthermore, when specifying @UuidGenerator, we can choose the concrete version of UUID to generate. This is defined by the style parameter. Let’s see the values that this parameter can take:
* RANDOM – generate UUID based on random numbers (version 4)
* TIME – generate time-based UUID (version 1)
* AUTO – this is the default option and is the same as RANDOM

	@Entity
	class WebSiteUser {

		@Id
		@UuidGenerator(style = UuidGenerator.Style.TIME)
		private UUID id;

		private LocalDate registrationDate;

		// getters and setters
	}

Also, Hibernate is intelligent enough to generate UUIDs for us if we use String as the Java ID type:

	@Entity
	class Element {

		@Id
		@UuidGenerator
		private String id;

		private String name;
	}
	
## What is a Filter?
A filter is a component that intercepts HTTP requests and responses in a web application.

**1. How Does a Filter Pass to the Next Filter?**
A filter passes the request and response to the next filter in the chain by calling:

	filterChain.doFilter(request, response);

Each filter performs its logic and then hands off the request/response to the next filter via filterChain.doFilter(...).

**2. How Does a Filter Terminate Execution and Stop Further Filters?**
If you do not call filterChain.doFilter(...), the execution stops at that filter. No other filters or controllers will run.
This is how filters can **block unauthorized** requests or **short-circuit** processing.

	if (!authenticated) {
		response.setStatus(HttpServletResponse.SC_UNAUTHORIZED);
		response.getWriter().write("Unauthorized");
		return; // important: don't call filterChain.doFilter(...)
	}

	// If authenticated:
	filterChain.doFilter(request, response);
	
**3. Request vs. Response Handling in Filters**
A filter runs once per request, but the doFilter(...) method runs in two phases:

| Phase    | Code before/after `filterChain.doFilter()` |
| -------- | ------------------------------------------ |
| Request  | Code **before** `filterChain.doFilter()`   |
| Response | Code **after** `filterChain.doFilter()`    |

**Concept**

	doFilter(request, response) {
		// 🔹 Runs on REQUEST path
		log("Request in");

		filterChain.doFilter(request, response);

		// 🔹 Runs on RESPONSE path
		log("Response out");
	}

Example with Logging:

	@Override
	protected void doFilterInternal(HttpServletRequest request,
									HttpServletResponse response,
									FilterChain filterChain) throws ServletException, IOException {
		long startTime = System.currentTimeMillis();
		System.out.println("Request URI: " + request.getRequestURI());

		filterChain.doFilter(request, response);

		long duration = System.currentTimeMillis() - startTime;
		System.out.println("Response Status: " + response.getStatus());
		System.out.println("Duration: " + duration + "ms");
	}

**Types of Filters in Spring:**
| Type                    | Description                                  |
| ----------------------- | -------------------------------------------- |
| `javax.servlet.Filter`  | Basic Servlet filter interface               |
| `OncePerRequestFilter`  | Ensures execution once per HTTP request      |
| Spring Security filters | Filters for auth, CSRF, etc. (part of chain) |

**Order of Filters**
Spring filters are ordered — you can control the order using the @Order annotation:

	@Order(1) // Lower means higher priority
	@Component
	public class LoggingFilter extends OncePerRequestFilter {

Or via a FilterRegistrationBean:

	import org.springframework.boot.web.servlet.FilterRegistrationBean;
	import org.springframework.context.annotation.Bean;
	import org.springframework.context.annotation.Configuration;

	@Configuration
	public class FilterConfig {

		@Bean
		public FilterRegistrationBean<LoggingFilter> loggingFilter(){
			FilterRegistrationBean<LoggingFilter> registrationBean = new FilterRegistrationBean<>();

			registrationBean.setFilter(new LoggingFilter());
			registrationBean.addUrlPatterns("/api/*");
			registrationBean.setOrder(1);  // Order of filter execution

			return registrationBean;
		}
	}



**Uses of Filters:**
* **Authentication and Authorization:** Filters can check if a user is authenticated and has the necessary permissions to access a resource.
* **Logging:** Filters can log incoming requests and outgoing responses for debugging and monitoring purposes.
* **Request and Response Modification:** Filters can modify request parameters or response headers before they reach the controller or client.
* **Input Validation:** Filters can validate request data before it's processed by the application.
* **Compression and Encryption:** Filters can compress or encrypt data for security or performance reasons.
* **Cross-Origin Resource Sharing (CORS):** Filters can handle CORS to allow requests from different domains.
* **Centralized Code:** Filters can centralize code that would otherwise be duplicated in different parts of the controller, such as security checks.


**Real-World Use Cases**

**Authentication Filter**

	public class AuthFilter extends OncePerRequestFilter {
		@Override
		protected void doFilterInternal(HttpServletRequest request,
										HttpServletResponse response,
										FilterChain filterChain)
				throws ServletException, IOException {

			String token = request.getHeader("Authorization");
			if (token == null || !token.equals("VALID_TOKEN")) {
				response.setStatus(HttpServletResponse.SC_UNAUTHORIZED);
				response.getWriter().write("Unauthorized");
				return;// Execution stops and sends the error message
			}

			filterChain.doFilter(request, response);  // passes to the next filter
		}
	}

**CORS Filter**

	@Component
	public class CorsFilter extends OncePerRequestFilter {
		@Override
		protected void doFilterInternal(HttpServletRequest request,
										HttpServletResponse response,
										FilterChain filterChain)
				throws ServletException, IOException {

			response.setHeader("Access-Control-Allow-Origin", "*");
			response.setHeader("Access-Control-Allow-Methods", "GET,POST,PUT,DELETE,OPTIONS");
			response.setHeader("Access-Control-Allow-Headers", "*");

			if ("OPTIONS".equalsIgnoreCase(request.getMethod())) {
				response.setStatus(HttpServletResponse.SC_OK);
				return;
			}

			filterChain.doFilter(request, response);
		}
	}

## What is a DispatcherServlet
In Spring MVC, the DispatcherServlet acts as the central front controller, handling all incoming requests and routing them to the appropriate controller based on the request URL and other factors.

**A front controller** is a design pattern used in web application development to centralize request handling. It acts as a single entry point for all incoming requests to a web application, directing them to the appropriate handler or module. 
This pattern simplifies request processing, improves code organization, and facilitates the implementation of cross-cutting concerns like logging and authentication. 

**Responsibilities of DispatcherServlet:**
* Receives incoming HTTP requests.
* Delegates requests to appropriate controllers (@Controller, @RestController).
* Handles view resolution (.jsp, .html, etc.).
* Invokes interceptors and exception handlers.
* Returns the final HTTP response to the client.

**Note:** Filters are applied before the DispatcherServlet processes the request.

**Typical Order:**
1. Filters (e.g., Authentication, Logging)
2. DispatcherServlet
3. Controller / HandlerMethod
4. Interceptors (optional)
5. ViewResolver (optional)
6. Response sent back

**Example:**
**🔸 Custom Filter (runs before DispatcherServlet):**

	@Component
	public class LoggingFilter extends OncePerRequestFilter {
		@Override
		protected void doFilterInternal(HttpServletRequest request,
										HttpServletResponse response,
										FilterChain filterChain)
				throws ServletException, IOException {

			System.out.println("Filter: Request URI is " + request.getRequestURI());

			// Proceed to DispatcherServlet
			filterChain.doFilter(request, response);

			System.out.println("Filter: Response status is " + response.getStatus());
		}
	}

**🔸 Controller (runs after DispatcherServlet receives the request):**

	@RestController
	public class MyController {
		@GetMapping("/hello")
		public String sayHello() {
			return "Hello from Controller!";
		}
	}

**🔄 Flow:**

	Client sends GET /hello
	→ LoggingFilter (pre-process)
	→ DispatcherServlet
	→ MyController
	← Response "Hello from Controller!"
	→ LoggingFilter (post-process)
	→ Client

## What are Interceptors
Interceptors in Spring are components that intercept HTTP requests and responses at the controller level.
They work inside the Spring MVC context, just before and after the controller method is executed.
**Interceptors are similar to filters** but are part of Spring's MVC framework, while filters are part of the Servlet API.

**🔸 Key Methods in HandlerInterceptor**

	public interface HandlerInterceptor {
		boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler);

		void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView);

		void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex);
	}

| Method              | Description                                                                | Works in REST | Common Use Cases                                                               |
| ------------------- | -------------------------------------------------------------------------- | ------------- | ------------------------------------------------------------------------------ |
| `preHandle()`       | Runs **before** the controller method is invoked. Return `false` to block. | ✅ Yes         | Authentication, authorization, logging setup (MDC), request validation         |
| `postHandle()`      | Runs **after** the controller method but **before** the view is rendered.  | ⚠️ Limited    | Modifying `ModelAndView` (MVC only), injecting common data into the view model |
| `afterCompletion()` | Runs **after** the view is rendered (like a finally block).                | ✅ Yes         | Logging, cleanup (e.g., `MDC.clear()`), auditing, exception tracking           |


**🌟 Common Uses:**
* Logging
* User session validation
* Authentication
* Authorization checks
* Modifying model attributes

**🔹 Full Example of Interceptor in Spring Boot**
**Step 1: Create the Interceptor**

	import org.springframework.stereotype.Component;
	import org.springframework.web.servlet.HandlerInterceptor;
	import jakarta.servlet.http.HttpServletRequest;
	import jakarta.servlet.http.HttpServletResponse;

	@Component
	public class AuthInterceptor implements HandlerInterceptor {

		@Override
		public boolean preHandle(HttpServletRequest request,
								 HttpServletResponse response,
								 Object handler) throws Exception {
			String authHeader = request.getHeader("Authorization");

			if (authHeader == null || !authHeader.equals("VALID_TOKEN")) {
				response.setStatus(HttpServletResponse.SC_UNAUTHORIZED);
				response.getWriter().write("Unauthorized Access");
				return false; // Block the request
			}

			System.out.println("Authorization successful.");
			return true; // Allow the request to proceed
		}

		@Override
		public void afterCompletion(HttpServletRequest request,
									HttpServletResponse response,
									Object handler,
									Exception ex) {
			System.out.println("Request completed for URI: " + request.getRequestURI());
		}
	}

**Step 2: Register the Interceptor**

	import org.springframework.beans.factory.annotation.Autowired;
	import org.springframework.context.annotation.Configuration;
	import org.springframework.web.servlet.config.annotation.InterceptorRegistry;
	import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

	@Configuration
	public class WebConfig implements WebMvcConfigurer {

		@Autowired
		private AuthInterceptor authInterceptor;

		@Override
		public void addInterceptors(InterceptorRegistry registry) {
			registry.addInterceptor(authInterceptor)
					.addPathPatterns("/api/**"); // Apply to specific routes
		}
	}

**Step 3: A Sample Controller**

	import org.springframework.web.bind.annotation.GetMapping;
	import org.springframework.web.bind.annotation.RestController;

	@RestController
	public class TestController {

		@GetMapping("/api/hello")
		public String hello() {
			return "Hello from secured controller!";
		}
	}

**Test Flow**
* Request: GET /api/hello without Authorization header → 401 Unauthorized
* Request: GET /api/hello with header Authorization: VALID_TOKEN → allowed

| Aspect                 | Filter                                   | Interceptor                          |
| ---------------------- | ---------------------------------------- | ------------------------------------ |
| API                    | Servlet API (`javax.servlet.Filter`)     | Spring MVC (`HandlerInterceptor`)    |
| Runs                   | Before/after `DispatcherServlet`         | Before/after controller execution    |
| Purpose                | General cross-cutting concerns           | Controller-specific logic            |
| Spring-aware           | ❌ No                                     | ✅ Yes                                |
| Access controller info | ❌ No                                    | ✅ Yes (can access `HandlerMethod`)  |
| Setup                  | `@Component` or `FilterRegistrationBean` | `WebMvcConfigurer.addInterceptors()` |




## What is @RequestHeader in Spring
The @RequestHeader annotation in Spring is used to bind a method parameter to a specific HTTP request header.
It allows you to access header information sent by the client.
**Basic Syntax:**

	@GetMapping("/example")
	public ResponseEntity<String> handleRequest(@RequestHeader("User-Agent") String userAgent) {
		return ResponseEntity.ok("Your User-Agent is: " + userAgent);
	}
**Request**

	GET /example
	User-Agent: Mozilla/5.0

**Response**

	Your User-Agent is: Mozilla/5.0





## What is @ResponseBody and @RequestBody in Spring
In Spring, @ResponseBody is an annotation that signals that a method's return value should be bound to the HTTP response body. 
Instead of treating the return value as a view name or model attribute, Spring directly writes it into the response.
In Spring Boot, the @ResponseBody annotation is used to convert Java objects into JSON responses.
This is commonly used in RESTful web services to return data, often in JSON or XML format.
Spring uses HttpMessageConverter implementations to convert the return object to the appropriate format based on the Accept header of the request.

When @ResponseBody is used at the class level (e.g., on a @RestController), it applies to all handler methods within that class. If used at the method level, it only applies to that specific method.

	@GetMapping("/greeting")
	@ResponseBody
	public String getGreeting() {
		return "Hello, world!";   // Response is the raw string
	}

	@GetMapping("/user")
	@ResponseBody
	public User getUser() {
		return new User("Alice", "alice@example.com");  // Responds with the User json object
	}
	
**Note:** If you use @RestController, you don’t need to use @ResponseBody explicitly — it’s implied.

In Spring, the @RequestBody annotation is used to bind the HTTP request body to a java object of the specified parameter type. 

	@PostMapping("/users")
	public ResponseEntity<String> createUser(@RequestBody User user) {
		return ResponseEntity.ok("Received user: " + user.getName());
	}


## What is @Controller and @RestController in Spring
A controller is responsible for handling HTTP request and returning HTTP response to client.
@Controller is used to create web controllers that return views, which is further resolved by view resolver.
@RestController combines @Controller and @ResponseBody to create web services that return JSON or XML data(RESTful services).

	@Controller
	public class WebController {

		@GetMapping("/home")
		public String home(Model model) {
			model.addAttribute("message", "Welcome to the web page!");
			return "home";  // Resolves to home.html in templates/
		}
	}
	
	
	@RestController
	public class ApiController {

		@GetMapping("/api/message")
		public Message getMessage() {
			return new Message("Hello from REST API!"); // Returns the JSON message object
		}
	}

## What is @ExceptionHandler in Spring
In Spring, the @ExceptionHandler annotation is used to handle exceptions thrown in controller methods. 
It allows you to define custom responses when specific exceptions occur.
Instead of scattering try-catch blocks throughout your controller methods, @ExceptionHandler centralizes exception handling logic in dedicated methods.
** Basic Usage Example**

	import org.springframework.http.HttpStatus;
	import org.springframework.http.ResponseEntity;
	import org.springframework.web.bind.annotation.ExceptionHandler;
	import org.springframework.web.bind.annotation.GetMapping;
	import org.springframework.web.bind.annotation.RestController;

	@RestController
	public class MyController {

		@GetMapping("/data")
		public String getData() {
			throw new IllegalArgumentException("Invalid input");
		}

		@ExceptionHandler(IllegalArgumentException.class)
		public ResponseEntity<String> handleIllegalArgumentException(IllegalArgumentException ex) {
			return new ResponseEntity<>(ex.getMessage(), HttpStatus.BAD_REQUEST);
		}
	}

In this example, when the /data endpoint is accessed, it throws an IllegalArgumentException, which is then caught by the handleIllegalArgumentException method, 
and it returns a 400 Bad Request response with the exception message.

**Best Practices**
Use @ExceptionHandler in:
* A controller: handles exceptions for that controller only.
* A @ControllerAdvice/@RestControllerAdvice class: handles exceptions application-wide.

## What is `@InitBinder` in Spring
`@InitBinder` is an annotation in Spring MVC used to customize the data binding process. 
It marks methods that initialize a WebDataBinder, which is responsible for:
* Binding HTTP request parameters to Java object properties (e.g., form data to model objects)
* Registering custom editors and formatters for specific data types
* Configuring allowed/disallowed fields during binding
* Adding validators
This helps control and customize how Spring converts web request data (typically strings) into your domain/model objects.
**Why is `@InitBinder` useful?**
When your controller accepts complex objects as parameters, Spring needs to convert the raw HTTP request parameters (strings) into Java types. 
Sometimes the default conversion is not enough or you want:
* Custom date formatting/parsing
* Custom editors to convert strings to enums, numbers, or other types
* To whitelist or blacklist fields that can be bound (security)
* To register custom validators for form validation
`@InitBinder` allows you to hook into this binding lifecycle and customize the binder for one or more controller methods.
**Where and How to use @InitBinder?**
* Defined inside a Spring MVC controller class or controller advice (annotated with @Controller or @RestController or @ControllerAdvice or @RestControllerAdvice)
* Annotated methods take a WebDataBinder parameter
* Can be limited to specific command/form object names by specifying the value attribute (optional)

**A Command Object** is a Java object automatically bound from HTTP request parameters eg. "person" is a command object in the below example.

**Example**
Imagine a Spring MVC controller handling a form to create a Person object with a Date field, which needs custom date parsing.
	import org.springframework.stereotype.Controller;
	import org.springframework.web.bind.WebDataBinder;
	import org.springframework.web.bind.annotation.InitBinder;
	import org.springframework.web.bind.annotation.PostMapping;
	import org.springframework.web.bind.annotation.ModelAttribute;
	import org.springframework.web.bind.annotation.GetMapping;
	import org.springframework.web.bind.annotation.RequestMapping;
	import org.springframework.format.annotation.DateTimeFormat;
	import org.springframework.beans.propertyeditors.CustomDateEditor;

	import java.text.SimpleDateFormat;
	import java.util.Date;

	@Controller
	@RequestMapping("/persons")
	public class PersonController {

		// Model class
		public static class Person {
			private String name;
			private Date birthDate;

			// getters/setters
			public String getName() { return name; }
			public void setName(String name) { this.name = name; }

			public Date getBirthDate() { return birthDate; }
			public void setBirthDate(Date birthDate) { this.birthDate = birthDate; }
		}

		// InitBinder method to customize binding for Person objects
		@InitBinder("person")
		public void initBinder(WebDataBinder binder) {
			// Define a date format for birthDate field
			SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");
			dateFormat.setLenient(false); // Strict parsing

			// Register a custom editor for Date.class that uses the above format
			// Converts from "yyyy-MM-dd" format to java.util.Date
			binder.registerCustomEditor(Date.class, new CustomDateEditor(dateFormat, true));
		}

		@GetMapping("/create")
		public String showForm() {
			return "personForm";  // Returns a form view
		}

		@PostMapping("/create")
		public String submitForm(@ModelAttribute("person") Person person) {
			// "person" is a command object — populated automatically from request parameters
		
			// Here birthDate string will be converted automatically using our custom editor
			// from "yyyy-MM-dd" format to java.util.Date
			System.out.println("Name: " + person.getName());
			System.out.println("BirthDate: " + person.getBirthDate());
			return "personResult";
		}
	}
Without this customization, Spring would throw a binding error or use default parsing which might not match your expected format.

**What `@InitBinder` works with**
`@InitBinder`is not limited to model attributes coming from views or forms — it works with any controller method parameter that Spring binds using a WebDataBinder. 
That includes:
* Model attributes from forms (traditional MVC)
When you're binding form data to a model attribute, like in server-side rendered HTML forms.
* DTOs in @ModelAttribute
This works even in APIs or services that don’t render views — if you use `@ModelAttribute` explicitly.
* DTOs in @RequestParam (for complex types)
Binding a group of request parameters into a complex object using `@RequestParam`.
	@GetMapping("/table")
    public String listTable(@RequestParam("sort") SortOptions sortOptions) {
        // /table?sort.field=name&sort.direction=asc
        return "table";
    }
* DTOs in @RequestMapping, @PostMapping, etc., when not using @RequestBody
This applies when a controller receives a complex object from form data or query string, not JSON, and does not use @RequestBody.
	public class ProductFilter {
		private String category;
		private Integer maxPrice;
		// getters/setters
	}

	@GetMapping("/products")
    public String listProducts(ProductFilter productFilter) {
        // Automatically bound from query params like ?category=Books&maxPrice=100
        return "productList";
    }
**Note:** `@InitBinder` does not apply to DTOs annotated with @RequestBody — because those are deserialized using Jackson, not the WebDataBinder.
	@PostMapping("/api/person")
	public ResponseEntity<?> create(@RequestBody PersonDTO dto) {
		// @InitBinder will NOT be triggered here
	}
**Why `@InitBinder` Doesn't Apply to `@RequestBody`**
* As explained above `@InitBinder` is tied to form data, URL parameters, and command objects, which are processed using WebDataBinder.
* `@RequestBody` uses message converters (like Jackson) instead, bypassing the WebDataBinder pipeline entirely.
* One of the tools to use to customize json deserialization when dealing with `@RequestBody` is `@JsonDeserialize`


**How does Spring decide which `@InitBinder` method to call?**
* You can specify one or more command/form object names on @InitBinder (e.g. @InitBinder("person")).
* Spring calls all methods annotated with @InitBinder that apply to the model attribute being bound.
* If no specific target name is given, the @InitBinder method applies to all command/form objects.

**Additional Use Cases of `@InitBinder`**
* **Registering Custom Property Editors**
To convert string IDs to Enum or other domain objects.
	@InitBinder
	public void initBinder(WebDataBinder binder) {
		binder.registerCustomEditor(MyEnum.class, new MyEnumPropertyEditor());
	}
* **White/Blacklisting Fields**
To prevent binding of sensitive fields:
	@InitBinder
	public void initBinder(WebDataBinder binder) {
		binder.setDisallowedFields("id", "password");
	}
* **Adding Validators**
	@InitBinder
	public void initBinder(WebDataBinder binder) {
		binder.addValidators(new PersonValidator());
	}

## What is `@JsonDeserialize` in Jackson
`@JsonDeserialize` is a Jackson annotation used in Java (especially with Spring Boot and REST APIs) to customize how JSON data is deserialized into Java objects. 
It’s typically used when default deserialization behavior doesn’t work (e.g. with custom formats, special data structures, or complex objects).
**Use Cases**
* Handling non-standard JSON formats
* Parsing custom date formats
* Deserializing polymorphic types
* Pre-processing values before mapping

**Example**
**Step 1: Create a Custom Deserializer**
	import com.fasterxml.jackson.core.JsonParser;
	import com.fasterxml.jackson.databind.DeserializationContext;
	import com.fasterxml.jackson.databind.JsonDeserializer;

	import java.io.IOException;
	import java.text.SimpleDateFormat;
	import java.util.Date;

	public class CustomDateDeserializer extends JsonDeserializer<Date> {
		private static final SimpleDateFormat formatter = new SimpleDateFormat("dd-MM-yyyy");

		@Override
		public Date deserialize(JsonParser p, DeserializationContext ctxt) throws IOException {
			try {
				return formatter.parse(p.getText());
			} catch (Exception e) {
				throw new RuntimeException(e);
			}
		}
	}
**Step 2: Apply @JsonDeserialize on the Model**
	import com.fasterxml.jackson.databind.annotation.JsonDeserialize;
	import java.util.Date;

	public class User {
		private String name;

		@JsonDeserialize(using = CustomDateDeserializer.class)
		private Date dob;

		// Getters and setters
	}
**Step 3: Spring Boot Controller**
	import org.springframework.web.bind.annotation.*;

	@RestController
	public class UserController {

		@PostMapping("/register")
		public String registerUser(@RequestBody User user) {
			return "User: " + user.getName() + ", DOB: " + user.getDob();
		}
	}
**Step 4: Sample Request**
POST /register
Content-Type: application/json

{
  "name": "Alice",
  "dob": "19-07-2025"
}
**Output:**
	User: Alice, DOB: Sat Jul 19 00:00:00 UTC 2025

You can also deserialize things like:
* Enum types with custom labels
* JSON values wrapped in other structures (e.g., arrays of key-value)
* Trimming or transforming strings
* Base64-decoded binary data

	
## What is @ControllerAdvice and @RestControllerAdvice
In Spring, @ControllerAdvice is an annotation used for centralizing exception handling logic and shared behavior across multiple controllers.
It enables the definition of methods that can handle exceptions thrown by any controller in the application, promoting code reusability and simplifying error management. 
A class annotated with @ControllerAdvice can include methods annotated with @ExceptionHandler, @ModelAttribute, and @InitBinder.
* **@ExceptionHandler**: Methods annotated with @ExceptionHandler handle specific exceptions thrown by controllers. When an exception occurs, Spring will delegate the handling to the appropriate @ExceptionHandler method based on the exception type.
* **@ModelAttribute**: Methods annotated with @ModelAttribute define model attributes that are added to the model before invoking any request handling method within a controller. This is useful for providing common data to multiple views.
* **@InitBinder**: Methods annotated with @InitBinder configure data binding for request parameters. They allow customization of how request parameters are converted to Java objects.

Example:

	@ControllerAdvice
	public class GlobalViewExceptionHandler {

		@ExceptionHandler(UserNotFoundException.class) // handles the UserNotFoundException thrown by any controller
		public String handleUserNotFound(UserNotFoundException ex, Model model) {
			model.addAttribute("error", ex.getMessage());
			return "error"; // resolves to error.html
		}
		
		@ModelAttribute // injects common data (e.g., app name, current user) into all views automatically
		public void addCommonAttributes(Model model) {
			model.addAttribute("appName", "My Awesome App");
		}
		
		@InitBinder
		public void initBinder(WebDataBinder binder) {
			binder.setDisallowedFields("id"); // prevent binding to 'id' field
		}
	}

@ControllerAdvice can be used in both MVC and REST web services, but in the latter case, it may require the @ResponseBody annotation to serialize responses directly to the HTTP response body.
But it is best for/recommended for web MVC.

@RestControllerAdvice in Spring combines the functionalities of @ControllerAdvice and @ResponseBody for global exception handling and shared behavior in RESTful APIs.
This means it can handle exceptions thrown by any @RestController in the application and return the response directly in the response body, typically as JSON or XML.

	@RestControllerAdvice
	public class GlobalExceptionHandler {

		@ExceptionHandler(ResourceNotFoundException.class) // handles the ResourceNotFoundException thrown by any rest controller
		@ResponseStatus(HttpStatus.NOT_FOUND)
		public ErrorResponse handleResourceNotFoundException(ResourceNotFoundException ex) {
			return new ErrorResponse("NOT_FOUND", ex.getMessage());
		}

		@ExceptionHandler(BadRequestException.class) // handles the BadRequestException thrown by any rest controller
		@ResponseStatus(HttpStatus.BAD_REQUEST)
		public ErrorResponse handleBadRequestException(BadRequestException ex) {
			return new ErrorResponse("BAD_REQUEST", ex.getMessage());
		}

		// Other exception handlers
	}

## What is @ResponseBodyAdvice
`ResponseBodyAdvice<T>` is an interface in Spring that lets you intercept and modify the response body before it is written to the client — typically in JSON or XML responses.
It is typically used in conjunction with the `@ControllerAdvice`/`@RestControllerAdvice` annotation to apply global changes to the response body across multiple controllers.
**Interface Definition** 

	public interface ResponseBodyAdvice<T> {

		boolean supports(MethodParameter returnType, Class<? extends HttpMessageConverter<?>> converterType);

		T beforeBodyWrite(
			T body,
			MethodParameter returnType,
			MediaType selectedContentType,
			Class<? extends HttpMessageConverter<?>> selectedConverterType,
			ServerHttpRequest request,
			ServerHttpResponse response
		);
	}

**🔑 Two Key Methods:**
| Method              | Purpose                                                   |
| ------------------- | --------------------------------------------------------- |
| `supports()`        | Tells Spring **when** to apply the advice                 |
| `beforeBodyWrite()` | Lets you **modify or wrap** the response before it’s sent |

**How it works:**
* A class implementing the ResponseBodyAdvice interface is created.
* The supports method is implemented to specify when the advice should be applied.
* The beforeBodyWrite method is implemented to modify the response.
* The class is annotated with `@ControllerAdvice`/`@RestControllerAdvice` to make it globally applicable.

**Use cases:**
* **Wrapping responses:** Wrapping the response in a common format/structure.
* **Adding Metadata:** such as custom headers, adding a status code, error message, or data field.
* **Modifying payloads:** Modifying the response payload, such as encrypting or formatting data.
* **Logging:** Logging the response body before it is sent to the client.
* **Conditional modifications:** Applying modifications based on specific conditions, such as the content type or status code.

In practice `ResponseBodyAdvice` is typically used with:
* @RestController
* @Controller methods annotated with @ResponseBody

**Example Use Case**
**✅ Goal: Wrap all API responses in a standard format like:**

	{
	  "status": "success",
	  "data": { ... },
	  "timestamp": "2025-06-12T14:33:15Z"
	}

**Full Implementation**
**1. ✅ Define a common response wrapper**

	public class ApiResponse<T> {
		private String status;
		private T data;
		private String timestamp;

		public ApiResponse(String status, T data) {
			this.status = status;
			this.data = data;
			this.timestamp = java.time.ZonedDateTime.now().toString();
		}

		// Getters and setters...
	}

**2. ✅ Implement ResponseBodyAdvice**

	import org.springframework.core.MethodParameter;
	import org.springframework.http.MediaType;
	import org.springframework.http.converter.HttpMessageConverter;
	import org.springframework.http.server.ServerHttpRequest;
	import org.springframework.http.server.ServerHttpResponse;
	import org.springframework.web.bind.annotation.ControllerAdvice;
	import org.springframework.web.servlet.mvc.method.annotation.ResponseBodyAdvice;

	@ControllerAdvice
	public class GlobalResponseWrapperAdvice implements ResponseBodyAdvice<Object> {

		@Override
		public boolean supports(MethodParameter returnType, Class<? extends HttpMessageConverter<?>> converterType) {
			// Apply to all @RestController methods
			return true;
		}

		@Override
		public Object beforeBodyWrite(Object body,
									  MethodParameter returnType,
									  MediaType selectedContentType,
									  Class<? extends HttpMessageConverter<?>> selectedConverterType,
									  ServerHttpRequest request,
									  ServerHttpResponse response) {

			// Don't wrap already wrapped responses or error responses
			if (body instanceof ApiResponse || selectedContentType.includes(MediaType.TEXT_HTML)) {
				return body;
			}

			return new ApiResponse<>("success", body);
		}
	}
	
**3. ✅ Sample Controller**

	@RestController
	@RequestMapping("/api")
	public class UserController {

		@GetMapping("/user")
		public User getUser() {
			return new User("alice", "alice@example.com");
		}
	}
**4. ✅ Output**
If `/api/user` returns:

	{
	  "username": "alice",
	  "email": "alice@example.com"
	}

It will be automatically wrapped like:

	{
	  "status": "success",
	  "data": {
		"username": "alice",
		"email": "alice@example.com"
	  },
	  "timestamp": "2025-06-12T14:33:15.409Z"
	}






## What is @EnableWebSecurity and @EnableMethodSecurity
@EnableWebSecurity is a Spring Security annotation applied to a Spring configuration class that enables web security features in a Spring application.
It enables the web security features and allows you to customize the security configuration for your web application.
This customization includes features like HTTP security (e.g., URL access restrictions, form-based login, etc.), authentication, and authorization rules.
You would typically use @EnableWebSecurity in a class that extends WebSecurityConfigurerAdapter  (although this is deprecated in newer versions), which is the class where you can override methods to configure the security of your application.


	@Configuration
	@EnableWebSecurity
	public class SecurityConfig extends WebSecurityConfigurerAdapter {

		@Override
		protected void configure(HttpSecurity http) throws Exception {
			// Define which URLs are allowed and which require authentication
			http
				.authorizeRequests()
					.antMatchers("/", "/home").permitAll() // Permit all for certain URLs
					.anyRequest().authenticated() // Any other request requires authentication
					.and()
				.formLogin()
					.loginPage("/login") // Specify custom login page
					.permitAll() // Allow everyone to access login page
					.and()
				.logout()
					.permitAll(); // Allow logout for everyone
		}
	}

@EnableWebSecurity is not strictly required when defining a SecurityFilterChain bean in Spring Security, particularly in newer versions (5.7+) where the component-based configuration is favored.

	@Bean
	public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
		// full HTTP security config...
		return http.build();
	}

@EnableMethodSecurity is an annotation applied to a Spring configuration class that enables method-level security in your application. 
It is used to secure methods in service classes, controllers, or any other bean in the Spring context. 
This annotation replaces @EnableGlobalMethodSecurity and offers several improvements, including bean-based configurations, segmented configurations, and the AuthorizationManager interface.
@EnableMethodSecurity supports JSR-250 annotations (@RolesAllowed), as well as Spring Security's @PreAuthorize, @PostAuthorize, @PreFilter, and @PostFilter annotations. 

To use @EnableMethodSecurity, you annotate a @Configuration class with it. For example:

	import org.springframework.context.annotation.Configuration;
	import org.springframework.security.config.annotation.method.configuration.EnableMethodSecurity;

	@Configuration
	@EnableMethodSecurity
	public class MethodSecurityConfig {
	}
	
Once enabled, you can secure individual methods using annotations like @PreAuthorize:

	import org.springframework.security.access.prepost.PreAuthorize;
	import org.springframework.stereotype.Service;

	@Service
	public class MyService {

		@PreAuthorize("hasRole('ADMIN')")
		public String adminOnlyMethod() {
			return "This method is only accessible to admins";
		}

		@PreAuthorize("hasAnyRole('USER', 'ADMIN')")
		public String userOrAdminMethod() {
			return "This method is accessible to users and admins";
		}
	}

## Nimbus JOSE + JWT library
This library is a popular and robust tool for handling JSON Web Tokens (JWTs) and JSON Object Signing and Encryption (JOSE) standards.

**What can Nimbus do**

| **Feature**              | **Description**                                          |
| ------------------------ | -------------------------------------------------------- |
| `JWT` creation & parsing | Create, sign, parse, encrypt, verify, and validate JWTs  |
| `JWS`                    | Handle signed tokens (e.g., `RS256`, `PS256`)            |
| `JWE`                    | Handle encrypted tokens                                  |
| `JWK` / `JWKS`           | Load and manage keys in JSON Web Key format              |
| `RSA`, `EC`, `HMAC`      | Supports multiple cryptographic algorithms               |
| Public key rotation      | JWKS endpoint support for automatic public key retrieval |



## What is @ParameterObject in springdoc
The @ParameterObject annotation in Springdoc is used to automatically expand a complex object into individual query parameters in the generated OpenAPI/swagger documentation. 
When using SpringDoc for OpenAPI/Swagger generation, it doesn't know by default how to expose the individual fields as query parameters in the OpenAPI spec.
@ParameterObject fixes that.
It is applied to a method parameter in a Spring controller, indicating that the fields of the annotated object should be treated as separate query parameters.

	@GetMapping("/search")
	public List<Product> searchProducts(@ParameterObject SearchCriteria criteria) {
		// ...
	}

	record SearchCriteria(
		String name,
		String category,
		Double minPrice,
		Double maxPrice
	) {}
	
Without @ParameterObject, the generated OpenAPI documentation might represent the SearchCriteria as a single request body, which is not ideal for query parameters. 
However, with @ParameterObject, Springdoc will expand SearchCriteria into individual query parameters: name, category, minPrice, and maxPrice.
This annotation simplifies the process of documenting complex query parameters and enhances the usability of the generated OpenAPI documentation.

## Logging in Spring
By default, Spring Boot:
* Uses Logback as the underlying logging implementation.
* Exposes logging through SLF4J (@Slf4j, LoggerFactory, etc.).
* Logs to console.
* Logs at INFO level by default.
* Has built-in support for different profiles, environments, and external log config.

Default log format:

	2025-06-04T12:00:00.123 INFO 12345 --- [ main] com.example.MyApp : Starting MyApp

**Configuring logging**
1. **Basic Config via application.properties or application.yml**
You can control log levels per package:

	# application.properties
	# Setting the logging levels
	logging.level.root=INFO
	logging.level.org.springframework.web=DEBUG
	logging.level.com.mycompany=TRACE

	# Customize log pattern in the console
	logging.pattern.console=%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n
	
	# Customize log pattern in the log file
	logging.pattern.file=%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n
	
	# Setting the log file path and the file name
	logging.file.path=./logs
    logging.file.name=myapp.log


Or in YAML:

	# application.yml
	logging:
	  file:
		path: ./logs
		name: myapp.log
	  level:
		root: INFO
		org.springframework: WARN
		com.myapp: DEBUG
	  pattern:
		console: "%d{yyyy-MM-dd HH:mm:ss} %-5level %logger{36} - %msg%n"
		file: "%d{yyyy-MM-dd HH:mm:ss} %-5level %logger{36} - %msg%n"

2. **Advanced customized Logging: creating logback.xml or logback-spring.xml file in src/main/resources**
Examples:

	<?xml version="1.0" encoding="UTF-8"?>
	<!-- 
	  Root Logback configuration file.
	  scan="true" enables periodic reloading of the config if the file changes.
	  scanPeriod="30 seconds" defines how often (every 30s) the file is checked for changes.
	-->
	<configuration scan="true" scanPeriod="30 seconds">

		<!-- Define a reusable log pattern for all appenders -->
		<!-- %d = date/time, %thread = thread name, %-5level = left-padded log level, %logger{36} = logger class name (max 36 chars), %msg = actual message -->
		<property name="LOG_PATTERN" value="%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n"/>

		<!-- Console Appender: outputs logs to the system console (stdout) -->
		<appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
			<encoder>
				<!-- Apply the defined log pattern -->
				<pattern>${LOG_PATTERN}</pattern>
			</encoder>
		</appender>

		<!-- File Appender: outputs logs to a file with rolling log files by day -->
		<appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
			<!-- Path to the current log file -->
			<file>logs/app.log</file>

			<!-- Rolling Policy: creates a new log file every day -->
			<rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
				<!-- Pattern for naming the rolled-over files: logs/app.2025-06-04.log, logs/app.2025-06-05.log, etc. -->
				<fileNamePattern>logs/app.%d{yyyy-MM-dd}.log</fileNamePattern>
				<!-- Keep logs for 7 days, older files will be deleted -->
				<maxHistory>7</maxHistory>
			</rollingPolicy>

			<encoder>
				<!-- Same pattern used for file logs -->
				<pattern>${LOG_PATTERN}</pattern>
			</encoder>
		</appender>

		<!-- Root logger: applies to everything unless a more specific logger is configured -->
		<root level="INFO">
			<!-- Output to both console and file -->
			<appender-ref ref="CONSOLE"/>
			<appender-ref ref="FILE"/>
		</root>

		<!-- Custom logger for your application package (e.g., com.myapp), set to DEBUG level -->
		<!-- Useful for getting detailed logs from your own code without enabling debug logs for everything -->
		<logger name="com.myapp" level="DEBUG"/>
	</configuration>

	<?xml version="1.0" encoding="UTF-8"?>
	<!DOCTYPE configuration>
	<configuration>

		<!-- Load properties from Spring Boot's application.properties or application.yml -->
		<!-- This allows referencing custom properties using ${...} -->
		<property resource="application.properties"/>

		<!-- Set a custom property that holds the microservice name -->
		<property name="springApplicationName" value="ms-enterprise-process-tracker"/>

		<!-- Console appender: logs to standard output -->
		<appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
			<encoder>
				<!-- Define a structured log pattern for clarity and filtering in log aggregators -->
				<pattern>
					%d{yyyy-MM-dd HH:mm:ss.SSS}                  <!-- Timestamp with milliseconds -->
					| LogLevel=%-5p                              <!-- Log level (e.g., INFO, WARN), left-padded to 5 characters -->
					| TransactionID=%X{TransactionID}            <!-- Transaction ID from MDC -->
					| MicroService=${springApplicationName}      <!-- Static microservice name property -->
					| ClientIP=%X{ClientIP}                      <!-- Client IP from MDC -->
					| Endpoint=%X{ProcessName}                   <!-- Logical process/endpoint name from MDC -->
					| Method=%X{Method}                          <!-- HTTP method or internal method name -->
					| ProcessId=%X{ProcessId}                    <!-- Internal process ID for tracking -->
					| LogType=%X{LogType}                        <!-- Custom log type (e.g., AUDIT, ERROR) -->
					| Identity=%X{Identity}                      <!-- User identity (e.g., username) -->
					| ResponseCode=%X{ResponseCode}              <!-- HTTP response code (e.g., 200, 401) -->
					| ErrorDescription=%X{Error}                 <!-- Description of any error that occurred -->
					| LogMessage=%m                              <!-- Actual log message -->
					%n                                           <!-- New line -->
				</pattern>
			</encoder>
		</appender>

		<!-- Root logger: applies to all logging unless overridden -->
		<!-- INFO level means DEBUG logs will be ignored unless specifically configured -->
		<root level="info">
			<appender-ref ref="STDOUT"/>
		</root>
	</configuration>


3. **Change/configure logging via Spring Boot Actuator**
**a)Enable the /loggers endpoint in your application.properties or application.yaml file:**

   management.endpoints.web.exposure.include=loggers
   management.endpoint.loggers.enabled=true
  
**b) Accessing and Configuring Log Levels:**
**View Loggers:**
You can view all loggers and their configured levels by sending a GET request to /actuator/loggers.

**Configure Log Level:**
To change the log level of a specific logger, send a POST request to /actuator/loggers/{logger.name} with a JSON payload specifying the desired configuredLevel. For example: 

     curl -X POST http://localhost:8080/actuator/loggers/com.example.MyClass -H 'Content-Type: application/json' -d '{"configuredLevel": "DEBUG"}'

**Available Log Levels:**
The following log levels can be configured: TRACE, DEBUG, INFO, WARN, ERROR, FATAL, OFF, and null.
**Reset Log Level:**
To reset a logger's level to its default, send a POST request with null as the configuredLevel.

In Logback (and Log4j), the % symbols in logging patterns denote conversion specifiers(special placeholders) that Logback replaces with actual values when formatting log messages.
**Examples of Common % Conversions**

| Pattern       | Meaning                                           | Example Output                    |
| ------------- | ------------------------------------------------- | --------------------------------- |
| `%d{pattern}` | Date/time of log event (`{}` specifies format)    | `2025-06-04 10:34:12`             |
| `%thread`     | Thread name                                       | `main`                            |
| `%level`      | Log level (e.g., `INFO`, `DEBUG`)                 | `INFO`                            |
| `%-5level`    | Log level, left-aligned, padded to 5 characters   | `INFO ` (with a space after)      |
| `%logger{36}` | Logger name (class name), trimmed to max 36 chars | `com.example.service.MyService`   |
| `%msg`        | The log message                                   | `Started the process`             |
| `%n`          | Newline                                           | Line break (platform-independent) |
| `%M`          | Method name                                       | `handleRequest`                   |
| `%F`          | File name where the log call was made             | `MyService.java`                  |
| `%L`          | Line number                                       | `123`                             |
| `%X{key}`     | MDC (Mapped Diagnostic Context) variable value    | e.g., request ID if set in MDC    |

Mapped Diagnostic Context (MDC) is a thread-local key-value store that allows you to add extra context to log messages.
You can use it to store information such as a user ID, session id and request ID


## Base64
Base64 is  binary-to-text encoding scheme used to convert binary data into a text format by encoding it into a base 64 representation.
This is particularly useful for transmitting binary data over text-based protocols, such as email or HTTP, which may not handle binary data well.
Base64 encoding uses 64 printable characters (A-Z, a-z, 0-9, +, /) to represent the data, making it a common way to embed images in HTML or store data in XML. 
The 3 main types of Base64:
**1. Standard Base64**
* Character set: A–Z, a–z, 0–9, +, /
* Padding: Uses = as padding at the end of the string.
* Use case: General-purpose encoding (e.g., email, file encoding, binary to text conversion).

**2. URL-safe Base64**
* Character set: A–Z, a–z, 0–9, -, _ (same as standard except replaces '+' and '/' with '-' and '_' respectively)
* Padding: Optional (some systems strip it).
* Use case: Web tokens (e.g., JWT which does not include padding), URLs, filename-safe data.

**3. MIME Base64 (Multi-line)**
* Character set: Same as standard base64.
* Line breaks: Inserts \r\n (carriage return and line feed) as line separators every 76 characters.
* Use case: Email (MIME encoding of attachments or body).

| Base64 Variant                | Java Encoder Method       | Java Decoder Method       | Use Case                         |
| ----------------------------- | ------------------------- | ------------------------- | -------------------------------- |
| **Standard Base64**           | `Base64.getEncoder()`     | `Base64.getDecoder()`     | Files, general-purpose encoding  |
| **URL-safe Base64**           | `Base64.getUrlEncoder()`  | `Base64.getUrlDecoder()`  | JWTs, URLs, web-safe tokens      |
| **MIME Base64 (with breaks)** | `Base64.getMimeEncoder()` | `Base64.getMimeDecoder()` | Email attachments, MIME messages |


##@PostConstruct and @PreDestroy in Spring boot
**@PostConstruct** in Spring Boot (and general Java EE/ Jakarta EE) is an annotation used to mark a method that should be executed after the bean has been constructed and dependency injection is complete(and all dependencies have been injected), 
but before the bean is used.
It’s an ideal place to put initialization logic.
This method is invoked only once.
**Rules:**
* The method must be void, public or protected (can be package-private, but not private).
* It must have no parameters.
* There must be only one such method per bean.
* The annotated method cannot be static, ensuring that it is associated with a specific bean instance.

**@PreDestroy** is called before the Spring bean is destroyed. 
It’s where you can place cleanup logic, such as closing resources.

**ExampleBean**

	package com.example.demo;

	import org.springframework.stereotype.Component;

	import javax.annotation.PostConstruct;
	import javax.annotation.PreDestroy;

	@Component
	public class ExampleBean {

		public ExampleBean() {
			System.out.println("Constructor: ExampleBean is created");
		}

		@PostConstruct
		public void init() {
			System.out.println("PostConstruct: ExampleBean is initialized");
		}

		@PreDestroy
		public void cleanup() {
			System.out.println("PreDestroy: ExampleBean is about to be destroyed");
		}
	}

When you run this Spring Boot application, you should see output similar to the following:

	Constructor: ExampleBean is created
	PostConstruct: ExampleBean is initialized
	
When you stop the application (e.g., by pressing Ctrl + C if running in the terminal), the @PreDestroy method will be called:

	PreDestroy: ExampleBean is about to be destroyed

## Checked and Unchecked Exceptions in java
**Checked Exceptions:** These exceptions are checked at compile time.
Java requires that checked exceptions be either:
* Declared in the method signature with throws
Or 
* caught and handled inside the method
They typically represent conditions that a well-written application should anticipate and recover from, such as I/O errors or file not found scenarios. 
Examples include: IOException, FileNotFoundException, ClassNotFoundException, InterruptedException, and SQLException.

**Unchecked Exceptions:** These exceptions are not checked at compile time; instead, they occur during runtime.
They are a subclass of RuntimeException, so the compiler does not require it to be declared or caught. 
They usually indicate programming errors or bugs that could have been avoided. 
Unchecked exceptions include:  NullPointerException, ArithmeticException, ArrayIndexOutOfBoundsException and IllegalArgumentException

**Custom Exceptions:** Programmers can also create their own exception classes by extending Exception (for checked exceptions) or RuntimeException (for unchecked exceptions). 
This allows for specific error conditions in an application to be handled.

## What is an instance and a subtype in java
In Java, an **instance** refers to a specific object created from a class. 
A **subtype** is a type that is a more specialized version of another type, known as the supertype.
In Java, this relationship is established through inheritance, where a subclass is considered a subtype of its superclass.

An instance of a subclass is also considered an instance of its superclass due to the "is-a" relationship. 
For example, if Dog is a subclass of Animal, a Dog object is both an instance of Dog and an instance of Animal.

## What is `instanceof`, `isInstance` and `isAssignableFrom` in java
| Keyword / Method           | What It Does                                                                            | Example                                               |
| -------------------------- | --------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| `instanceof`               | Checks if an **object** is an instance of a class or subclass                           | `"hello" instanceof String // true`                   |
| `Class.isInstance(obj)`    | Same as `instanceof`, but **dynamically** at runtime using reflection                   | `String.class.isInstance("hello") // true`            |
| `Class.isAssignableFrom()` | Checks if one **class** can be assigned to another (i.e., is a subclass or interface)   | `Object.class.isAssignableFrom(String.class) // true` |
 
**Class.isInstance(Object obj)**
Same as instanceof, but for runtime reflection.
Useful when the class type is not known at compile time (e.g., in frameworks or generics).
Remember: isInstance() checks actual type hierarchy, not just shared interfaces or Object ancestry.
**Example:**

	Object text = "Hello";
	Class<?> clazz = String.class;

	System.out.println(clazz.isInstance(text)); // true

	clazz = Number.class;
	System.out.println(clazz.isInstance(text)); // false: checks actual type, "hello" actual type is String

 
**Class.isAssignableFrom(Class<?>)**
Check if one class can be assigned to another — i.e., if a class is a subtype of another.
**Syntax:**

	ClassA.isAssignableFrom(ClassB)

**Reads as:** Can a ClassB be assigned to a ClassA variable?
**Example:**

	System.out.println(Object.class.isAssignableFrom(String.class));  // true
	System.out.println(String.class.isAssignableFrom(Object.class));  // false

## `MethodParameter` in spring
In Spring, `MethodParameter` is a class that encapsulates the metadata of a method parameter. 
It provides access to information about the parameter, such as its type, annotations, and index within the method's parameter list.
MethodParameter offers various methods to access parameter metadata:

| Method                                | Purpose                                       |
| ------------------------------------- | --------------------------------------------- |
| `getParameterType()`                  | Gets raw type (e.g., `List`)                  |
| `getGenericParameterType()`           | Gets full generic info (e.g., `List<String>`) |
| `getParameterIndex()`                 | Index in method signature                     |
| `getMethod()`                         | The `Method` owning the parameter             |
| `getParameterAnnotation(Class)`       | Get specific annotation on the parameter      |
| `hasParameterAnnotation(Class)`       | Check if annotation exists                    |
| `nested()` / `increaseNestingLevel()` | Handle nested generic structures              |
| `getContainingClass()`                | Get class owning the method                   |

**Example Reference Code**

	public class MyController {
		public void processData(@RequestParam String name, List<List<String>> values) {}
	}

	// In main method or test
	Method method = MyController.class.getMethod("processData", String.class, List.class);
	MethodParameter param1 = new MethodParameter(method, 1); // List<List<String>>

	System.out.println(param1.getParameterType());                       // class java.util.List
	System.out.println(param1.getGenericParameterType());                // java.util.List<java.util.List<java.lang.String>> (if generic type is retained)
	System.out.println(param1.getParameterIndex());                      // 1
	System.out.println(param1.getMethod().getName());                    // "processData"
	System.out.println(param1.hasParameterAnnotation(RequestParam.class)); // false (only param0 has it)

	MethodParameter param0 = new MethodParameter(method, 0);
	System.out.println(param0.getParameterAnnotation(RequestParam.class)); // @RequestParam

	param1.increaseNestingLevel(); // for List<List<String>>
	System.out.println(param1.getNestedGenericParameterType());          // List<String>

`MethodParameter` can also be used to represent the return type of a method.
You can represent the return type of a method by passing an index of -1 when constructing the `MethodParameter` instance.

**Constructor Usage:**
	MethodParameter(Method method, int parameterIndex)

* If `parameterIndex >= 0`: Represents a method parameter.
* If `parameterIndex == -1`: Represents the return type of the method.

**Example: Using MethodParameter for Return Type**

	import org.springframework.core.MethodParameter;

	import java.lang.reflect.Method;
	import java.util.List;

	public class MyService {
		public List<String> getNames() {
			return List.of("Alice", "Bob");
		}

		public static void main(String[] args) throws Exception {
			Method method = MyService.class.getMethod("getNames");

			// -1 indicates return type
			MethodParameter returnParam = new MethodParameter(method, -1);

			System.out.println("Raw return type: " + returnParam.getParameterType());
			System.out.println("Generic return type: " + returnParam.getGenericParameterType());
		}
	}



## Type erasure in java and Type reference in jackson
**Type erasure** can be explained as the process of enforcing type constraints only at compile time and discarding the element type information at runtime.
**Short Definition** process that removes generic type information at runtime and replaces it with the upper bound or Object.
During compilation, the Java compiler erases all type parameters. For example, List<String> becomes List.
**Why Type Erasure?**
* **Backward Compatibility:** Allows code using generics to work with older Java versions that don't support them.
* **Runtime Efficiency:** Generics don't add runtime overhead because type information is removed after compilation.
**Consequences of Type Erasure:**
* **No Runtime Type Information:** You can't use instanceof operator (`new T() or if (x instanceof T)`)or casts with parameterized types because type information is not available at runtime.
* **Bridge Methods:** The compiler may generate bridge methods to maintain polymorphism when a class extends a parameterized class or implements a parameterized interface.

**⚠️ Problem Example:**

	List<String> list = new ArrayList<>();
	List<Integer> list2 = new ArrayList<>();

	System.out.println(list.getClass() == list2.getClass()); // true

Even though they're declared with different types, the type info is erased, so they're both just ArrayList at runtime.

**TypeReference** is a jackson library abstract class used to obtain full generic type information at runtime, particularly when dealing with deserialization of JSON objects. 
It is used to preserve generic type information that might be lost due to type erasure in java.

**🔄 Example without TypeReference (this won't work correctly):**

	ObjectMapper mapper = new ObjectMapper();
	List<Person> people = mapper.readValue(json, List.class); // BAD: No type info for Person

This will compile, but at runtime, Jackson can’t tell what kind of objects are in the List, so you’ll get a List<LinkedHashMap> instead of List<Person>.

**✅ Using TypeReference to keep type info:**

	ObjectMapper mapper = new ObjectMapper();

	List<Person> people = mapper.readValue(
		json,
		new TypeReference<List<Person>>() {}
	);

Now Jackson can deserialize each element of the list as a Person, thanks to the anonymous subclass of TypeReference retaining the generic type info.

**Summary:**
| Concept           | Description                                                                                      |
| ----------------- | ------------------------------------------------------------------------------------------------ |
| **Type Erasure**  | Java removes generic type info at runtime.                                                       |
| **TypeReference** | Jackson's way of retaining generic type info to work around erasure, especially for collections. |

## Multi-module Spring Project
A multi-module Spring project is a Maven or Gradle-based project that consists of a parent project and multiple sub-modules, each serving a specific concern or layer of an application (e.g., web, service, repository, domain). 
This modular approach allows for better separation of concerns, reusability, and maintainability of code in large-scale enterprise applications.
In a multi-module spring project:
* **Parent Project (Root):** Manages dependencies, build configuration, and aggregates modules.
* **Modules (Sub-projects):** Each is an independent Maven/Gradle module, typically representing a layer (like api, service, data, etc.).

**Example Structure**
Let's say we're building a simple Employee Management System. The structure could look like this:

	employee-management/
	│
	├── pom.xml                       <-- Parent POM
	├── employee-api/                <-- API module (controllers, DTOs)
	│   └── pom.xml
	├── employee-service/            <-- Business logic module
	│   └── pom.xml
	├── employee-data/               <-- Data access module (JPA, Repositories)
	│   └── pom.xml
	├── employee-common/             <-- Shared code (Utils, exceptions, constants)
	│   └── pom.xml
	└── employee-app/                <-- Main Spring Boot app module
		└── pom.xml


## Issues faced
1. Why create an admin role on the fly yet a script with the roles should be ran first(on user service)
2. Why write a function to verify a role and throw error yet we can use hasAuthority (on user service) 
3. searching of fields with @Lob, Postgres sets the fields as oid
4. map strictly: modelMapper.getConfiguration().setMatchingStrategy(MatchingStrategies.STRICT);
5. 

## Possible red flags
1. Doubt if findByEmailIgnoreCase should be used since subject is set to userId(JWTUtils.java):

		if (principal instanceof Jwt jwt) {
            return userRepository.findByEmailIgnoreCase(jwt.getSubject()).orElse(null);
        }
		
2. @RequestHeader("Authorization") String otpToken used in authservice method resendOTP and logout
3. lastUsedAt set twice in JWTUtils.saveToken() method
4. MDC.put(METHOD, request.getMethod()); called twice in LogInterceptor prehandle method

## Issues to research further
1. Encrypting/hashing data 
2. Encryption algos and how they work
3. Can liquibase generate a schema from a database
4. Can liquibase generate actual data from tables in a database
5. Interceptors in spring
6. What is JSR 250 and segmented configurations
7. What is OpenID Connect (OIDC) & OIDC compliant
8. CORS, iframes and csrf
9. Logging
10. Rest Best Practices
11. Encrypting api data 
12. Why hash secret keys, modes of aes encryption

## To Do
1. Create a JWT feature to generate and validate tokens
2. foreign tokens should also be validated