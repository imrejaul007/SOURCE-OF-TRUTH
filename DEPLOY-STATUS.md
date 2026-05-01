# REZ Platform — Deployment Status
**Last Updated:** 2026-04-30

## REZ Ecosystem Services

### Backend Services

| Service | GitHub | Status |
|---------|--------|--------|
| rez-auth-service | [Link](https://github.com/imrejaul007/rez-auth-service) | ✅ Deployed |
| rez-merchant-service | [Link](https://github.com/imrejaul007/rez-merchant-service) | ✅ Deployed |
| rez-order-service | [Link](https://github.com/imrejaul007/rez-order-service) | ✅ Deployed |
| rez-payment-service | [Link](https://github.com/imrejaul007/rez-payment-service) | ✅ Deployed |
| rez-wallet-service | [Link](https://github.com/imrejaul007/rez-wallet-service) | ✅ Deployed |
| rez-catalog-service | [Link](https://github.com/imrejaul007/rez-catalog-service) | ✅ Deployed |
| rez-gamification-service | [Link](https://github.com/imrejaul007/rez-gamification-service) | ✅ Deployed |
| rez-notification-events | [Link](https://github.com/imrejaul007/rez-notification-events) | ✅ Deployed |
| analytics-events | [Link](https://github.com/imrejaul007/analytics-events) | ✅ Deployed |
| rez-api-gateway | [Link](https://github.com/imrejaul007/rez-api-gateway) | ✅ Deployed |

### Mobile Apps

| App | GitHub | Platform | Status |
|-----|--------|---------|--------|
| consumer-app | [Link](https://github.com/imrejaul007/consumer-app) | React Native | ✅ Live |
| admin-app | [Link](https://github.com/imrejaul007/admin-app) | React Native | ✅ Live |

---

## Deploy URLs

### API Gateway
- **Production:** https://rez-api-gateway.onrender.com

### Services
| Service | Production URL |
|---------|---------------|
| Auth | https://rez-auth-service.onrender.com |
| Merchant | https://rez-merchant-service.onrender.com |
| Order | https://rez-order-service.onrender.com |
| Payment | https://rez-payment-service.onrender.com |
| Wallet | https://rez-wallet-service.onrender.com |

---

## Security Status

| Check | Status |
|-------|--------|
| Rate Limiting | ✅ All services |
| Fail-fast startup | ✅ All services |
| RBAC | ✅ Merchant service |
| CORS explicit domains | ✅ Gateway |
| Security headers | ✅ Order service |
| MongoDB AUTH | ⏳ Pending |
| Redis AUTH | ⏳ Pending |

---

## Performance Status

| Optimization | Status |
|-------------|--------|
| Gzip compression | ✅ All services |
| Cursor pagination | ✅ Orders |
| Database indexes | ✅ Migration ready |
| Prometheus metrics | ✅ All services |
| Prometheus alerts | ✅ Defined |
| ELK stack | ⏳ Pending |

---

## CorpPerks - Enterprise Benefits Platform

**GitHub:** [CorpPerks](https://github.com/imrejaul007/CorpPerks)

### Services (Ready to Deploy)

| Service | Port | Status |
|---------|------|--------|
| rez-corpperks-service | 4013 | Ready |
| rez-hotel-service | 4015 | Ready |
| rez-procurement-service | 4012 | Ready |

### Deploy
```bash
git clone https://github.com/imrejaul007/CorpPerks.git
cd CorpPerks
docker-compose up -d
```

### Features
- Corporate Gifting
- Corporate Hotel Booking
- Corporate Procurement
- Dual Wallet System
- Benefits Configuration
- GST Invoicing
- HRIS Integration
- Analytics Dashboard

---

## Quick Links

- [Render Dashboard](https://dashboard.render.com)
- [MongoDB Atlas](https://cloud.mongodb.com)
- [GitHub Organization](https://github.com/imrejaul007)
- [CorpPerks](https://github.com/imrejaul007/CorpPerks)
