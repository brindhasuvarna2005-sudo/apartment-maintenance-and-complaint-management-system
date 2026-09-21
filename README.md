# Apartment Maintenance & Complaint Management System — Backend

A role-based, full-stack maintenance and complaint management platform built as the capstone project for the Capgemini FUEL Full-Stack Java Development Program. This repository contains the backend REST API.

## Overview

The system lets residents raise maintenance complaints and lets staff manage them through a fixed lifecycle, with role-based access control and full CRUD coverage across normalized relational entities. The frontend (React) lives in a separate repository: [apartment-maintenance-frontend](https://github.com/brindhasuvarna2005-sudo/apartment-maintenance-frontend).

## Tech Stack

- **Java 17**
- **Spring Boot**
- **Spring Data JPA** / **Hibernate**
- **MySQL**
- **REST API** (tested with Postman)

## Key Features

- Full CRUD coverage across 5 normalized (3NF) relational entities, with JPA-mapped domain relationships
- Fixed complaint workflow: `OPEN → IN_PROGRESS → RESOLVED → CLOSED`, with protected-delete constraints and field-level validation
- Role-based access enforcing business rules at the service layer
- All endpoints verified end-to-end with Postman

## A Bug I Fixed

Every `GET` endpoint was silently returning a 500 error. Root cause: a `LazyInitializationException` caused by the Hibernate session closing before lazy-loaded associations were accessed. Fixed by applying `@Transactional(readOnly = true)` on the relevant service methods and adding structured exception logging so the failure mode would be visible immediately if it recurred.

## Getting Started

### Prerequisites
- Java 17+
- Maven
- MySQL

### Setup
1. Clone the repo:
```bash
   git clone https://github.com/brindhasuvarna2005-sudo/apartment-maintenance-and-complaint-management-system.git
```
2. Create a MySQL database and update `src/main/resources/application.properties` with your own credentials:
```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/apartment_maintenance_db
   spring.datasource.username=your_username
   spring.datasource.password=your_password
```
3. Run the application:
```bash
   mvn spring-boot:run
```
4. The API will be available at `http://localhost:8080` (or your configured port).

## Author

Brindha Suvarna — [GitHub](https://github.com/brindhasuvarna2005-sudo)