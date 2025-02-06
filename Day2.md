# **Student Manual: Advanced Java Concepts**

## **Day 2: Advanced Java Concepts (8 Hours)**

### **1. Sorting and Searching (1 Hour)**
#### **What is Sorting and Searching?**
Sorting is the process of arranging elements in a specific order (ascending/descending), while searching is finding a particular element in a collection.

#### **Why Use Sorting and Searching?**
- Efficiently retrieves and processes data.
- Reduces lookup time in large datasets.
- Improves database indexing and retrieval performance.

#### **Where to Use Sorting and Searching?**
- Searching for a customer in a banking system.
- Sorting transactions by amount in an account statement.
- E-commerce product listings based on price or popularity.

#### **How to Use Sorting and Searching?**
- Implement `Comparable` for natural ordering.
- Use `Comparator` for custom sorting.
- Use `binary search` for efficient searching in sorted lists.

#### **Example: Sorting Customers by Account Balance**
```java
import java.util.*;

class Customer implements Comparable<Customer> {
    String name;
    double balance;

    Customer(String name, double balance) {
        this.name = name;
        this.balance = balance;
    }

    // Implement Comparable for natural sorting
    public int compareTo(Customer other) {
        return Double.compare(this.balance, other.balance);
    }
}

public class Bank {
    public static void main(String[] args) {
        List<Customer> customers = new ArrayList<>();
        customers.add(new Customer("Alice", 3000));
        customers.add(new Customer("Bob", 1500));
        customers.add(new Customer("Charlie", 5000));
        
        Collections.sort(customers);
        
        customers.forEach(c -> System.out.println(c.name + " - " + c.balance));
    }
}
```

#### **Real-time Usage**
- Sorting customers based on account balance.
- Searching for a customer by name in banking applications.

---
### **2. Multithreading Basics (2 Hours)**
#### **What is Multithreading?**
Multithreading is a programming technique that allows multiple threads to run concurrently within a program.

#### **Why Use Multithreading?**
- Enhances performance and responsiveness.
- Efficient CPU utilization.
- Enables parallel execution of tasks.

#### **Where to Use Multithreading?**
- Processing multiple bank transactions simultaneously.
- Real-time stock price updates.

#### **How to Use Multithreading?**
- Use `Thread` class or implement `Runnable` interface.
- Manage thread lifecycle.

#### **Example: Simulating Multiple Customer Transactions**
```java
class BankTransaction implements Runnable {
    private String transactionType;
    private double amount;

    BankTransaction(String transactionType, double amount) {
        this.transactionType = transactionType;
        this.amount = amount;
    }

    public void run() {
        System.out.println(Thread.currentThread().getName() + " processing " + transactionType + " of $" + amount);
    }
}

public class MultiThreadingExample {
    public static void main(String[] args) {
        Thread t1 = new Thread(new BankTransaction("Deposit", 1000));
        Thread t2 = new Thread(new BankTransaction("Withdrawal", 500));
        
        t1.start();
        t2.start();
    }
}
```

#### **Real-time Usage**
- Handling multiple user transactions in banking.
- Managing parallel downloads in a file transfer system.

---
### **3. Thread Synchronization (2 Hours)**
#### **What is Thread Synchronization?**
Synchronization ensures that multiple threads do not interfere with each other while accessing shared resources.

#### **Why Use Thread Synchronization?**
- Prevents data inconsistency and race conditions.
- Ensures thread safety when modifying shared variables.

#### **Where to Use Thread Synchronization?**
- Managing account balance updates in banking applications.
- Handling concurrent bookings in an online ticket system.

#### **How to Use Thread Synchronization?**
- Use `synchronized` keyword.
- Utilize `ExecutorService` for thread pooling.

#### **Example: Synchronizing Deposits and Withdrawals**
```java
class Account {
    private double balance = 1000;
    
    synchronized void deposit(double amount) {
        balance += amount;
        System.out.println("Deposited: " + amount + " | Balance: " + balance);
    }
    
    synchronized void withdraw(double amount) {
        if (balance >= amount) {
            balance -= amount;
            System.out.println("Withdrawn: " + amount + " | Balance: " + balance);
        } else {
            System.out.println("Insufficient balance!");
        }
    }
}
```
#### **Real-time Usage**
- ATM transactions.
- Flight booking systems.

---
### **4. Concurrency Utilities (2 Hours)**
#### **What are Concurrency Utilities?**
Java provides concurrency utilities like `CountDownLatch`, `CyclicBarrier`, and `Semaphore` for efficient thread management.

#### **Why Use Concurrency Utilities?**
- Handles high-volume transactions effectively.
- Prevents deadlocks and race conditions.

#### **Where to Use Concurrency Utilities?**
- Simulating high transaction loads in banking applications.
- Implementing distributed computing solutions.

#### **How to Use Concurrency Utilities?**
- Use `CountDownLatch` to wait for multiple tasks to finish.
- Use `CyclicBarrier` to synchronize multiple threads.
- Use `Semaphore` to limit concurrent access.

#### **Example: Using CountDownLatch for Batch Processing**
```java
import java.util.concurrent.CountDownLatch;

class TransactionThread extends Thread {
    private CountDownLatch latch;
    TransactionThread(CountDownLatch latch) { this.latch = latch; }
    
    public void run() {
        System.out.println(Thread.currentThread().getName() + " processing transaction");
        latch.countDown();
    }
}

public class ConcurrencyExample {
    public static void main(String[] args) throws InterruptedException {
        CountDownLatch latch = new CountDownLatch(3);
        
        new TransactionThread(latch).start();
        new TransactionThread(latch).start();
        new TransactionThread(latch).start();
        
        latch.await();
        System.out.println("All transactions processed");
    }
}
```
#### **Real-time Usage**
- High-volume transaction handling.
- Managing bulk data processing.

---
### **5. Java 11 Features (1 Hour)**
#### **What’s New in Java 11?**
- Enhanced `String` methods.
- Improved `HTTP Client API`.

#### **Why Use Java 11 Features?**
- Simplifies coding.
- Improves performance and security.

#### **Where to Use Java 11 Features?**
- Making external API calls.
- Processing and formatting strings efficiently.

#### **How to Use Java 11 Features?**
- Use `strip()`, `isBlank()`, `repeat()` for string manipulation.
- Use `HttpClient` for making HTTP requests.

#### **Example: Using HTTP Client**
```java
import java.net.http.*;
import java.net.URI;
import java.io.*;

public class HttpClientExample {
    public static void main(String[] args) throws Exception {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder().uri(URI.create("https://api.example.com/data")).build();
        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
        System.out.println(response.body());
    }
}
```
#### **Real-time Usage**
- Fetching stock prices.
- Retrieving customer data from APIs.

