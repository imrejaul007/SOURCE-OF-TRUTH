# REZ Platform — Source of Truth

**Last Updated:** 2026-05-02

**ReZ Mind** — AI-powered commerce intelligence (separate repo: `rez-intent-graph`)

Single place to find everything about the REZ platform. Read this before solving any issue, building any feature, or debugging anything.

---

## 🚀 Quick Navigation

### Getting Started
| Document | Description |
|----------|-------------|
| [ARCHITECTURE.md](ARCHITECTURE.md) | System architecture overview |
| [SERVICES.md](SERVICES.md) | All microservices catalog |
| [APPS.md](APPS.md) | All applications |
| [PACKAGES.md](PACKAGES.md) | Shared packages |
| [DEPLOYMENT.md](DEPLOYMENT.md) | Deployment guide |
| [CONNECTIVITY.md](CONNECTIVITY.md) | Architecture diagrams |

### Growth Services (NEW 2026-05-02)
| Document | Description |
|----------|-------------|
| [GROWTH-SERVICES-ARCHITECTURE.md](GROWTH-SERVICES-ARCHITECTURE.md) | Ads, Marketing, Notification, Analytics Hub |

### Intelligence Layer
| Document | Description |
|----------|-------------|
| [EVENT-SCHEMAS.md](EVENT-SCHEMAS.md) | Event schemas (inventory.low, order.completed, payment.success) |
| [OPERATIONAL-LAYER.md](OPERATIONAL-LAYER.md) | Event Platform, Action Engine, Feedback Service |

### First Loop Testing
| Document | Description |
|----------|-------------|
| [STRESS-TEST-PLAN.md](STRESS-TEST-PLAN.md) | Comprehensive stress test plan with failure scenarios |
| [LOOP-MONITORING.md](LOOP-MONITORING.md) | Monitoring dashboard and Prometheus metrics |

### Security & Audit
| Document | Description |
|----------|-------------|
| [SECURITY.md](SECURITY.md) | Security hardening guide |
| [MONGODB-AUTH-GUIDE.md](MONGODB-AUTH-GUIDE.md) | MongoDB authentication |
| [REDIS-AUTH-GUIDE.md](REDIS-AUTH-GUIDE.md) | Redis authentication |
| [COMPREHENSIVE-AUDIT-2026-05-01-FULL.md](COMPREHENSIVE-AUDIT-2026-05-01-FULL.md) | Full ecosystem audit |

---

## 🏗️ Architecture (2026-05-01)

### NEW: Complete Loop Architecture

```
Events → Intelligence → Decisions → Actions → Feedback → Repeat
```

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    OPERATIONAL LAYER (NEW)                              │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌─────────────┐    ┌─────────────────┐    ┌─────────────────┐       │
│  │   BizOS     │───►│ Event Platform  │───►│   ReZ Mind     │       │
│  │ (emit)     │    │ (route/validate)│    │ (AI agents)    │       │
│  └─────────────┘    └─────────────────┘    └────────┬────────┘       │
│                                                     │                 │
│  ┌─────────────┐    ┌─────────────────┐    ┌────────▼────────┐       │
│  │ Feedback   │◄───│  Action Engine  │◄───│  Decision      │       │
│  │ Service    │    │  (guardrails)   │    │  Engine        │       │
│  └─────────────┘    └─────────────────┘    └─────────────────┘       │
│                                                     │                 │
│                             ┌─────────────────────────┘                 │
│                             ▼                                         │
│                    ┌─────────────────┐                              │
│                    │   NextaBiZ     │                              │
│                    │ (Procurement)  │                              │
│                    └─────────────────┘                              │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### First Closed Loop: Inventory → Reorder

```
Stock drops below threshold
         ↓
emit inventory.low event
         ↓
Event Platform validates & routes
         ↓
ReZ Mind processes intent
         ↓
Action Engine decides action level
         ↓
Draft PO created in NextaBiZ
         ↓
Merchant approves/rejects
         ↓
Feedback recorded
         ↓
AdaptiveScoringAgent learns
```

---

## 🧠 Intelligence Layer (NEW)

### Components Created (2026-05-01)

| Component | Path | Purpose |
|-----------|------|---------|
| **rez-event-platform** | `../rez-event-platform/` | Central event bus with schema registry |
| **rez-action-engine** | `../rez-action-engine/` | Decision execution with guardrails |
| **rez-feedback-service** | `../rez-feedback-service/` | Learning infrastructure |
| **rez-first-loop** | `../rez-first-loop/` | First closed loop integration |

### Event Schemas

| Event | Schema | Status |
|-------|--------|--------|
| `inventory.low` | [EVENT-SCHEMAS.md](EVENT-SCHEMAS.md) | ✅ Defined |
| `order.completed` | [EVENT-SCHEMAS.md](EVENT-SCHEMAS.md) | ✅ Defined |
| `payment.success` | [EVENT-SCHEMAS.md](EVENT-SCHEMAS.md) | ✅ Defined |

---

## 🧪 First Loop Testing (NEW)

### Stress Test Plan

Run comprehensive tests on the first loop:

| Test | Purpose | Target |
|------|---------|--------|
| Event Platform Failure | System recovery | 100% recovery |
| Duplicate Events | Idempotency | 0 duplicates |
| ReZ Mind Timeout | Fallback handling | < 5s |
| Action Engine Failure | Retry logic | 100% recovery |
| NextaBiZ Unavailable | Graceful degradation | Pending status |
| Rapid Fire Events | Coalescing | < 5 actions |
| Feedback Missing | Implicit capture | > 90% |

### Run Tests

```bash
cd rez-first-loop
npm run test:stress
```

### Loop Reliability Score

```
Target: > 99% before scaling
Warning: < 95%
Critical: < 90%
```

Components:
- Event Delivery (20%)
- Idempotency (20%)
- Action Success (25%)
- Feedback Capture (20%)
- Learning Loop (15%)

### Monitoring

- **Dashboard:** `http://localhost:3000/d/first-loop-monitor`
- **Metrics:** Prometheus queries in [LOOP-MONITORING.md](LOOP-MONITORING.md)

---

## 🔒 Security (Updated 2026-05-01)

### ✅ Fixed
- [x] Rate limiting on all services
- [x] Fail-fast startup (env vars required)
- [x] RBAC middleware implemented
- [x] CORS explicit domains
- [x] Security headers

### ⚠️ In Progress
- [ ] MongoDB AUTH - Guide created, deployment pending
- [ ] Redis AUTH - Guide created, deployment pending
- [ ] Credentials rotation - Need to execute

### 📋 Security Guides
| Document | Description |
|----------|-------------|
| [SECURITY.md](SECURITY.md) | Complete security hardening guide |
| [MONGODB-AUTH-GUIDE.md](MONGODB-AUTH-GUIDE.md) | MongoDB auth setup |
| [REDIS-AUTH-GUIDE.md](REDIS-AUTH-GUIDE.md) | Redis auth setup |

---

## 📊 Services (Updated)

| Service | Port | Git | Status |
|---------|------|-----|--------|
| **NEW: rez-event-platform** | 4008 | TBD | Ready |
| **NEW: rez-action-engine** | 4009 | TBD | Ready |
| **NEW: rez-feedback-service** | 4010 | TBD | Ready |

---

## 🔗 Quick Links

### Core Services
| Service | GitHub | Deploy |
|---------|--------|--------|
| rez-auth-service | imrejaul007/rez-auth-service | Render |
| rez-wallet-service | imrejaul007/rez-wallet-service | Render |
| rez-order-service | imrejaul007/rez-order-service | Render |
| rez-payment-service | imrejaul007/rez-payment-service | Render |
| rez-merchant-service | imrejaul007/rez-merchant-service | Render |
| rez-api-gateway | imrejaul007/rez-api-gateway | Render |

### NEW: Intelligence Services
| Service | Local Path | Purpose |
|---------|------------|---------|
| rez-event-platform | `../rez-event-platform/` | Central event bus |
| rez-action-engine | `../rez-action-engine/` | Action execution |
| rez-feedback-service | `../rez-feedback-service/` | Learning feedback |
| rez-first-loop | `../rez-first-loop/` | First loop integration |

---

## 📱 Apps

| App | GitHub | Platform |
|-----|--------|----------|
| rez-app-consumer | imrejaul007/rez-app-consumer | Expo/React Native |
| rez-app-marchant | imrejaul007/rez-app-marchant | Expo/React Native |
| rez-app-admin | imrejaul007/rez-app-admin | Expo/React Native |
| rez-now | imrejaul007/rez-now | Next.js |
| Rendez | imrejaul007/Rendez | React Native |
| Hotel OTA | imrejaul007/hotel-ota | Node.js, Next.js |

---

## 📝 Key Rules

1. **NEVER commit secrets** — use placeholder names only
2. **Local dev** — use ports from LOCAL-PORTS.md
3. **Cross-service** — use `*_SERVICE_URL` env vars
4. **Types** — import from `rez-shared` or local `types/`
5. **Auth** — use `x-internal-token` for service-to-service
6. **Logging** — use structured JSON format
7. **Events** — emit via rez-event-platform with schema validation

---

## 🚀 Deployment Order

### Week 1: Security
```bash
# Enable MongoDB AUTH
docker compose up -d mongodb
# See MONGODB-AUTH-GUIDE.md

# Enable Redis AUTH
docker compose up -d redis
# See REDIS-AUTH-GUIDE.md
```

### Week 1-2: Event Platform
```bash
# Deploy Event Platform
cd rez-event-platform
npm install && npm run build
npm start

# Deploy Action Engine
cd ../rez-action-engine
npm install && npm run build
npm start

# Deploy Feedback Service
cd ../rez-feedback-service
npm install && npm run build
npm start
```

### Week 2-4: First Loop
```bash
# Integrate with BizOS
cd rez-merchant-service/src/events
# See inventory.events.ts

# Test the loop
cd ../rez-first-loop
npm test
```

---

## Contributing

1. Check this folder before starting any work
2. Document all changes here
3. Security issues → responsible disclosure
4. Deployment changes → PR review required
5. New events → Update EVENT-SCHEMAS.md

---

**Last Major Update:** 2026-05-01
- Added Event Platform, Action Engine, Feedback Service
- Added First Closed Loop integration
- Enabled MongoDB/Redis AUTH guides
