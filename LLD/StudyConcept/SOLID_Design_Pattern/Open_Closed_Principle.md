# Open Closed Principle

## Definition
- As per OCP, Software entities ( classes, modules, functions, etc) should open for extension, but closed for modification.
- This means that the behaviour of a module can be extended without modifying its source code.
- The goal is to reduce the risk of breaking existing functionality when requiring.

## Real Life Analogy
- Power adapter
  - **Problem**
    - Imagine you travel from India to the UK
    - Your indian charger won't be fit into UK power socket
  - **Solution** 
    - Instead of Buying new charger, you use travel adapter.
    - The adapter extends your existing charger's usability.
    - you did not modify the original charger itself.
- Bus to Train
  - Suppose we have bus
  - If Bus get fulled we can't expand but If Train get fully field with passenger
  - there is chance of Add new Train compartment

## Real Word Example
- Let's now used region based tax calculation (eg. India, US, UK) in an invoicing System to explain the OCP
- As an invoicing system grows, it must handle tax rules for different regions
  - India : GST  18%
  - US : Sales Tax 8%
  - UK : VAT 12%

**Bad Design:**
```java
class InvoiceProcessor{
    public double calculateAmountAfterTax(String region, double amount){
        if(region.equalsIgnoreCase("India")){
            return amount + amount * 0.18;
        } else if(region.equalsIgnoreCase("US")){
            return amount + amount * 0.08;
        } else if(region.equalsIgnoreCase("UK")){
            return amount + amount * 0.12;
        } else {
            return amount;
        }
    }
}
```
**Problems in above code:**
- Adding new region (eg. Germany) require modifying this method.
- You risk breaking existing logic while adding new functionality.
- Hard to test, maintain, or scale
- Violates OCP

**Good Design:**

```java
// Tax strategy interface
interface TaxCalculator {
    double calculateTax(double amount);
}

// Implementing Region-specific tax calculator
class IndiaTaxCalculator implements TaxCalculator {
    double calculateTax(double amount) {
        return  amount * 0.18;
    }
}

// Implementing Region-specific tax calculator
class USTaxCalculator implements TaxCalculator {
    double calculateTax(double amount) {
        return amount * 0.08;
    }
}

// Implementing Region-specific tax calculator
class UKTaxCalculator implements TaxCalculator {
    double calculateTax(double amount) {
        return amount * 0.12;
    }
}

// Using dependancy Injecction
class Invoice {
    private double amount;
    private TaxCalculator taxCalculator;

    public Invoice(double amount, TaxCalculator taxCalculator) {
        this.amount = amount;
        this.taxCalculator = taxCalculator;
    }

    public double getTotalAmount(){
        return amount + taxCalculator.calculateTax(amount);
    }
}

class Main{
    public static void main(String[] args) {
        double amount = 1000.0;
        Invoice indiaInvoice = new Invoice(amount, new IndiaTaxCalculator());
        System.out.println(indiaInvoice.getTotalAmount());

        Invoice usInvoice = new Invoice(amount, new USTaxCalculator());
        System.out.println(indiaInvoice.getTotalAmount());

        Invoice ukInvoice = new Invoice(amount, new UKTaxCalculator());
        System.out.println(indiaInvoice.getTotalAmount());
        
    }
}
```

**Explanation :**
- Define a Tax Strategy interface.
- Implement Region-specific Tax Calculator.
- Using dependency injection.
- Main running code.

**Assume that now, we want to support Germany with 15% tax**
```java
class GermanyTaxCalculator implements  TaxCalculator{
    public double calculateTax(double amount){
        return amount * 0.18;
    }
}
```

## When to apply OCP
- In the following scenario it is useful
  - When **module is expected to change or evolve due** to shifting business or technical requirements.
  - When there is a need to extend functionality without modifying existing, tested code.
  - When developing frameworks, plugin, or extensible systems such as billing engines, tas calculators or UI components.

## Common misconception about OCP
- Open/Closed means code should never be changed again.
  - The principle emphasizes avoiding changes to core logic while allowing behavior to be extended safely
- OCP leads to too many classes, so it's overkill
  - It true that applying OCP often results in more classes or interface.
  - However, this trade-off typically improves modularity, testability and maintainability
- OCP makes the code harder to read
  - In small or short-lived projects, added abstraction can feel unnecessary
  - But in system with complex behaviour  or frequent changes, well-structured extensibility can actually improve clarity by separating concern and reducing conditional logic
- OCP should always applied upfront
- Refactoring contradicts OCP
- OCP makes retesting legacy code unnecessary
  - No, only new extensions still require thorough testing to ensure correctness and integration.