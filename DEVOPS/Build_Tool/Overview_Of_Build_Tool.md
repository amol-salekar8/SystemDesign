# Build Tool

**Why we used ?**
- Backbone of modern software development, automating the process of **turning raw source code into deployable** applications.
-  **Instead of relying on repetitive manual steps**, build tools handle compilation, testing, dependency management, and packaging making the development lifecycle faster, more consistent, and less error-prone.
- **Note :**
  - Build tools are crucial to the state of the art in software development. 
  - They **eliminate the need for human labor** and its accompanying inconsistencies and inefficiencies. 
  - Adopting build tools allows teams to **deliver high-quality software** more efficiently, enhancing the whole development process.

********

## Challenges in Manual Processes
- **Human errors :** Misconfigurations, overlooked stages, and the omission of crucial files
- **Inefficiency :** Doing the same thing repeatedly by hand is very expensive on time energy, which is turn slow down development & cause irritation.
- **Inconsistency :** It arrises when different developer use their individual manual technique to complete a build, making it difficult to work together and keep up with the project.
- **Scalability Challenges :** Manual process management becomes more time-consuming & error-prone as the scope of the project expands.

******

## Why use Build Tools? 
- Build tool have characteristics and features that speed up and improve the building & deployment of software applications.
1) **Automation :** ( reduce manual work )
   - It **eliminates the requirement for manual involvement & error** by automating the process.
   - This is helpful while working on complicated projects or frequently modifying the code.
2) **Consistent :** ( already write script )
   - It guarantees reproducible outcome across the wide range of development settings & platforms by strictly **adhering to prescribed build process**.
   - As a result, fewer problems with software deployment due to improper configuration will occur.
3) **Dependency Management :** ( download dependency according to script )
   - It makes it simpler to **include third-party code in the project** by handling requirements on external libraries & frameworks.
   - They can streamline the development process by automatically downloading, managing, and changing dependencies.
4) **Task Parallelism :** ( multi task)
   - Many build programs can run multiple tasks simultaneously, reducing build times and boosting productivity.
   - It is beneficial for large projects with many moving parts.
5) **Incremental Builds :** ( Instead of entire do the changed file)
   - Tools for construction allow for progressive construction, which saves time and materials.
   -  **Instead of recompiling the entire application, they detect changes in the source code and merely recompile the affected sections**.
6) **CI/CD Integration :**
   - This helps to automate the build & deployment procedures fully.
   - This synchronization allows for dependable software delivery in a short amount of time by continuously integrating and deploying updates to production settings.
7) **Code compilation :** ( convert source to binary )
   - The process by which build tools transform source code into binary executables or intermediary representations.
   - This process aids in detecting syntax faults and other problems during the development phase.
8) **Testing and Quality Assurance :**
   -  Automated tests may be run as part of the build process to make sure that new features and fixes to the code don’t break anything & that the code is up to the quality standards that have been established.
9) **Compatible and expandable :**
   - These resources are compatible with numerous languages, frameworks, and operating systems.
   - You can modify them to meet the requirements of your project by adding new features, such as plugins or scripts written by hand.
10) **Deployment and Packaging :**
    - They simplify transferring software to end-users or different groups by helping package it into deployable formats.

********

| Feature | 	Software Build Tools         |	DevOps / CI Build Tools |
|----------|-------------------------------|-----------------------|
|Purpose| 	Build and package code       |	Automate the development pipeline
|Scope	| Only building the application |	Full CI/CD workflow
|Used By| 	Developers                   |	DevOps engineers / automation systems
|Output	| Executable or build artifact  |	Automated build + test + deployment
|Examples| 	Ant, Maven, Gradle           |	Jenkins, GitHub Actions

********

## Build Tools
1️⃣ [**Jenkins**](../Jenkins/Jenkins_Core.md)
   - **Description :**
      - Jenkins is a widely used open-source automation server that makes CI/CD procedures easier. 
      - It allows programmers to rapidly and reliably create, test, & release software. 
      - It works with multiple programming languages and can run on various platforms (Windows, Linux, and macOS).
   - **Features :**
     - A simple setup process across several environments. 
     - Allows for flexible plugin-based integration with various third-party tools and technologies.
     - Scaling up to more computers is now possible with distributed builds.
     - Features native VCS integration (Git, Subversion, etc.).
     - Allows for in-depth tracking and reports.
   - **Advantages :**
     - Extensive plugin ecosystem allows for great personalization and adaptability.
     - Lots of people who care about it and lots of information about it.
     - It has an intuitive design that makes it simple for everyone, not just programmers.
     - Allows easier deployment in cloud settings by supporting integration with cloud services.
     - Ideal for tasks of any scale and scope.
   - **Limitations :**
     - Requires a lot of resources, especially for large-scale implementations.
     - Additional settings and programming may be necessary for managing complex pipelines.
     - Inadequate configuration and maintenance could introduce security risks.
********
2️⃣ [**Gradle :**](Gradle.md)
   - **Description :**
     - The open-source [build automation](https://www.browserstack.com/guide/build-automation) tool Gradle places a premium on adaptability and speed. 
     - It defines build scripts with a Groovy-based DSL (Domain-Specific Language).
   - **Feature :**
     - Encourage readability and maintainability, such as declarative & brief build scripts.
     - **Management of dependencies** that makes use of intensive caching & parallel resolution.
     - Allows for the **construction of multiple projects** dependent on one another.
     - Gradle Wrapper enables reproducible builds in several IDEs.
     - Easily expandable through plugins; works with various other programs and hardware.
   - **Advantage :**
     - Incremental construction capabilities provide for quick and efficient build times.
     - **Exceptionally adaptable**, letting you make changes for each project.
     - It’s **flexible** because it works with Java and other languages too.
   - **Limitations :**
     - More difficult to pick up if you’re unfamiliar with Groovy or DSLs.
     - There isn’t much help for aging software or Java versions.
********
3️⃣ [**Maven :**](Maven.md)
  - **Description :**
    - Apache Maven is a popular build automation tool that has found its niche in Java development. 
    - It **controls construction via XML-based Project Object Model (POM)** files.
  - **Features :**
    - This method prioritizes convention over configuration, which **streamlines project setup & cuts down on configuration time and hassle**.
    - Full **control of dependencies through a centralized location** (Maven Central).
    - Assists in various project phases (clean, compile, test, package, install, etc.).
    - Supports the use of common frameworks and methods throughout a project.
    - Compatibility with major revision management tools such as Git, Subversion, etc.
  - **Advantage :**
    - It’s simple to begin going, especially for Java-based initiatives.
    - Robust help keep track of direct and indirect links between projects.
    - Support for a large variety of plugins and integration with other systems.
    - Well suited for enterprise-scale initiatives with intricate dependency graphs.
  - **Limitations :**
    - Less adaptability than Gradle due to a more dogmatic approach.
    - Projects with many dependencies take more time to construct.
  

********

# Software Development Build Tool
- Apache Ant
- Maven
- Gradle
  

## Maven vs Gradle

| Content       | Maven                          | Gradle |
|---------------|--------------------------------|---------|
| Based on      | Developing java based software | Developing domain specific language project |
| Focus         | It focus on developing application within deadline | It focuses on developing application by adding new feature |
| Configuration | It uses Extensiable Markup language or XML for making project structure | Gradle uses Groovy-based domain specific language or making project structure |
| Language      | Maven support development in language in Scala, C#, and ruby | Gradle support development in language like Java, C, C++, and groovy |
| Customization | Provide limited number of parameter and is not much customizable | Highly customizable providing a large range of IDE support |
| Performance   | Maven does not used build cache, that makes the build time slower | It perform bettter than Maven as it tracks only the current task |
| Project Size  | Small | Large and complex |

