# REZ Platform — Source of Truth

**Last Updated:** 2026-04-30

Single place to find everything about the REZ platform. Read this before solving any issue, building any feature, or debugging anything.

---

## 🚀 Quick Navigation

### Getting Started
| Document | Description |
|----------|-------------|
| [ARCHITECTURE.md](ARCHITECTURE.md) | System architecture overview |
| [DEPLOY-STATUS.md](DEPLOY-STATUS.md) | Live deployment URLs and status |
| [ENV-VARS.md](ENV-VARS.md) | All environment variables |
| [LOCAL-PORTS.md](LOCAL-PORTS.md) | Local development ports |

### Services
| Document | Description |
|----------|-------------|
| [SERVICES.md](SERVICES.md) | All microservices catalog |
| [API-ENDPOINTS.md](API-ENDPOINTS.md) | API endpoints reference |
| [REPOS.md](REPOS.md) | All 20+ repositories |

### Security & Audit
| Document | Description |
|----------|-------------|
| [MASTER-AUDIT-2026.md](MASTER-AUDIT-2026.md) | **Start here** - Complete audit (84/84 fixed) |
| [SECURITY-HARDENING-PLAN.md](SECURITY-HARDENING-PLAN.md) | Security roadmap |
| [OPS-003-NO-API-GATEWAY.md](OPS-003-NO-API-GATEWAY.md) | API Gateway fixes |
| [REDIS-AUTH-GUIDE.md](REDIS-AUTH-GUIDE.md) | Redis authentication |
| [MONGODB-AUTH-GUIDE.md](MONGODB-AUTH-GUIDE.md) | MongoDB authentication |

### Performance & Observability
| Document | Description |
|----------|-------------|
| [PERFORMANCE-OPTIMIZATION-PLAN.md](PERFORMANCE-OPTIMIZATION-PLAN.md) | Performance roadmap |
| [OBSERVABILITY-PLAN.md](OBSERVABILITY-PLAN.md) | Logging, metrics, tracing |
| [ELK-DEPLOYMENT-GUIDE.md](ELK-DEPLOYMENT-GUIDE.md) | ELK stack deployment |
| [prometheus-alerts.yml](prometheus-alerts.yml) | Prometheus alert rules |

---

## 📊 Audit Summary

**All 84 issues resolved across 7 audit waves.**

| Wave | Date | Issues | Status |
|------|------|--------|--------|
| Wave 8 | Apr 29 | OPS-003: Rate limiting, auth | ✅ Fixed |
| Wave 9 | Apr 29 | 84 critical/high/medium/low | ✅ Fixed |
| Wave 10 | Apr 30 | OAuth2, RBAC | ✅ Fixed |
| Wave 11 | Apr 30 | Fail-fast startup | ✅ Fixed |
| Wave 12 | Apr 30 | Gateway CORS, eval fix | ✅ Fixed |
| Wave 13 | Apr 30 | Frontend security | ✅ Fixed |
| Wave 14 | Apr 30 | Compression, pagination | ✅ Fixed |

---

## 🏗️ Architecture

### Services
```
API Gateway (Kong + Nginx)
├── /api/auth/*        → rez-auth-service
├── /api/merchant/*   → rez-merchant-service
├── /api/orders/*     → rez-order-service
├── /api/payments/*   → rez-payment-service
├── /api/wallet/*     → rez-wallet-service
├── /api/catalog/*    → rez-catalog-service
├── /api/gamification → rez-gamification-service
└── /api/*           → rez-backend (monolith)
```

### Data Flow
```
Client → Cloudflare → Kong Gateway → Services → MongoDB/Redis
                              ↓
                        intent-graph (RTMN)
```

---

## 🔗 Quick Links

| Service | GitHub | Deploy |
|---------|--------|---------|
| rez-auth-service | [Link](https://github.com/imrejaul007/rez-auth-service) | [Render](https://rez-auth-service.onrender.com) |
| rez-merchant-service | [Link](https://github.com/imrejaul007/rez-merchant-service) | [Render](https://rez-merchant-service.onrender.com) |
| rez-order-service | [Link](https://github.com/imrejaul007/rez-order-service) | [Render](https://rez-order-service.onrender.com) |
| rez-payment-service | [Link](https://github.com/imrejaul007/rez-payment-service) | [Render](https://rez-payment-service.onrender.com) |
| rez-wallet-service | [Link](https://github.com/imrejaul007/rez-wallet-service) | [Render](https://rez-wallet-service.onrender.com) |
| rez-api-gateway | [Link](https://github.com/imrejaul007/rez-api-gateway) | [Render](https://rez-api-gateway.onrender.com) |

---

## 📱 Apps

| App | GitHub | Platform |
|-----|--------|----------|
| consumer-app | [Link](https://github.com/imrejaul007/consumer-app) | Expo/React Native |
| admin-app | [Link](https://github.com/imrejaul007/admin-app) | Expo/React Native |
| vesper-app | [Link](https://github.com/imrejaul007/vesper) | Expo/React Native |

---

## 🔒 Security Checklist

- [x] Rate limiting on all services
- [x] Fail-fast startup (env vars required)
- [x] RBAC middleware implemented
- [x] CORS explicit domains
- [x] Security headers
- [ ] MongoDB AUTH enabled
- [ ] Redis AUTH enabled
- [ ] Credentials rotated
- [ ] ELK deployed

---

## ⚡ Performance Checklist

- [x] Gzip compression (all services)
- [x] Cursor pagination (orders)
- [x] Database indexes (migration ready)
- [x] Security headers
- [x] Prometheus metrics
- [ ] ELK deployed
- [ ] Response caching optimization

---

## 📝 Key Rules

1. **NEVER commit secrets** — use placeholder names only
2. **Local dev** — use ports from LOCAL-PORTS.md
3. **Cross-service** — use `*_SERVICE_URL` env vars
4. **Types** — import from `rez-shared` or local `types/`
5. **Auth** — use `x-internal-token` for service-to-service
6. **Logging** — use structured JSON format

---

## 🐛 Bug Tracking

See `docs/Gaps/` for detailed issue tracking:
- `10-REZ-NOW/` - ReZ Now issues (13 fixed, 1 partial)
- `09-CROSS-SERVICE-2026/` - Cross-service inconsistencies
- `11-CROSS-SERVICE-CONNECTIONS/` - Connection issues

---

## Contributing

1. Check this folder before starting any work
2. Document all changes here
3. Security issues → responsible disclosure
4. Deployment changes → PR review required
