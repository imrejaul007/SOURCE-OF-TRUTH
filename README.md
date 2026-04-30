# REZ Platform — Source of Truth

**Last Updated:** 2026-04-30

**ReZ Mind** — AI-powered commerce intelligence (separate repo: `rez-intent-graph`)

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
| [ALL-FEATURES.md](ALL-FEATURES.md) | Complete feature list |

### Implementation
| Document | Description |
|----------|-------------|
| [IMPLEMENTATION-PLAN.md](IMPLEMENTATION-PLAN.md) | **START HERE** - Full roadmap based on consultant + audit |
| [INDEX.md](INDEX.md) | Complete file map |

### Services
| Document | Description |
|----------|-------------|
| [SERVICES.md](SERVICES.md) | All microservices catalog |
| [API-ENDPOINTS.md](API-ENDPOINTS.md) | API endpoints reference |
| [API-DOCUMENTATION.md](API-DOCUMENTATION.md) | API documentation |
| [REPOS.md](REPOS.md) | All 20+ repositories |

### Apps & Integration
| Document | Description |
|----------|-------------|
| [APP-INTEGRATION-GUIDE.md](APP-INTEGRATION-GUIDE.md) | Consumer/admin app integration |
| [AGENT-SWARM-API.md](AGENT-SWARM-API.md) | Agent swarm API |
| [BUSINESS-MODEL.md](BUSINESS-MODEL.md) | Business model and revenue |

### Security & Audit
| Document | Description |
|----------|-------------|
| [MASTER-AUDIT-2026.md](MASTER-AUDIT-2026.md) | **Start here** - Complete audit (84/84 fixed) |
| [AUDIT-WAVE-9-COMPLETE.md](AUDIT-WAVE-9-COMPLETE.md) | Wave 9 audit |
| [AUDIT-WAVE-10.md](AUDIT-WAVE-10.md) | Wave 10 audit |
| [AUDIT-WAVE-11-COMPLETE.md](AUDIT-WAVE-11-COMPLETE.md) | Wave 11 audit |
| [AUDIT-WAVE-12-COMPLETE.md](AUDIT-WAVE-12-COMPLETE.md) | Wave 12 audit |
| [AUDIT-WAVE-13-COMPLETE.md](AUDIT-WAVE-13-COMPLETE.md) | Wave 13 audit |
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

**New audit (2026-04-30):** 87 issues found across 21 apps, 17 services, 13 packages

| Category | Critical | High | Medium | Low | Total |
|----------|---------|------|--------|-----|-------|
| Issues | 8 | 15 | 32 | 32 | **87** |

**Previous audit:** 84/84 issues fixed (Waves 8-14)

See [COMPREHENSIVE-AUDIT-2026-04-30.md](COMPREHENSIVE-AUDIT-2026-04-30.md) for details.

### Critical Issues to Fix First
1. Git conflict markers in 3 services
2. Wrong package name in rez-scheduler-service
3. MongoDB/Redis AUTH not enabled

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

### Data Flow (Current → Target)

**Current State:**
```
API → API → API (loops incomplete)
```

**Target State:**
```
User Action → Event Bus → Services → ReZ Mind → AI Agents → Insights → Copilot
                     ↓
              Analytics / Notifications / Finance
```

See [IMPLEMENTATION-PLAN.md](IMPLEMENTATION-PLAN.md) for the 5 closed loops:
1. Consumer → Merchant
2. Merchant → Operations (BizOS)
3. Procurement (NextaBiZ)
4. Hotel (StayOwn)
5. Growth (AdBazaar)

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
| rez-app-consumer | [Link](https://github.com/imrejaul007/rez-app-consumer) | Expo/React Native |
| rez-app-marchant | [Link](https://github.com/imrejaul007/rez-app-marchant) | Expo/React Native |
| rez-app-admin | [Link](https://github.com/imrejaul007/rez-app-admin) | Expo/React Native |
| rez-now | [Link](https://github.com/imrejaul007/rez-now) | Next.js |
| rez-web-menu | [Link](https://github.com/imrejaul007/rez-web-menu) | Next.js |
| Rendez | [Link](https://github.com/imrejaul007/Rendez) | React Native |
| Hotel OTA (StayOwn) | [Link](https://github.com/imrejaul007/hotel-ota) | Node.js, Next.js |

---

## 📱 Hotel Stack — StayOwn

| App | Purpose |
|-----|---------|
| ota-web | Customer booking website |
| mobile | StayOwn Mobile (iOS/Android) |
| admin | Admin Dashboard |
| hotel-panel | Hotel staff management |
| corporate-panel | Corporate account management |
| api | Backend API (includes Room QR) |
| hotel-pms | Property Management System |

### Room QR
- **Location:** `Hotel OTA/apps/api/src/routes/room-qr.routes.ts`
- **Purpose:** Guest services when scanning room QR code

---

## 🔒 Security Checklist

- [x] Rate limiting on all services
- [x] Fail-fast startup (env vars required)
- [x] RBAC middleware implemented
- [x] CORS explicit domains
- [x] Security headers
- [ ] MongoDB AUTH enabled ❌
- [ ] Redis AUTH enabled ❌
- [ ] Credentials rotated ❌
- [ ] ELK deployed ❌

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
