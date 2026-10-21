# Student Information System — Legacy Prototype

An educational Student Information System (SIS) prototype built with Node.js, Express, EJS, and MariaDB. It demonstrates modular controllers, services, repositories, validation, and academic resource management.

> **Legacy project / not production-ready.** This is the original academic CRUD prototype, separate from the actively maintained [SIS-API](https://github.com/alialnabulsi/SIS-API). Do not deploy it publicly or connect it to real university data. Authentication, authorization, and password handling require security remediation.

## Tech Stack

| Technology | Purpose |
| --- | --- |
| Node.js / JavaScript | Application runtime (CommonJS) |
| Express 4 | HTTP routes and middleware |
| MariaDB | Relational database through the `mariadb` driver |
| EJS | Server-rendered dashboard pages |
| express-validator | Request validation |
| bcrypt (dependency) | Password-hashing library; correct end-to-end use is not assured by this prototype |

The code uses repository-level SQL queries rather than a fully integrated Sequelize ORM.

## Project Structure

```text
Student-Information-System/
├── index.js          # Express setup and route mounting
├── config/           # MariaDB connection pool
├── routes/           # Academic and user resource routes
├── controllers/      # HTTP request handlers
├── services/         # Service-layer operations
├── repositories/     # Database queries
├── models/           # Data representations
├── validators/       # Input validators
├── middleware/       # Experimental security utilities
├── views/            # EJS dashboards
└── public/           # Static browser assets
```

## API Overview

The application mounts resource routers under `/api/sis`. The table below reflects route prefixes in `index.js`; individual supported methods vary by router.

| Resource group | Base path |
| --- | --- |
| Users | `/api/sis/user` |
| Students | `/api/sis/student` |
| Instructors and advisors | `/api/sis/instructor`, `/api/sis/advisor` |
| Roles and administration | `/api/sis/role`, `/api/sis/user-role`, `/api/sis/admin` |
| Academic organization | `/api/sis/campus`, `/api/sis/faculty`, `/api/sis/department` |
| Programs and subjects | `/api/sis/program`, `/api/sis/course`, `/api/sis/course-program`, `/api/sis/major`, `/api/sis/minor`, `/api/sis/prerequisite` |
| Scheduling and enrollment | `/api/sis/semester`, `/api/sis/section`, `/api/sis/schedule`, `/api/sis/enrollment` |
| Facilities | `/api/sis/building`, `/api/sis/location`, `/api/sis/room` |
| Exams and academic holds | `/api/sis/final-exam`, `/api/sis/final-exam-schedule`, `/api/sis/hold`, `/api/sis/student-hold` |
| Contact information | `/api/sis/phone-number` |

Examples of routes defined by the source code:

```http
GET /api/sis/user
GET /api/sis/user/id/:userID
POST /api/sis/user
GET /api/sis/course
GET /api/sis/course/:courseID
```

These are **code-reference examples only**. They should not be interpreted as safe-to-expose public endpoints.

## Local Development

**Prerequisite:** A MariaDB database matching the models/repositories. A complete database initialization migration is **not included** in this repository, so cloning it alone is not sufficient to run every endpoint.

1. Install Node.js and a compatible MariaDB server.
2. Clone the repository and install packages:
   ```bash
   git clone https://github.com/alialnabulsi/Student-Information-System.git
   cd Student-Information-System
   npm install
   ```
3. Create a local `.env` with these variables:
   ```env
   DB_HOST=127.0.0.1
   DB_USER=your_local_user
   DB_PASS=your_local_password
   DB_NAME=your_local_database
   PORT=5000
   ```
4. Provide a compatible **nonproduction** database schema, then start:
   ```bash
   npm run dev
   ```

The root page serves an EJS view at `http://localhost:5000/`. This repository's `npm test` script is a placeholder, not a test suite.

## Known Limitations and Security

- Current route wiring does not enforce authenticated or role-authorized access to administrative and destructive operations.
- User password comparison in the legacy model uses direct string equality; do not rely on it to protect credentials.
- The repository does not include a reproducible database schema migration.
- Some legacy naming, dependencies, and error handling still need review.

**Use [SIS-API](https://github.com/alialnabulsi/SIS-API) for the Balamandian integration.** The two repositories have different architectures and security models.
