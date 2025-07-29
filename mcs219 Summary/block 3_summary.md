Summary of block 3.pdf:

This academic text, spanning three units (9, 10, and 11), provides a comprehensive overview of Object-Oriented Design (OOD) within the broader context of Object-Oriented Analysis and Design (OOAD). It details the transition from analysis to design, key design activities, and considerations for optimizing and documenting a system.

### Unit 9: Basics of System Design

**Main Ideas:**
*   **OOAD as an Evolutionary Approach:** OOAD differs from Structured Analysis and Design (SAD) by using classes and objects as fundamental building blocks, harnessing the power of object-based and object-oriented programming. It iteratively links Object-Oriented Analysis (OOA), Design (OOD), and Programming (OOP).
*   **Transition from OOA to OOD:** The OOA phase produces models (Object, Functional, Dynamic) from a user perspective, which are then refined in OOD for implementation, incorporating non-functional requirements and actual software components.
*   **Core OOD Activities:** System decomposition into subsystems, identification and management of concurrency, handling of persistent data, control flow mechanisms, and managing boundary conditions.

**Key Points:**

*   **OOA Model Validation:** Before OOD, the OOA model is checked for completeness (object usage, attribute types, associations), correctness (understandable classes, consistent with requirements), and consistency (unique class names, generalization hierarchy).
*   **System Decomposition (Breaking Into Subsystems):**
    *   Reduces complexity, allows concurrent development by individual teams.
    *   Subsystems are cohesive units with minimal interaction (loosely coupled).
    *   Can be off-the-shelf components.
    *   **Vertical Partitioning:** Divides system into independent subsystems at the same abstraction level (e.g., User Management, Purchase Management).
    *   **Horizontal Partitioning:** Divides a subsystem into layers, with each layer providing services to a higher layer (e.g., Purchase Management into Login, Shopping Cart, Payment Gateway).
    *   Subsystems interact via defined interfaces, which hide internal implementation.
*   **Coupling and Cohesion:**
    *   **Cohesion:** Measures independence *within* a subsystem (desirable: high cohesion).
    *   **Coupling:** Measures dependencies *between* subsystems (desirable: low coupling).
    *   A trade-off exists: increasing cohesion can sometimes increase coupling due to more interfaces. Designers aim for high cohesion and low coupling.
    *   Example: Introducing a `DATA STORAGE MANAGEMENT` subsystem to reduce direct coupling between application subsystems and the database.
*   **Concurrency Identification:**
    *   Allows simultaneous execution of multiple objects/tasks.
    *   Crucial for multi-user or computationally intensive systems.
    *   Requires synchronization algorithms to prevent issues like **Deadlock** (cyclic hold-n-wait) and **Starvation** (prolonged waiting due to higher-priority tasks).
*   **Management of a Data Store:**
    *   Distinguishes **Transient Objects** (deleted after shutdown) from **Persistent Objects** (must exist after shutdown, requiring databases).
    *   **Data Storage Strategies:**
        *   **Flat Files:** Simple, fast access, but limited data management features.
        *   **Relational Databases (RDBMS):** Higher abstraction, structured data (tables/relations), complex queries, ACID properties (Atomicity, Consistency, Isolation, Durability), concurrency, access control.
        *   **Object-Oriented Databases (OODBMS):** Store data as objects, support OOP properties (inheritance, ADT), highest abstraction, direct OOD translation, but potentially slower for queries and harder to manage than RDBMS.
*   **Controlling Events Between Objects (Control Flow):**
    *   Defines the order of program execution in response to events.
    *   **Control Strategies:**
        *   **Procedure-driven:** Sequential execution (legacy systems).
        *   **Event-driven:** Execution triggered by user actions (e.g., GUI applications).
        *   **Thread-based:** Concurrent execution using parallelism (powerful, independent threads).
    *   Control objects record events, manage temporary states, and initiate operations.
*   **Handling Boundary Conditions:**
    *   Defines system behavior at initiation, shutdown, and during failures.
    *   Not covered in OOA.
    *   Involves use cases for:
        *   **Persistent Objects/Classes:** Administrator actions for creating, modifying, or deleting objects not handled in normal system flow.
        *   **Start and Shutdown:** Procedures for starting, configuring, and shutting down each subsystem.
        *   **Exception Handling:** Mechanisms for managing hardware or software failures to prevent abrupt shutdowns and provide appropriate user messages.

**Conclusion:**
Unit 9 establishes the foundational principles of Object-Oriented System Design, emphasizing the iterative refinement of analysis models, strategic decomposition, and the management of critical system aspects like data persistence, concurrency, and error handling for robust implementation.

---

### Unit 10: Object Design

**Main Ideas:**
*   **From "What" to "How":** Object design translates the high-level, informal "what" of the analysis model into the detailed, implementable "how" of the design model, adapting to the actual computing environment.
*   **Refinement and Optimization:** This phase involves breaking down complex operations, choosing efficient algorithms and data structures, and optimizing design for performance while balancing clarity and maintainability.
*   **Integration of OO Concepts:** It details how inheritance hierarchies are adjusted and associations are mapped into the design for effective implementation.

**Key Points:**

*   **Object Design Purpose:** To map the analysis model (robust structure) to implementation details, considering efficiency, performance, real-time requirements, and programming language properties. It may introduce new classes and operations.
*   **Object Design Steps:**
    *   Creating links between high-level requirements and low-level services (e.g., OS, libraries).
    *   Realizing use cases through operations, breaking down responsibilities into manageable actions.
    *   Formulating algorithms for operations, considering computational complexity, ease of implementation, and flexibility (simple vs. optimized versions).
    *   Selecting appropriate data structures (e.g., container classes like lists, sets, dictionaries).
    *   Defining internal classes and operations (messages/methods) based on attribute changes, derived data, or framework requirements.
    *   Assigning operations to the most suitable classes, typically the "receiver of action" or "focal class."
    *   Refactoring for clean design.
*   **Design Optimization:**
    *   A trade-off between efficiency and clarity/reusability.
    *   **Efficient Access Paths:** Introducing redundant associations or indexes (e.g., hashing) to speed up data retrieval, but considering additional memory and update costs.
    *   **Rearranging Computing Tasks:** Optimizing the execution order of algorithms (e.g., filtering on smaller sets first).
    *   **Saving Intermediate Results:** Storing derived attributes (computed from other attributes) to avoid re-computation, with updates handled explicitly, periodically, or via active values.
*   **Implementation of Control:**
    *   Involves designing "controller classes" that manage interactions and sequence behavior.
    *   Steps for implementing an application's state model: identifying stateful classes, finding triggering events, merging state diagrams into code (handling loops, alternative paths, exceptions), and validating against other state, class, and sequence diagrams for consistency.
*   **Adjustment of Inheritance:**
    *   **Rearranging Classes and Operations:** Identifying common operations across classes and adjusting their signatures (optional arguments, special cases, generalized names, irrelevant operations as `no_op`) to facilitate common ancestors.
    *   **Abstraction of Common Behavior:** Creating abstract superclasses for shared features and specialized subclasses for unique aspects. This promotes reusability, modularity, and extensibility.
*   **Design of Associations:**
    *   Involves deciding which classes to implement, attribute types, and mapping composition relationships.
    *   **Association Traversals:** Implementing associations (one-to-one, one-to-many, many-to-many) as fields (pointers) in classes.
    *   **One-way Associations:** Implemented as a pointer attribute in one class.
    *   **Bidirectional Associations:** Requires careful implementation (e.g., pointers in both directions with synchronization) or can be simplified to a single-sided association if traversal frequency differs.

**Conclusion:**
Unit 10 delves into the practicalities of transforming analysis models into concrete object designs, emphasizing algorithmic considerations, performance optimization, and the meticulous structuring of class hierarchies and associations to prepare for efficient implementation.

---

### Unit 11: Advance Object Design

**Main Ideas:**
*   **Deepening OOD Concepts:** This unit expands on control implementation, inheritance, and association design, offering more nuanced approaches and details.
*   **Object Representation and Optimization Strategies:** It explores different ways objects and their attributes can be represented and reiterates the importance of strategic optimization.
*   **Design Documentation:** A crucial aspect of software engineering, focusing on the systematic recording of design decisions for maintenance and reuse.

**Key Points:**

*   **Control and its Implementation (Advanced):**
    *   **State Machine:** A behavioral model using State Transition Diagrams (STDs) to represent how an object changes states based on events and conditions.
    *   **Control as a State within Program:** Converting STDs into code using sequential statements, conditional branches, loops, and exception handling.
    *   **Control as a State Machine Engine:** Implementing a dedicated "State Machine" class where objects can call an engine to determine their next state and actions.
    *   **Control as a Concurrent Task:**
        *   Addresses inherent parallelism and resource economy.
        *   Uses constructs like coroutines, fork/join, message passing, semaphores (or monitors), and threads.
        *   Distinguishes between **Intra-object concurrency** (threads within the same process) and **Inter-object concurrency** (independent objects executing simultaneously).
        *   Emphasizes resolving concurrency problems (deadlocks, data disintegration) at the design level.
*   **Inheritance Adjustment (Refined):**
    *   Beyond basic rearrangement and abstraction, it suggests **Delegation** as an alternative to inheritance when a "has-a" relationship is more appropriate than an "is-a" relationship (e.g., a Stack "has a" Linked List, rather than "is a" Linked List, to avoid inheriting unneeded operations).
*   **Association Design (Detailed):**
    *   Defines associations as relationships between objects, represented by links with labels, multiplicity, and role names.
    *   **Modeling Steps:** Data-driven view (navigation), Behavior-driven view (interaction), defining multiplicity and role names.
    *   **Types of Associations:**
        *   **Association (Weak):** Objects can exist independently.
        *   **Aggregation (Stronger):** Whole-part relationship where the "part" can exist without the "whole."
        *   **Composition (Strongest):** Whole-part relationship where the "part" cannot exist without the "whole" (death relationship).
    *   **UML Association Constraints:** Implicit, Ordered, Changeable, Add Only, Frozen.
    *   **Analyzing Association Traversal:** While inherently bidirectional, unidirectional is often preferred for easier implementation. Bidirectional can be implemented via pointers in both classes (requiring synchronization) or a separate "association class" for linking attributes.
*   **Object Representation:**
    *   Focuses on how objects and their attributes are implemented, often as basic data types or by forming new classes for attributes themselves (e.g., `EIN` as an attribute vs. a separate `EIN` object).
    *   Emphasizes the trade-off between combining classes and explicit representation for minimizing cost, execution time, and memory.
    *   Reinforces the benefits of object modeling: access to OOP features, design/software reuse, and applicability to complex problems.
*   **Design Optimization (Re-emphasis):**
    *   Reiterates the balance between efficiency (time, space, cost) and other criteria like maintainability, reusability, and understanding.
    *   Strategies include adding redundant associations (e.g., for indexing), optimizing algorithm order, and saving derived values to avoid re-computation.
    *   Introduces **Reification Behavior** as a technique to store, pass, or modify behavior at runtime.
*   **Design Documentation:**
    *   Crucial for maintenance and reuse of software components.
    *   Types: User, System (includes design documentation), Project.
    *   **Content Classification:** Static overview (platform, architecture), Dynamic overview (events, control flow), Class interface/implementation descriptions, Task interface/implementation descriptions.
    *   **Importance:** Facilitates multi-developer projects, iterative development, versioning, testing, and long-term maintenance.
    *   **Features of Good Documentation:** Organized, structured, summarized, reliable, covers all requirements, and emphasizes pictorial representation.

**Conclusion:**
Unit 11 provides a deeper dive into specific OOD techniques, offering advanced considerations for control, inheritance, and association, alongside practical advice on object representation, optimization, and the critical role of comprehensive design documentation in the software development lifecycle. The overall text underscores that OOAD is a systematic, iterative process aimed at creating robust, maintainable, and reusable software systems.