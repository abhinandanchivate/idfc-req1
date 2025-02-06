# Student Manual: Core Java Fundamentals

## **Day 1: Core Java Fundamentals (8 Hours)**

### **1. OOP Basics (1 Hour)**
#### **What is Object-Oriented Programming (OOP)?**
Object-Oriented Programming (OOP) is a paradigm based on the concept of "objects," which can encapsulate data and behavior. It promotes modularity, reusability, and scalability.

#### **Why Use OOP?**
- Encourages code reusability via inheritance.
- Enhances maintainability through encapsulation.
- Enables polymorphism for dynamic behavior.

#### **Where to Use OOP?**
- Software development involving complex entities, e.g., Banking Systems, E-commerce Platforms.

#### **How to Use OOP?**
- Define classes and objects.
- Use constructors for initialization.
- Implement inheritance and method overriding.

#### **Example: Customer Class with Constructor and Method Overloading**
```java
class Customer {
    String name;
    int age;
    
    // Constructor
    Customer(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // Method Overloading
    void display() {
        System.out.println("Customer Name: " + name);
    }
    void display(String message) {
        System.out.println(message + " " + name);
    }
}
```
#### **Real-time Usage**
- Representing users in a banking application.
- Defining objects in game development.

---
### **2. Polymorphism (2 Hours)**
#### **What is Polymorphism?**
Polymorphism allows a single interface to represent different types of behaviors, enhancing flexibility in design.

#### **Why Use Polymorphism?**
- Reduces code duplication.
- Improves scalability.

#### **Where to Use Polymorphism?**
- Implementing payment gateways where different methods (CreditCard, PayPal) have a common interface.

#### **How to Use Polymorphism?**
- Method Overloading: Multiple methods with the same name but different parameters.
- Method Overriding: Redefining a method in a subclass.

#### **Example: Implementing SavingsAccount and CurrentAccount**
```java
abstract class Account {
    abstract void accountType();
}

class SavingsAccount extends Account {
    void accountType() {
        System.out.println("Savings Account");
    }
}

class CurrentAccount extends Account {
    void accountType() {
        System.out.println("Current Account");
    }
}
```
#### **Real-time Usage**
- Defining different types of bank accounts in a banking system.
- Implementing different logging mechanisms.

---
### **3. Interfaces and Functional Interfaces (1 Hour)**
#### **What is an Interface?**
An interface in Java is a blueprint of a class that defines methods without implementations.

#### **Why Use Interfaces?**
- Promotes multiple inheritance.
- Enhances code flexibility and modularity.

#### **Where to Use Interfaces?**
- Implementing different types of transactions (debit, credit).

#### **How to Use Interfaces?**
- Use `interface` keyword.
- Implement it in multiple classes.

#### **Example: AccountOperations Interface**
```java
interface AccountOperations {
    void deposit(double amount);
    void withdraw(double amount);
}

class SavingsAccount implements AccountOperations {
    public void deposit(double amount) {
        System.out.println("Deposited " + amount + " in Savings Account");
    }
    public void withdraw(double amount) {
        System.out.println("Withdrawn " + amount + " from Savings Account");
    }
}
```
#### **Real-time Usage**
- Payment processing in financial applications.
- Implementing multiple authentication mechanisms.

---
### **4. Banking App Design (1 Hour)**
#### **What is a Banking System Design?**
A banking system design involves structuring entities and defining their relationships to ensure seamless functionality.

#### **Why Use UML Diagrams?**
- Helps visualize class relationships.
- Simplifies system design.

#### **Where to Use UML Diagrams?**
- Designing banking applications.
- Modeling inventory management systems.

#### **How to Use UML Diagrams?**
- Identify entities like Bank, Customer, Account.
- Define relationships (e.g., Customer has multiple Accounts).

#### **Example UML Class Diagram**
- **Entities:** Bank, Customer, Account
- **Relationships:**
  - A **Customer** has one or more **Accounts**.
  - A **Bank** manages multiple **Customers**.

#### **Real-time Usage**
- Used in software architecture planning before coding begins.

---
### **5. Exception Handling Basics (2 Hours)**
#### **What is Exception Handling?**
Exception handling in Java allows handling runtime errors gracefully without crashing the program.

#### **Why Use Exception Handling?**
- Prevents program termination.
- Improves fault tolerance.

#### **Where to Use Exception Handling?**
- Handling invalid bank transactions.
- Managing API request failures.

#### **How to Use Exception Handling?**
- Use `try`, `catch`, `finally` blocks.
- Define custom exceptions.

#### **Example: Custom Exception for Insufficient Balance**
```java
class InsufficientBalanceException extends Exception {
    InsufficientBalanceException(String message) {
        super(message);
    }
}

class Account {
    double balance = 500;
    void withdraw(double amount) throws InsufficientBalanceException {
        if(amount > balance) {
            throw new InsufficientBalanceException("Insufficient Balance!");
        }
        balance -= amount;
    }
}
```
#### **Real-time Usage**
- Preventing invalid operations in a banking system.
- Handling incorrect user input in a web application.

---
### **6. Collections in Java (1 Hour)**
#### **What are Collections?**
Collections in Java provide a framework to store, manipulate, and retrieve data efficiently.

#### **Why Use Collections?**
- Reduces memory usage compared to arrays.
- Allows dynamic data storage.

#### **Where to Use Collections?**
- Storing customer transactions in a banking application.
- Managing user sessions in web applications.

#### **How to Use Collections?**
- Use `List`, `Set`, `Map` interfaces.

#### **Example: Storing Transactions Using Collections**
```java
import java.util.*;

class Bank {
    HashMap<Integer, List<String>> transactions = new HashMap<>();
    void addTransaction(int customerId, String transaction) {
        transactions.putIfAbsent(customerId, new ArrayList<>());
        transactions.get(customerId).add(transaction);
    }
}
```
#### **Real-time Usage**
- Managing accounts by customer ID.
- Implementing shopping cart functionality.

---
This manual provides a structured approach to learning Core Java fundamentals. Each section builds upon the previous one to develop a strong foundation for real-world Java applications.

