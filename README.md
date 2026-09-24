<div align="center">

# Hi, I'm Kamal 👋

**Junior Java Backend Developer · Moscow**

[![Telegram](https://img.shields.io/badge/Telegram-@k__musaev-26A5E4?style=flat&logo=telegram&logoColor=white)](https://t.me/k_musaev)
[![Email](https://img.shields.io/badge/Email-kmm__work%40proton.me-005FF9?style=flat)](mailto:kmm_work@proton.me)

**English** · [Русский](https://github.com/b1oodraider/b1oodraider/blob/main/README.ru.md)

</div>

---

I'm a junior Java developer, self-taught in Java and the Spring ecosystem. I've built three backend projects from scratch and am now developing a microservice-based one.

I have six months of commercial development experience — production, business logic, tasks from a business analyst — though not in Java. I'm looking for an internship or a junior position where I can grow on real-world tasks.

## 🛠 Tech stack

| | |
|---|---|
| **Language** | Java (21 in learning projects, 25 in the microservice one), OOP, multithreading |
| **Backend** | Spring Boot (3.x in learning projects, 4.x in the microservice one), Spring MVC, Spring Security, Spring Data JPA, Hibernate, Spring Cloud Gateway |
| **Data** | PostgreSQL, SQL, JDBC, Liquibase, Redis |
| **Integrations** | REST, JWT, OpenAPI / Swagger, gRPC + protobuf, Apache Kafka |
| **Testing** | JUnit 5, Mockito, MockMvc, Testcontainers, Spring Security Test |
| **Infrastructure** | Docker (multi-stage), Docker Compose, Linux, Git, Maven, GitHub Actions |

## 🚀 Projects

### [dating](https://github.com/b1oodraider/dating)

Microservice backend for a dating app. Under active development; I'm building it solo.

**Four services:**

- **`dating-core`** — registration and authentication (Spring Security + JWT, access/refresh token pair), profiles (Spring Data JPA, PostgreSQL, Liquibase migrations), likes and matches
- **`matching`** — fetches profiles from core over gRPC: parallel calls with a per-call timeout, so one unavailable profile doesn't break the whole result
- **`api-gateway`** — Spring Cloud Gateway: single entry point, routing, Redis-based rate limiting
- **`notification`** — idempotent Kafka consumer

**The most interesting problem: a race condition on simultaneous mutual likes**

The first version checked for the reverse like before inserting a match, and a concurrent test produced two matches for the same pair. I fixed it at the database level: the pair is canonicalized (smaller id, larger id) and protected by a unique constraint, and an insert conflict is treated as "match already exists". The insert runs in a separate transaction — otherwise the constraint violation marks the outer transaction as rollback-only and there's no way to recover from the conflict. Covered by a concurrent integration test: exactly one match and exactly one Kafka event per pair.

**Also in the project:**

- Domain events are published to Kafka via Spring Modulith's event publication registry: the event record is committed in the same transaction as the match and republished on failure
- Tests: integration tests on Testcontainers (PostgreSQL, Kafka), gRPC integration tests, transaction rollback tests, concurrency tests
- Docker Compose, CI on GitHub Actions (build and tests across all modules)
- Open tasks and known limitations are tracked right in the code — `TODO`s describing exactly what isn't done yet and why

### Earlier projects

| Project | Description | Stack |
|---|---|---|
| **[Bank_rest_app](https://github.com/b1oodraider/Bank_rest_app)** | REST service for banking operations: card management, transfers between accounts, JWT authentication, role-based access | Spring Boot 3, Spring Security + JWT, PostgreSQL + Liquibase, SpringDoc OpenAPI, Docker multi-stage + Compose |
| **[Market2](https://github.com/b1oodraider/Market2)** | E-commerce app: registration, catalog, cart (local and server-side) | Spring Boot 3, Thymeleaf + vanilla SPA, Spring Security, PostgreSQL + Liquibase, JUnit 5 / MockMvc / Spring Security Test, Docker multi-stage + Compose |
| **[TaskManager](https://github.com/b1oodraider/TaskManager)** | Task manager REST API: task CRUD, JWT authentication | OpenAPI 3.0, Spring Data JPA + PostgreSQL, Docker Compose |

## 💼 Experience

**Developer Intern (1C:Enterprise) — Kirgu, Makhachkala**
*February – July 2025*

- Development and support of an internal accounting system for a retail chain — production environment, real users
- Reports on inventory levels and employee performance: from a business analyst's request → data model → a finished report used daily
- A fiscal receipt template and improvements to the print form builder
- Optimization of modules and queries; finding bottlenecks in data exchange with external systems
- Supporting code in production

## 🔭 Currently

Working on `dating`: improving candidate selection in `matching` and paying down technical debt from the TODOs. In parallel, I'm porting the project to Java 21 / Spring Boot 3.x so I'm not tied to whichever stack version a work project turns out to use.

## 🎯 Looking for

- Java / Spring internships and junior positions
- Remote or hybrid preferred; on-site in Moscow or Saint Petersburg is also an option

## 🌐 English

B1 — I read technical documentation and English-language source code comfortably.

## 📫 Contacts

- **Telegram:** [@k_musaev](https://t.me/k_musaev)
- **Email:** kmm_work@mail.ru
