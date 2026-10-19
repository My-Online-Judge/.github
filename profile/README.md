# My Online Judge

**My Online Judge** is an open-source online judge platform for programming practice, algorithmic problem solving, and competitive programming.

The project is built as a modular, event-driven system with dedicated services for identity, problem management, submissions, judging, and deployment.

## Highlights

- Secure authentication with password login and Google OAuth
- JWT-based authorization using RSA signatures and JWKS
- Users, roles, permissions, login attempts, and access bans
- Problem statements, test cases, and per-problem statistics
- Asynchronous submission processing through Apache Kafka
- Distributed judge workers and sandboxed code execution
- Real-time verdict streaming through Server-Sent Events
- Internal gRPC communication between services
- Redis-based revocation, ban, and distributed-state support
- Prometheus metrics and OpenTelemetry tracing
- Docker Compose deployment for the complete platform
- Benchmarking and chaos testing for reliability evaluation

## Architecture

```text
Browser
   │
   ├── judge-portal
   │
   └── oj-api-gateway
          │
          ├── oj-identity-service
          │       └── PostgreSQL
          │
          ├── oj-problem-service
          │       ├── PostgreSQL
          │       └── MinIO
          │
          └── oj-submission-service
                  ├── PostgreSQL
                  ├── Kafka
                  └── Redis
                          │
                          └── judge-worker
                                  │
                                  └── judge-server sandbox
```

## Repositories

| Repository | Description |
|---|---|
| [`judge-portal`](https://github.com/My-Online-Judge/judge-portal) | Vue-based web portal for users, problems, submissions, and administration |
| [`oj-api-gateway`](https://github.com/My-Online-Judge/oj-api-gateway) | Public API gateway responsible for routing, CORS, client-IP handling, access bans, and token revocation |
| [`oj-identity-service`](https://github.com/My-Online-Judge/oj-identity-service) | Authentication and identity service with users, roles, permissions, OAuth, JWT, and security controls |
| [`oj-problem-service`](https://github.com/My-Online-Judge/oj-problem-service) | Problem, test case, judge specification, and problem statistics service |
| [`oj-submission-service`](https://github.com/My-Online-Judge/oj-submission-service) | Submission lifecycle, judge dispatching, verdict recording, SSE streaming, and judge-server registry |
| [`judge-worker`](https://github.com/My-Online-Judge/judge-worker) | Kafka-based worker that dispatches submissions to judge sandboxes and publishes verdicts |
| [`oj-common`](https://github.com/My-Online-Judge/oj-common) | Shared Java library for security, JWT verification, Redis, gRPC, events, and API responses |
| [`judge-deployment`](https://github.com/My-Online-Judge/judge-deployment) | Docker Compose stack for running the complete Online Judge platform |
| [`judge-api`](https://github.com/My-Online-Judge/judge-api) | Archived predecessor of the separated submission service |
| [`judge-server`](https://github.com/My-Online-Judge/judge-server) | Legacy judge server component |

## Technology Stack

- **Frontend:** Vue 3, Vite, and Nginx
- **Backend:** Java 17, Spring Boot, and Spring Cloud Gateway
- **Worker services:** Python
- **Databases:** PostgreSQL
- **Messaging:** Apache Kafka
- **Caching and coordination:** Redis
- **Object storage:** MinIO
- **Internal communication:** gRPC
- **Authentication:** JWT, RSA, JWKS, and Google OAuth
- **Observability:** Prometheus, OpenTelemetry, and Jaeger
- **Deployment:** Docker Compose
- **Code execution:** Isolated judge-server sandboxes

## Project Goals

My Online Judge aims to provide a reliable, maintainable, and extensible foundation for online programming education and competitive programming.

The platform focuses on:

1. Clear separation of responsibilities between services
2. Secure and isolated code execution
3. Reliable asynchronous judging workflows
4. Observable and debuggable distributed services
5. Reproducible local and production-like deployment
6. Continuous performance, load, and chaos testing

## Development Status

The platform is actively evolving from a monolithic architecture toward independently deployable services. The current architecture separates identity, problem, submission, gateway, worker, and deployment responsibilities into dedicated repositories.

## Contributing

Contributions, bug reports, architecture discussions, and improvement ideas are welcome.

Before contributing, please review the documentation and development instructions in the relevant repository.
