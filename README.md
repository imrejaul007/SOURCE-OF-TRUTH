# REZ Platform — Source of Truth

**Last Updated:** 2026-05-02
**Version:** 3.0.0

---

```
╔═══════════════════════════════════════════════════════════════════════════════╗
║                                                                             ║
║         REZ PLATFORM - OPERATING SYSTEM FOR LOCAL COMMERCE                  ║
║                                                                             ║
║                    Events → Intelligence → Decisions → Growth                ║
║                                                                             ║
╚═══════════════════════════════════════════════════════════════════════════════╝
```

---

## 🚀 QUICK START (For Developer)

### Step 1: Deploy REZ Mind (Priority)

**Deploy these 3 services FIRST:**

| # | Service | GitHub | Port |
|---|---------|--------|------|
| 1 | Event Platform | [imrejaul007/rez-event-platform](https://github.com/imrejaul007/rez-event-platform) | 4008 |
| 2 | Action Engine | [imrejaul007/rez-action-engine](https://github.com/imrejaul007/rez-action-engine) | 4009 |
| 3 | Feedback Service | [imrejaul007/rez-feedback-service](https://github.com/imrejaul007/rez-feedback-service) | 4010 |
| 4 | First Loop | [imrejaul007/rez-first-loop](https://github.com/imrejaul007/rez-first-loop) | Worker |

**How to Deploy:**
```
1. Go to: https://dashboard.render.com
2. New → Web Service
3. Connect GitHub repo
4. Use settings from DEPLOYMENT-GUIDE.md
5. Add MONGODB_URI env var
```

### Step 2: Update App Env Vars

After Event Platform is live:
```bash
REZ_MIND_URL=https://rez-event-platform.onrender.com
EXPO_PUBLIC_REZ_MIND_URL=https://rez-event-platform.onrender.com
NEXT_PUBLIC_REZ_MIND_URL=https://rez-event-platform.onrender.com
```

### Step 3: Test

```bash
curl https://rez-event-platform.onrender.com/health
```

---

## 📁 DOCUMENTATION STRUCTURE

### For Deployment
| Document | Purpose |
|----------|---------|
| [DEPLOYMENT-GUIDE.md](DEPLOYMENT-GUIDE.md) | **Complete deployment guide** |
| [DEPLOYMENT-QUICK-REF.md](DEPLOYMENT-QUICK-REF.md) | **Quick deploy card** |
| [DEPLOY-FIX-REPORT-2026-05-02.md](DEPLOY-FIX-REPORT-2026-05-02.md) | **Deploy fix log** — all fixes, new services, build errors resolved |
| [BUILD-STATUS.md](BUILD-STATUS.md) | **Build status** — per-service build/deploy status |
| [FIXED-ISSUES.md](FIXED-ISSUES.md) | **Fix log** — all issues and resolutions |
| [REPOS.md](REPOS.md) | All repos with links |

### For Architecture
| Document | Purpose |
|----------|---------|
| [ARCHITECTURE.md](ARCHITECTURE.md) | System architecture |
| [REZ-MIND-V2.md](REZ-MIND-V2.md) | REZ Mind intelligence layer |
| [GROWTH-SERVICES.md](GROWTH-SERVICES.md) | Ads, marketing, analytics |

### For Development
| Document | Purpose |
|----------|---------|
| [API-ENDPOINTS.md](API-ENDPOINTS.md) | All API endpoints |
| [INTEGRATION-GUIDE.md](INTEGRATION-GUIDE.md) | How to integrate apps |
| [EVENT-SCHEMAS.md](EVENT-SCHEMAS.md) | Event schemas |

---

## 🧠 REZ MIND (Intelligence Layer)

**Refined Vision:** Behavioral Signal Engine - not "knows everything"

```
Events → Signal Processing → Intelligence → Decisions → Feedback → Learning
```

### Services (Deploy Order)
| Tier | Service | Port | Purpose |
|------|---------|------|---------|
| **CRITICAL** | Event Platform | 4008 | Event ingestion hub |
| **CRITICAL** | Action Engine | 4009 | Decision engine |
| **CRITICAL** | Feedback Service | 4010 | Learning loop |
| **Intelligence** | User Intelligence | 3004 | User profiles |
| **Intelligence** | Merchant Intelligence | 4012 | Merchant profiles |
| **Intelligence** | Intent Predictor | 4018 | Intent prediction |
| **Intelligence** | Intelligence Hub | 4020 | Unified profiles |
| **Delivery** | Targeting Engine | 3003 | Campaign targeting |
| **Delivery** | Recommendation Engine | 3001 | Product recommendations |
| **Delivery** | Personalization Engine | 4017 | Content ranking |
| **Delivery** | Push Service | 4013 | Notifications |
| **Dashboards** | Merchant Copilot | 4022 | Merchant dashboard |
| **Dashboards** | Consumer Copilot | 4021 | Consumer dashboard |
| **Dashboards** | AdBazaar | 4025 | Intent-based ads |
| **Dashboards** | Feature Flags | 4030 | Feature toggles |
| **Dashboards** | Observability | 4031 | Logs & traces |

**All services have render.yaml** - Ready for one-click deploy.

---

## 📱 APPS

### Consumer Apps
| App | REZ Mind | GitHub |
|-----|----------|--------|
| rez-app-consumer | ✅ | [Link](https://github.com/imrejaul007/rez-app-consumer) |
| rez-now | ✅ | [Link](https://github.com/imrejaul007/rez-now) |
| rendez | ✅ | [Link](https://github.com/imrejaul007/Rendez) |
| rez-karma-app | 🔄 | - |

### Merchant Apps
| App | REZ Mind | GitHub |
|-----|----------|--------|
| rez-app-merchant | ✅ | [Link](https://github.com/imrejaul007/rez-app-marchant) |
| rez-restopapa | 🔄 | - |
| rez-pms-app | 🔄 | - |

### Admin
| App | GitHub |
|-----|--------|
| rez-app-admin | [Link](https://github.com/imrejaul007/rez-app-admin) |

---

## 🔧 CORE BACKEND SERVICES

| Service | GitHub | Status |
|---------|--------|--------|
| rez-api-gateway | [Link](https://github.com/imrejaul007/rez-api-gateway) | Active |
| rez-auth-service | [Link](https://github.com/imrejaul007/rez-auth-service) | Active |
| rez-order-service | [Link](https://github.com/imrejaul007/rez-order-service) | Active |
| rez-payment-service | [Link](https://github.com/imrejaul007/rez-payment-service) | Active |
| rez-search-service | [Link](https://github.com/imrejaul007/rez-search-service) | Active |
| rez-wallet-service | [Link](https://github.com/imrejaul007/rez-wallet-service) | Active |
| rez-catalog-service | [Link](https://github.com/imrejaul007/rez-catalog-service) | Active |
| rez-merchant-service | [Link](https://github.com/imrejaul007/rez-merchant-service) | Active |
| rez-gamification-service | [Link](https://github.com/imrejaul007/rez-gamification-service) | Active |

---

## 📊 CHAT & SUPPORT

| Component | Status | REZ Mind Ready |
|-----------|--------|----------------|
| Rendez messaging | ✅ | ❌ |
| Admin support tickets | ✅ | ❌ |
| Merchant chat | ✅ | ❌ |
| Consumer chat | ✅ | ❌ |
| Support Copilot | ❌ | N/A |

**See:** [CHAT-SUPPORT-STATUS.md](CHAT-SUPPORT-STATUS.md)

---

## 🔒 SECURITY

| Item | Status |
|------|--------|
| Rate limiting | ✅ |
| RBAC middleware | ✅ |
| CORS explicit domains | ✅ |
| Security headers | ✅ |
| MongoDB AUTH | ✅ Config ready |
| Redis AUTH | ✅ Config ready |

**See:** [SECURITY.md](SECURITY.md)

---

## 📈 LAUNCH PHASES

| Phase | Features | Safety |
|-------|----------|--------|
| **Phase 1: Internal** | Merchant Copilot ON, Learning OFF | Maximum |
| **Phase 2: Controlled** | 5-20 merchants, safe mode | High |
| **Phase 3: Progressive** | Learning ON, Full Personalization | Medium |

---

## 🎯 CONSULTANT REFINEMENTS

Key correction:
- ❌ "ReZ Mind knows everything"
- ✅ "ReZ Mind continuously learns patterns and predicts intent"

**See:** [REZ-MIND-V2.md](REZ-MIND-V2.md)

---

## ⚡ QUICK COMMANDS

```bash
# Check feature flags
curl https://rez-event-platform.onrender.com/flags

# Send test event
curl -X POST https://rez-event-platform.onrender.com/webhook/merchant/order \
  -H "Content-Type: application/json" \
  -d '{"merchant_id":"test","order_id":"123","total_amount":500}'
```

---

## 📞 NEED HELP?

1. Read DEPLOYMENT-GUIDE.md for step-by-step
2. Check REPOS.md for all repo links
3. See INTEGRATION-GUIDE.md for app integration

---

**Last Updated:** 2026-05-02
**Maintained by:** REZ Team
