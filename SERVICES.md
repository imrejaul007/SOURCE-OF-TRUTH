# REZ Services Catalog
**Last Updated:** 2026-04-30

---

## Overview

The REZ ecosystem consists of 8 backend microservices + 3 mobile apps + 1 gateway.

---

## Backend Services

### Core Services

| Service | GitHub | Render | Port | Description |
|---------|--------|--------|------|-------------|
| rez-auth-service | [Link](https://github.com/imrejaul007/rez-auth-service) | [Link](https://rez-auth-service.onrender.com) | 4002 | Authentication, OAuth, MFA |
| rez-merchant-service | [Link](https://github.com/imrejaul007/rez-merchant-service) | [Link](https://rez-merchant-service.onrender.com) | 4005 | Merchant management, team, products |
| rez-order-service | [Link](https://github.com/imrejaul007/rez-order-service) | [Link](https://rez-order-service.onrender.com) | 4005 | Order processing, state machine |
| rez-payment-service | [Link](https://github.com/imrejaul007/rez-payment-service) | [Link](https://rez-payment-service.onrender.com) | 4001 | Payment processing, Razorpay |
| rez-wallet-service | [Link](https://github.com/imrejaul007/rez-wallet-service) | [Link](https://rez-wallet-service.onrender.com) | 4004 | Wallet, BNPL, credit |
| rez-catalog-service | [Link](https://github.com/imrejaul007/rez-catalog-service) | N/A | 4007 | Product catalog, search |
| rez-gamification-service | [Link](https://github.com/imrejaul007/rez-gamification-service) | N/A | 3004 | Points, streaks, achievements |
| rez-notification-events | [Link](https://github.com/imrejaul007/rez-notification-events) | N/A | 3005 | Push notifications, email |
| analytics-events | [Link](https://github.com/imrejaul007/analytics-events) | N/A | 3006 | Analytics pipeline |
| rez-api-gateway | [Link](https://github.com/imrejaul007/rez-api-gateway) | N/A | N/A | Kong + Nginx gateway |

### Supporting Services

| Service | GitHub | Description |
|---------|--------|-------------|
| rez-intent-graph | [Link](https://github.com/imrejaul007/rez-intent-graph) | AI/ML intent capture |
| rez-shared | [Link](https://github.com/imrejaul007/shared-types) | Shared types and utilities |
| rez-client | N/A | Internal HTTP client SDK |

---

## Mobile Apps

| App | GitHub | Platform | Status |
|-----|----|---------|--------|
| consumer-app | [Link](https://github.com/imrejaul007/consumer-app) | React Native | ✅ Live |
| admin-app | [Link](https://github.com/imrejaul007/admin-app) | React Native | ✅ Live |

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
       ↓
   API Gateway (Kong)
       ↓
┌──────┼──────┐
↓      ↓      ↓
Auth  Order  Payment → Wallet
       ↓
    Merchant
       ↓
    Catalog
       ↓
   Gamification
```

---

## Ports (Local Development)

| Service | Port |
|---------|------|
| rez-auth-service | 4002 |
| rez-merchant-service | 4005 |
| rez-order-service | 4005 |
| rez-payment-service | 4001 |
| rez-wallet-service | 4004 |
| rez-catalog-service | 4007 |
| rez-gamification-service | 3004 |
| rez-notification-events | 3005 |
| analytics-events | 3006 |

---

## Environment Variables

### Required for All Services
```env
NODE_ENV=production
PORT=<service-port>
MONGODB_URI=mongodb+srv://...
REDIS_URL=rediss://...
SENTRY_DSN=https://...
```

### Service-Specific
```env
# Auth
JWT_SECRET=<64-char-hex>
OTP_TOTP_ENCRYPTION_KEY=<32-char-hex>

# Payment
RAZORPAY_KEY_ID=rzp_...
RAZORPAY_KEY_SECRET=...
RAZORPAY_WEBHOOK_SECRET=...

# Internal
INTERNAL_SERVICE_TOKENS_JSON=[{"serviceId":"order-service","token":"..."}]
```

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
|---------|---------|
| All | GET /metrics (Prometheus) |
| All | Sentry for errors |
| All | OpenTelemetry traces |

---

## Last Audit

**Date:** 2026-04-30
**Result:** 84/84 issues resolved
**Report:** MASTER-AUDIT-2026.md
