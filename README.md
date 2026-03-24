# Online Shop

A RESTful online shop API built with Go, following clean architecture principles.

## Tech Stack

- **Language:** Go 1.22+
- **Router:** [chi](https://github.com/go-chi/chi)
- **Database:** PostgreSQL via [pgx](https://github.com/jackc/pgx)
- **Auth:** JWT (HS256) with [golang-jwt](https://github.com/golang-jwt/jwt)
- **Passwords:** bcrypt via `golang.org/x/crypto`

## Project Structure

```
online-shop/
├── cmd/server/main.go          # Entry point
├── internal/
│   ├── config/                 # Env-based configuration
│   ├── database/               # PostgreSQL connection pool
│   ├── handler/                # HTTP handlers (controllers)
│   ├── middleware/              # JWT auth & admin guard
│   ├── models/                 # Domain structs & request/response types
│   ├── repository/             # Data access layer (SQL queries)
│   ├── router/                 # Route definitions
│   └── service/                # Business logic
├── migrations/                 # SQL migration files
├── .env.example                # Environment variable template
└── go.mod
```

## Getting Started

### 1. Prerequisites

- Go 1.22+
- PostgreSQL 14+

### 2. Database setup

```bash
createdb online_shop
psql -d online_shop -f migrations/001_init.up.sql
```

### 3. Configuration

```bash
cp .env.example .env
# Edit .env with your database credentials and JWT secret
```

### 4. Run

```bash
go run ./cmd/server
```

The server starts on `:8080` by default.

## API Endpoints

| Method | Path                         | Auth     | Description             |
|--------|------------------------------|----------|-------------------------|
| POST   | `/api/v1/auth/register`      | —        | Register a new user     |
| POST   | `/api/v1/auth/login`         | —        | Login, receive JWT      |
| GET    | `/api/v1/products`           | —        | List products (filtered)|
| GET    | `/api/v1/products/{id}`      | —        | Get product by ID       |
| GET    | `/api/v1/categories`         | —        | List categories         |
| GET    | `/api/v1/categories/{id}`    | —        | Get category by ID      |
| POST   | `/api/v1/orders`             | Customer | Create an order         |
| GET    | `/api/v1/orders/my`          | Customer | List my orders          |
| GET    | `/api/v1/orders/{id}`        | Customer | Get order details       |
| POST   | `/api/v1/products`           | Admin    | Create a product        |
| PUT    | `/api/v1/products/{id}`      | Admin    | Update a product        |
| DELETE | `/api/v1/products/{id}`      | Admin    | Delete a product        |
| POST   | `/api/v1/categories`         | Admin    | Create a category       |
| PUT    | `/api/v1/categories/{id}`    | Admin    | Update a category       |
| DELETE | `/api/v1/categories/{id}`    | Admin    | Delete a category       |
| PUT    | `/api/v1/orders/{id}/status` | Admin    | Update order status     |
