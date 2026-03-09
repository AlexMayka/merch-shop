# Merch Shop

REST API service for an internal merch store where employees purchase items using virtual currency (coins). Features JWT authentication, clean architecture, and load-tested performance at 1000 RPS.

[![Go](https://img.shields.io/badge/Go-1.23+-00ADD8?style=flat-square&logo=go)](https://golang.org)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-336791?style=flat-square&logo=postgresql&logoColor=white)](https://postgresql.org)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?style=flat-square&logo=docker&logoColor=white)](https://docker.com)

## Key Features

- **Merch Marketplace** — 10 items with fixed coin prices, instant purchases
- **Coin Transfers** — peer-to-peer coin transfers between employees
- **Transaction History** — full audit trail of purchases and transfers
- **JWT Authentication** — secure token-based auth with middleware
- **Clean Architecture** — controllers → services → repositories separation
- **High Performance** — 1000 RPS with 99.99% responses under 50ms (k6)
- **Test Coverage** — 53% unit tests + full E2E suite

## Tech Stack

| Component | Technology |
|-----------|------------|
| Language | Go 1.23 |
| Framework | Gin |
| Database | PostgreSQL |
| Auth | JWT (bcrypt + token refresh) |
| Migrations | Goose |
| Logging | Logrus |
| Testing | Unit + E2E + k6 load tests |
| Deploy | Docker + Docker Compose |

## Quick Start

```bash
git clone https://github.com/AlexMayka/merch-shop.git
cd merch-shop
docker-compose up --build
```

Service available at `http://localhost:8080`

## API Endpoints

| Method | URL | Description | Auth |
|--------|-----|-------------|------|
| `POST` | `/api/auth` | Login / register (auto-creates on first login) | No |
| `GET` | `/api/buy/:item` | Purchase merch item | JWT |
| `POST` | `/api/sendCoin` | Transfer coins to another employee | JWT |
| `GET` | `/api/info` | Balance, purchases, transfer history | JWT |

## Architecture

```
cmd/                    # Application entry point
internal/
├── controllers/        # HTTP request handlers
├── services/           # Business logic layer
├── repositories/       # Database access layer
├── models/             # Data models
├── dto/                # Request/response objects
├── middleware/          # JWT auth + logging
├── routes/             # Route definitions
└── utils/              # Error handling
migrations/             # SQL migrations (Goose)
pkg/                    # Shared packages (DB, JWT, logger)
tests/
├── unit_test/          # Unit tests with mocks
├── e2e/                # Integration tests
└── loadtest.js         # k6 load test scenario
```

## Load Test Results

Tested with k6 at 1000 RPS sustained load:

- **99.99%** of requests completed under **50ms**
- Zero failed transactions under load
- Concurrent coin operations remain consistent (no negative balances)

## Running Tests

```bash
# Unit tests
go test ./tests/unit_test -v

# E2E tests (requires running DB)
go test ./tests/e2e -v
```

## License

MIT
