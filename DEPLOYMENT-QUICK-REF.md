# REZ Platform — Deployment Quick Reference

**Version:** 2.0.0 | **Date:** 2026-05-02

---

## 🚀 DEPLOY IN ORDER

### TIER 1 - CRITICAL (Deploy First)
```
1. Event Platform     → 4008
2. Action Engine      → 4009
3. Feedback Service   → 4010
```

### TIER 2 - INTELLIGENCE
```
4.  User Intelligence       → 3004
5.  Merchant Intelligence   → 4012
6.  Intent Predictor        → 4018
7.  Intelligence Hub        → 4020
```

### TIER 3 - DELIVERY
```
8.  Targeting Engine         → 3003
9.  Recommendation Engine    → 3001
10. Personalization Engine   → 4017
11. Push Service            → 4013
```

### TIER 4 - DASHBOARDS
```
12. Merchant Copilot        → 4022
13. Consumer Copilot        → 4021
14. AdBazaar               → 4025
15. Feature Flags           → 4030
16. Observability           → 4031
```

---

## 📋 DEPLOY COMMANDS

### Render Dashboard
```
https://dashboard.render.com
```

### Clone & Deploy
```bash
# Clone repo
git clone https://github.com/imrejaul007/REPO_NAME.git
cd REPO_NAME

# Install & Start
npm install
npm start
```

---

## 🔧 ENV VARS (All Services)

```bash
NODE_ENV=production
PORT=XXXX
MONGODB_URI=mongodb+srv://...
REDIS_HOST=redis-xxxx.redns.redisdb.com
REDIS_PORT=6379
REDIS_PASSWORD=xxxx
```

### REZ Mind (After Deploy)
```bash
REZ_MIND_URL=https://rez-event-platform.onrender.com
```

---

## 🧪 TEST COMMANDS

```bash
# Health check
curl https://SERVICE.onrender.com/health

# Send test event
curl -X POST https://rez-event-platform.onrender.com/webhook/merchant/order \
  -H "Content-Type: application/json" \
  -d '{"merchant_id":"test","order_id":"123","total_amount":500}'
```

---

## 📊 SERVICE URLs (After Deploy)

| Service | URL |
|---------|-----|
| Event Platform | https://rez-event-platform.onrender.com |
| Action Engine | https://rez-action-engine.onrender.com |
| Feedback Service | https://rez-feedback-service.onrender.com |
| User Intelligence | https://rez-user-intelligence.onrender.com |
| Merchant Intelligence | https://rez-merchant-intelligence.onrender.com |
| Intent Predictor | https://rez-intent-predictor.onrender.com |
| Intelligence Hub | https://rez-intelligence-hub.onrender.com |
| Targeting Engine | https://rez-targeting-engine.onrender.com |
| Recommendation Engine | https://rez-recommendation-engine.onrender.com |
| Personalization Engine | https://rez-personalization-engine.onrender.com |
| Push Service | https://rez-push-service.onrender.com |
| Merchant Copilot | https://rez-merchant-copilot.onrender.com |
| Consumer Copilot | https://rez-consumer-copilot.onrender.com |
| AdBazaar | https://rez-adbazaar.onrender.com |
| Feature Flags | https://rez-feature-flags.onrender.com |
| Observability | https://rez-observability.onrender.com |

---

## ✅ CHECKLIST

```
[ ] Tier 1 deployed (3 services)
[ ] Tier 2 deployed (4 services)
[ ] Tier 3 deployed (4 services)
[ ] Tier 4 deployed (5 services)
[ ] REZ_MIND_URL updated in apps
[ ] Health checks passing
[ ] Test event successful
```

---

## 📁 KEY DOCS

| Doc | Purpose |
|-----|---------|
| [DEPLOYMENT-GUIDE.md](DEPLOYMENT-GUIDE.md) | Full guide |
| [REPOS.md](REPOS.md) | All repos |
| [REZ-MIND-V2.md](REZ-MIND-V2.md) | Vision |
| [CHAT-SUPPORT-STATUS.md](CHAT-SUPPORT-STATUS.md) | Chat status |

---

## 🔢 PORTS REFERENCE

| Port | Service |
|------|---------|
| 3001 | Recommendation Engine |
| 3003 | Targeting Engine |
| 3004 | User Intelligence |
| 4008 | Event Platform |
| 4009 | Action Engine |
| 4010 | Feedback Service |
| 4012 | Merchant Intelligence |
| 4013 | Push Service |
| 4017 | Personalization Engine |
| 4018 | Intent Predictor |
| 4020 | Intelligence Hub |
| 4021 | Consumer Copilot |
| 4022 | Merchant Copilot |
| 4025 | AdBazaar |
| 4030 | Feature Flags |
| 4031 | Observability |

---

**Quick Start:** Deploy Event Platform → Add REZ_MIND_URL to apps → Test
