# REZ Platform — Deployment Status
**Last Updated:** 2026-05-01 (Gen 68: Marketing services unified - AdBazaar connected to rez-ads-service)

## REZ Ecosystem Services

### Marketing Services

| Service | Port | Purpose | AdBazaar |
|---------|------|---------|-----------|
| [rez-ads-service](https://github.com/imrejaul007/rez-ads-service) | 4007 | Digital ad campaigns, impressions, clicks, conversions | ✅ Connected |
| [rez-marketing-service](https://github.com/imrejaul007/rez-marketing-service) | 4000 | Broadcasts, audience targeting, automation | ✅ Connected |
| [rez-intent-graph](https://github.com/imrejaul007/rez-intent-graph) | 4001 | User intent capture & analysis | ✅ Connected |
| [AdBazaar](https://github.com/imrejaul007/adBazaar) | Vercel | Offline ad marketplace | Hub |

#### rez-ads-service Endpoints (AdBazaar)
| Endpoint | Description |
|----------|-------------|
| `POST /adbazaar/campaign` | Create campaign from AdBazaar |
| `POST /adbazaar/impression` | Track ad impressions |
| `POST /adbazaar/click` | Track ad clicks |
| `POST /adbazaar/conversion` | Track conversions |
| `GET /adbazaar/analytics` | Get campaign analytics |

#### AdBazaar Integration
```typescript
// src/lib/adsService.ts - Connect to rez-ads-service
// src/lib/marketing.ts - Connect to rez-marketing-service  
// src/lib/rezMarketing.ts - Unified marketing API
```

### Backend Services

| Service | GitHub | Status |
|---------|--------|--------|
| rez-backend (main) | [Link](https://github.com/imrejaul007/rez-backend) | ✅ Deployed |
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

### Karma Suite

| Service | GitHub | Status |
|---------|--------|--------|
| rez-karma-service | [Link](https://github.com/imrejaul007/Karma) | ✅ Deployed |
| rez-karma-app | [Link](https://github.com/imrejaul007/rez-karma-app) | ✅ Deployed |
| rez-karma-mobile | [Link](https://github.com/imrejaul007/rez-karma-mobile) | ✅ APK Ready |

### Mobile Apps

| App | GitHub | Platform | Status |
|-----|--------|---------|--------|
| rez-app-consumer | [Link](https://github.com/imrejaul007/rez-app-consumer) | React Native | ✅ Live |
| rez-app-marchant | [Link](https://github.com/imrejaul007/rez-app-marchant) | React Native | ✅ Live |
| rez-app-admin | [Link](https://github.com/imrejaul007/rez-app-admin) | React Native | ✅ Live |

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

### For Developer - Deploy Now

```bash
git clone https://github.com/imrejaul007/CorpPerks.git
cd CorpPerks
docker-compose up -d
```

### Required Environment Variables

```env
# rez-corpperks-service
MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/corpperks
CORS_ORIGIN=https://admin.rez.money,https://rez-app.vercel.app

# rez-hotel-service
MAKCORPS_API_KEY=your_key

# rez-procurement-service
NEXTABIZZ_API_KEY=your_key
```

### Services & Ports

| Service | Port | Health Endpoint |
|---------|------|-----------------|
| rez-corpperks-service | 4013 | /health |
| rez-hotel-service | 4015 | /health |
| rez-procurement-service | 4012 | /health |

### Key API Endpoints

| Endpoint | Purpose |
|----------|---------|
| `GET /api/wallet/combined/:employeeId` | Get both wallets |
| `POST /api/benefits-config/resolve` | Check benefits |
| `POST /api/wallet/employee-corporate/:id/allocate` | Allocate |
| `POST /api/campaigns` | Create campaign |
| `POST /api/gst/invoices` | Create invoice |

### Features

- Corporate Gifting (campaigns)
- Corporate Hotel Booking (Makcorps)
- Corporate Procurement (NextaBizz)
- Dual Wallet System (Personal + Corporate)
- Benefits Configuration (Merchant > Company > Platform)
- GST Invoicing
- HRIS Integration (GreytHR, BambooHR, Zoho)
- Analytics Dashboard

### Documentation

| File | Purpose |
|------|---------|
| `docs/DEPLOYMENT-GUIDE.md` | Full deploy instructions |
| `docs/API-REFERENCE.md` | Complete API docs |
| `docs/QUICK-REFERENCE.md` | Quick commands |
| `docs/WALLET-SYSTEM.md` | Wallet architecture |

### Deploy Options

1. **Docker:** `docker-compose up -d`
2. **Render Blueprint:** Use `render.yaml`
3. **Manual:** Deploy each service separately

---

## Quick Links

- [Render Dashboard](https://dashboard.render.com)
- [MongoDB Atlas](https://cloud.mongodb.com)
- [GitHub Organization](https://github.com/imrejaul007)
- [CorpPerks](https://github.com/imrejaul007/CorpPerks)
