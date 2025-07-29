Summary of block 2.pdf:

This academic text introduces three core models in Object-Oriented Analysis and Design (OOAD): Object Modeling, Dynamic Modeling, and Functional Modeling. It details the concepts, notations, and applications of each.

---

### Unit 6: Object Modeling

**Main Idea:** Object modeling focuses on identifying the static structure of a system by defining objects, classes, their attributes, and relationships. It is the first step in object-oriented design and aims to decompose a system into interacting objects.

**Key Concepts & Points:**

*   **Goal of Object Design:** Object-oriented decomposition, identifying system objects and their interactions. Aims for closer problem domain representation, easy incremental change, and reuse.
*   **Object Modeling Process:** Identify objects, structures, attributes, associations, and services. Represented by object diagrams.
*   **Advanced Modeling Concepts:**
    *   **Aggregation:**
        *   Represents a "has-a" or "part-of" relationship (e.g., a house *has* rooms).
        *   A tightly coupled form of association where a complex object is an assembly of component objects.
        *   UML Notation: A hollow diamond attached to the "whole" class.
        *   Distinguished from generalization by tests like "part of" phrase, propagation of operations/attributes, and intrinsic asymmetry.
    *   **Composition:**
        *   A stronger form of aggregation implying exclusive ownership (parts cannot exist without the whole).
        *   UML Notation: A filled diamond attached to the "whole" class.
    *   **Abstract Class:**
        *   Specifies required behaviors (operations/methods) without providing their actual implementations (methods without a body).
        *   Cannot be instantiated directly; must be subclassed.
        *   Purpose: Organize specific subclasses, provide common functionality, and enforce method overriding.
    *   **Multiple Inheritance:**
        *   Allows a class to inherit features from more than one parent class.
        *   **Advantages:** Reduces duplication, increases reusability, closely reflects real-world structures.
        *   **Disadvantages:** Can lead to complex and ambiguous situations, not supported by all OO languages.
        *   **Workarounds (if single inheritance is supported):** Delegation (using aggregation of roles) and Nested Generalization.
    *   **Generalization and Specialization:**
        *   **Generalization:** A bottom-up activity of extracting common properties from subclasses and placing them in a superclass (e.g., `Salaried Worker` and `Hourly Worker` generalize to `Employee`).
        *   **Specialization:** A top-down activity of defining a new class that inherits characteristics from a higher class and adds new ones.
        *   They are reverse processes.
        *   Inheritance rules: Query operations inherited; update operations inherited across extensions but blocked across restrictions; methods cannot change public interface but can be refined.
*   **Meta Data and Keys:**
    *   **Metadata:** Data that describes other data (e.g., class description for an object).
    *   **Key:** An attribute or combination of attributes used to identify an object.
        *   **Primary Key:** Uniquely identifies an object instance.
        *   **Candidate Key:** Possible primary keys not chosen.
        *   **Secondary Key:** May not uniquely identify but describes a set of instances with common characteristics.
*   **Integrity Constraints:** Rules to maintain data consistency and validity.
    *   **Referential Integrity:** Rules for associations, especially when related objects are inserted or deleted.
        *   **Insert Rules:** Define conditions for inserting a dependent class instance (e.g., Dependent, Automatic, Nullify, Default, Customized, No Effect).
    *   **Domain Integrity:** Constraints on valid values an attribute can assume (e.g., data type, length, range, uniqueness, nullability).
    *   **Triggering Operation Integrity Rules:** Govern insert, delete, update, and retrieval validity, involving effects of operations on other classes or attributes. Composed of an event/condition and an action set.

**Conclusion:** Object modeling is fundamental to OOAD, providing a stable, maintainable design by focusing on object structure and relationships like aggregation, composition, and generalization. It also incorporates essential database concepts like metadata, keys, and integrity constraints to ensure data consistency.

---

### Unit 7: Dynamic Modeling

**Main Idea:** Dynamic modeling describes the time-dependent behavior of a system and its objects, focusing on the sequence of operations, events that cause state changes, and the states themselves. It's crucial for interactive systems.

**Key Concepts & Points:**

*   **Purpose:** Shows time-dependent behavior, sequences of operations, and how objects change state in response to external stimuli. Captures control information.
*   **Events:**
    *   "Something that happened at a point of time" with no specific duration (instantaneous).
    *   A one-way transmission of information.
    *   **Concurrent Events:** Unrelated events occurring simultaneously without affecting each other.
    *   **Event Classes:** Name for common event structures, can have attributes (e.g., `Mouse button clicked (location)`).
    *   **Scenario and Event Traces:** A sequence of events occurring during a particular system execution.
*   **State and State Diagram:**
    *   **State:** A condition during an object's life where it satisfies some condition, performs an action, or waits for an event. Objects remain in a state for a finite time.
    *   **Actions:** Atomic, non-interruptible operations performed within a state or during a transition.
    *   **Activities:** Ongoing, continuous operations associated with a state.
    *   **Statechart Diagrams (State Machine):**
        *   Graphical representation of states and transitions.
        *   Shows possible states of an object and the transitions (triggered by events/conditions) that cause a change in state.
        *   UML Notation: States as rounded rectangles, transitions as arrows labeled `Event / Action`.
        *   Includes Initial State (solid circle) and Final State (bull's eye).
*   **Elements of a State Diagram:**
    *   **Initial State:** Starting point of flow.
    *   **State:** Condition of an object at an instant.
    *   **Transition:** Arrow indicating state change, labeled with trigger event/action.
    *   **History States (H):** Allows an object to return to its last active substate.
    *   **Event / Action:** The trigger causing a transition.
    *   **Signal:** A message sent by an event to cause a transition.
    *   **Final State:** End of the state diagram.
*   **Advanced Concepts:**
    *   **Entry and Exit Actions:** Atomic actions performed specifically upon entering or exiting a state.
    *   **Guard Condition:** A Boolean expression `[guard-condition]` that must be true for a transition to occur. Evaluated when the event fires.
    *   **Internal Transitions:** Actions performed in response to events while in a state, without changing the state.
*   **Concurrency:**
    *   Describes systems where objects can change state independently.
    *   Represented by **Concurrent Substates** (tiling a state's graphic region with dashed lines), where each subregion is a concurrent substate with its own nested state diagram.
    *   **Composite States:** States decomposed into concurrent (AND-relationships) or mutually exclusive (OR-relationships) substates.
    *   Aggregation often implies concurrency, as component states can undergo transitions in parallel.

**Conclusion:** Dynamic modeling, primarily through state diagrams, provides a crucial understanding of how a system behaves over time. It captures the sequences of events, states, and operations, illustrating the system's responsiveness to stimuli and the control flow within it.

---

### Unit 8: Functional Modeling

**Main Idea:** Functional modeling focuses on the data transformations within a system, illustrating "what" operations do. It uses Data Flow Diagrams (DFDs) to show the flow of data from inputs, through processes, to outputs, and the data stores involved.

**Key Concepts & Points:**

*   **Purpose:** Graphical representation of the object-oriented analysis model, focusing on processes that transform input data into desired output. Views the system as a "black box."
*   **Limitations:** Does *not* show *how*, *when*, or *why* transformations occur.
*   **Data Flow Diagrams (DFD):**
    *   Simple graphical technique to represent data flow, processing, and storage.
    *   Emphasizes hierarchical decomposition (abstract to detailed) to manage complexity. Also called "bubble chart."
*   **Features of a DFD (Symbols):**
    *   **Processes (Circles/Bubbles):** Functions that transform data. Have fixed inputs and outputs.
    *   **Data Flows (Labeled Arrows):** Represent information/data moving between processes, actors, or data stores.
        *   Can fork to send data to multiple destinations.
        *   **Synchronous Data Flow:** Direct connection, immediate use, processes operate at same speed.
        *   **Asynchronous Data Flow:** Data store sits between processes, allowing independent operation.
    *   **Actors (Rectangles):** External entities (sources or sinks) that interact with the system by providing input or consuming output.
    *   **Data Stores (Parallel Lines/Rounded Rectangle):** Passive objects representing data repositories (e.g., databases, files). Used for reading or writing data by processes.
    *   **Output Symbol (Chopped Rectangle):** Represents a hard copy output.
    *   **Constraints (String in Braces):** Limitations or conditions on data or processes (e.g., `{Dept: Sales}`).
    *   **Control Flows (Dotted Lines):** Signals generated by a process to start or stop other processes (typically Boolean values).
*   **Design Flaws in DFD:**
    *   **Beginner Flaws:**
        *   Context diagram must have only one bubble.
        *   External entities only appear in the context diagram (Level 0).
        *   Each process should decompose into 3-7 bubbles.
        *   **Balancing DFD:** Data flow in/out of a process must match the next higher level.
    *   **Representing Control Information:** DFDs are *not* flowcharts; they cannot capture "when," "why," or "how" transformations occur.
    *   **Poor Diagramming (Input/Output Mismatches):**
        *   **Black Hole:** Process has input flows but no output flows.
        *   **Miracle:** Process has output flows but no input flows.
        *   **Grey Hole:** Process outputs are greater than its inputs.
    *   **Illegal Data Flows:** Data stores can only connect to processes, not directly to other data stores or external entities.
*   **Sample Functional Model:** Demonstrates DFD decomposition up to Level 3 for an Online Shopping System (OSS), illustrating how abstract processes are refined into more atomic sub-processes.
*   **Functional Vs. Object Vs. Dynamic Model:**
    *   **Object Model:** Focuses on the *static structure* (attributes, operations) and *how* an object is implemented. (Class and Object Diagrams).
    *   **Dynamic Model:** Focuses on the *control aspect*, *temporal behavior*, and *when* operations occur in response to stimuli. (Interaction and State Transition Diagrams).
    *   **Functional Model:** Focuses on the *functional aspects* (processes, data transformations) and *what* operations do. (Data Flow Diagrams).
    *   **Interrelation:** These three models work together. Processes in the functional model often correspond to operations in the object model. The dynamic model specifies when active objects (actors) perform actions, while data stores (passive objects) respond to queries and updates in the functional model.

**Conclusion:** Functional modeling provides a clear, hierarchical view of data transformation within a system using DFDs. It complements object and dynamic models by detailing the "what" of system operations, ensuring a comprehensive understanding of the software system.