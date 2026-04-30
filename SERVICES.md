# REZ Services Catalog
**Last Updated:** 2026-04-30

---

## Overview

The REZ ecosystem consists of 17 backend microservices across core, supporting, and CorpPerks categories.

---

## Backend Services

### Core Services (9 microservices)

| Service | GitHub | Render | Port | Description |
|---------|--------|--------|------|-------------|
| rez-api-gateway | [Link](https://github.com/imrejaul007/rez-api-gateway) | N/A | 5002 | Kong + Nginx gateway, routes to microservices |
| rez-auth-service | [Link](https://github.com/imrejaul007/rez-auth-service) | [Link](https://rez-auth-service.onrender.com) | 4002 | Authentication, OTP, TOTP, JWT, OAuth2 |
| rez-merchant-service | [Link](https://github.com/imrejaul007/rez-merchant-service) | [Link](https://rez-merchant-service.onrender.com) | 4005 | Merchant management, teams, products |
| rez-order-service | [Link](https://github.com/imrejaul007/rez-order-service) | [Link](https://rez-order-service.onrender.com) | 3008 | Order processing, state machine, BullMQ |
| rez-payment-service | [Link](https://github.com/imrejaul007/rez-payment-service) | [Link](https://rez-payment-service.onrender.com) | 4001 | Payment processing, Razorpay integration |
| rez-wallet-service | [Link](https://github.com/imrejaul007/rez-wallet-service) | [Link](https://rez-wallet-service.onrender.com) | 3010 | Wallet, BNPL, credit, coins |
| rez-catalog-service | [Link](https://github.com/imrejaul007/rez-catalog-service) | N/A | 3005 | Product catalog, categories, Redis caching |
| rez-search-service | [Link](https://github.com/imrejaul007/rez-search-service) | N/A | 4003 | Full-text search, autocomplete, intent capture |
| rez-gamification-service | [Link](https://github.com/imrejaul007/rez-gamification-service) | N/A | 3001 | Points, streaks, achievements, leaderboards |

### Supporting Services (5 microservices)

| Service | GitHub | Port | Description |
|---------|--------|------|-------------|
| rez-ads-service | [Link](https://github.com/imrejaul007/rez-ads-service) | 4007 | Ad campaigns, placements, analytics |
| rez-marketing-service | [Link](https://github.com/imrejaul007/rez-marketing-service) | 4000 | WhatsApp, SMS, Email, Push notifications |
| rez-scheduler-service | [Link](https://github.com/imrejaul007/rez-scheduler-service) | 3012 | Cron jobs, BullMQ orchestration |
| rez-finance-service | [Link](https://github.com/imrejaul007/rez-finance-service) | 4005 | Loans, credit scoring, BNPL limits |
| rez-karma-service | [Link](https://github.com/imrejaul007/Karma) | 3009 | Social impact, karma points, batch conversion |

### Event Workers (3 services)

| Service | GitHub | Port | Description |
|---------|--------|------|-------------|
| rez-notification-events | [Link](https://github.com/imrejaul007/rez-notification-events) | 3005 | Push notifications, email |
| analytics-events | [Link](https://github.com/imrejaul007/analytics-events) | 3006 | Analytics pipeline |
| rez-media-events | [Link](https://github.com/imrejaul007/rez-media-events) | 3008 | Media processing |

### CorpPerks Services (4 microservices)

| Service | GitHub | Port | Description |
|---------|--------|------|-------------|
| rez-corpperks-service | Built-in | 4013 | CorpPerks Gateway API, benefits management |
| rez-hotel-service | Built-in | 4011 | Hotel OTA (Makcorps integration) |
| rez-procurement-service | Built-in | 4012 | Procurement (NextaBizz integration) |
| rez-intent-graph | [Link](https://github.com/imrejaul007/rez-intent-graph) | 3001/3005 | AI/ML intent capture, 8 autonomous agents |

---

## Mobile Apps

| App | GitHub | Platform | Status |
|-----|--------|---------|--------|
| consumer-app | [Link](https://github.com/imrejaul007/consumer-app) | React Native | Live |
| admin-app | [Link](https://github.com/imrejaul007/admin-app) | React Native | Live |

---

## Infrastructure

| Component | Technology | Purpose |
|-----------|-----------|---------|
| Database | MongoDB Atlas | Primary data store |
| Cache | Redis Cloud | Sessions, rate limiting |
| Gateway | Kong + Nginx | API gateway |
| CDN | Cloudflare | DDoS, SSL, caching |
| Monitoring | Prometheus + Grafana | Metrics |
| Logging | ELK Stack | Log aggregation |
| CI/CD | GitHub Actions | Deployment |

---

## Service Dependencies

```
Consumer App / Admin App
           |
           v
      API Gateway (Kong)
           |
     +-----+-----+-----+-----+-----+
     v     v     v     v     v     v
   Auth  Order Payment Wallet Catalog Search
     |     |     |       |       |
     +-----+-----+-------+-------+
           |
           v
       Merchant
           |
           v
       Gamification
           |
           v
         Karma
```

---

## Ports (Local Development)

| Service | Port | Local URL | Notes |
|---------|------|-----------|-------|
| rez-api-gateway | 5002 | http://localhost:5002 | Routes to all microservices |
| rez-auth-service | 4002 | http://localhost:4002 | Auth, OTP, JWT |
| rez-merchant-service | 4005 | http://localhost:4005 | Merchant CRUD |
| rez-order-service | 3008 | http://localhost:3008 | Order lifecycle, BullMQ |
| rez-payment-service | 4001 | http://localhost:4001 | Razorpay, refunds |
| rez-wallet-service | 3010 | http://localhost:3010 | Wallet, coins, balance |
| rez-catalog-service | 3005 | http://localhost:3005 | Products, categories |
| rez-search-service | 4003 | http://localhost:4003 | Full-text search |
| rez-gamification-service | 3001 | http://localhost:3001 | BullMQ + HTTP API |
| rez-ads-service | 4007 | http://localhost:4007 | HTTP API |
| rez-marketing-service | 4000 | http://localhost:4000 | BullMQ worker |
| rez-scheduler-service | 3012 | http://localhost:3012 | Cron jobs |
| rez-finance-service | 4005 | http://localhost:4005 | Finance service |
| rez-karma-service | 3009 | http://localhost:3009 | Social impact |
| rez-notification-events | 3005 | http://localhost:3005 | BullMQ worker |
| analytics-events | 3006 | http://localhost:3006 | Event tracking |
| rez-media-events | 3008 | http://localhost:3008 | BullMQ worker |
| rez-intent-graph | 3001/3005 | http://localhost:3001/3005 | AI agents |

### CorpPerks Services
| Service | Port | Local URL | Notes |
|---------|------|-----------|-------|
| rez-corpperks-service | 4013 | http://localhost:4013 | CorpPerks Gateway API |
| rez-hotel-service | 4011 | http://localhost:4011 | Makcorps Hotel Proxy |
| rez-procurement-service | 4012 | http://localhost:4012 | NextaBizz Procurement |

---

## Health Endpoints

| Service | Endpoint |
|---------|----------|
| All | GET /health |
| All | GET /health/ready |
| All | GET /health/live |
| Gateway | GET /healthz |

---

## Monitoring

| Service | Metrics |
|---------|----------|
| All | GET /metrics (Prometheus) |
| All | Sentry for errors |
| All | OpenTelemetry traces |

---

## Last Audit

**Date:** 2026-04-30
**Result:** Phase 0 Documentation complete
- Created comprehensive README.md for all 17 services
- Updated SOURCE-OF-TRUTH files
- Enhanced .env.example files with descriptions
