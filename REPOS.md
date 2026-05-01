# REZ Platform - All Repositories (Updated 2026-05-01)

GitHub org: `imrejaul007`
Last updated: 2026-05-01
Audit Status: COMPLETE

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                              REZ ECOSYSTEM                                          │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐  │
│  │ CONSUMER APPS                                                              │  │
│  │ ├── ReZ Consumer App (rez-app-consumer)                                     │  │
│  │ ├── ReZ Now (rez-now-app)                                                  │  │
│  │ ├── Web Menu (rez-web-menu)                                                │  │
│  │ ├── rendez (rez-rendez-app)                                                │  │
│  │ └── Karma App (rez-karma-app)                                              │  │
│  └──────────────────────────────────────────────────────────────────────────────┘  │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐  │
│  │ MERCHANT APPS                                                              │  │
│  │ ├── Merchant OS (rez-app-merchant)                                          │  │
│  │ ├── RestoPapa (rez-restopapa)                                              │  │
│  │ └── PMS (rez-pms-app)                                                      │  │
│  └──────────────────────────────────────────────────────────────────────────────┘  │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐  │
│  │ CORE BACKEND                                                               │  │
│  │ ├── API Gateway (rez-api-gateway)                                           │  │
│  │ ├── Business OS (rez-business-os)                                           │  │
│  │ └── Admin (rez-app-admin)                                                   │  │
│  └──────────────────────────────────────────────────────────────────────────────┘  │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐  │
│  │ CORE SERVICES                                                              │  │
│  │ ├── Auth Service (rez-auth-service)              - port 4001                │  │
│  │ ├── Wallet Service (rez-wallet-service)           - port 4002                │  │
│  │ ├── Payment Service (rez-payment-service)         - port 4003                │  │
│  │ ├── Order Service (rez-order-service)             - port 4004                │  │
│  │ ├── Catalog Service (rez-catalog-service)         - port 4005                │  │
│  │ ├── Search Service (rez-search-service)           - port 4006                │  │
│  │ ├── Gamification Service (rez-gamification-service) - port 4007               │  │
│  │ ├── Merchant Service (rez-merchant-service)       - port 4005                │  │
│  │ └── More services...                                                        │  │
│  └──────────────────────────────────────────────────────────────────────────────┘  │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐  │
│  │ REZ MIND - INTELLIGENCE LAYER                                               │  │
│  │                                                                              │  │
│  │ EVENT FLOW:                                                                 │  │
│  │ Consumer/Merchant Apps → Event Platform → Action Engine → Feedback → Learning│  │
│  │                                                                              │  │
│  │ INTELLIGENCE:                                                               │  │
│  │ ├── User Intelligence (Port 3004)                                            │  │
│  │ ├── Merchant Intelligence (Port 4012)                                         │  │
│  │ ├── Intent Predictor (Port 4018)                                             │  │
│  │ └── Intelligence Hub (Port 4020)                                              │  │
│  │                                                                              │  │
│  │ TARGETING & DELIVERY:                                                        │  │
│  │ ├── Targeting Engine (Port 3003)                                             │  │
│  │ ├── Recommendation Engine (Port 3001)                                         │  │
│  │ ├── Personalization Engine (Port 4017)                                       │  │
│  │ ├── Push Service (Port 4013)                                                 │  │
│  │ └── AdBazaar (Port 4025)                                                     │  │
│  │                                                                              │  │
│  │ COPILOTS:                                                                   │  │
│  │ ├── Merchant Copilot (Port 4022)                                             │  │
│  │ ├── Consumer Copilot (Port 4021)                                             │  │
│  │ └── Ad Copilot (Port 4021)                                                   │  │
│  │                                                                              │  │
│  │ SAFETY:                                                                     │  │
│  │ ├── Feature Flags (Port 4030)                                                │  │
│  │ └── Observability (Port 4031)                                                │  │
│  └──────────────────────────────────────────────────────────────────────────────┘  │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

---

## REZ Mind - The Brain

### Philosophy
```
Raw Events → Process → Derive Signals → Store Intelligence

❌ NOT: Store everything
✅ YES: Store structured, usable intelligence
```

### User Flow Example (Rejaul)
```
1. Rejaul uses ReZ App, ReZ Now, rendez, Karma
2. Events flow to Event Platform
3. ReZ Mind derives intelligence (NOT raw data)
4. Stores: preferences, intent, segments, scores
5. Powers: search, recommendations, ads, insights
```

### User Intelligence Stored
```json
{
  "user_id": "rejaul_123",
  "preferences": ["biryani", "pizza"],
  "intent": "looking_for_dinner",
  "segments": ["foodies", "deal_seekers"],
  "scores": { "ltv": 15000, "churn_risk": 0.2 }
}
```

### What ReZ Mind Does NOT Store
- ❌ Raw search queries
- ❌ Individual transactions
- ❌ Location history
- ❌ Personal details

---

## All Repositories

### Consumer Apps
| Repo | Description |
|------|-------------|
| [rez-app-consumer](https://github.com/imrejaul007/rez-app-consumer) | Main consumer app |
| [rez-now-app](https://github.com/imrejaul007/rez-now-app) | Quick ordering app |
| [rez-web-menu](https://github.com/imrejaul007/rez-web-menu) | Web ordering |
| [rez-rendez-app](https://github.com/imrejaul007/rez-rendez-app) | Reservation app |
| [rez-karma-app](https://github.com/imrejaul007/rez-karma-app) | Loyalty rewards |

### Merchant Apps
| Repo | Description |
|------|-------------|
| [rez-app-merchant](https://github.com/imrejaul007/rez-app-merchant) | Merchant dashboard |
| [rez-restopapa](https://github.com/imrejaul007/rez-restopapa) | Restaurant management |
| [rez-pms-app](https://github.com/imrejaul007/rez-pms-app) | Property management |

### Core Backend
| Repo | Description |
|------|-------------|
| [rez-api-gateway](https://github.com/imrejaul007/rez-api-gateway) | API Gateway |
| [rez-business-os](https://github.com/imrejaul007/rez-business-os) | Business dashboard |
| [rez-app-admin](https://github.com/imrejaul007/rez-app-admin) | Admin panel |

### Core Services
| Repo | Port | Description |
|------|------|-------------|
| [rez-auth-service](https://github.com/imrejaul007/rez-auth-service) | 4001 | Authentication |
| [rez-wallet-service](https://github.com/imrejaul007/rez-wallet-service) | 4002 | Wallet/Points |
| [rez-payment-service](https://github.com/imrejaul007/rez-payment-service) | 4003 | Payments |
| [rez-order-service](https://github.com/imrejaul007/rez-order-service) | 4004 | Order management |
| [rez-merchant-service](https://github.com/imrejaul007/rez-merchant-service) | 4005 | Merchant management |
| [rez-catalog-service](https://github.com/imrejaul007/rez-catalog-service) | 4006 | Product catalog |
| [rez-search-service](https://github.com/imrejaul007/rez-search-service) | 4007 | Search |
| [rez-gamification-service](https://github.com/imrejaul007/rez-gamification-service) | 4008 | Gamification |
| [rez-marketing-service](https://github.com/imrejaul007/rez-marketing-service) | - | Marketing + AdBazaar |

### REZ Mind - Intelligence Layer
| Repo | Port | Description |
|------|------|-------------|
| [rez-event-platform](https://github.com/imrejaul007/REZ-event-platform) | 4008 | Event ingestion |
| [rez-action-engine](https://github.com/imrejaul007/REZ-action-engine) | 4009 | Decision engine |
| [rez-feedback-service](https://github.com/imrejaul007/REZ-feedback-service) | 4010 | Learning loop |
| [rez-user-intelligence](https://github.com/imrejaul007/REZ-user-intelligence-service) | 3004 | User profiles |
| [rez-merchant-intelligence](https://github.com/imrejaul007/REZ-merchant-intelligence-service) | 4012 | Merchant profiles |
| [rez-intent-predictor](https://github.com/imrejaul007/REZ-intent-predictor) | 4018 | Intent prediction |
| [rez-intelligence-hub](https://github.com/imrejaul007/REZ-intelligence-hub) | 4020 | Unified profiles |

### Targeting & Delivery
| Repo | Port | Description |
|------|------|-------------|
| [rez-targeting-engine](https://github.com/imrejaul007/REZ-targeting-engine) | 3003 | Campaign targeting |
| [rez-recommendation-engine](https://github.com/imrejaul007/REZ-recommendation-engine) | 3001 | Product recommendations |
| [rez-personalization-engine](https://github.com/imrejaul007/REZ-personalization-engine) | 4017 | Content ranking |
| [rez-push-service](https://github.com/imrejaul007/REZ-push-service) | 4013 | Notifications |
| [rez-adbazaar](https://github.com/imrejaul007/REZ-adbazaar) | 4025 | Intent-based ads |

### Copilots
| Repo | Port | Description |
|------|------|-------------|
| [rez-merchant-copilot](https://github.com/imrejaul007/REZ-merchant-copilot) | 4022 | Merchant insights |
| [rez-consumer-copilot](https://github.com/imrejaul007/REZ-consumer-copilot) | 4021 | Consumer personalization |
| [rez-ad-copilot](https://github.com/imrejaul007/REZ-ad-copilot) | 4021 | Ad optimization |

### Safety & Operations
| Repo | Port | Description |
|------|------|-------------|
| [rez-feature-flags](https://github.com/imrejaul007/REZ-feature-flags) | 4030 | Feature toggles |
| [rez-observability](https://github.com/imrejaul007/REZ-observability) | 4031 | Logs & traces |

### Integration SDK
| Repo | Description |
|------|-------------|
| [REZ-mind-client](https://github.com/imrejaul007/REZ-mind-client) | App integration SDK |

---

## AdBazaar - Intent-Based Ad Targeting

### What is AdBazaar?
AdBazaar shows ads based on **user intent**, not surveillance.

### How It Works
```
User searches "spa"
    ↓
ReZ Mind detects: Intent = "looking_for_service"
    ↓
AdBazaar shows: Spa/salon ads
    ↓
NOT: Shows ads based on past browsing history
```

### User Segments
| Segment | Description | Users |
|--------|-------------|-------|
| Foodies | Frequent food orders | 1.8K |
| Deal Seekers | Price sensitive | 950 |
| VIP | High LTV | 180 |
| New Users | < 7 days | 1.2K |
| At Risk | 14+ days inactive | 340 |
| Wellness | Spa/salon/fitness | 620 |

### Intent Mapping
| User Intent | Ad Types Shown |
|-------------|----------------|
| looking_for_food | restaurant, food delivery |
| looking_for_dinner | dinner deals, biryani |
| looking_for_service | spa, salon |
| ordering | free delivery, discounts |
| booking | appointments, hotels |
| browsing | general promotions |

### Privacy First
- ❌ No personal data stored
- ❌ No browsing history
- ❌ No location tracking
- ✅ Intent-based targeting
- ✅ Consent-based personalization
- ✅ Users can opt-out

### AdBazaar Endpoints
```
GET  /segments          - List all segments
GET  /ads               - List all ads
POST /ads               - Create new ad
POST /targeting/predict - Predict targeting match
GET  /stats             - Campaign statistics
POST /track/impression  - Track ad view
POST /track/click       - Track ad click
POST /track/conversion   - Track conversion
GET  /dashboard         - Dashboard data
```

---

## Integration - Connecting Apps to ReZ Mind

### Quick Setup
```bash
# Copy REZ Mind Client to your app
cp -r REZ-MIND-CLIENT your-app/services/
```

### Merchant App Integration
```typescript
import { rezMind } from '../services/ReZMindClient';

// Order completed
await rezMind.merchant.sendOrderCompleted({
  merchant_id: 'merchant_123',
  order_id: 'order_456',
  items: [{ item_id: 'biryani', quantity: 2, price: 250 }],
  total_amount: 580
});

// Inventory low
await rezMind.merchant.sendInventoryLow({
  merchant_id: 'merchant_123',
  item_id: 'biryani',
  current_stock: 3,
  threshold: 5
});
```

### Consumer App Integration
```typescript
// User searches
await rezMind.consumer.sendSearch({
  user_id: 'user_123',
  query: 'biryani',
  results_count: 15,
  clicked_item: 'biryani_large'
});

// User views item
await rezMind.consumer.sendView({
  user_id: 'user_123',
  item_id: 'biryani',
  duration_seconds: 15
});
```

---

## Service Ports

| Port | Service | Status |
|------|---------|--------|
| 3001 | Recommendation Engine | Ready |
| 3003 | Targeting Engine | Ready |
| 3004 | User Intelligence | Ready |
| 4008 | Event Platform | Ready |
| 4009 | Action Engine | Ready |
| 4010 | Feedback Service | Ready |
| 4012 | Merchant Intelligence | Ready |
| 4013 | Push Service | Ready |
| 4017 | Personalization | Ready |
| 4018 | Intent Predictor | Ready |
| 4020 | Intelligence Hub | Ready |
| 4021 | Consumer Copilot | Ready |
| 4022 | Merchant Copilot | Ready |
| 4025 | AdBazaar | Ready |
| 4030 | Feature Flags | Ready |
| 4031 | Observability | Ready |

---

## Feature Flags (Safe Mode)

| Flag | Default | Description |
|------|---------|-------------|
| learning_enabled | OFF | ML learning |
| adaptive_enabled | OFF | Adaptive decisions |
| personalization_enabled | ON | Personalization |
| recommendations_enabled | ON | Product recommendations |
| ads_enabled | OFF | Targeted ads |
| push_enabled | ON | Push notifications |
| auto_execute_safe | ON | Auto-execute SAFE |

---

## Safety Thresholds

```javascript
RISKY: confidence < 0.7 OR decisions < 5
SEMI_SAFE: confidence >= 0.7 AND decisions >= 5
SAFE: confidence >= 0.9 AND approval_rate >= 0.8 AND decisions >= 10
```

---

## 5-Layer Database Design

```
┌─────────────────────────────────────────────────────┐
│ 1. IDENTITY (users, merchants) │
├─────────────────────────────────────────────────────┤
│ 2. EVENTS (raw, short-term, 30 days TTL) │
├─────────────────────────────────────────────────────┤
│ 3. INTELLIGENCE (CORE - derived, permanent) │
├─────────────────────────────────────────────────────┤
│ 4. DECISIONS (suggestions) │
├─────────────────────────────────────────────────────┤
│ 5. FEEDBACK (outcomes) │
└─────────────────────────────────────────────────────┘
```

---

## Deployment URLs (Production)

| Service | URL |
|---------|-----|
| Event Platform | https://rez-event-platform.onrender.com |
| Action Engine | https://rez-action-engine.onrender.com |
| Feedback Service | https://rez-feedback-service.onrender.com |
| Merchant Copilot | https://rez-merchant-copilot.onrender.com |
| Consumer Copilot | https://rez-consumer-copilot.onrender.com |
| AdBazaar | https://rez-adbazaar.onrender.com |
| Feature Flags | https://rez-feature-flags.onrender.com |

---

## Status Summary

| Category | Count | Status |
|----------|-------|--------|
| Consumer Apps | 5 | Built |
| Merchant Apps | 3 | Built |
| Core Backend | 3 | Built |
| Core Services | 10+ | Built |
| REZ Mind Services | 15+ | Built |
| Integration SDK | 1 | Built |
| **Total** | **40+** | **Complete** |

---

Last updated: 2026-05-01
By: Claude Code
