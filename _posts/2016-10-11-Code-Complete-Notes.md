---
title:  "Code Complete Reading Notes"
excerpt: "Notes for Code Complete"
categories:
  - Blog
tags:
  - CODE_DEBUG_LIFE
use_math: false
---
# Code Complete Notes

## Part I: Laying the Foundation

### Chapter 1 Software Construction

#### 1.1 What is Software Construction

Problem definition, requirements development, construction planning, software architecture/high-level design, detailed design, coding and debugging, unit testing, integration testing, integration, system testing, corrective maintenance.

#### 1.2 Why is Software Construction Important?

#### 1.3 How to Read This Book

### Chapter 2 Metaphors for a Richer Understanding of Software

#### 2.1 The importance of Metaphors

#### 2.2 How to Use Software Metaphors

Algorithm vs. Heuristic

Conceptualizing the problem

#### 2.3 Common Software Metaphors

Software Penmanship: writing code.

> “In software construction, trying to create truly original work is often less effective than focusing on the reuse of design ideas, code and test cases from previous projects.”

Software Farming: Growing a System
>“By taking small steps, you minimize the trouble you can get into at any one time.”

Software Oyster Farming: System Accretion

Make the simplest possible version of the system that will run and add functions to it gradually.

Software Construction: Building Software

Building software construction benefit from appropriate levels of planning.

For large projects, over-engineering is sometimes beneficial solely due to the construction complexity.

Applying Software Techniques: The Intellectual Toolbox

> “People who are effective at developing high-quality software have spent years accumulating dozens of techniques, tricks, and magic incantations.”

> “The more you learn about programming, the more you fill your mental toolbox with analytical tools and the knowledge of when to use them and how to use them correctly.”

## Chapter 3 Measure Twice, Cut Once: Upstream Prerequisites

#### 3.1 Importance of Prerequisites

(High quality practices) emphasize quality at the beginning(planning and designing), middle(construction), and end(system testing) of a project.

The overarching goal of preparation is risk reduction.

If the work isn’t being done well in the first place, doing more of it will not be useful.

Some programmers do know how to perform upstream activities, but they don’t prepare because they can’t resist the urge to begin coding as soon as possible.

The architect consumes the requirements; the designer consumes the architecture; and the coder consumes the design.

It pays to do things right the first time.

In general, the principle is to find an error as close as possible to the time at which it was introduced.

#### 3.2 Determine the Kind of Software You’re Working On

Table 3-2 Typical Good Practices for Three Common Kinds of Software Projects

Sequential vs. Iterative Approaches

#### 3.3 Problem-Definition Prerequisite

#### 3.4 Requirements Prerequisite

An explicit set of requirements is helpful.

#### 3.5 Architecture Prerequisite

The quality of the architecture determines the conceptual integrity of the system, which in turn determines the ultimate quality of the system.

A system architecture

* Needs an overview that describes the system in broad terms
* Specifies the major classes to be used
* Describes the major files and table designs to be used. Data should normally be accessed directly by only one subsystem or class, except through access classes or routines that allow access to the data in controlled and abstract way.
* Identifies business rules and describes their impact have on the system’s design.
* Specifies user interface design. The architecture should be modularized so that a new user interface can be substituted without affecting the business rules and output parts of the program.
* Describes a plan for managing scarce resources such as database connections, threads and handles.
* Describes the approach to design-level and code-level security.
* Specifies performance if it is a concern.
* Describes scalability. If scalability is not an issue, the architecture should make that assumption explicit.
* Describes possible localization of the program.
* Describes Input/Output
* Specifies error processing. (Detailed discussion in the book)
* Describes fault tolerance.

Architectural feasibility

Overengineering for robustness.

Buy-vs.-Build Decisions.

Reuse decisions.

Describe a strategies for handling changes that show up in development.

General architectural quality.

#### 3.6 Amount of Time to Spend on Upstream Prerequisites

10-20% effort and about 20-30% schedule

### Chapter 4 Key Construction Decisions

#### 4.1 Choice of Programming Language

Programmers are more productive using a familiar language than an unfamiliar one.

Programmers working with high-level languages achieve better productivity and quality than those working with lower-level languages.

#### 4.2 Programming Conventions

Before construction begins, spell out the programming conventions you’ll use.

#### 4.3 Your Location on the Technology Wave

Understanding the distinction between programming in a language and programming into one is critical. If your language lacks the constructs that you want to use or is prone to other kinds of problems, try to compensate them. Invent your own coding conventions, standards, class libraries, and other augmentations.

#### 4.4 Selection of Major Construction Practices

## Part II: Creating High-Quality Code

### Chapter 5: Design in Construction

#### 5.1 Design Challenges

* Design is the activity that links requirements to coding and debugging.
* Design is a wicked problem - it can only be clearly defined by solving it.
* Design is a sloppy process - it is hard to know when your design is “good enough” (most common answer to that question is “when you’re out of time”).
* Design is about tradeoffs and priorities
* Design involves restrictions - the point of design is partly to create possibilities and partly to restrict possibilities.
* Design is nondeterministic
* Design is a heuristic process - “rules of thumb” or “things to try that sometimes work”. No tool is right for everything.
* Design is emergent - designs evolve and improve through reviews, discussion and experience.

#### 5.2 Key Design Concepts

Software’s primary technical imperative has to be managing complexity.

Minimize the amount of a program you have to think about at any one time. Dividing the system into subsystems and keeping the routines short.

Desirable Characteristics of a design:

* Minimal Complexity
* Ease of maintenance
* Loose coupling
* Extensibility
* Reusability
* High fan-in
* Low-to-medium fan-out
* Portability
* Leanness
* Stratification
* Standard Techniques

Levels of design:

* Software system
* Division into subsystems/packages - minimize communication between subsystems. Common subsystems:
    * Business rules
    * User interface
    * Database access
    * System dependencies
* Division into classes within packages
* Division into data and routines within classes
* Internal routine design

#### 5.3 Design Building Blocks: Heuristics

Designing objects:

* Identify the objects and their attributes (methods and data)
* Determine what can be done to each object
* Determine what each object is allowed to do to other objects
* Determine the parts of each object that will be visible to other objects
* Define each object’s interface

Form consistent abstraction for each level.

Encapsulate Implementation details - encapsulation helps to manage complexity by forbidding you to look at the complexity.

Inherit when it simplifies the design - inheritance can produce great benefits when used well but do great damage when used naively.

Hide secrets - emphasizing on hiding complexity. Minor changes to a system might affect several routines within a class, but they should not ripple beyond the class interface. There are two categories of secrets:

Hiding complexity so that your brain doesn’t have to deal with it unless you’re specifically concerned with it.

Hiding sources of change so that when change occurs, the effects are localized.

Identify items that seem likely to change - some common areas:

* Business rules
* Hardware dependencies
* Input and output
* Nonstandard language features
* Difficult design and construction areas
* Status variables
* Data-size constraints
* Separate items that seem likely to change - compartmentalize each volatile component into its own class or with other components that may change at the same time.
* Isolate items that seem likely to change - design the interclass interfaces to be insensitive to the potential changes. The class’s interface should protect its secrets.

Anticipate different degrees of change.

Keep coupling loose - small number of connections between modules, documenting global data connection and make it obvious, work on flexibility.

Kinds of coupling:

* Simple-data-parameter coupling - normal and acceptable coupling. Couple two modules by passing primitive data types or in a parameter lists.
* Simple-object coupling - fine. A module is simple-object coupled to an object if it instantiates that object.
* Object-parameter coupling. Passing object instead of primitive data types.
* Semantic coupling - not too good. This occurs when one module doesn’t use syntactic element of another module but of some semantic knowledge of another module’s inner workings, such as control flags or sequential global data modification. This is dangerous practice because computer may not detect errors.

Look for common design patterns. Some popular design patterns:

* Abstract factory - supports creation of sets of related objects by specifying the kind of set but the kinds of each specific object.
* Adapter - Converts the interface of a class to a different interface.
Bridge - builds an interface and an implementation in such a way that either can vary without the other varying.
* Composite - consists of an object that contains additional objects of its own type so the client code can interact with the top-level object and not concern itself with all the detailed objects.
* Decorator - attaches responsibilities to an object dynamically, without creating specific subclasses for each possible configuration of responsibilities.
* Facade - Provides a consistent interface to code that wouldn’t otherwise offer a consistent interface.
* Factory Method - instantiates classes derived from a specific base class without needing to keep track of the individual derived classes anywhere but the Factory Method.
* Iterator - A server object that provides access to each element in a set sequentially.
* Observer - Keeps multiple objects in sync with one another by making an object responsible for notifying the set of related objects about changes to any member of the set.
* Singleton - provides global access to a class that has one and only one instance.
* Strategy - defines a set of algorithms or behaviors that are dynamically interchangeable with each other.

Template Method - defines the structure of an algorithm but leaves some of the detailed implementation to subclasses.

Aim for strong cohesion - the more the code in a class supports a central purpose, the more easily your brain can remember everythign the code does.

Build hierarchies

Formalize class contracts

Assign responsibilities

Design for test

Avoid failure

Choose binding time consciously

Make central points of control

Consider using brute force

Draw a diagram

Keep your design modular

#### 5.4 Design Practices

Iterate over the design.

Divide and conquer.

Top-down and bottom-up design approaches.

Experimental prototyping.

Collaborative design.

Capturing the design work - insert design documentation into the code, capture discussion and decision on a wiki, write email summaries, use a digital camera for whiteboard drawings, save design flip charts, use CRC (class, responsibility, collaborator) cards

#### 5.5 Comments on Popular Methodologies

### Chapter 6: Working Classes

> A class is a collection of data and routines that share a cohesive, well-defined responsibility..... A key to beging an effective programmer is maximizing the portion of a program that you can safely ignore while working on any one section of code.

#### 6.1 Class Foundations: Abstract Data Types (ADTs)

> An abstract data type is a collection of data and operations that work on that data. The operations both describe the data to the rest of the program and allow the rest of the program change the data.

Using ADT can reduce seemingly ad hoc code and is a better programmer practice.

Some benefits of using ADTs:

* Hide implementation details.
* Changes don't affect the whole programming. Also more centrailzed control over class functionalities.
* Make the interface more informative.
* Easier to improve performance. Change core routines to make things faster.
* The program is more obviously correct - it becomes more self-documenting.
* No need to pass data all over the program.
* Enable one to work with real-world entities rather than low-level implementation structures.

Some guidelines:

* Build or use typical low-level data types as ADTs.
* Treat common objects such as files as ADTs.
* Refer to an ADT independently of the medium it is stored on.

For non-object-oriented languages, you have to handle multiple instances of data with ADTs yourself by making operation purpose more explicit.

#### Good Class Interface

> The first and probably most important step in creating a high-quality class is creating a good interface.

Be sure to understand what abstract the class is implementing and only implement one ADT at a time. Do not add public members that are inconsistent with the interface abstraction. Consider abstraction and cohesion together.

Encapsulation helps enforce abstraction. Make sure you

* Minimize accessibility of classes and members.
* Do not expose member data in public.
* Avoid putting private implementation details into a class's interface. E.g. do not declare private member in your header files.
* Do not make assumptions about the class's users. A class should make no assumption how the interface will/won't be used.
* Avoid friend classes - they compromise encapsulation.
* Do not put a routine into the public interface just because it uses only public routines.
* Favor read-time convenience to write-time convenience. Write for readability.
* Be very, very wary of semantic violation of encapsulation. The implementation should take care of routines such as initialization and termination automatically, instead of relying on how public methods are called.
* Watch for coupling that is too tight.
    * Minimize accessibility of classes and members.
    * Avoid friend classes, because they're tightly coupled.
    * Make data private rather than protected in a base class to make derived classes less tightly coupled to the base class.
    * Avoid exposing member data in a class's public interface.
    * Observe the "Law of Demeter".

#### 6.3 Design and Implementation Issues

##### Containment ("has a" relationships)

> Containment is the simple idea that a class contains a primitive data element or object...... Containment is the work-horse technique in object-oriented programming.

* Implement "has a" through containment
* Implement "has a" through private inheritance as a last resort
* Be critical of classes that contain more than about 7 data members (which is about as many items as a person can remember in the background).

##### Inheritance ("is a" relationship)

> Inheritance is the idea that one class is a specification of another class. The purpose of inheritance is to create simpler code by defining a base class that specifies common elements of two or more derived classes.

* Implement "is a" through public inheritance
* Design and document for inheritance or prohibit it
* Adhere to the Liskov Substitution Principle (LSP) - you shouldn't inherit a base class unless the derived class truly "is a" more specific version of the base class.
* Be sure to inherit only what you want to inherit. Inherited routines are divided into
    * An abstract overridable routine - the interface is inherited but not implementation
    * An overridable routine - the default implementation is inherited but it can be overrided
    * A non-overridable routine - the implementation is inherited and finalized.
* Do not "override" a non-overridable member function - do not reuse names of non-overridable base-class routines in derived classes.
* Move common interfaces, data, and behavior as high as possible in the inheritance
* Be suspicious of classes of which there is only one instance. (Singleton pattern is an exception to this guideline)
* Be suspicious of classes that override a routine and do nothing inside the derived routine.
* Avoid deep inheritance trees. It is suggested to limit the maximum inheritance level to 6.
* Prefer polymorphism to extensive type checking.
* Make all data private, not protected.

Multiple inheritance is powerful but dangerous.

##### Member Functions and data

Guidelines for implementing member functions and member data

* Keep the number of routines in a class as small as possible
* Disallow implicitly generated member functions and operators you don't want
* Minimize the member of different routines called by a class
* Minimize indirect routine calls to other classes. "Law of Demeter" - If object A instantiate Object B, it can call any of Object B's routines, but it should avoid calling routines on objects provided by Object B.
* In general, minimize the extent to which a class collaborates with other classes.

##### Constructors

Guidelines for constructors

* Initialize all member data in all constructors, if possible
* Enforce the singleton property by using a private constructor (hide public constructor)
* Prefer deep copies to shallow copies until proven otherwise

#### 6.4 Reasons to Create a Class

A list of good reasons to create a class

* Model real-world object
* Model abstract objects
* Reduce complexity
* Isolate complexity
* Hide implementation details
* Limit effects of changes
* Hide global data
* Streamline parameter passing
* Make central points of control
* Facilitate reusable code
* Plan for a family of programs
* Package related operations
* Accomplish a specific refactoring

Avoid the follwing classes

* God classes
* Eliminate irrelevant classes
* Classes named after verbs - a class has only behavior but no data is generally not really a class

### Chapter 7: High-Quality Routines

### Chapter 8: Defensive Programming

### Chapter 9: The Pseudocode Programming Process

## Part III: Variables

### Chapter 10: General Issues in Using Variables

### Chapter 11: The Power of Variable Names

### Chapter 12: Fundamental Data Types

### Chapter 13: Unusual Data Types

## Part IV: Statements

### Chapter 14: Organizing Straight-Line Code

### Chapter 15: Using Conditionals

### Chapter 16: Controlling Loops

### Chapter 17: Unusual Control Structures

### Chapter 18: Table-Driven Methods

### Chapter 19: General Control Issues

## Part V: Code Improvements

### Chapter 20: The Software-Quality Landscape

### Chapter 21: Collaborative Construction

### Chapter 22: Developer Testing

### Chapter 23: Debugging

### Chapter 24: Refactoring

### Chapter 25: Code-Tuning Strategies

### Chapter 26: Code-Tuning Techniques

## Part VI: System Considerations

### Chapter 27: How Program Size Affects Construction

### Chapter 28: Managing Construction

### Chapter 29: Integration

### Chapter 30: Programming Tools

## Part VII: Software Craftsmanship

### Chapter 31: Layout and Style

### Chapter 32: Self-Documenting Code

### Chapter 33: Personal Character

### Chapter 34: Themes in Software Craftsmanship

### Chapter 35: Where to Find More Information
