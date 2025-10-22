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

| Role                       | Responsibility                                |
| -------------------------- | --------------------------------------------- |
| **Backend Developer**      | API endpoints, models, and business logic     |
| **Database Administrator** | Database schema, indexing, and optimization   |
| **DevOps Engineer**        | CI/CD pipelines, Docker, and deployment       |
| **QA Engineer**            | Testing and quality assurance                 |
| **Project Lead**           | Architecture, documentation, and coordination |

---

## 🧩 Next Steps

* Add CI/CD pipelines with GitHub Actions.
* Deploy to AWS / Render / Railway.
* Implement caching, pagination, and rate limiting.
* Extend GraphQL queries and mutations.

