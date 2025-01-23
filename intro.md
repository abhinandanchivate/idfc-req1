## 5-Day Core Java & Spring Boot Training Manual

### Background

In today's digital economy, banking systems must handle vast amounts of customer data, transactions, and accounts efficiently and securely. Traditional banking applications often face challenges such as scalability, performance, and security. To address these challenges, modern banking applications leverage technologies such as Java Spring Boot for backend services and RESTful APIs to provide seamless integration with frontend applications.

This training manual covers a hands-on approach to building a robust banking system using Java, Spring Boot, and related technologies. Participants will learn how to design and implement core banking functionalities, such as customer management, account operations, and transaction processing, while applying best practices in software development.

### Banking Application Case Study

#### Objective

To develop a full-fledged banking application that handles customer accounts, transactions, and account operations efficiently. The system should be scalable, secure, and maintainable using Java, Spring Boot, and REST APIs.

#### Entities Involved

1. **Customer**

   - Attributes:
     - `customerId` (Unique ID)
     - `name`
     - `email`
     - `phoneNumber`
     - `address`
     - `dateOfBirth`
   - Relationships:
     - One-to-Many with Account

2. **Account**

   - Attributes:
     - `accountId` (Unique ID)
     - `accountType` (Savings/Current)
     - `balance`
     - `customerId` (Foreign Key)
     - `openedDate`
     - `status`
   - Relationships:
     - One-to-Many with Transactions

3. **Transaction**

   - Attributes:
     - `transactionId` (Unique ID)
     - `accountId` (Foreign Key)
     - `transactionType` (Credit/Debit)
     - `amount`
     - `timestamp`
     - `description`

#### Use Cases

1. **Customer Management:**

   - Create new customers
   - Retrieve customer details
   - Update customer information
   - Delete customers

2. **Account Management:**

   - Open new accounts
   - View account details
   - Deposit and withdraw funds
   - Close accounts

3. **Transaction Processing:**

   - Process transactions (credit/debit)
   - Retrieve transaction history
   - Generate monthly account statements

#### Architectural Flow

1. **Client Layer:**

   - Frontend (Angular/React)
   - REST API Calls

2. **Service Layer:**

   - Spring Boot Microservices
   - Business Logic Implementation
   - Layered Architecture (Controller, Service, Repository)
   - AOP for logging and audit

3. **Data Layer:**

   - Spring Data JPA for persistence
   - PostgreSQL/MySQL database

#### REST API Endpoints

1. **Customer Controller:**

   - `POST /customers` - Create a new customer
   - `GET /customers/{id}` - Retrieve customer details
   - `PUT /customers/{id}` - Update customer details
   - `DELETE /customers/{id}` - Remove customer

2. **Account Controller:**

   - `POST /accounts` - Open a new account
   - `GET /accounts/{id}` - Get account details
   - `PUT /accounts/deposit` - Deposit funds
   - `PUT /accounts/withdraw` - Withdraw funds

3. **Transaction Controller:**

   - `POST /transactions` - Record a new transaction
   - `GET /transactions/account/{id}` - Retrieve account transaction history

#### Implementation Steps

1. **Set Up Spring Boot Project:**

   - Configure dependencies (Spring Boot, JPA, Lombok, PostgreSQL)

2. **Entity Creation and Repository Setup:**

   - Define `Customer`, `Account`, `Transaction` entities
   - Implement JPA repositories

3. **Service and Controller Implementation:**

   - Implement business logic in service layer
   - Expose RESTful endpoints

4. **Exception Handling and Validation:**

   - Custom exceptions for insufficient balance, invalid accounts
   - Input validation using annotations
   - Implement `@ControllerAdvice` for centralized exception handling

5. **AOP for Logging and Auditing:**

   - Implement cross-cutting concerns like logging and auditing using Spring AOP
   - Use `@Before`, `@After`, and `@Around` advice annotations for tracking method executions

#### Conclusion

The banking application case study provides an end-to-end view of developing a robust financial application using Core Java and Spring Boot. Participants will gain hands-on experience with developing RESTful APIs, managing data persistence, implementing security measures, and deploying applications to production environments.

