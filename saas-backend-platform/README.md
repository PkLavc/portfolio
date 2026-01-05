# Multi-Tenant SaaS Backend for Small Business Management

A production-ready backend API built with NestJS, designed for small business management systems. Features multi-tenancy, authentication, CRUD operations, background job processing, and payment integration.

## Architecture Overview

This application follows clean architecture principles with clear separation of concerns:

- **Controllers**: Handle HTTP requests and responses
- **Services**: Contain business logic
- **Repositories**: Data access layer (via Prisma)
- **DTOs**: Data transfer objects for validation
- **Modules**: Feature-based organization

## Tech Stack

- **Language**: TypeScript
- **Runtime**: Node.js
- **Framework**: NestJS
- **Database**: PostgreSQL
- **ORM**: Prisma
- **Authentication**: JWT with Passport
- **Cache/Queue**: Redis (for future background jobs)
- **Background Jobs**: (simulated)
- **Containerization**: Docker
- **Environment Config**: dotenv

## Features

### Authentication & Authorization
- User registration and login
- JWT-based authentication
- Role-based access control (Admin/User)
- Password hashing with bcrypt

### Multi-Tenancy
- Organization-based data isolation
- Row-level multi-tenancy
- Users belong to organizations

### CRUD Modules
- **Users**: Manage organization users
- **Organizations**: Admin-only management
- **Projects**: Organization-specific projects
- **Tasks**: Project-specific tasks with assignment

All modules include:
- Pagination
- Filtering
- Sorting
- Input validation
- Error handling

### Background Processing
- Asynchronous email sending simulation (logged to console)
- Job retries and failure handling (simplified)
- Logging

### External Integration
- Mocked Stripe payment processing
- Webhook endpoint for payment events

### Testing
- Unit tests for services
- Basic e2e test for authentication

## Environment Variables

Create a `.env` file in the root directory:

```env
# Database
DATABASE_URL="postgresql://username:password@localhost:5432/portfolio_saas?schema=public"

# JWT
JWT_SECRET="your-secret-key"
JWT_EXPIRES_IN="1h"

# Redis
REDIS_URL="redis://localhost:6379"

# Email (simulation)
EMAIL_HOST="smtp.gmail.com"
EMAIL_PORT=587
EMAIL_USER="your-email@gmail.com"
EMAIL_PASS="your-password"

# Payment (Stripe sandbox)
STRIPE_SECRET_KEY="sk_test_..."
STRIPE_WEBHOOK_SECRET="whsec_..."
```

## How to Run Locally

### Prerequisites
- Node.js (v18+)
- PostgreSQL
- Redis
- Docker (optional)

### Local Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd portfolio-saas-backend
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up database**
   ```bash
   # Start PostgreSQL and Redis locally or via Docker
   docker run --name postgres -e POSTGRES_USER=username -e POSTGRES_PASSWORD=password -e POSTGRES_DB=portfolio_saas -p 5432:5432 -d postgres:15
   docker run --name redis -p 6379:6379 -d redis:7-alpine
   ```

4. **Configure environment**
   ```bash
   cp .env.example .env
   # Edit .env with your values
   ```

5. **Run database migrations**
   ```bash
   npm run prisma:migrate
   npm run prisma:generate
   ```

6. **Start the application**
   ```bash
   npm run start:dev
   ```

The API will be available at `http://localhost:3000`.

### Docker Setup

1. **Build and run with Docker Compose**
   ```bash
   docker-compose up --build
   ```

This will start the app, PostgreSQL, and Redis.

## API Documentation

### Authentication

#### Register
```http
POST /auth/register
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "password123",
  "firstName": "John",
  "lastName": "Doe",
  "organizationId": "org-id"
}
```

#### Login
```http
POST /auth/login
Content-Type: application/json

{
  "username": "user@example.com",
  "password": "password123"
}
```

Response:
```json
{
  "access_token": "jwt-token-here"
}
```

### Organizations (Admin only)

#### Create Organization
```http
POST /organizations
Authorization: Bearer <token>
Content-Type: application/json

{
  "name": "My Company"
}
```

#### List Organizations
```http
GET /organizations?page=1&limit=10&name=search
Authorization: Bearer <token>
```

### Projects

#### Create Project
```http
POST /projects
Authorization: Bearer <token>
Content-Type: application/json

{
  "name": "Website Redesign",
  "description": "Redesign company website"
}
```

#### List Projects
```http
GET /projects?page=1&limit=10&name=search
Authorization: Bearer <token>
```

### Tasks

#### Create Task
```http
POST /tasks
Authorization: Bearer <token>
Content-Type: application/json

{
  "title": "Design homepage",
  "description": "Create new homepage design",
  "projectId": "project-id"
}
```

#### List Tasks
```http
GET /tasks?page=1&limit=10&status=pending
Authorization: Bearer <token>
```

### Payments

#### Create Payment Intent
```http
POST /payments/create-intent
Content-Type: application/json

{
  "amount": 1000,
  "currency": "usd"
}
```

#### Webhook
```http
POST /payments/webhook
Content-Type: application/json
Stripe-Signature: <signature>

{
  "type": "payment_intent.succeeded",
  "data": { ... }
}
```

## Design Decisions

### Multi-Tenancy
- **Row-based multi-tenancy**: Each table includes `organizationId` for data isolation
- **Pros**: Simple, scalable, no schema duplication
- **Cons**: Requires careful query filtering

### Authentication
- **JWT with Passport**: Industry standard, stateless
- **Role-based**: Simple ADMIN/USER roles
- **Password hashing**: bcrypt for security

### Background Jobs
- **BullMQ with Redis**: Reliable queue system
- **Email simulation**: Logs instead of actual sending for demo

### Payment Integration
- **Mocked Stripe**: Simulates real payment processing
- **Webhook handling**: Basic event processing

### Database
- **PostgreSQL**: Robust, ACID compliant
- **Prisma**: Type-safe ORM, migrations, schema management

### Architecture
- **NestJS modules**: Feature-based organization
- **Dependency injection**: Testable, maintainable code
- **Validation**: class-validator for input validation

## Testing

```bash
# Unit tests
npm run test

# E2E tests
npm run test:e2e

# Coverage
npm run test:cov
```

## Deployment

This application is containerized with Docker and can be deployed to any cloud platform supporting Docker containers (AWS ECS, Google Cloud Run, Azure Container Instances, etc.).

For production:
1. Use environment-specific configs
2. Set up proper database migrations
3. Configure monitoring and logging
4. Implement rate limiting
5. Add API versioning
6. Set up CI/CD pipeline

## Contributing

1. Follow the existing code style
2. Write tests for new features
3. Update documentation
4. Use meaningful commit messages

## License

This project is licensed under the MIT License.