<div align="center">

# 🏪 Merch Shop

**REST API for an internal merch store with virtual currency**

[![Go](https://img.shields.io/badge/Go-1.23+-00ADD8?style=for-the-badge&logo=go&logoColor=white)](https://golang.org)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-336791?style=for-the-badge&logo=postgresql&logoColor=white)](https://postgresql.org)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://docker.com)
[![k6](https://img.shields.io/badge/k6-Load_Tested-7D64FF?style=for-the-badge&logo=k6&logoColor=white)](https://k6.io)

<br>

<table>
<tr>
<td align="center"><h3>⚡ 1000 RPS</h3><sub>sustained load</sub></td>
<td align="center"><h3>< 50ms</h3><sub>99.99% latency</sub></td>
<td align="center"><h3>53%</h3><sub>test coverage</sub></td>
<td align="center"><h3>0</h3><sub>failed transactions</sub></td>
</tr>
</table>

</div>

---

## 💡 What It Does

Employees receive **1000 coins** on registration and can:

- 🛒 **Buy merch** — 10 items from t-shirts to hoodies at fixed prices
- 💸 **Transfer coins** — send coins to colleagues as thanks or gifts
- 📊 **Track history** — view purchases, incoming and outgoing transfers

All operations are **atomic** — no negative balances, no self-transfers, full audit trail.

---

## 🏗️ Architecture

Built with **Clean Architecture** — easy to extend, test, and maintain:

```
cmd/                    → Entry point
internal/
├── controllers/        → HTTP handlers (Gin)
├── services/           → Business logic
├── repositories/       → PostgreSQL queries
├── models/             → Domain entities
├── dto/                → Request/Response schemas
├── middleware/          → JWT auth + request logging
└── routes/             → API routing
migrations/             → Goose SQL migrations
tests/
├── unit_test/          → Service layer tests (mocks)
├── e2e/                → Integration tests (real DB)
└── loadtest.js         → k6 scenario (1000 RPS)
```

---

## 🔌 API

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| `POST` | `/api/auth` | Register / login (auto-creates user) | — |
| `GET` | `/api/buy/:item` | Purchase merch item | JWT |
| `POST` | `/api/sendCoin` | Transfer coins to colleague | JWT |
| `GET` | `/api/info` | Balance + full transaction history | JWT |

---

## 🛠 Tech Stack

| | Technology | Purpose |
|-|------------|---------|
| 🔧 | **Go + Gin** | Fast HTTP framework |
| 🗄 | **PostgreSQL** | Persistent storage with indexes |
| 🔐 | **JWT + bcrypt** | Auth with password hashing |
| 📦 | **Docker Compose** | One-command deployment |
| 🔄 | **Goose** | Database migrations |
| 📝 | **Logrus** | Structured logging |
| 🧪 | **k6** | Load testing at 1000 RPS |

---

## 🚀 Quick Start

```bash
git clone https://github.com/AlexMayka/merch-shop.git
cd merch-shop
docker-compose up --build
```

API available at `http://localhost:8080`

---

## 📈 Performance

Load tested with **k6** at 1000 concurrent RPS:

| Metric | Result |
|--------|--------|
| Throughput | **1000 req/s** sustained |
| p99.99 latency | **< 50ms** |
| Failed requests | **0** |
| Concurrent safety | Verified (no race conditions) |

Optimized SQL queries — aggregating user info in a **single query** instead of N+1.

---

## 🧪 Tests

```bash
go test ./tests/unit_test -v   # Unit tests
go test ./tests/e2e -v         # E2E tests (requires DB)
```

## License

MIT
