---
title: Prepare for JAVA Certification, (5)
search: true
tags: 
  - JAVA
  - OCAJP
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
classes: wide
---
Design classes.

## Class Inheritance

1. Extending a class using keyword `extends`
2. Private variable in parent class
    1. Subclass cannot access parent class's private 
    2. If we have an instance of a subclass, that private variable from parent class exists
3. Class Access Modifiers
    - `public` can be referenced and used in **any class**
    - `default package private` by **subclass** or **class within same package**.
4. Java Objects  
    if you look at the inheritance structure of any class, it will always end with java.lang.Object on the top of the tree
5. Compiler Enhancements Constructor  
    - compiler inserts a no-argument constructor `super()`if the first statement is not a call to parent constructor.
      ```java
      //following definitions are equivalent
      
      public class Moss {                           }
      public class Moss { public Moss(){          } }
      public class Moss { public Moss(){ super(); } }
      ```
    - if parent class doesn't have a no-argument constructor, you **must** create one constructor in clild class, explicitly call a parent constructor via the `super()`
      ```java
      public class Mammal { public Mammal(int age) { } }
      
      public class Elephant extends Mammal { 
        public Elephant() {  }// DOES NOT COMPILE   
      }
      
      public class Elephant extends Mammal {
        public Elephant() { super(10); } //WILL COMPILE, an explicit call to a parent constructor.
      }
      ```
6. **Constructor Deﬁnition Rules**
    - First statement of every constructor is a call to another constructor. Within the class using `this()`, or to parent using `super()`.
    - The super() call may not be used after the first statement of the constructor.
    - If no `super()` exists, compiler will insert one at the beginning of constructor.
    - If the parent doesn’t have a no-argument constructor and the child doesn’t define any constructors, the compiler will **throw an error**
    - If the parent doesn’t have a no-argument constructor, the compiler requires an explicit call to a parent constructor **in each child constructor**.
    
    ```java
    class Primate { public Primate() { System.out.println("Primate"); } }
    class Ape extends Primate { public Ape() { System.out.println("Ape"); } }
    public class Chimpanzee extends Ape { public static void main(String[] args) { new Chimpanzee(); } }
    
    //Primate Ape
    ```
7. Calling Inherited Class Members
   - If the parent class and child class are part of the **same package**, the child class may also use any **default members** defined in the parent class.
   - A child class may **never access a private member** of the parent class
   - Can explicitly reference a member of the parent class by using the super keyword
   - Inheriting a class grants us access to the **public and protected members** of the parent class.

8. **Overriding a Method**: 
    - there is a method defined in both the parent and child class, you want to define a new version of an existing method in a child class. 
    - You declare a new method with **same signature and return type**. 
    - **signiature includes the name and lsit of input parameters**
    - use `super` to reference parent version method
    - clild class method must be at least as accessible or more accessbile than parent class
    - child class may not throw a checked exception newer or broader. (**no bigger exception**)
    - return value must be the same or a subclass
9. **Overloading**  
    - an overloaded method will use a **different signature** than an overridden method.
    - Check: access modifiers, return types and exceptions
      ```java
      public class Bird {
        public void fly() { System.out.println("Bird is flying");} 
        public void eat(int food) { System.out.println("Bird is eating "+food+" units of food"); }
      }
      
      public class Eagle extends Bird {
        public int fly(int height) { 
          System.out.println("Bird is flying at "+height+" meters"); return height; 
        } 
        
        public int eat(int food) { // DOES NOT COMPILE, return type not right
          System.out.println("Bird is eating "+food+" units of food");
          return food; 
        }
      }
      
      //fly() is overloaded, since signature changes from a no-argument constructor to one int argument
      //eat() is overridden, since signature is the same. 
      ```
    
10. **Hiding Static Methods**  
    - A **hidden method** occurs when a static method with same name and signature in both parent and child classes. 
    - Rules for overriding apply for hidden method. 
    - New rule: **stay static, or stay not static, remain the same**
    - if it has static, in method it will call parent variable
    - if don't have static, in will call instance variable
11. Inheriting Variables
    - **Hiding Variables**: you define a variable with the same name as a variable in a parent class.
    - explicit use of the `super` keyword to reference a hidden variable