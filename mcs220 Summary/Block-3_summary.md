Summary of Block-3.pdf:

This academic text provides a comprehensive introduction to Spring Boot and its integration with Hibernate (an Object-Relational Mapping tool) for developing robust Java applications, particularly focusing on Data Access Layer simplification and CRUD operations.

---

### Main Ideas and Key Points:

The text is structured into three units:

**Unit 9: Introduction to Spring Boot**

*   **Purpose of Spring Boot:**
    *   Addresses the tedious and error-prone configuration and dependency management of traditional Spring-based enterprise applications.
    *   Aims for fast, secured, and cost-effective development of production-ready Spring applications and services.
    *   Provides "auto-configuration out-of-the-box" and embeds servers (like Tomcat) to simplify deployment and reduce boilerplate code.
    *   Enhances the Spring framework with Rapid Application Development (RAD) features.
*   **Core Components and Working:**
    *   **Entry Point:** A class with a `main` method annotated with `@SpringBootApplication`.
    *   `@SpringBootApplication` comprises:
        *   `@EnableAutoConfiguration`: Automatically applies auto-configuration beans based on classpath dependencies (e.g., auto-configures H2 as in-memory DB if present).
        *   `@ComponentScan`: Scans for Spring components (controllers, services, configurations) from the root package.
        *   `@Configuration`: Enables annotation-based configuration and defines `@Bean` methods.
    *   **Other Annotations:** Introduces conditional annotations like `@ConditionalOnClass`, `@ConditionalOnBean`, `@ConditionalOnProperty`, `@ConditionalOnResource` for conditional bean creation.
    *   **Spring Boot Starters:**
        *   Convenient dependency descriptors that simplify dependency management by providing compatible versions of related technologies (e.g., `spring-boot-starter-web` for web applications including Tomcat, Spring MVC, Jackson).
        *   Follows naming pattern `spring-boot-starter-*`.
    *   **Project Structure:** Recommends placing the main application class in the root package for effective component scanning.
    *   **Spring Boot Runners:**
        *   `ApplicationRunner` and `CommandLineRunner` are functional interfaces that allow executing specific code immediately after the Spring Boot application starts.
*   **Developer Tools and Monitoring:**
    *   **Spring Boot DevTools:** Enhances development experience and productivity by:
        *   **Automatic Restart:** Detects code changes and automatically restarts the application.
        *   **Live Reload:** Triggers browser refresh automatically when resources (e.g., templates) are changed.
        *   **Property Defaults:** Disables caching for template technologies during development.
    *   **Spring Boot Actuator:** Provides production-ready features for monitoring and managing applications, exposing operational information via HTTP and JMX endpoints.
        *   **Endpoints:** `/health` (health status), `/info` (general app info), `/metrics` (application metrics via Micrometer), `/env` (environment properties).
        *   By default, only `/health` and `/info` are exposed; others can be enabled via `management.endpoints.web.exposure.include=*`.
*   **Application Properties:**
    *   Supports externalized configuration for different environments (dev, test, prod).
    *   Properties can be defined via: Command Line Arguments (highest precedence), `application.properties` file, `application.yml` file (supports hierarchical data).
    *   `@Value` annotation: Used to inject property values into Java code.
    *   **Active Profiles:** Allows using different property sets for different environments (e.g., `application-dev.properties`, `application-prod.properties`). Can be activated via command line or IDE. YAML files can consolidate profiles using `---` delimiters.
*   **Running Spring Boot Applications:**
    *   **Maven Plugin:** `spring-boot-maven-plugin` is recommended for building, testing, and packaging.
    *   **Exploded Form:** `mvn spring-boot:run` starts the application with an embedded server.
    *   **Stand-Alone Packaged Application:** `mvn clean package spring-boot:repackage` creates an executable JAR. `java -jar <FileName>` runs the JAR without needing a classpath.
    *   **WAR Deployment:** Applications can be packaged as WAR files (by changing `packaging` in `pom.xml` and extending `SpringBootServletInitializer`) for deployment on external servlet containers like Tomcat.

**Unit 10: Configuration of Hibernate (ORM)**

*   **Object-Relational Mapping (ORM):**
    *   A programming technique to convert data between incompatible type systems (e.g., Java objects and relational database tables).
    *   Enables CRUD operations without direct SQL, abstracting database interaction.
*   **Hibernate Overview:**
    *   An open-source Java persistence framework and a popular **JPA provider**.
    *   Maps POJOs to relational database tables, allowing developers to focus on business logic rather than boilerplate SQL.
    *   **Advantages:** Open Source, High Performance, Lightweight, Database independent, Caching, Scalability, Lazy Loading, Hibernate Query Language (HQL).
*   **JPA, Hibernate, and Spring Data JPA Relationship:**
    *   **JPA (Java Persistence API):** A *specification* defining APIs for ORM and persistent object management. It has no implementation itself.
    *   **Hibernate:** A concrete *implementation* (provider) of the JPA specification.
    *   **Spring Data JPA:** A Spring sub-project that *simplifies data access* for relational stores. It's *not a JPA provider* but *wraps* a JPA provider (defaults to Hibernate) and adds features like a "no-code repository pattern" to abstract the DAO layer.
*   **Hibernate Architecture and Key Objects:**
    *   **Configuration:** Defines database properties and entity mappings (programmatically or via `hibernate.cfg.xml`/`hibernate.properties`).
    *   **SessionFactory:** Immutable, thread-safe, heavyweight object created once per database, used to create `Session` objects.
    *   **Session:** Lightweight, per-interaction object, wraps JDBC connection, provides first-level cache.
    *   **Transaction:** Represents a unit of work with the database, ensuring data consistency and rollback.
    *   **Query:** Used to retrieve data using SQL or HQL.
    *   **Persistent Objects:** POJOs mapped by Hibernate, annotated with `@Entity`.
*   **Caching in Hibernate:**
    *   **First-level Cache:** Default and cannot be disabled. Session-scoped, reducing queries within a single transaction.
    *   **Second-level Cache:** Global, SessionFactory-scoped. Improves performance by caching data across multiple sessions.
*   **Hibernate Annotations:**
    *   `@Entity`: Marks a POJO as a persistent entity mapped to a database table.
    *   `@Id`: Designates the primary key field.
    *   `@GeneratedValue`: Specifies strategy for ID generation (e.g., `IDENTITY`, `AUTO`).
    *   `@Table`: Customizes the name of the mapped database table.
    *   `@Column`: Customizes column details (name, length, nullability, uniqueness).
    *   `@Transient`: Marks a field as non-persistent (not mapped to a database column).
    *   `@Temporal`: Used to map `java.util.Date` or `java.util.Calendar` to specific SQL date/time types. (Java 8 `java.time` types map directly without this).
*   **Hibernate Entity Lifecycle States:**
    *   **Transient:** A newly created object, not associated with a Hibernate session or database.
    *   **Persistent:** An object associated with a Hibernate session, changes are tracked and synchronized with the database.
    *   **Detached:** An object that was once persistent but is no longer associated with a session. Changes are not tracked. Can be re-attached.
    *   **Removed:** An object marked for deletion via `session.delete()`.
*   **Hibernate CRUD Operations (Method Differences):**
    *   **`get()` vs. `load()`:**
        *   `get()`: Returns `NULL` if the entity is not found; hits the database immediately.
        *   `load()`: Throws a `RuntimeException` if not found; often returns a proxy and may delay database hit (lazy loading).
    *   **`persist()` vs. `save()` vs. `saveOrUpdate()`:**
        *   `persist()`: JPA standard, returns `void`. ID is not guaranteed immediately. Throws exception if called on a detached object.
        *   `save()`: Hibernate specific, returns the generated ID. Assigns ID immediately. Creates a new persistent instance for detached objects (can lead to duplicates).
        *   `saveOrUpdate()`: A versatile method that performs `save()` if the entity has no ID or is transient, and `update()` if it has an ID or is detached. It re-attaches detached instances without creating duplicates.
*   **Hibernate Query Language (HQL):** An object-oriented query language similar to SQL, but uses class names and property names instead of table and column names. Supports Select, Update, Delete, and bulk Insert operations (`INSERT INTO ... SELECT ...`).

**Unit 11: CRUD Application Using Spring Boot and Hibernate**

*   **Spring Data Repository Abstraction:**
    *   Significantly reduces boilerplate code for data access layers.
    *   Provides different interfaces for varying functionalities:
        *   **`CrudRepository`:** Offers basic CRUD operations (save, findById, findAll, delete, count).
        *   **`PagingAndSortingRepository`:** Extends `CrudRepository` and adds methods for pagination and sorting (`findAll(Sort)`, `findAll(Pageable)`).
        *   **`JpaRepository`:** Extends `PagingAndSortingRepository` and provides more JPA-specific operations (e.g., `flush`, `saveAndFlush`, batch operations). It is the most commonly used.
    *   Spring Data automatically generates implementations for repository interfaces based on method names (e.g., `findByTitleContaining`, `findByFirstNameAndLastName`).
    *   Custom queries can be defined using the `@Query` annotation (supporting named or ordinal parameters).
*   **Hibernate Association Mappings:**
    *   Establishes relationships between POJO entities (and thus database tables) as attributes in the model.
    *   Can be **unidirectional** (one entity references the other) or **bidirectional** (both entities reference each other).
    *   Represented by foreign key relationships in the underlying database tables.
    *   **Types of Associations:**
        *   **One-to-Many / Many-to-One (`@OneToMany`, `@ManyToOne`):**
            *   `@JoinColumn`: Used to specify the foreign key column.
            *   **Owning Side:** The side that defines the foreign key column (e.g., `@ManyToOne` side).
            *   **`mappedBy`:** Used on the non-owning side in bidirectional relationships to indicate the mapping is defined by the other entity.
            *   **Eager vs. Lazy Loading:**
                *   **Lazy (default for `@OneToMany`):** Related entities are loaded only when explicitly accessed, improving performance by deferring queries.
                *   **Eager (default for `@ManyToOne`):** Related entities are loaded immediately along with the primary entity, potentially impacting performance if not all related data is needed. Fetch type can be configured.
            *   **Cascading Operations (`cascade = CascadeType.*`):** Propagates persistence operations (save, delete, merge, etc.) from a parent entity to its associated child entities. JPA provides `ALL`, `PERSIST`, `MERGE`, `REFRESH`, `REMOVE`, `DETACH`. Hibernate also offers additional cascade types.
        *   **One-to-One (`@OneToOne`):**
            *   Can be implemented with a foreign key (`@JoinColumn`).
            *   Can be implemented with a shared primary key (`@PrimaryKeyJoinColumn`, `@MapsId`) for storage optimization.
        *   **Many-to-Many (`@ManyToMany`):**
            *   Requires an intermediate join table in the database.
            *   `@JoinTable`: Used to define the name of the join table and its foreign key columns (`joinColumns` for owning side, `inverseJoinColumns` for inverse side).
*   **Practical CRUD Implementation (using Spring Boot, Spring Data JPA, and Hibernate):**
    *   Demonstrates how to build a RESTful API for Book and Author entities (many-to-many relationship).
    *   **Create:** Uses `bookRepository.save(entity)` with `@PostMapping`.
    *   **Read:** Uses `bookRepository.findAll()`, and custom query methods like `findByTitleContaining`, `findByTitleLike`, and `@Query` annotated methods with `@GetMapping`.
    *   **Update:** Uses `bookRepository.save(entity)` (if entity has an ID) with `@PutMapping`.
    *   **Delete:** Uses `bookRepository.deleteById(id)` with `@DeleteMapping`.

---

### Conclusion:

The academic text effectively introduces Spring Boot as a powerful framework for rapidly developing and deploying production-ready Java applications by minimizing configuration and boilerplate code. It then delves into Hibernate as the default JPA provider, explaining its core architecture, entity lifecycle, and fundamental CRUD operations. Finally, it demonstrates how Spring Boot and Spring Data JPA, combined with Hibernate's association mappings, create a highly abstracted and efficient data access layer, simplifying complex database interactions for developers building modern applications. The emphasis is on increasing productivity and reducing development effort through intelligent auto-configuration, robust developer tools, and "no-code" repository patterns.