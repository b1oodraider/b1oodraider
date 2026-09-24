<div align="center">

# Привет! Меня зовут Камал 👋

**Junior Java Backend Developer · Москва**

[![Telegram](https://img.shields.io/badge/Telegram-@k__musaev-26A5E4?style=flat&logo=telegram&logoColor=white)](https://t.me/k_musaev)
[![Email](https://img.shields.io/badge/Email-kmm__work%40mail.ru-005FF9?style=flat)](mailto:kmm_work@mail.ru)

[English](https://github.com/b1oodraider/b1oodraider/blob/main/README.md) · **Русский**

</div>

---

Junior Java-разработчик. Самостоятельно изучаю Java и Spring-экосистему: собрал три backend-проекта с нуля, сейчас развиваю микросервисный.

Есть полгода коммерческой разработки — прод, бизнес-логика, задачи от аналитика. Коммерческого опыта на Java нет. Ищу стажировку или Junior-позицию, чтобы расти на боевых задачах.

## 🛠 Стек

| | |
|---|---|
| **Язык** | Java (учебные проекты — 21, микросервисный — 25), ООП, многопоточность |
| **Backend** | Spring Boot (3.x в учебных, 4.x в микросервисном), Spring MVC, Spring Security, Spring Data JPA, Hibernate, Spring Cloud Gateway |
| **Данные** | PostgreSQL, SQL, JDBC, Liquibase, Redis |
| **Интеграции** | REST, JWT, OpenAPI / Swagger, gRPC + protobuf, Apache Kafka |
| **Тесты** | JUnit 5, Mockito, MockMvc, Testcontainers, Spring Security Test |
| **Инфраструктура** | Docker (multi-stage), Docker Compose, Linux, Git, Maven, GitHub Actions |

## 🚀 Проекты

### [dating](https://github.com/b1oodraider/dating)

Микросервисный бэкенд дейтинг-приложения. В активной разработке, пишу один.

**Четыре сервиса:**

- **`dating-core`** — регистрация и аутентификация (Spring Security + JWT, пара access/refresh), профили (Spring Data JPA, PostgreSQL, миграции Liquibase), лайки и матчи
- **`matching`** — получение профилей из core по gRPC: параллельные вызовы с таймаутом на каждый, недоступность отдельного профиля не роняет выдачу
- **`api-gateway`** — Spring Cloud Gateway: единая точка входа, маршрутизация, rate limiting на Redis
- **`notification`** — идемпотентный консюмер Kafka

**Самая интересная задача — гонка при одновременном взаимном лайке**

Первая версия проверяла обратный лайк перед вставкой матча, и на конкурентном тесте я получал два матча на одну пару. Решил на уровне БД: канонизация пары (меньший id, больший id) + уникальное ограничение, конфликт вставки трактуется как «матч уже создан». Вставка вынесена в отдельную транзакцию — иначе нарушение ограничения помечает внешнюю транзакцию rollback-only и восстановиться после конфликта невозможно. Проверяется конкурентным интеграционным тестом: ровно один матч и ровно одно событие в Kafka на пару.

**Ещё в проекте:**

- Доменные события уходят в Kafka через реестр публикаций Spring Modulith: запись о событии фиксируется в одной транзакции с созданием матча и переотправляется при сбое
- Тесты: интеграционные на Testcontainers (PostgreSQL, Kafka), gRPC-интеграционные, rollback-тесты транзакций, конкурентные
- Docker Compose, CI на GitHub Actions (сборка и тесты по всем модулям)
- Открытые задачи и известные ограничения веду прямо в коде — `TODO` с описанием того, что именно не закрыто и почему

### Ранние проекты

| Проект | Описание | Стек |
|---|---|---|
| **[Bank_rest_app](https://github.com/b1oodraider/Bank_rest_app)** | REST-сервис банковских операций: управление картами, переводы между счетами, JWT-аутентификация, ролевая модель | Spring Boot 3, Spring Security + JWT, PostgreSQL + Liquibase, SpringDoc OpenAPI, Docker multi-stage + Compose |
| **[Market2](https://github.com/b1oodraider/Market2)** | E-commerce: регистрация, каталог, корзина (локальная и серверная) | Spring Boot 3, Thymeleaf + vanilla-SPA, Spring Security, PostgreSQL + Liquibase, JUnit 5 / MockMvc / Spring Security Test, Docker multi-stage + Compose |
| **[TaskManager](https://github.com/b1oodraider/TaskManager)** | REST API таск-менеджера: CRUD задач, JWT-аутентификация | OpenAPI 3.0, Spring Data JPA + PostgreSQL, Docker Compose |

## 💼 Опыт

**Стажёр-разработчик (1С:Предприятие) — Киргу, Махачкала**
*Февраль — июль 2025*

- Разработка и поддержка внутренней учётной системы розничной сети — продуктивная среда, реальные пользователи
- Отчётность по остаткам товаров и по работе сотрудников: задача от бизнес-аналитика → модель данных → готовый отчёт в ежедневном использовании
- Шаблон фискального чека и доработка конструктора печатных форм
- Оптимизация модулей и запросов, поиск узких мест в обмене данными с внешними системами
- Сопровождение кода в проде

## 🔭 Сейчас

Развиваю `dating`: дорабатываю отбор кандидатов в `matching`, закрываю технический долг из TODO. Параллельно переношу проект на Java 21 / Spring Boot 3.x — чтобы не зависеть от того, какая версия стека окажется в рабочем проекте.

## 🎯 Ищу

- Стажировку или Junior-позицию на Java / Spring
- Приоритет — удалёнка или гибрид; офис в Москве и Санкт-Петербурге тоже рассматриваю

## 🌐 Английский

B1 — техническую документацию и англоязычные исходники читаю свободно.

## 📫 Контакты

- **Telegram:** [@k_musaev](https://t.me/k_musaev)
- **Email:** kmm_work@mail.ru
