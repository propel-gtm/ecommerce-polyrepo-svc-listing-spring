# Listing Service (Spring Boot)

A microservice for managing product listings in an e-commerce platform. Provides both REST and gRPC interfaces.

## 🎯 About This Repository

This repository is part of the **ecommerce-polyrepo** project - a polyrepo setup designed for testing the [Propel](https://propel.us) code review feature across multiple microservices.

### Role in Microservices Architecture

The Listing Service handles **product catalog and search functionality**:

```
┌──────────────┐
│ API Gateway  │
│   (Go/Gin)   │
└──────┬───────┘
       │ gRPC
       ▼
┌──────────────────┐
│ Listing Service  │
│  (Spring Boot)   │
│   [THIS REPO]    │
│                  │
│ • Product CRUD   │
│ • Categories     │
│ • Search/Filter  │
│ • REST + gRPC    │
└──────────────────┘
```

### Quick Start (Standalone Testing)

To test this service independently:

```bash
# 1. Ensure Java 17+ and Maven 3.8+ are installed
java -version
mvn -version

# 2. Build the project
mvn clean package

# 3. Run the application
mvn spring-boot:run

# 4. Test REST endpoints
curl http://localhost:8080/api/v1/products

# 5. Test specific product
curl http://localhost:8080/api/v1/products/1

# 6. Search products
curl http://localhost:8080/api/v1/products/search?query=laptop
```

**Note:** This service can run independently with an embedded H2 database for testing. For production, it integrates with PostgreSQL and other services via gRPC. The gRPC server runs on port 9090. See the [parent polyrepo](https://github.com/jasonyuezhang/ecommerce-polyrepo) for full stack setup.

---

## Features

- Product CRUD operations
- Category management
- Search and filtering
- REST API endpoints
- gRPC service interface

## Tech Stack

- Java 17
- Spring Boot 3.x
- Spring Data JPA
- gRPC
- PostgreSQL
- Docker

## Getting Started

### Prerequisites

- JDK 17+
- Maven 3.8+
- Docker (optional)

### Running Locally

```bash
# Build the project
mvn clean package

# Run the application
mvn spring-boot:run
```

### Docker

```bash
# Build Docker image
docker build -t svc-listing-spring .

# Run container
docker run -p 8080:8080 -p 9090:9090 svc-listing-spring
```

## API Endpoints

### Products

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /api/v1/products | List all products |
| GET | /api/v1/products/{id} | Get product by ID |
| POST | /api/v1/products | Create new product |
| PUT | /api/v1/products/{id} | Update product |
| DELETE | /api/v1/products/{id} | Delete product |
| GET | /api/v1/products/category/{categoryId} | Get products by category |
| GET | /api/v1/products/search?query={query} | Search products |

## gRPC Services

The service exposes gRPC endpoints on port 9090:

- `GetProduct` - Retrieve a single product
- `ListProducts` - List products with pagination
- `CreateProduct` - Create a new product
- `UpdateProduct` - Update an existing product
- `DeleteProduct` - Delete a product

## Configuration

Key configuration options in `application.yml`:

| Property | Description | Default |
|----------|-------------|---------|
| server.port | HTTP port | 8080 |
| grpc.server.port | gRPC port | 9090 |
| spring.datasource.url | Database URL | jdbc:postgresql://localhost:5432/listing |

## License

MIT
