# Identity & Access Management Platform

## Overview

This project is a Spring Boot–based Identity & Access Management (IAM) platform designed to demonstrate secure authentication workflows, OTP-based account activation, temporary token lifecycle management, and backend security concepts.

The application follows a multi-step authentication process using Spring Security, session management, BCrypt password hashing, and scheduled background cleanup tasks.

The project was built to explore real-world backend authentication architecture beyond basic CRUD applications.

---

# Features

## Authentication & Authorization

- User Registration
- Secure Login System
- OTP-Based Account Activation
- Session-Based Authentication Flow
- Temporary Token Generation
- Token Validation
- Token Refresh
- Token Invalidation

---

## Security Features

- BCrypt Password Hashing
- Secure Credential Validation
- Session-Based OTP Authorization
- Protected Route Handling
- Authentication Event Logging
- Temporary Token Lifecycle Management
- Automatic Cleanup of Inactive Accounts

---

## User Lifecycle Management

- Users are initially registered as inactive
- OTP verification required for account activation
- Inactive users are automatically deleted after timeout
- Background scheduler continuously monitors inactive accounts

---

## Observability & Logging

The application uses SLF4J logging to track:

- User registration
- Login attempts
- OTP verification
- Token issuance
- Token refresh operations
- Token invalidation
- Account cleanup tasks

---

# Authentication Flow

```text
User Registration
        ↓
Password Hashing (BCrypt)
        ↓
User Stored as Inactive
        ↓
User Login
        ↓
Credential Validation
        ↓
OTP Verification
        ↓
Account Activation
        ↓
Access Granted
```

---

# Temporary Token Flow

```text
Authenticated User
        ↓
Issue Temporary Token
        ↓
Validate Token
        ↓
Refresh Token
        ↓
Invalidate Token
```

---

# Tech Stack

| Technology | Purpose |
|---|---|
| Java 17 | Core Language |
| Spring Boot | Backend Framework |
| Spring Security | Authentication & Authorization |
| Spring Data JPA | Database Access |
| H2 Database | Embedded Database |
| Thymeleaf | Server-Side Rendering |
| BCrypt | Password Hashing |
| SLF4J | Logging |
| Maven | Build Tool |

---

# Project Structure

```text
src/main/java/io/github/bnojdev/sso
│
├── config/               # Security configuration
├── controller/           # MVC and REST controllers
├── model/                # Entity and DTO models
├── repository/           # JPA repositories
├── scheduler/            # Scheduled cleanup tasks
├── service/              # Business logic layer
├── security/             # Authentication utilities
└── util/                 # Helper utilities

src/main/resources/
│
├── templates/            # Thymeleaf templates
├── static/               # CSS & static assets
└── application.properties
```

---

# API Endpoints

## Authentication Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/login` | Login page |
| POST | `/login` | Authenticate user |
| GET | `/register` | Registration page |
| POST | `/register` | Register new user |
| GET | `/otp` | OTP verification page |
| POST | `/otp` | Verify OTP |

---

## Temporary Token Endpoints

| Method | Endpoint | Description |
|---|---|---|
| POST | `/temporary-token/issue` | Generate temporary token |
| POST | `/temporary-token/validate` | Validate token |
| POST | `/temporary-token/refresh` | Refresh temporary token |
| POST | `/temporary-token/invalidate` | Invalidate token |

---

# Registration Workflow

1. User submits:
   - Email
   - Username
   - Password

2. Password is securely hashed using BCrypt

3. User account is stored as inactive

4. User must log in and complete OTP verification

5. Upon successful OTP validation:
   - Account becomes activated
   - User gains access to protected resources

6. If OTP activation is not completed within 30 seconds:
   - Scheduled cleanup task removes inactive account

---

# Security Architecture

## Password Security

Passwords are never stored in plain text.

The application uses BCrypt hashing:

```java
passwordEncoder.encode(rawPassword)
```

---

## Session-Based OTP Authorization

OTP access is controlled using secure session flags:

```text
otpAllowed = true
```

This prevents unauthorized direct OTP access.

---

## Temporary Token Lifecycle

The platform supports:

- Token issuance
- Token validation
- Token refresh
- Token invalidation

This simulates real-world authentication token workflows.

---

# Scheduled Cleanup System

A scheduled background task runs periodically to remove inactive accounts that exceed the activation timeout.

Purpose:
- prevent stale registrations
- maintain database hygiene
- simulate lifecycle management

---

# Logging & Monitoring

The application logs:

- Authentication attempts
- Login success/failure
- OTP verification events
- Token operations
- Cleanup operations

This improves:
- observability
- debugging
- auditability

---

# How to Run

## Clone Repository

```bash
git clone https://github.com/bnojdev/SSO.git
```

---

## Build Project

```bash
mvn clean install
```

---

## Run Application

```bash
mvn spring-boot:run
```

---

# Application URLs

| Service | URL |
|---|---|
| Login Page | http://localhost:8086/login |
| Registration Page | http://localhost:8086/register |
| H2 Console | http://localhost:8086/h2-console |

---

# H2 Database Configuration

| Property | Value |
|---|---|
| JDBC URL | `jdbc:h2:file:./data/sso-db` |
| Username | `sa` |
| Password | *(empty)* |

---

# Default OTP

```text
686856
```

---

# Technical Highlights

This project demonstrates:

- Authentication workflow design
- Secure password handling
- OTP-based verification flow
- Session management
- Temporary token lifecycle handling
- Scheduled background processing
- Layered Spring Boot architecture
- MVC design pattern
- Logging and audit trail implementation
- Backend security practices

---

# Future Enhancements

## Security Improvements

- JWT-Based Authentication
- Refresh Token Rotation
- OAuth2 Authorization Server
- Role-Based Access Control (RBAC)
- Multi-Factor Authentication (MFA)
- Redis Session Storage
- Distributed Session Management
- Login Rate Limiting
- Token Blacklisting

---

## Infrastructure Improvements

- PostgreSQL Migration
- Docker Containerization
- Redis Integration
- API Gateway Integration
- Centralized Logging
- Prometheus Metrics
- Grafana Monitoring

---

## Scalability Enhancements

- Stateless Authentication
- Distributed Authentication Services
- Redis-Based OTP Storage
- Event-Driven Authentication Flow
- Kafka Integration

---

# Project Motivation

This project was created to explore:

- authentication system architecture
- secure user lifecycle management
- Spring Security internals
- token management workflows
- session handling
- backend security engineering

The goal was to move beyond traditional CRUD applications and build a backend system focused on real authentication workflows.

---

# Status

Actively evolving backend authentication platform focused on secure identity management and scalable authentication workflows.

---

# Author

GitHub:
https://github.com/bnojdev

---
