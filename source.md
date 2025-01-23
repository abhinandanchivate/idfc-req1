Here's the complete code for the banking application case study using the latest version of Spring Boot, including `application.yml` configuration, pagination, and a Postman collection.

---

### Project Structure

```
banking-app/
│-- src/
│   ├── main/
│   │   ├── java/com/bankingapp/
│   │   │   ├── controller/
│   │   │   ├── entity/
│   │   │   ├── exception/
│   │   │   ├── repository/
│   │   │   ├── service/
│   │   │   └── BankingApplication.java
│   ├── resources/
│   │   ├── application.yml
│-- pom.xml
│-- README.md
│-- postman_collection.json
```

---

### 1. `pom.xml` (Dependencies)

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
    </dependency>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <scope>provided</scope>
    </dependency>
</dependencies>
```

---

### 2. `application.yml`

```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/bankingdb
    username: postgres
    password: admin
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
    properties:
      hibernate:
        dialect: org.hibernate.dialect.PostgreSQLDialect
  server:
    port: 8080
```

---

### 3. `BankingApplication.java`

```java
package com.bankingapp;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class BankingApplication {
    public static void main(String[] args) {
        SpringApplication.run(BankingApplication.class, args);
    }
}
```

---

### 4. Entities

#### `Customer.java`
```java
package com.bankingapp.entity;

import lombok.Data;
import javax.persistence.*;
import java.util.List;

@Entity
@Data
public class Customer {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long customerId;
    private String name;
    private String email;
    private String phoneNumber;
    private String address;
    private String dateOfBirth;

    @OneToMany(mappedBy = "customer")
    private List<Account> accounts;
}
```

#### `Account.java`
```java
package com.bankingapp.entity;

import lombok.Data;
import javax.persistence.*;
import java.util.List;

@Entity
@Data
public class Account {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long accountId;
    private String accountType;
    private Double balance;
    private String openedDate;
    private String status;

    @ManyToOne
    @JoinColumn(name = "customerId")
    private Customer customer;

    @OneToMany(mappedBy = "account")
    private List<Transaction> transactions;
}
```

#### `Transaction.java`
```java
package com.bankingapp.entity;

import lombok.Data;
import javax.persistence.*;
import java.time.LocalDateTime;

@Entity
@Data
public class Transaction {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long transactionId;
    private String transactionType;
    private Double amount;
    private LocalDateTime timestamp;
    private String description;

    @ManyToOne
    @JoinColumn(name = "accountId")
    private Account account;
}
```

---

### 5. Repositories with Pagination

#### `CustomerRepository.java`
```java
package com.bankingapp.repository;

import com.bankingapp.entity.Customer;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;

public interface CustomerRepository extends JpaRepository<Customer, Long> {
    Page<Customer> findAll(Pageable pageable);
}
```

---

### 6. Service Layer

#### `CustomerService.java`
```java
package com.bankingapp.service;

import com.bankingapp.entity.Customer;
import com.bankingapp.repository.CustomerRepository;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;
import org.springframework.stereotype.Service;

@Service
public class CustomerService {
    private final CustomerRepository customerRepository;

    public CustomerService(CustomerRepository customerRepository) {
        this.customerRepository = customerRepository;
    }

    public Customer createCustomer(Customer customer) {
        return customerRepository.save(customer);
    }

    public Page<Customer> getAllCustomers(Pageable pageable) {
        return customerRepository.findAll(pageable);
    }
}
```

---

### 7. Controllers

#### `CustomerController.java`
```java
package com.bankingapp.controller;

import com.bankingapp.entity.Customer;
import com.bankingapp.service.CustomerService;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/customers")
public class CustomerController {
    private final CustomerService customerService;

    public CustomerController(CustomerService customerService) {
        this.customerService = customerService;
    }

    @PostMapping
    public Customer createCustomer(@RequestBody Customer customer) {
        return customerService.createCustomer(customer);
    }

    @GetMapping
    public Page<Customer> getAllCustomers(Pageable pageable) {
        return customerService.getAllCustomers(pageable);
    }
}
```

---

### 8. Exception Handling

#### `GlobalExceptionHandler.java`
```java
package com.bankingapp.exception;

import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.*;

@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(Exception.class)
    @ResponseStatus(HttpStatus.BAD_REQUEST)
    public String handleException(Exception ex) {
        return ex.getMessage();
    }
}
```

---

Here's the complete code for the **Account** and **Transaction** entities, including their respective controllers, services, and repositories.

---

### **1. Entity Classes**

#### `Account.java`
```java
package com.bankingapp.entity;

import lombok.Data;
import javax.persistence.*;
import java.util.List;

@Entity
@Data
public class Account {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long accountId;
    private String accountType;
    private Double balance;
    private String openedDate;
    private String status;

    @ManyToOne
    @JoinColumn(name = "customerId")
    private Customer customer;

    @OneToMany(mappedBy = "account")
    private List<Transaction> transactions;
}
```

#### `Transaction.java`
```java
package com.bankingapp.entity;

import lombok.Data;
import javax.persistence.*;
import java.time.LocalDateTime;

@Entity
@Data
public class Transaction {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long transactionId;
    private String transactionType;
    private Double amount;
    private LocalDateTime timestamp;
    private String description;

    @ManyToOne
    @JoinColumn(name = "accountId")
    private Account account;
}
```

---

### **2. Repository Interfaces**

#### `AccountRepository.java`
```java
package com.bankingapp.repository;

import com.bankingapp.entity.Account;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;

public interface AccountRepository extends JpaRepository<Account, Long> {
    Page<Account> findAll(Pageable pageable);
}
```

#### `TransactionRepository.java`
```java
package com.bankingapp.repository;

import com.bankingapp.entity.Transaction;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;

public interface TransactionRepository extends JpaRepository<Transaction, Long> {
    Page<Transaction> findAllByAccount_AccountId(Long accountId, Pageable pageable);
}
```

---

### **3. Service Layer**

#### `AccountService.java`
```java
package com.bankingapp.service;

import com.bankingapp.entity.Account;
import com.bankingapp.repository.AccountRepository;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;
import org.springframework.stereotype.Service;

import java.util.Optional;

@Service
public class AccountService {
    private final AccountRepository accountRepository;

    public AccountService(AccountRepository accountRepository) {
        this.accountRepository = accountRepository;
    }

    public Account openAccount(Account account) {
        return accountRepository.save(account);
    }

    public Optional<Account> getAccountById(Long id) {
        return accountRepository.findById(id);
    }

    public Page<Account> getAllAccounts(Pageable pageable) {
        return accountRepository.findAll(pageable);
    }

    public void deposit(Long accountId, Double amount) {
        Account account = accountRepository.findById(accountId).orElseThrow(() -> new RuntimeException("Account not found"));
        account.setBalance(account.getBalance() + amount);
        accountRepository.save(account);
    }

    public void withdraw(Long accountId, Double amount) {
        Account account = accountRepository.findById(accountId).orElseThrow(() -> new RuntimeException("Account not found"));
        if (account.getBalance() < amount) {
            throw new RuntimeException("Insufficient balance");
        }
        account.setBalance(account.getBalance() - amount);
        accountRepository.save(account);
    }
}
```

#### `TransactionService.java`
```java
package com.bankingapp.service;

import com.bankingapp.entity.Transaction;
import com.bankingapp.repository.TransactionRepository;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;
import org.springframework.stereotype.Service;

@Service
public class TransactionService {
    private final TransactionRepository transactionRepository;

    public TransactionService(TransactionRepository transactionRepository) {
        this.transactionRepository = transactionRepository;
    }

    public Transaction createTransaction(Transaction transaction) {
        return transactionRepository.save(transaction);
    }

    public Page<Transaction> getTransactionsByAccountId(Long accountId, Pageable pageable) {
        return transactionRepository.findAllByAccount_AccountId(accountId, pageable);
    }
}
```

---

### **4. Controller Layer**

#### `AccountController.java`
```java
package com.bankingapp.controller;

import com.bankingapp.entity.Account;
import com.bankingapp.service.AccountService;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;
import org.springframework.web.bind.annotation.*;

import java.util.Optional;

@RestController
@RequestMapping("/accounts")
public class AccountController {
    private final AccountService accountService;

    public AccountController(AccountService accountService) {
        this.accountService = accountService;
    }

    @PostMapping
    public Account openAccount(@RequestBody Account account) {
        return accountService.openAccount(account);
    }

    @GetMapping("/{id}")
    public Optional<Account> getAccountById(@PathVariable Long id) {
        return accountService.getAccountById(id);
    }

    @GetMapping
    public Page<Account> getAllAccounts(Pageable pageable) {
        return accountService.getAllAccounts(pageable);
    }

    @PutMapping("/{id}/deposit")
    public String deposit(@PathVariable Long id, @RequestParam Double amount) {
        accountService.deposit(id, amount);
        return "Deposit successful";
    }

    @PutMapping("/{id}/withdraw")
    public String withdraw(@PathVariable Long id, @RequestParam Double amount) {
        accountService.withdraw(id, amount);
        return "Withdrawal successful";
    }
}
```

#### `TransactionController.java`
```java
package com.bankingapp.controller;

import com.bankingapp.entity.Transaction;
import com.bankingapp.service.TransactionService;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/transactions")
public class TransactionController {
    private final TransactionService transactionService;

    public TransactionController(TransactionService transactionService) {
        this.transactionService = transactionService;
    }

    @PostMapping
    public Transaction recordTransaction(@RequestBody Transaction transaction) {
        return transactionService.createTransaction(transaction);
    }

    @GetMapping("/account/{accountId}")
    public Page<Transaction> getTransactionsByAccount(@PathVariable Long accountId, Pageable pageable) {
        return transactionService.getTransactionsByAccountId(accountId, pageable);
    }
}
```

---

### **5. Postman Collection (JSON)**

```json
{
  "info": {
    "name": "Banking App API",
    "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
  },
  "item": [
    {
      "name": "Open Account",
      "request": {
        "method": "POST",
        "url": "http://localhost:8080/accounts",
        "header": [{ "key": "Content-Type", "value": "application/json" }],
        "body": {
          "mode": "raw",
          "raw": "{\"accountType\":\"Savings\",\"balance\":1000.0,\"openedDate\":\"2024-06-01\",\"status\":\"Active\"}"
        }
      }
    },
    {
      "name": "Get All Accounts",
      "request": {
        "method": "GET",
        "url": "http://localhost:8080/accounts?page=0&size=5"
      }
    }
  ]
}
```

---

This provides the complete code for the **Account** and **Transaction** entities, including pagination support and Postman API testing collection. Let me know if you need any additional features or explanations.

---

This setup includes pagination, exception handling, and a Postman collection for testing. Let me know if you need additional refinements.
