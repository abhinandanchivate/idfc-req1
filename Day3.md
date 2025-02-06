# Student Manual: Spring Core and Boot Basics

## **Day 3: Spring Core and Boot Basics (8 Hours)**

---

## **1. Introduction to Spring Framework (1 Hour)**
### **What is the Spring Framework?**
Spring is a powerful framework for building Java-based enterprise applications. It provides infrastructure support for developing applications with features like dependency injection (DI), aspect-oriented programming (AOP), and transaction management.

### **Why Use Spring?**
- Simplifies enterprise Java development.
- Provides a loosely coupled architecture with DI.
- Manages application lifecycle through IoC (Inversion of Control) container.
- Supports declarative transaction management and security.

### **Where to Use It?**
- Web applications (Spring MVC, Spring Boot)
- Microservices (Spring Boot, Spring Cloud)
- Enterprise applications (Banking, E-commerce, etc.)
- Integration with databases, messaging systems, and external APIs.

### **How to Use It?**
Spring uses an IoC container to manage beans and their dependencies. You can configure beans using XML or Java-based configuration.

#### **Example:** Defining Beans using XML Configuration
```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="customerService" class="com.example.CustomerService" />
</beans>
```

#### **Example:** Java-based Configuration
```java
@Configuration
public class AppConfig {
    @Bean
    public CustomerService customerService() {
        return new CustomerService();
    }
}
```

#### **Hands-on Exercise:**
- Set up a simple Spring project.
- Define beans using XML and Java-based configuration.

---

## **2. Spring Configuration (1 Hour)**
### **What are Spring Annotations?**
Annotations help in reducing XML configuration and making the code more readable.

### **Why Use Annotations?**
- Eliminates the need for XML configuration.
- Improves code readability and maintainability.
- Enables auto-wiring of dependencies.

### **Common Annotations and Usage:**
| Annotation | Purpose |
|------------|----------|
| @Component | Marks a class as a Spring-managed bean |
| @Service | Specialized @Component for service layer |
| @Repository | Specialized @Component for data access layer |
| @Autowired | Injects dependencies automatically |

#### **Example:** Using Annotations for Bean Creation
```java
@Component
public class CustomerService {
    public void processCustomer() {
        System.out.println("Processing customer...");
    }
}
```

#### **Hands-on Exercise:**
- Convert XML-based bean definitions to annotation-based components.
- Use @Autowired to inject dependencies.

---

## **3. Spring Boot Introduction (1 Hour)**
### **What is Spring Boot?**
Spring Boot is an extension of the Spring Framework that simplifies the setup and development of Spring applications with minimal configuration.

### **Why Use Spring Boot?**
- Reduces boilerplate configuration.
- Embedded server (Tomcat, Jetty, etc.).
- Built-in dependency management via Spring Boot Starters.
- Production-ready features like health checks and metrics.

### **Where to Use It?**
- Microservices development.
- RESTful API development.
- Standalone and enterprise applications.

#### **Example:** Setting Up a Spring Boot Application
```java
@SpringBootApplication
public class BankingApplication {
    public static void main(String[] args) {
        SpringApplication.run(BankingApplication.class, args);
    }
}
```

#### **Hands-on Exercise:**
- Create a Spring Boot application.
- Configure application properties.

---

## **4. Spring Boot Application Layering (2 Hours)**
### **What is Application Layering?**
A structured way to separate concerns in an application using different layers:
1. **Controller Layer**: Handles incoming requests.
2. **Service Layer**: Business logic processing.
3. **Repository Layer**: Data access layer.

### **Why Use Layered Architecture?**
- Improves code maintainability.
- Enhances scalability and testability.

#### **Example:** Implementing Layers
```java
@RestController
@RequestMapping("/customers")
public class CustomerController {
    @Autowired
    private CustomerService customerService;
    
    @GetMapping("/{id}")
    public Customer getCustomer(@PathVariable Long id) {
        return customerService.getCustomerById(id);
    }
}
```

#### **Hands-on Exercise:**
- Build a layered banking system with Controller, Service, and Repository.

---

## **5. Spring Data JPA Basics (2 Hours)**
### **What is JPA?**
Java Persistence API (JPA) is a standard for mapping Java objects to relational database tables.

### **Why Use Spring Data JPA?**
- Simplifies database operations.
- Reduces boilerplate code.

### **Where to Use It?**
- Any application requiring database CRUD operations.

#### **Example:** Mapping Entities with JPA
```java
@Entity
public class Customer {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
}
```

#### **Hands-on Exercise:**
- Map Customer and Account entities.
- Implement CRUD operations using JpaRepository.

---

## **6. Custom Queries with JPA (1 Hour)**
### **What are JPQL and Native Queries?**
- **JPQL**: Object-oriented query language for JPA.
- **Native Queries**: Raw SQL queries executed in JPA.

### **Why Use Custom Queries?**
- Retrieve complex data that default repository methods can't fetch.

### **Example:** Custom Queries in JPA
```java
@Repository
public interface CustomerRepository extends JpaRepository<Customer, Long> {
    @Query("SELECT c FROM Customer c WHERE c.balance > :balance")
    List<Customer> findCustomersWithHighBalance(@Param("balance") Double balance);
}
```

#### **Hands-on Exercise:**
- Implement complex search queries for customers by balance range.

---

## **Conclusion**
By the end of this session, students will be able to:
- Set up and configure a Spring Boot application.
- Implement IoC and dependency injection.
- Create a layered architecture for enterprise applications.
- Work with JPA for database persistence.
- Build RESTful APIs with Spring Boot.

This structured approach ensures a comprehensive understanding of Spring Core and Boot Basics.

