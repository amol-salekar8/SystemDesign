# Single Responsibility Principle

## Defination
- A class should have only one reason to change.
- In other words class should have only one job, one responsibility, and one purpose.
- If class takes more responsibility, it becomes coupled.
- This means if one responsibility changes, the other responsibility may be also affected

## Real life analogy
- Example 1 : **Restaurant**
  - Imagine a chef who is responsible for cooking, cleaning, serving food and ordering groceries.
  - If the chef is busy cleaning, they can't focus on cooking and the quality of food may suffer.
  - Instead, different people should handle each task
  - This way, each person focus on their specific responsibility, leading to better result overall.
- Example 2 : **Traffic management**
  - Suppose we want go from mumbai to pune and there is one route i.e. Mumbai Pune Expressway and its working fine
  - Suppose in that highway we send all the vehicle of Nashik direction to the Mumbai Pune Expressway
  - There is possibility of traffic jam and its get affected to vehicle that going to pune
  - that why we have another route for pune and nashik

## Significance of SRP
- Understand with LeetCode compiler and currently compiler does following thing.
  - Adds Driver code
  - Perform syntax chec
  - Runs code with already fed test cases
  - Stores the output in Database.
  - Returns the necessary output to the user.
- If we implement this functionality in single class it would violate the SRP
- Instead, we can break it down into smaller classes, each with SRP
  - DriverCodeGenerator : Responsible to add driver code
  - SyntaxChecker : Responsible to performing syntax checks.
  - TestRunner : Responsible for running code with test cases.
  - DatabaseManager : responsible to store output in the database.
  - UserOutputHandler : Responsible for returning output to the user.
- Another name class Coordinator can be added to coordinate between all these classes/module.
- By using SRP we can make code more readable, maintainable, reusable, and less prone to bug. 

## Advantage of SRP 
- **Improved Maintainability :** 
  - Changes in one part won't affect to other part
- **Enhanced Readability :**
  - Smaller Focused classes are easier to read and understand.
- **Better Reusability :**
- **Facilitates Testing :**
  - Smaller classes are easier to test, as they have fewer responsibility
- **Lower Risk in Changes :**
  - Since each class handles only one concern, changes made to it are less likely to less error prone in implement class

## Common Mistake When Violating SRP

- Mixing Database logic with Business Logic
- Compiling UI code with business logic

## Note
**Q. Is SRP just for classes ?**
- No, SRP can be applied to methods, modules, microservice and even entire systems.
- The key is to ensure that each component should have only one responsibility and changes in one area won't affect to other.

## Real Life Implementation
- DatabaseConnection logic
- BusinessConnection logic 
- ThirdParty Connection logic
