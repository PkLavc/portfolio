# Portfolio

A backend engineering portfolio showcasing production-oriented systems focused on scalability, maintainability, and cloud-native architecture.

## Projects

### SaaS Backend Platform

**Location**: `/saas-backend-platform`  
**Status**: Completed  
**Tech Stack**: TypeScript, Node.js, NestJS, PostgreSQL, Prisma, JWT, Redis, Docker

Multi-tenant SaaS backend for business management with production-oriented architecture.

#### Architecture
- Clean Architecture: Modular controllers, services, repositories, DTOs
- Multi-Tenancy: Row-based data isolation by organization
- Authentication: JWT with role-based access control
- Database: PostgreSQL with Prisma ORM

#### Features
- User Management: Registration, authentication, organization-scoped access
- CRUD Operations: RESTful APIs for users, organizations, projects, tasks
- Querying: Pagination, filtering, sorting
- Payment Processing: Mocked Stripe API for demonstration purposes
- Background Jobs: Asynchronous email processing
- Validation: Input validation and error handling

#### Development
- Containerization: Docker Compose with PostgreSQL and Redis
- Testing: Jest unit and e2e tests
- Code Quality: TypeScript, ESLint, Prettier

#### API Endpoints
- `POST /auth/register` - User registration
- `POST /auth/login` - Authentication
- `GET /organizations` - List organizations (Admin)
- `GET /projects` - Organization projects
- `GET /tasks` - Project tasks
- `POST /payments/create-intent` - Payment intent

#### Setup
```bash
cd saas-backend-platform
npm install
docker-compose up -d
npm run prisma:migrate
npm run start:dev
```

---

### Event-Driven Integration Service

**Location**: `/event-driven-integration-service`  
**Status**: Completed  
**Tech Stack**: TypeScript, Node.js, NestJS, PostgreSQL, Prisma, Redis, BullMQ, Docker

Event-driven service for webhook processing with asynchronous architecture.

#### Architecture
- Event-Driven Design: Queue-based processing with BullMQ and Redis
- Observability: OpenTelemetry tracing, Winston logging, Jaeger integration
- Database: PostgreSQL with Prisma
- Health Monitoring: Health checks and metrics

#### Features
- Webhook Processing: Asynchronous handling with retries
- Queue Management: Job scheduling and monitoring
- Logging: Structured logging with Winston
- Tracing: Distributed tracing
- Error Handling: Retry and failure management

#### Development
- Containerization: Docker Compose
- Code Quality: TypeScript, NestJS best practices

#### Setup
```bash
cd event-driven-integration-service
npm install
docker-compose up -d
npm run prisma:migrate
npm run start:dev
```

---

### Cloud Deployment Showcase

**Location**: `/cloud-deployment-showcase`  
**Status**: Completed  
**Tech Stack**: Railway, Docker, Nginx, GitHub Actions, PostgreSQL, Redis

Production deployment configuration for the Event-Driven Integration Service.

This project focuses on deployment patterns and infrastructure configuration rather than application feature development.

#### Infrastructure
- Cloud Platform: Railway with auto-scaling
- Load Balancing: Nginx reverse proxy
- Security: HTTPS, environment variables
- CI/CD: GitHub Actions for deployment
- Monitoring: Health checks, logging, tracing

#### Features
- Production Deployment: Containerized application on Railway
- Infrastructure as Code: Railway and Docker configuration
- Automation: CI/CD pipeline
- Observability: Integrated monitoring

#### Deployment
```bash
cd cloud-deployment-showcase
# Deploy via Railway or GitHub Actions
```

## Repository Structure

```
.
├── saas-backend-platform/          # Multi-tenant SaaS backend
│   ├── src/
│   ├── prisma/
│   ├── test/
│   ├── docker-compose.yml
│   └── README.md
├── event-driven-integration-service/  # Event-driven webhook service
│   ├── src/
│   ├── prisma/
│   ├── logs/
│   ├── docker-compose.yml
│   └── README.md
├── cloud-deployment-showcase/      # Cloud deployment & infrastructure
│   ├── Dockerfile.prod
│   ├── nginx.conf
│   ├── railway.toml
│   ├── deploy.sh
│   └── README.md
├── README.md              # This file
└── .gitignore
```

## Technologies

- Languages: TypeScript, SQL, Shell
- Frameworks: NestJS, Node.js
- Databases: PostgreSQL
- ORMs: Prisma
- Authentication: JWT, Passport
- Queues: BullMQ, Redis
- Observability: OpenTelemetry, Jaeger, Winston
- Containerization: Docker, Docker Compose
- Cloud Platforms: Railway
- Load Balancing: Nginx
- CI/CD: GitHub Actions
- Testing: Jest, Supertest
- Code Quality: ESLint, Prettier

## Expertise Demonstrated

- Scalable SaaS application development
- Multi-tenant architecture
- Event-driven systems and asynchronous processing
- Observability and distributed tracing
- Cloud deployment and infrastructure
- CI/CD automation
- Security practices for production
- RESTful API design and database optimization
- Authentication and authorization
- Containerization and orchestration
- Testing strategies and maintainability

## Contact

Review the codebase for architectural decisions and implementation details.

---

*Portfolio focused on backend engineering.*