# REZ Ecosystem Index
**Last Updated:** 2026-04-30

## Complete File Map

### 📚 Documentation

| Category | Files |
|----------|-------|
| **Start Here** | README.md, ARCHITECTURE.md, SERVICES.md |
| **Security** | MASTER-AUDIT-2026.md, SECURITY-HARDENING-PLAN.md, OPS-003-NO-API-GATEWAY.md |
| **Performance** | PERFORMANCE-OPTIMIZATION-PLAN.md, OBSERVABILITY-PLAN.md |
| **Deployment** | ELK-DEPLOYMENT-GUIDE.md, MONGODB-AUTH-GUIDE.md, REDIS-AUTH-GUIDE.md |

### 🔒 Security

| Document | Contents |
|----------|----------|
| MASTER-AUDIT-2026.md | 84 issues across 14 services, all fixed |
| SECURITY-HARDENING-PLAN.md | Credentials rotation, MongoDB auth, Redis auth, mTLS |
| OPS-003-NO-API-GATEWAY.md | API Gateway fixes |
| AUDIT-WAVE-*.md | Detailed fix logs |

### ⚡ Performance

| Document | Contents |
|----------|----------|
| PERFORMANCE-OPTIMIZATION-PLAN.md | Cursor pagination, indexes, caching |
| OBSERVABILITY-PLAN.md | ELK, Prometheus, alerting |
| prometheus-alerts.yml | Alert rules for all services |
| ELK-DEPLOYMENT-GUIDE.md | How to deploy ELK stack |

### 🚀 Deployment

| Document | Contents |
|----------|----------|
| DEPLOY-STATUS.md | Live deployment URLs |
| SERVICES.md | Service catalog with links |
| REPOS.md | All 20+ repositories |
| ENV-VARS.md | Environment variables reference |

### 📱 Apps

| Document | Contents |
|----------|----------|
| consumer-app | Restaurant ordering app |
| admin-app | Merchant admin dashboard |
| vesper-app | Dating app |

---

## Quick Reference

### Service URLs
```
API Gateway:  https://rez-api-gateway.onrender.com
Auth:         https://rez-auth-service.onrender.com
Merchant:     https://rez-merchant-service.onrender.com
Order:        https://rez-order-service.onrender.com
Payment:      https://rez-payment-service.onrender.com
Wallet:       https://rez-wallet-service.onrender.com
```

### GitHub Repos
```
https://github.com/imrejaul007/rez-auth-service
https://github.com/imrejaul007/rez-merchant-service
https://github.com/imrejaul007/rez-order-service
https://github.com/imrejaul007/rez-payment-service
https://github.com/imrejaul007/rez-wallet-service
https://github.com/imrejaul007/rez-api-gateway
https://github.com/imrejaul007/consumer-app
https://github.com/imrejaul007/admin-app
https://github.com/imrejaul007/vesper
```

### Local Ports
```
Auth:        4002
Merchant:    4005
Order:       4005
Payment:     4001
Wallet:      4004
Catalog:     4007
Gamification: 3004
Notification: 3005
Analytics:    3006
```

---

## Issue Status

| Category | Total | Fixed | Pending |
|----------|-------|-------|---------|
| Critical | 19 | 19 | 0 |
| High | 15 | 15 | 0 |
| Medium | 30 | 30 | 0 |
| Low | 20 | 20 | 0 |
| **TOTAL** | **84** | **84** | **0** |

---

## Next Steps

1. ✅ All code changes committed
2. ⏳ Rotate exposed credentials (manual)
3. ⏳ Enable MongoDB AUTH (manual)
4. ⏳ Enable Redis AUTH (manual)
5. ⏳ Deploy ELK stack (manual)

See SECURITY-HARDENING-PLAN.md for details.
