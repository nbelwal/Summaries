Summary of block 4.pdf:

This academic text, comprising Units 12, 13, and 14, provides a comprehensive overview of strategies for implementing object-oriented designs into executable code and mapping object models to relational databases.

---

### Unit 12: Implementation Strategies-1

This unit focuses on the initial transformation of object design models, particularly UML class diagrams, into source code in a programming language.

**Main Ideas & Key Points:**
*   **Design to Code Transformation:** The process of converting object design elements (classes, relationships) into programming language constructs. While straightforward for classes, associations pose a challenge as most languages lack direct paradigms for them.
*   **Creating Class Definitions:**
    *   UML Class Diagrams provide a blueprint (classes, attributes, operations, relationships).
    *   This information is sufficient to create basic class definitions in object-oriented languages (e.g., C++, Java).
    *   UML tools can automate the generation of basic class code.
*   **Implementing Associations:**
    *   Associations represent relationships between classes (via their objects), distinct from links (instances of associations).
    *   In programming, associations are implemented as reference models where objects reference each other.
    *   **Two Key Aspects of Implementation:**
        1.  **Data Declaration:** Defining data members in one class to store references to objects of the associated class.
        2.  **Manipulation:** Ensuring client code interacts with associations without seeing underlying implementation details.
    *   **Types of Associations and Implementation Strategies:**
        *   **Unidirectional Implementations (one-way traversal):** Maintaining the association in only one direction.
            *   **Optional Associations (0..1):** Implemented using a simple reference variable; can be `null` if no association exists.
            *   **One-to-One Associations (1):** Implemented using an attribute that holds a reference to a single instance of the associated class.
            *   **Associations with Multiplicity 'Many' (0..* or 1..*):** Implemented using a suitable container class (e.g., `Vector`, `List`, `Set`) to hold multiple references/pointers to associated objects.
        *   **Bi-directional Implementations (two-way traversal):** Maintaining the association in both directions, requiring a pair of references.
            *   More complex to maintain due to consistency requirements (updates on one side must reflect on the other).
            *   **One-to-One and Optional:** Both classes contain attributes referencing each other. Constructors often initialize these links.
            *   **One-to-Many:** The "many" side typically uses a collection (e.g., `Set`), while the "one" side holds a single reference. The "one" side often manages link consistency.
            *   **Immutable Association:** Associations whose state cannot be modified after creation (inherently thread-safe, higher security). Each class defines a data member referencing the associated object.

**Conclusion:** Unit 12 lays the groundwork for transforming static object designs into code, with a particular focus on the nuanced implementation of various types of class associations due to the lack of direct language support.

---

### Unit 13: Implementation Strategies-2

This unit extends implementation strategies to cover the dynamic behavior of object-oriented systems, including method creation, constraints, statecharts, and data persistence.

**Main Ideas & Key Points:**
*   **Creating Methods from Collaboration Diagrams:**
    *   **Collaboration Diagram (Communication Diagram):** A UML interaction diagram depicting relationships and chronological interactions between objects to perform a specific task (e.g., a use case). Focuses on object structure and interrelation.
    *   **Elements:** Actors, objects, communication links, and sequenced messages.
    *   **Implementation:** Messages exchanged in the diagram translate directly into method calls and definitions in the source code.
*   **Implementing Constraints:**
    *   **Constraint:** A condition that restricts the semantics of an element, which must always be true (e.g., an employee's name cannot be null).
    *   **Purpose:** Control software behavior, reflect problem domain rules, validate object states at runtime, ensure data integrity.
    *   **Application:** Can be applied to single elements (classes, attributes, links) and specified using curly braces `{}`.
    *   **RDBMS Analogs:** NOT NULL, UNIQUE, PRIMARY KEY, FOREIGN KEY constraints.
    *   **Implementation:** Often integrated directly into code logic (e.g., `if` statements, annotations in modern languages) to verify conditions at runtime.
*   **Implementing State Charts:**
    *   **Statechart Diagram:** Used in dynamic modeling to define the behavior of a particular class by showing its states, events that trigger transitions, and actions performed during transitions.
    *   **Implementation Strategies:**
        1.  **Switch Statement:** The most basic method where a scalar variable represents the current state, and a `switch` statement handles events based on this state.
            *   **Drawbacks:** Inflexible for new states, code duplication, poor reusability.
        2.  **Helper Object:** An object-oriented alternative where each state is represented by a separate "helper" object. The domain object delegates incoming messages to its current helper object.
            *   **Benefits:** Reduces redundancy, improves reusability.
            *   Involves an abstract state class and derived classes for each specific state.
        3.  **Collaborator Object:** An improved approach over helper objects. The context class retains a single collaborator object that represents the current active state and maintains references to all state objects (created once). The context object delegates events to this collaborator.
            *   **Benefit:** No new object creation for state transitions, state-specific code resides in one class.
*   **Persistency:**
    *   **Persistence:** The property by which an object or data survives even after the program that created it concludes. Crucial for enterprise applications.
    *   **Types:** Data persistence (saving/restoring data), process persistence (long-running processes), object persistence (object not removed unless erased).
    *   **Persistent vs. Non-Persistent Data:**
        *   **Persistent Data:** Has a longer lifetime, saved to a permanent store (database, file), is steady, restorable, and accessible after application closure.
        *   **Non-Persistent Data:** Volatile, exists only during application execution (e.g., in RAM), lost upon program termination.
    *   **Serialization:** The process of converting an object into a byte stream for storage (memory, database, file) or transmission. Deserialization is the reverse. Enables platform-independent object persistence.

**Conclusion:** Unit 13 elaborates on implementing the dynamic aspects of an object-oriented system using collaboration diagrams for method derivation, integrating constraints for rule enforcement, applying various strategies for statechart implementation, and ensuring data and object persistence through mechanisms like serialization.

---

### Unit 14: Objects Mapping with Databases

This unit addresses the critical challenge of mapping object-oriented models, which are naturally hierarchical and relationship-rich, to the tabular structure of relational databases.

**Main Ideas & Key Points:**
*   **Relational Database Schema for Object Models:**
    *   **DBMS Concepts:** Software for managing permanent data (integrity, security, recovery, sharing).
    *   **Database Schema:** The design/outline of a database (table names, columns, data types, constraints, relationships).
    *   **RDBMS Logical Data Structure:** Data stored in relations (tables) with tuples (rows) and attributes (columns).
    *   **RDBMS Concepts:**
        *   **SQL:** Structured Query Language for DDL (schema definition) and DML (data manipulation).
        *   **Integrity Rules:** Entity Integrity (Primary Key uniqueness) and Referential Integrity (Foreign Key consistency).
        *   **Normal Forms (1NF, 2NF, 3NF):** Used to reduce data redundancy and avoid update anomalies during database design.
        *   **Views:** Virtual tables for data security and simplified access.
*   **Extended Three Schema Architecture for Object Models:**
    *   Adapts the traditional External, Conceptual, and Internal schema levels to object modeling.
    *   Object models are used for external and conceptual schemas, which are then transformed into a table model.
    *   Views and interfaces connect external tables to conceptual tables, which then map to the internal (physical) schema via SQL commands.
*   **The Use of Object IDs (OID):**
    *   Unique identifiers for objects/entities, often serving as primary keys in database tables.
    *   **Advantages:** Stability (referencing objects consistently), especially for associations.
    *   **Disadvantages:** RDBMS does not natively support OIDs; they must be defined as attributes.
*   **Mapping Object Classes to Tables:**
    *   Each object class typically translates to one or more relational tables.
    *   Class attributes become table columns. Not all attributes are mapped (e.g., temporary ones).
    *   Tables can be partitioned horizontally (rows) or vertically (columns) for efficiency.
    *   Constraints (NOT NULL, PRIMARY KEY) are added during table creation.
*   **Mapping Associations to Tables:** The strategy depends on the association type and multiplicity.
    *   **Binary Associations:**
        *   **One-to-One:** Primary key of one table is included as a Foreign Key in the other table. Can also be merged into a single table (with care to avoid redundancy).
        *   **One-to-Many:**
            1.  Foreign Key in the "many" side's table (most common).
            2.  Create a distinct associative table for the relationship.
    *   **Many-to-Many:** Always maps to a distinct **associative table**. This table contains the primary keys of both related classes as foreign keys (forming a composite primary key) and any attributes specific to the relationship.
    *   **Ternary Associations (three classes):** All three classes map to distinct tables. The relationship itself is mapped to *another* distinct table, whose primary key is a composite of the primary keys of all three participating classes, along with any relationship-specific attributes.
*   **Mapping Generalizations (Inheritance) to Tables:** Several strategies exist:
    1.  **Map superclass and each subclass to a table:** All entities (superclass and subclasses) get their own tables. Subclass tables include the superclass's primary key.
    2.  **Map each subclass to a table (superclass not mapped):** Superclass attributes are duplicated in all subclass tables. This is suitable for disjoint and complete inheritance.
    3.  **Map the superclass to a single table:** All attributes from the superclass and all subclasses are combined into one large table. This introduces null values for attributes not applicable to a specific subclass instance.
*   **Interfacing to Databases:**
    *   **Challenge:** Object-oriented systems and relational databases are fundamentally different (OO is object-centric with data+behavior; RDBMS is data-centric).
    *   **Solution:** Interfacing software (e.g., JDBC API for Java) is required to bridge this gap, allowing OO applications to read, write, and manipulate data in RDBMS. This involves connecting to the database, sending queries, and processing results.

**Conclusion:** Unit 14 addresses the crucial practical aspect of persistent storage for object-oriented systems by detailing various strategies for mapping complex object models (classes, associations, generalizations) to the structured format of relational databases, acknowledging the inherent differences and the need for specialized interfacing mechanisms.