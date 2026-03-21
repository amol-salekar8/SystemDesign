# Introduction 

## What it is?
- Let's understand with simple real life example. Think of **building a house**.
  - **High Level Design (HLD)** : 
    - is like the architecture blueprint
    - It says where the rooms will be, how big they are, and how they're connected
  - **Low Level Design (LLD) :**
    - is like where the switches go, how the plumbing is laid out, what material to use.
- So LLD is all about the small, detailed planning you do before actually building the house.

## Definition
- LLD is where actual code start to take shape.
- It's crucial phase in the software development lifecycle that focuses on the detailed design of individual component or module of system.
- It involves specifying the internal structure, algorithms and data structure that will be used to implement the system's functionality.
- It also acts as bridge between HLD and actual coding.

## Coding Example 
- A simple example of LLD would be basic of login system for website where LLD would be
  - forming different details component like login(), signUp(), forgotPassword() along their functionality.

## Key Characteristics of LLD
- **Granular and Code level :**
  - LLD dives deep into the finals details of how each component will function.
  - It defines classes, functions, variables, and data structure.
  - **Example :**
    - Instead of saying "we need user authentication", LLD shows how its built, what classes handle it what methods validate login, and what happens on failure.
- **Implementation Focused :**
  - LLD is directly linked to how the actual code will be written.
  - It acts as blueprint for developers, guiding logic, flow and structure of modules.
  - If often includes pseudocode, flow diagrams, and sequence diagrams that show real-time data flow between functions.
- **Applies OOP principle :**
  - LLD makes heavy use of **OOP** concept like Classes, inheritance, abstraction, encapsulation, and polymorphism.
  - This help build modular, reusable, and maintainable system.
  - **Example :** a base class **Notification** class might have subclasses like **EmailNotification** and **SMSNotification** using inheritance and polymorphism.

## HLD vs LLD
| Aspect | HLD | LLD|
|-----|-----|------|
| Purpose | System overview and module | Detailed implementation and logic |
| Level of detail | Abstract | Highly detailed |
|Focus | Architecture, module, interfaces | Class diagram, methods details |
| Outcome | Module, System diagrams | Detailed class/ method diagrams |

## Importance of LLD
- Avoids code reworks
- Improves collaboration
- Promotes Scalability
- Encourage Best Practice

