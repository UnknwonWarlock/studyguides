# <u>OOP Final</u>

## <u>UML Multiplicity</u>

### Mandatory

> - Single
>   - (just the number)
> - Multivalued
>   - (starting amount ... end amount [* = as many as desired])

### Optional

> - Single
>   - (0 ... 1)
> - Multivalued
>   - (*, 0 ... *, 0 ... 2)

### Other

> - Usually seen with containers
>   - Vectors
>   - Arrays, etc
> - C++17 std::optional or boost::optional

### Examples

> ![Alt text](assets/OOP/umlMult.png)

## <u>Generalization (Inheritance)</u>

### Overview

> - IS A relationship
> - To solve a design problem, if there is no design problem don't use inheritance
> - Abstract Class - class with at least one pure virtual function (virtual return methodName() = 0)
> - Polymorphism - Single interface to entities of different types
> - Static Polymorphism - Overloading functions and templates
> - Dynamic Polymorphism - Virtual methods

### Problems to solve with Generalization

> - Multiple Related Classes (graduate and undergraduate students)
> - Bidirectional Association

### Examples

> ![Alt text](assets/OOP/general.png)

## <u>Association</u>

> - HAS A relationship
> - One class has an element of another class

### Composition

> #### General
>
> > - Target belongs only to the source
> > - Source controls the lifetime of the target
> > - These Objects are fields/data members, or pointers/references to objects created internally
> > - EX: Source = University Target = College
>
> #### Example
>
> > ![Alt text](assets/OOP/composition.png)

### Aggregation

> #### General
>
> > - Part of relationship
> > - Special kind of association with roles and multiplicities often used
> > - Targets may be shared with source but source doesn't control targets' lifetime
> > - These fields are pointers/references to type of the object and are created externally
> > - EX: Source = Club Target = Person
>
> #### Example
>
> > ![Alt text](assets/OOP/aggregate.png)

### Aggregation vs Composition

> - Prefer Composition over Aggregation whenever possible

## <u>Direct Inheritance</u>

> ```c++
> DerivedClass : public BaseClass
> {
>     
> };
> ```

## <u>Inheritance from Handler used by Base class</u>

> ```c++
> BaseClass
> {
>     private:
>     	//can only be set in member initialization list
>     	BaseClassHandler &handler;
> };
> 
> BaseClassHandler
> {
>     virtual void method(){};
>     virtual void method2(){};
> };
> 
> MyHandler : public BaseClassHandler
> {
>     //implement it
> };
> 
> MyHandler hand;
> BaseClass myObject(hand);
> ```

## <u>Template?</u>

> ```c++
> //Works to accept lamda functions
> template<typename name1, typename name2, typename name3, ... >
> 
> //When using in a class method must reference it is a template
> className<templateName>::methodName(){}
> 
> //Can say what template when calling an object declaraction
> Myclass<int> a;
> 
> //can set a template parameter to have a default type
> template<typename name1 = char>
> 
> //Need a template<> for every method that requires templates
> ```

## <u>RAII</u>

> ### What is it?
>
> - Resource Acquisition Is Initialization
>   - Holding a resource is tied to an object's lifetime
>     - Constructor: Allocate Resource
>     - Deconstructor: Free Resource
>
> ### Why is it important?
>
> - It prevents:
>   - Memory leaks
>   - Invalid use of resource
>   - Double free
>
> ### Interfaces
>
> - Constructor - allocate resource
> - Deconstructor - free resource
> - Direct Access - provides direct access to resource
> - Boolean - check if resource exists
> - Copy Assignment - Transfer resource control to a new RAII Object
> - Deallocate - free resource before deconstructor
>
> ### How to Implement?
>
> - Smart Pointers:
>   - shared_ptr : C++11
>   - unique_ptr : C++11
>   - auto_ptr : Deprecated in C++17
> - Use Cases
>   - Optional
>     - Solution : std::optional
>   - Lazy Initialization
>     - Solution : std::unique_ptr
>   - With a Library
>     - Solution : seperation of concerns?

## <u>Coupling</u>

> - Must be limited and Controlled
> - Entropy of systems and designs increases coupling
> - Increasing cohesion may lead to more coupling 
>
> ### What is it?
>
> - degree of interdependence between software modules; a measure of how closely connected two routines or modules are; the strength of the relationships between modules.
> - External measure of the relationships of a class to other classes
>
> ### Why is it Important?
>
> - Perhaps most important characteristic of a system
> - Effects:
>   - Development Path
>   - How a system is broken up for testing
>   - How much reuse can be performed
>   - Greatly Effects : the complexity of a system
>
> ### Extras
>
> - States of Coupling:
>   - Tightly - hard to use separately, test, develop, and maintain
>   - Loosely - much easier to use separately, test, develop, and maintain
>   - Uncoupled - Can be developed, tested, maintained, and used separately.
> - Types of Coupling:
>   - Message (very best) - Parameters are passed via a non-private data format
>   - Data coupling (best) - One module only passed the data needed by the other module
>   - Stamp - One module passes more data then needed to another module
>   - Control - Client passes a flag or command that explicitly controls what the called code is doing
>   - Common - Using global variables, i.e., global coupling
>   - Content (worst) - A module directly references the content of another module, Content coupled modules are inextricably interlinked.
>     - Exposing data members as public is a form of this

## <u>Design Patterns</u>

> - Need to way to communicate about the repeating patterns that come up
> - Issues:
>   - Must be widely applicable
>   - Need safe solutions
>   - Need efficient solutions
> - Origins:
>   - Each pattern describes a problem which occurs over and over again in our environment and then describes the core of the solution to that problem, in such a way that you can use the solution a million times over, without every doing it in the same way twice
> - Design Patterns:
>   - *Design Patterns: Elements of Reusable Object-Oriented Software* 
> - Elements of Design Patterns:
>   - Name
>   - Problem
>   - Solution
>   - Consequences
> - Pattern Categories:
>   - Creational - How objects are created
>   - Behavioral - Algorithms and the assignment of responsibilities between objects
>   - Structural - How classes and objects are composed to form larger objects

## <u>Template Method</u>

> - Fundamental technique for code reuse
> - Leads to IoC
> - Applicability:
>   - Implement *invariant* parts of an algorithm and leave it up to subclasses to implement behavior that can vary
>   - factor and localize common behavior in subclasses to avoid code duplication
>   - control subclass extensions with “hook” operations
> - Consequences:
>   - *primitive operations* (i.e., abstract operations) must be overridden
>   - *hook operations* - default behavior that subclasses can extend if necessary. may be overridden and often does nothing by result
>
> ### Example
>
> ![Alt text](assets/OOP/template.png)

## <u>Factory Method</u>

> - Frameworks use abstract classes to define and maintain relationships between objects
> - Also responsible for creating these objects
> - However, knowledge of what type of object to create may not be in the framework
> - Applicability:
>   - Classes can’t anticipate the class of objects it must create
>   - Classes want subclasses to specify the objects it creates
>   - Classes delegate responsibility to one of several helper subclasses, and you want to localize the knowledge of which helper subclass is the delegate
> - Participants:
>   - Product
>     - Defines the interface of objects the *factory method* creates
>   - ConcreteProduct
>     - Implements the Product interface
>   - Creator
>     - Declares the *factory method*, which returns an object of type Product
>   - ConcreteCreator
>     - Overrides the factory method to return an instance of a ConcreteProduct.
> - Consequences:
>   - Code only deals with Product interfaces, so can work with any user-defined ConcreteProduct classes
>   - Does require client to subclass Creator for each unique ConcreteProduct
>   - Can define a non-abstract default, e.g, CreateFileDialog, that subclasses can override if needed
>
> ### Examples
>
> ![Alt text](assets/OOP/factory.png)

## <u>Composite</u>

> - Compose objects into tree structures to represent part-whole hierarchies
> - Applicability:
>   - Use When you Want to represent part-whole hierarchies of objects
>   - Use when you Want clients to be able to ignore the difference between compositions of objects and individual objects, as clients will treat all objects in the composite structure uniformly
> - Participants:
>   - Component
>     - Declares the interface for objects in the composition
>   - Client
>     - Manipulates objects in the composition through the Component interface
>   - Composite
>     - Defines behavior for components having children
>   - Leaf
>     - Represents leaf object (leaf’s have no children) in the composition
> - Consequences:
>   - A class hierarchy of primitive and composite objects which permits recursive structures
>   - Clients are simple as they handle primitive and composite objects the same
>   - Can add new kinds of components, both Composite or Leaf, that work automatically with existing client code
>   - Can make the design overly general, as any kind of Component can be added
>
> ### Example
>
> ![Alt text](assets/OOP/composite.png)

## <u>Command</u>

> - Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations
> - Applicability:
>   - Use when you want to:
>     - Parameterize objects by an action to perform, as Menultem objects did above. eCommands are an object-oriented replacement for callbacks.
>     - specify, queue, and execute requests at different times
>     - Support undo.
> - Participants:
>   - Command - Declares an interface for executing an operation.
>   - ConcreteCommand (e.g., PasteCommand, OpenCommand)    
>     - Defines a binding between a Receiver object and an action.
>     - Implements `execute()` by invoking the corresponding operation(s) on Receiver
>   - Client (e.g., Application) Creates a ConcreteCommand object and sets its receive
>   - Invoker (e.g., Menultem) Asks the command to carry out the request
>   - Receiver (e.g., Document, Application) Knows how to perform the operations associated with carrying out a request
> - Consequences:
>   - Command decouples the object that invokes the operation from the one that knows how to perform it
>   - Commands are first-class objects, and can be manipulated and extended like any other object.
>   - Multiple commands can be assembled into a composite command (e.g., MacroCommand), and are instances of the Composite pattern
>   - Easy to add new Commands, because you don’t have to change existing classes.
>
> ### Examples
>
> ![Alt text](assets/OOP/command.png)

## <u>Adapter</u>

> - Convert the interface of a class into another interface clients expect
> - Applicability:
>   - Want to use an existing class, and its interface does not match the one you need
>   - Want to create a reusable class that cooperates with unrelated or unforeseen classes, that is, classes that don’t necessarily have compatible interfaces.
>   - *object adapter* Need to use several existing subclasses, but it’s impractical to adapt their interface by subclassing every one
> - Participants:
>   - Target (e.g., Shape)    
>     - Defines the domain-specific interface that Client uses
>   - Client (e.g., DrawingEditor)    
>     - Collaborates with objects conforming to the Target interface
>   - Adaptee (e.g., TextView)    
>     - Defines an existing interface that needs adapting.
>   - Adapter (e.g., TextShape)    
>     - Adapts the interface of Adaptee to the Target interface
> - Consequences:
>   - Class Adapter    
>     - Adapts Adaptee to Target by committing to a concrete Adaptee class, which does not allow adaptation of a class and it subclasses
>     - Since Adapter is a subclass of Adaptee, Adapter can override some of Adaptee’s behavior
>     - Introduces only one object, with no further pointer indirection
>   - Object Adapter
>     - A single Adapter can work with a class and all of its subclasses
>     - Does not directly allow subclassing Adaptee behavior
>
> ### Examples
>
> ![Alt text](assets/OOP/adapter.png)
>
> ![Alt text](assets/OOP/oadapter.png)

## <u>Facade</u>

> - Provide a unified interface to a set of interfaces in a subsystem
> - Applicability:
>   - se the Facade pattern when you want to provide a simple interface to a complex subsystem
>   - There are many dependencies between clients and the implementation classes of an abstraction
>   - You want to layer your subsystems
> - Participant:
>   - Facade (e.g., Compiler)    
>     - Knows which subsystem classes are responsible for a request and delegates client requests to appropriate subsystem objects
>   - *subsystem classes* (e.g., Scanner, Parser, ProgramNode, etc.)
>     - Handle work assigned by the Facade object
>     - Have no knowledge of the Facade, and keep no references or pointers to the Facade
>     - Are not marked as part of the pattern
> - Consequences (benefits)
>   - Shields clients from subsystem components reducing the number of objects that clients deal with and making the subsystem easier to use
>   - Promotes weak coupling between the client and the subsystems
>   - Reduces need for recompilation
>   - Simplifies porting to other platforms
>   - Allows a choice between ease of use and generality as clients can use the subsystems directly
>
> ### Examples
>
> ![Alt text](assets/OOP/facade.png)

## <u>Singleton</u>

> - Ensure a class only has one instance, and provide a global point of access to it
> - Participants:
>   - *Singleton*    
>     - Defines an instance operation that lets clients access a unique instance
>     - The instance (in C++) is a static member function
>     - Class may be responsible for creating its own unique instance (typical)
> - Consequences:
>   - Controls access to sole instance
>   - In place of global variables, avoids polluting the global name space
>   - The Singleton class may be subclassed
>   - Once in place, can change your mind and allow more than one instance
>   - More flexible than static member functions, which are not polymorphic (i.e., cannot make them virtual)
>
> ### Examples
>
> ![Alt text](assets/OOP/singleton.png)

## <u>Dependency Injection</u>

> - Define a family of algorithms, encapsulate each one, and make them interchangeable. Strategy lets the algorithm vary independently from clients that use it.
> - Broader form of Inversion of Control
> - Once chosen, doesn’t tend to change during runtime
> - Primary purpose is for *testing*
> - Often extends the interface beyond that of the regular client

## <u>Exception Handling</u>

> - std::logic_error - faulty logic within the program such as violating logical preconditions or class invariants and may be preventable
>   - `std::invalid_argument` argument value has not been accepted
>   - `std::domain_error` inputs are outside of the domain on which an operation is defined
>   - `std::length_error` exceed implementation defined length limits for some object
>   - `std::out_of_range` access elements out of defined range
> - std::runtime_error - errors due to events beyond the scope of the program and can not be easily predicted
>   - `std::range_error` result of a computation cannot be represented by the destination type
>   - `std::overflow_error` arithmetic overflow errors, i.e., result of a computation is too large for the destination type
>   - `std::underflow_error`result of a computation is a subnormal floating-point value

> ```c++
> try
> {
>     //code to try
> }
> catch (std::exception &e)
> {
>     std::cerr << e.what() << std::endl;
> }
> 
> //Example of a custom exception
> class XMLParserError : public std::exception
> {
>     private:
>         std::string whatArg;
> 
>     public:
> 
>         explicit XMLParserError()
>         {}
>         explicit XMLParserError(const std::string& arg) : whatArg(arg)
>         {}
> 
>         const char* what() const throw()
>         {
>             return &whatArg[0]; 
>         }    
> };
> ```

## <u>Software Architecture</u>

### <u>Layered</u>

> - Hierarchical decomposition of a system into subsystems (layers) with each providing a higher level of services provided from lower level subsystems
> - *closed architecture* each layer can only depend on the layer immediately below
> - *open architecture* each layer can access any layer below

### <u>Pipe & Filter</u>

> - Subsystems are called *filters* and associations between the filters are called *pipes*
> - Filters only know the content and format of data being received and produced, nothing about the other filters in the system
> - Filters are executed concurrently and synchronization is done via pipes
> - Very reconfigurable
> - Transformational systems

## <u>Encapsulation & Information Hiding</u>

### <u>Encapsulation</u>

> - the bundling of data with the methods that operate on that data

### <u>Information Hiding</u>

> - hide the internal representation, or state, of an object from the outside

## <u>Dynamic & Static Dispatch, VTables</u>

### <u>Dynamic Dispatch</u>

> - selecting which implementation of a polymorphic operation (method or function) to call at run time
> - Requires additional data in the executable
> - C++ only supports *single dispatch*.

### <u>Static Dispatch</u>

> - Which operation (method or function) will be called is determined at compile time
> - Fast as a call can be made
> - Preferred by the compiler for these reasons

### <u>VTables</u>

> - *virtual table*
> - Created for every class that has virtual methods, or derives from a class with virtual methods
> - First part if for typeinfo and other things
> - Rest is an array of function pointers

## <u>C++ Inheritance Specifiers</u>

> - override
>   - allows virtual function to override the base class virtual requirements. (const and non-const)
> - final
>   - On a class, enforces that the class cannot be derived from
>   - On a method, enforces that the method cannot be overriden

## <u>C++ Constructor Specifiers</u>

> - explicit
>   - The `explicit` specifier prevents the compiler from using that constructor for implicit conversion
>   - Consider a good practice of always using `explicit` on single-parameter constructors until it causes a problem
> - mutable
>   - Data members with `mutable` are able to change and still allow the object to be const
>   - *bitwise const*
>     - Not a single bit can change
>   - *logical const*
>     - The behavior of the object will not change
>     - *bitwise const* implies logical const
> - default
>   - Indicates that the compiler-provided constructor is implicit, even if does not appear according to the constructor rules
>   - Can be applied to other constructors, standard methods, and destructors
> - delete





