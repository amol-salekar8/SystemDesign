# Software Design Principle

- Software design principle are guideline that helps software developers create systems that are easy to understand, maintain, and extend.
- These principles can be applied on both HLD and LLD
1) **DRY : [ Don't Repeat Yourself ](#dry-dont-repeat-yourself)**
2) **KISS  : [ Keep It Simple Stupid ](#kiss-keep-it-simple-stupid)**
3) **YAGNI : [ You Aren't Gonna Need It ](#yagni-you-arent-gonna-need-it)**


## DRY (Don't Repeat Yourself)

**What it is?**
- This principle state that every piece of knowledge mus have single, unambiguous, authoritative representation within a system.
- In simple term **avoid duplication** of logic or code
- Repeatating code makes the system hard to maintain and error-prone
- If change is required, you might forget to update all occurrences.

****
**Importance**
- Reduce redundancy
- Easier maintainance
- Single point of change

****

**Example**
```java
// Before DRY
public void area(){
    
    int length = 10, width = 20;
    int area1 = length*width;
    System.out.println(area1);
    
    int length2 = 10, width2 = 20;
    int area2 = length2 *width2;
    System.out.println(area2);
}

// After DRY
public void area(){

    int length = 10, width = 20;
    System.out.println(calculateArea(length, width));

    int length2 = 10, width2 = 20;
    iSystem.out.println(calculateArea(length2, width2));
}

public int calculateArea(int length, int width){
    return length * width;  
}

```

****

**Applying DRY in Practice**
- Identify repetitive code and replace it with a single,reusable code segment.
- Extract common functionality into methods or utility classes.
- Leverage libraries and frameworks when available.
- Refactor duplicate logic regularly across classes or layers.

****

**When not use ?**
- **Premature abstraction :**
  - Don't extract common code to early.
  - At first glance, two code blocks might look similar, but they could change in different ways later.
  - Extracting them into a shared method can create unnecessary coupling between unrelated parts.
- **Performance-Critical code:** 
  - Don't apply DRY to performance - sensitive code if it causes inefficiency.
  - Sometimes, repeating optimized low-level logic is faster than calling a generalized, reusable method.
  - Function calls, indirection, or generic wrappers might reduce  performance or block compiler optimization like inlining.
- **Sacrificing readability :**
  - if extracting repeated code makes the code less readable, prefer clarity over DRYness.
- **Legacy codebase :**
  - Don't refactor legacy code unless necessary and well-tested.
  - Legacy code might not have tests or complete documentation. 
  - Introducing DRY by extracting shared logic can accidentally change behaviour.

## KISS (Keep It Simple Stupid)

**What it is ?**
- This princple state that simplicity should be key goal in design and unnecessary complexity should be avoided.
- Use the simplest possible solutions that works.
- Avoid clever, convoluted code.
****

**Importance**
- Easier debugging.
- Improved readability
- Better maintainability.
- Faster development.
****

**Example :**
```java

// Before KISS
public boolean isEven(int number){
    boolean isEven = true;
    if(number % 2 == 0 ){
        isEven = true;
    }else {
        isEven = false;
    }
    return  isEven;
}

// After KISS
public  boolean isEven(int number){
    return  number % 2 == 0;
}

```



## YAGNI (You Aren't Gonna Need It)
**What it is ?**
- This principle state that **Always  implement things when you actually need them, neven when you just foresee that you need them**
- In simple term **Don't add functionality until it's necessary.**
- Avoid building feature that you think you might need in the future.

****

**Example :**
- Assume you have been asked to build note taking app that allows users to create a note and view notes.
- Now you start thinking ahead 
  - "What if later they want categories? Or tagging? Or syncing with Google Drive? should I prepare for that?"
  - This creates a lot of unnecessary complexity and wastage of tiime.
****

**Importance :**
- Reduced waste
- Simplified codebase
- Faster development

****

**When not to Use YAGNI ?**
- **When requirement is well known**
  - If feature is guaranteed and soon to be implemented, preparing for it now might be more efficient.
- Performance-Critical areas