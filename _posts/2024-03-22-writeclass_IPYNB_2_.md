---
toc: True
comments: True
layout: post
title: Writing Classes (Unit 5)
description: Focus on 2021 FRQ. classes tips and tricks
authors: Vivian, Aliya, Justin, Shivansh
---

# What to Know

for more info on classes go here: [csawesome_resource](https://runestone.academy/ns/books/published/csawesome/Unit5-Writing-Classes/topic-5-1-parts-of-class.html)

- Classes are the blueprints for making objects. When you create objects, you create new instances of that class and what you can do with those instances is determined by what methods are defined in the class.

## Specifically for AP Test: 
- Implement class with instance variables, methods, constructors 
- Inheritance (extend class, override methods), but just because you're using the methods of seperate classes in new classes DOES NOT mean you use extend when declaring class header
- Use object or class from one class in another class
- Use classes to store methods if they ask you to write classes
- Realistically the only things you need to worry about is remembering to make instance variables and constructors if they ask to write one and to actually put everything within the class


```Java
public class Example 
{
    // instance variables
    private String var1;
    private int var2;

    // Constructor
    public Example(String initVar1, int initVar2)
    {
        var1 = initVar1;
        var2 = initVar2;
    }

    // Method to print instance variable values, again NOT 
    public void print()
    {
        System.out.println("Var1: " + var1);
        System.out.println("Var2: " + var2);
    }

    // Main method for testing, NOT NEEDED FOR TEST USUALLY
    public static void main(String[] args)
    {
        // Creating instances of Example class
        Example e1 = new Example("Value1", 10);
        Example e2 = new Example("Value2", 20);

        // Calling print method for each instance
        e1.print();
        e2.print();
    }
}
```

## Example Time

The CB question usually provides you with setters and getters but no additional parameters or a constructor. Here is what the given class for SingleTable looks like when all the methods are written. 

- This question asks that you write a new class called CombinedTable which uses the methods of the SingleTable class to determine the "desirability" of the combined tables.


```Java
public class SingleTable {
    
    int seats;
    int height;
    double viewQuality;

    public SingleTable(int seats, int height, double viewQuality) {
        this.seats = seats;
        this.height = height;
        this.viewQuality = viewQuality;
    }

    //returns number of seats at this table. value is always greater than or equal to 4
    public int getNumSeats() {
        return this.seats;
    }

    //returns the height of table in cm
    public int getHeight() {
        return this.height;
    }

    //returns the quality of the view from this table
    public double getViewQuality() {
        return this.viewQuality;
    }

    //sets the quality of the view from this table to [value]
    public void setViewQuality(double newQuality) {
        this.viewQuality = newQuality;
    }

    public static void main(String[] args) {
        //single table values that were given in the question!
        SingleTable t1 = new SingleTable(4, 74, 60.0);
        SingleTable t2 = new SingleTable(8, 74, 70.0);
        SingleTable t3 = new SingleTable(12, 76, 75.0);
    }

}
```

## Tip
The first thing you want to do is make the instructions simpler. RCB initially gives you a huge chunk of paragraph that will hurt your head. So after doing a skim, quickly write down what the basic objectives of this class are. Here is what I've gathered:
- when combining two single tables, subtract two seats to get combined table seat count
- if the height of combined table is level, desirability is the avg of the single tables
- if the height of combined table isn't level, desirability is the avg of the single tables - 10

Looking to the net chunk of info CB gives, they literally hand over what methods you need to make
![frq2lesson](https://github.com/Codemaxxers/codemaxxerblog/blob/main/images/frq2lesson.png?raw=true)


```Java
public class CombinedTable {

    private SingleTable table1;
    private SingleTable table2;

    //constructor
    //uses t1 and t2 from SingleTable class
    public CombinedTable(SingleTable t1, SingleTable t2) {
        table1 = t1;
        table2 = t2;
    }

    public boolean canSeat(int n) {

        int cap = table1.getNumSeats() + table2.getNumSeats() - 2;

        if (n <= cap) {
            return true;
        }
        else {
            return false;
        }
    }

    public double getDesirability(int height, double quality){
        double desirability;
        if (table1.getHeight() == table2.getHeight()) {
            desirability = (table1.getViewQuality() + table2.getViewQuality()) / 2;
        }
        else {
            desirability = ((table1.getViewQuality() + table2.getViewQuality()) / 2) - 10;
        } 
        return desirability; 
    }
    
}
```

## Points Conclusion
1. Class header (1 point)
2. (Private) instance variables (1 point)
3. Constructor (1 point)
4. Methods headers (1 point per method)
5. Using methods from SingleTable object (1 point per method)
4. Methods works(1 point each)

Will lose points if:
- array/collection access confusion ([] or get)
- extra code that has side-effect, such as printint to output, incorrect precondition check, etc.
- local variables used but none declared
- destruction of persistent data, such as changing value referenced by parameter
- void method or constructor that returns value

Will NOT lose points if: 
- private or public qualifier on local variable
- missing public qualifier on class or constructor header

## Commonly Missed
- Not declaring any SingleTable instance variables

## HACKS

(a) Describe the different features needed to create a class and what their purpose is.

(b) Code: 
Create a Java class BankAccount to represent a simple bank account. This class should have the following attributes:

- accountHolder (String): The name of the account holder.
balance (double): The current balance in the account.
Implement the following mutator (setter) methods for the BankAccount class:

- setAccountHolder(String name): Sets the name of the account holder.
- deposit(double amount): Deposits a given amount into the account.
- withdraw(double amount): Withdraws a given amount from the account, but only if the withdrawal amount is less than or equal to the current balance.

Ensure that the balance is never negative.
