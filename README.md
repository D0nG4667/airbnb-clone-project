# 🏡 Airbnb Clone Backend

## 📖 Overview

The **Airbnb Clone** project is a full-stack backend application designed to replicate the functionality of the popular Airbnb platform. It focuses on building a **robust, scalable, and secure booking system**, where users can list properties, make reservations, process payments, and leave reviews.

This project emphasizes **backend engineering best practices**, covering topics like API development, database design, CI/CD, and containerized deployment — reflecting a real-world software engineering environment.

---

## 🎯 Project Goals

* **User Management:** Secure registration, authentication, and profile management.
* **Property Management:** Enable property owners (hosts) to create, update, and manage listings.
* **Booking System:** Allow guests to book properties, manage stays, and handle cancellations.
* **Payment Processing:** Integrate payment gateway support for booking transactions.
* **Review System:** Allow users to submit reviews and ratings.
* **Scalability & Optimization:** Leverage caching, indexing, and background jobs for efficiency.
* **API Documentation:** Provide OpenAPI (Swagger) and GraphQL endpoints for developers.

---

## 🧰 Technology Stack

| Category              | Technology                         | Description                                               |
| --------------------- | ---------------------------------- | --------------------------------------------------------- |
| **Backend Framework** | **Django**                         | Python web framework for scalable backend development.    |
| **API Layer**         | **Django REST Framework (DRF)**    | Provides RESTful APIs for CRUD operations.                |
| **Query Language**    | **GraphQL (Graphene-Django)**      | Flexible and efficient data querying layer.               |
| **Database**          | **PostgreSQL**                     | Reliable relational database for storing structured data. |
| **Caching / Queue**   | **Redis + Celery**                 | For caching, async jobs, and background task management.  |
| **Containerization**  | **Docker & Docker Compose**        | Consistent development and production environment.        |
| **CI/CD**             | **GitHub Actions**                 | Automated testing, linting, and deployment pipelines.     |
| **Authentication**    | **JWT (JSON Web Tokens)**          | Secure token-based authentication.                        |
| **Testing**           | **Pytest / Django Test Framework** | Unit and integration testing.                             |

---

## 🏗️ Project Structure

```
airbnb-clone-backend/
│
├── app/
│   ├── users/                # User management module
│   ├── properties/           # Property listings module
│   ├── bookings/             # Booking and reservation module
│   ├── payments/             # Payment and transaction module
│   ├── reviews/              # Review and rating module
│   ├── core/                 # Core utilities, middleware, settings
│   ├── schema/               # GraphQL schema definitions
│   └── manage.py             # Django entry point
│
├── docker/
│   ├── web.Dockerfile        # Dockerfile for Django API
│   ├── redis.Dockerfile      # Optional Redis image customization
│
├── compose/
│   └── docker-compose.yml    # Compose configuration for multi-service setup
│
├── requirements.txt          # Python dependencies
├── .env.example              # Environment variables template
├── .github/
│   └── workflows/
│       └── ci-cd.yml         # GitHub Actions pipeline
│
├── docs/
│   ├── API_REFERENCE.md      # API documentation (OpenAPI / Swagger)
│   ├── SCHEMA.md             # GraphQL schema overview
│   └── SETUP.md              # Setup guide and commands
│
└── README.md                 # Project overview (this file)
```

---

## ⚙️ Setup Instructions

### **1. Clone the Repository**

```bash
git clone https://github.com/<your-username>/airbnb-clone-backend.git
cd airbnb-clone-backend
```

---

### **2. Configure Environment Variables**

Copy the `.env.example` file to `.env`:

```bash
cp .env.example .env
```

Edit your `.env` file with actual credentials:

```env
POSTGRES_DB=airbnb_db
POSTGRES_USER=airbnb_user
POSTGRES_PASSWORD=airbnb_pass
SECRET_KEY=your_django_secret_key
DEBUG=True
ALLOWED_HOSTS=*
REDIS_URL=redis://redis:6379/0
```

---

### **3. Build and Run with Docker**

Ensure Docker and Docker Compose are installed, then run:

```bash
docker-compose up --build
```

This will start:

* Django API service
* PostgreSQL database
* Redis (for caching / Celery)

---

### **4. Run Database Migrations**

After containers are up, run migrations:

```bash
docker-compose exec web python manage.py migrate
```

---

### **5. Create a Superuser**

```bash
docker-compose exec web python manage.py createsuperuser
```

---

### **6. Access the Application**

* **API Root:** [http://localhost:8000/api/](http://localhost:8000/api/)
* **Admin Panel:** [http://localhost:8000/admin/](http://localhost:8000/admin/)
* **GraphQL Playground:** [http://localhost:8000/graphql/](http://localhost:8000/graphql/)

---

### **7. Run Tests**

```bash
docker-compose exec web pytest
```

---

## 📘 Documentation

* **REST API:** `/swagger/` (auto-generated from OpenAPI)
* **GraphQL Endpoint:** `/graphql/`
* **Docs:** See `/docs/` folder for detailed schema and setup notes.

---

## 👥 Team Roles

A well-structured development team ensures smooth collaboration and clear ownership of responsibilities.
The roles below reflect both the project needs and the **recommended team structure** from [ITRexGroup](https://itrexgroup.com/blog/software-development-team-structure/).

| **Role**                                     | **Responsibility**                                                                                                                                                                                                                                           |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Backend Developer**                        | Implements core business logic, API endpoints, and database models. Ensures API performance, data integrity, and integration with authentication and payment services. Collaborates with DevOps and QA to maintain code quality and system reliability.      |
| **Database Administrator (DBA)**             | Designs and maintains the database schema (tables, relationships, indexes). Monitors performance, optimizes queries, ensures data consistency, and manages database backups and migrations.                                                                  |
| **DevOps Engineer**                          | Handles deployment, monitoring, and scaling using tools like Docker and GitHub Actions. Maintains CI/CD pipelines, manages environment configuration, and ensures system uptime, scalability, and automation.                                                |
| **QA Engineer**                              | Ensures product quality through automated and manual testing. Verifies business logic, API endpoints, and integrations. Works closely with developers to detect, document, and fix bugs early in the development lifecycle.                                  |
| **Project Lead / Software Architect**        | Oversees the entire technical direction and ensures architectural consistency across modules. Defines coding standards, reviews pull requests, and facilitates team coordination. Balances trade-offs between scalability, performance, and maintainability. |
| **Team Coordinator / GitHub Workflow Owner** | Manages GitHub repositories, branching strategy, and code review processes. Enforces consistent documentation (README, API Docs), organizes sprints, and ensures collaboration between roles.                                                                |

---

### 💡 Additional Notes

* This team structure ensures each component of the project — from backend logic to infrastructure and testing — is owned and optimized by a dedicated specialist.
* According to [ITRexGroup](https://itrexgroup.com/blog/software-development-team-structure/), balanced teams reduce bottlenecks and accelerate delivery by combining complementary expertise across development, QA, and DevOps.

---

## 🧩 Database Design

The database is the backbone of the Airbnb Clone backend, enabling efficient data storage, retrieval, and scalability. This section outlines the design principles, entities, attributes, relationships, normalization, schema details, and indexing strategies.

---

### **Database Design Principles**

1. **Entity-Relationship (ER) Diagrams**  
   ER diagrams visually represent entities (tables), attributes (columns), and relationships between entities. They help in understanding data organization and designing a coherent schema.

2. **Normalization**  
   Normalization organizes data to reduce redundancy and ensure data integrity.  
   * **1NF:** Ensure atomic values and unique records.  
   * **2NF:** All non-key attributes fully depend on the primary key.  
   * **3NF:** Attributes depend only on the primary key.  

3. **Schema Design**  
   Schema design defines tables, columns, data types, keys, and constraints. It provides a blueprint for database implementation.

4. **Practical Steps**  
   * Create ER diagrams using tools like Lucidchart, draw.io, or ERDPlus.  
   * Normalize tables to remove redundancy.  
   * Define the schema with primary keys, foreign keys, and constraints.  
   * Apply indexing to optimize queries.

---

### **Entities & Attributes**

**Users**

* `user_id`: PK, UUID, Indexed  
* `first_name`, `last_name`: VARCHAR, NOT NULL  
* `email`: VARCHAR, UNIQUE, NOT NULL  
* `password_hash`: VARCHAR, NOT NULL  
* `phone_number`: VARCHAR, NULL  
* `role`: ENUM (guest, host, admin), NOT NULL  
* `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  

**Properties**

* `property_id`: PK, UUID, Indexed  
* `host_id`: FK → Users(user_id)  
* `name`, `description`, `location`: NOT NULL  
* `pricepernight`: DECIMAL, NOT NULL  
* `created_at`, `updated_at`: TIMESTAMP  

**Bookings**

* `booking_id`: PK, UUID, Indexed  
* `property_id`: FK → Properties(property_id)  
* `user_id`: FK → Users(user_id)  
* `start_date`, `end_date`: DATE, NOT NULL  
* `total_price`: DECIMAL, NOT NULL  
* `status`: ENUM (pending, confirmed, canceled), NOT NULL  
* `created_at`: TIMESTAMP  

**Payments**

* `payment_id`: PK, UUID, Indexed  
* `booking_id`: FK → Bookings(booking_id)  
* `amount`: DECIMAL, NOT NULL  
* `payment_date`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  
* `payment_method`: ENUM (credit_card, paypal, stripe), NOT NULL  

**Reviews**

* `review_id`: PK, UUID, Indexed  
* `property_id`: FK → Properties(property_id)  
* `user_id`: FK → Users(user_id)  
* `rating`: INTEGER, 1–5  
* `comment`: TEXT, NOT NULL  
* `created_at`: TIMESTAMP  

**Messages**

* `message_id`: PK, UUID, Indexed  
* `sender_id`, `recipient_id`: FK → Users(user_id)  
* `message_body`: TEXT, NOT NULL  
* `sent_at`: TIMESTAMP  

---

### **Constraints**

* **Users:** Unique `email`; NOT NULL on required fields.  
* **Properties:** FK `host_id`; NOT NULL on essential attributes.  
* **Bookings:** FKs `property_id` and `user_id`; valid ENUM `status`.  
* **Payments:** FK `booking_id` linked to a valid booking.  
* **Reviews:** Rating 1–5; FKs on `property_id` and `user_id`.  
* **Messages:** FKs on `sender_id` and `recipient_id`.  

---

### **Indexing**

* Primary keys are automatically indexed.  
* Additional indexes:
  * `email` in Users  
  * `property_id` in Properties and Bookings  
  * `booking_id` in Bookings and Payments  

---

### **ER Diagram (Mermaid)**

```mermaid
erDiagram
    USERS {
        UUID user_id PK
        string first_name
        string last_name
        string email
        string password_hash
        string phone_number
        enum role
        datetime created_at
    }
    PROPERTIES {
        UUID property_id PK
        UUID host_id FK
        string name
        text description
        string location
        decimal pricepernight
        datetime created_at
        datetime updated_at
    }
    BOOKINGS {
        UUID booking_id PK
        UUID property_id FK
        UUID user_id FK
        date start_date
        date end_date
        decimal total_price
        enum status
        datetime created_at
    }
    PAYMENTS {
        UUID payment_id PK
        UUID booking_id FK
        decimal amount
        datetime payment_date
        enum payment_method
    }
    REVIEWS {
        UUID review_id PK
        UUID property_id FK
        UUID user_id FK
        int rating
        text comment
        datetime created_at
    }
    MESSAGES {
        UUID message_id PK
        UUID sender_id FK
        UUID recipient_id FK
        text message_body
        datetime sent_at
    }

    USERS ||--o{ PROPERTIES : "hosts"
    USERS ||--o{ BOOKINGS : "makes"
    PROPERTIES ||--o{ BOOKINGS : "has"
    BOOKINGS ||--|| PAYMENTS : "pays"
    PROPERTIES ||--o{ REVIEWS : "receives"
    USERS ||--o{ REVIEWS : "writes"
    USERS ||--o{ MESSAGES : "sends"
    USERS ||--o{ MESSAGES : "receives"
```

> **Tip:** If your Markdown viewer doesn't render Mermaid, view the diagram on [mermaid.live](https://mermaid.live/) (paste the diagram block there) or enable Mermaid support in your editor.

---

## 🌟 Feature Breakdown

The Airbnb Clone project incorporates a wide range of core functionalities designed to deliver a seamless experience for both guests and hosts. Each feature reflects essential aspects of a real-world booking platform, ensuring scalability, reliability, and ease of use.

### 👤 User Management

This module enables secure user registration, authentication, and profile management. Users can sign up as guests or hosts, update personal information, and manage their activity within the platform. It forms the foundation for all user-related interactions across the system.

### 🏠 Property Management

Hosts can create, update, and delete property listings with detailed descriptions, pricing, and amenities. This feature allows guests to browse, search, and filter properties based on location, price, and preferences, enhancing discoverability and engagement.

### 📅 Booking System

The booking system allows guests to reserve properties for specific dates, ensuring availability through robust validation. It manages the full reservation lifecycle — from booking creation to check-in and check-out — while maintaining consistency across users and properties.

### 💳 Payment Processing

This feature integrates secure payment gateways to handle transactions related to bookings. It ensures that payment records are accurately stored, verified, and linked to their corresponding bookings, enabling a trustworthy and transparent transaction flow.

### ⭐ Review System

After completing their stays, guests can leave reviews and ratings for properties. This fosters trust within the community, helping future guests make informed decisions while enabling hosts to receive feedback and improve their offerings.

### ⚡ Data Optimization & Performance

To enhance responsiveness, the backend implements database indexing, caching, and optimized query handling. These measures ensure that frequently accessed data — such as property listings or booking details — is retrieved efficiently, providing a smooth user experience.

### 🧠 API Documentation

All backend endpoints are documented using the OpenAPI standard, ensuring clear and consistent API specifications. Additionally, GraphQL support allows flexible data queries, empowering developers and clients to retrieve precisely what they need in a single request.

---

## 🏗️ System Architecture

The Airbnb Clone backend is built with a modular, scalable architecture that separates concerns across different layers and services. This design ensures maintainability, performance, and ease of feature expansion.

### Architecture Overview

1. **Client Layer**  
   Users interact with the system via web or mobile clients. Clients send requests to the backend through RESTful API endpoints or GraphQL queries.

2. **API Layer**  
   The Django backend, powered by Django REST Framework (DRF) and GraphQL (Graphene-Django), handles incoming requests. It manages business logic, user authentication, permissions, and data validation.

3. **Service Layer**  
   Contains core modules responsible for the main application features:
   * **User Management** – Handles registration, login, and profile management.
   * **Property Management** – Manages property listings and search functionalities.
   * **Booking System** – Handles reservations, availability checks, and booking lifecycle.
   * **Payment Processing** – Processes transactions securely.
   * **Review System** – Manages property reviews and ratings.

4. **Database Layer**  
   PostgreSQL stores structured data including users, properties, bookings, payments, and reviews. Indexing and optimized queries ensure high performance.

5. **Caching & Async Layer**  
   Redis is used for caching frequently accessed data and session management. Celery handles background tasks such as sending notifications and processing asynchronous payments.

6. **External Integrations**  
   The system can integrate with third-party services such as payment gateways, email services, and analytics platforms, providing additional functionality without compromising core system performance.

### Architecture Diagram (Mermaid)

```mermaid
graph LR
    Client[Users: Web & Mobile]
    API[API Layer: Django + DRF / GraphQL]
    Service[Service Layer: Users, Properties, Bookings, Payments, Reviews]
    DB[Database: PostgreSQL]
    Cache[Cache & Async: Redis + Celery]
    External[External Services: Payment, Email, Analytics]

    Client --> API
    API --> Service
    Service --> DB
    Service --> Cache
    Service --> External
```

---

## 🔒 API Security

Security is a critical aspect of the Airbnb Clone backend, ensuring that sensitive data, user interactions, and financial transactions remain protected. The following measures are implemented to safeguard the system:

### **1. Authentication**

All users must authenticate using secure methods before accessing protected endpoints.

* **Implementation:** JSON Web Tokens (JWT) for stateless authentication.  
* **Importance:** Ensures that only registered users can access their data, preventing unauthorized access to profiles, bookings, or payments.

### **2. Authorization**

Different users have different levels of access based on roles (guest, host, admin).  

* **Implementation:** Role-based access control (RBAC) to restrict actions on resources.  
* **Importance:** Prevents users from performing actions they are not allowed to (e.g., guests cannot modify property listings).

### **3. Rate Limiting**

API requests are monitored and limited to prevent abuse.  

* **Implementation:** Throttling via Django REST Framework’s rate-limiting features.  
* **Importance:** Protects the backend from denial-of-service (DoS) attacks and ensures fair usage for all users.

### **4. Data Validation & Sanitization**

All incoming data is validated to prevent malicious input.  

* **Implementation:** Serializer validation in DRF and input sanitization for forms and queries.  
* **Importance:** Prevents SQL injection, XSS attacks, and ensures the integrity of stored data.

### **5. Secure Payments**

Financial transactions are handled securely with encrypted communication and verified payment gateways.  

* **Implementation:** HTTPS, tokenized payment processing, and secure storage of transaction references (no sensitive card data stored).  
* **Importance:** Protects users’ financial information and ensures trust in the platform.

### **6. Logging & Monitoring**

All security-related events are logged and monitored.  

* **Implementation:** Centralized logging and alerts for suspicious activities.  
* **Importance:** Allows early detection of breaches, audit trails, and compliance with security standards.

---

## ⚙️ CI/CD Pipeline

Continuous Integration (CI) and Continuous Deployment (CD) are essential practices in modern software development that automate testing, building, and deployment of code changes. Implementing CI/CD ensures that new features, bug fixes, and updates are delivered reliably and efficiently, while minimizing human error.

### **Importance for the Airbnb Clone Project**

* **Automated Testing:** Every code change is automatically tested to ensure it does not break existing functionality.  
* **Faster Deployment:** Approved changes can be deployed to staging or production environments quickly and consistently.  
* **Code Quality & Consistency:** Enforces coding standards, linting, and validation before merging changes.  
* **Reduced Human Error:** Automation reduces manual intervention, lowering the risk of misconfigured deployments or missed tests.  
* **Scalability & Reliability:** Supports multiple developers working concurrently while maintaining a stable production environment.

### **Tools & Technologies**

* **GitHub Actions:** Automates workflows for testing, building, and deployment.  
* **Docker:** Ensures consistent containerized environments across development, staging, and production.  
* **Docker Compose:** Manages multi-service dependencies for local development and testing.  
* **PostgreSQL & Redis:** Services included in CI/CD pipelines for integration testing.  
* **Optional:** Tools like **Sentry** or **New Relic** can monitor deployments and catch runtime errors.

## 🧩 To Do

* Add CI/CD pipelines with GitHub Actions.
* Deploy to AWS / Render / Railway.
* Implement caching, pagination, and rate limiting.
* Extend GraphQL queries and mutations.
