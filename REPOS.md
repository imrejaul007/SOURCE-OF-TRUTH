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
│  │ ├── Ads Service (rez-ads-service)                 - port 4008                │  │
│  │ ├── Automation Service (rez-automation-service)                              │  │
│  │ ├── Finance Service (rez-finance-service)                                   │  │
│  │ ├── Insights Service (rez-insights-service)                                 │  │
│  │ ├── Intent Graph (rez-intent-graph)                                         │  │
│  │ └── Error Intelligence (rez-error-intelligence)                              │  │
│  └──────────────────────────────────────────────────────────────────────────────┘  │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐  │
│  │ REZ MIND - INTELLIGENCE LAYER                                               │  │
│  │                                                                              │  │
│  │ ├── Event Platform (rez-event-platform)            - port 4008                │  │
│  │ ├── Action Engine (rez-action-engine)               - port 4009                │  │
│  │ ├── Feedback Service (rez-feedback-service)        - port 4010                │  │
│  │ ├── User Intelligence (rez-user-intelligence)      - port 3004                │  │
│  │ ├── Merchant Intelligence (rez-merchant-intelligence) - port 4012               │  │
│  │ ├── Intent Predictor (rez-intent-predictor)       - port 4018                │  │
│  │ ├── Intelligence Hub (rez-intelligence-hub)        - port 4020                │  │
│  │ ├── Ad Copilot (rez-ad-copilot)                   - port 4021                │  │
│  │ └── Merchant Copilot (rez-merchant-copilot)       - port 4022                │  │
│  └──────────────────────────────────────────────────────────────────────────────┘  │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐  │
│  │ TARGETING & DELIVERY                                                        │  │
│  │ ├── Targeting Engine (rez-targeting-engine)        - port 3003                │  │
│  │ ├── Recommendation Engine (rez-recommendation-engine) - port 3001              │  │
│  │ ├── Personalization Engine (rez-personalization-engine) - port 4017            │  │
│  │ └── Push Service (rez-push-service)               - port 4013                │  │
│  └──────────────────────────────────────────────────────────────────────────────┘  │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

---

## REZ MIND - THE BRAIN

### What It Knows

#### User Profile (Derived Signals)
```json
{
  "user_id": "user_123",
  "preferences": {
    "cuisines": ["biryani", "pizza"],
    "price_sensitivity": "medium",
    "time_pattern": "evening_user",
    "dietary_restrictions": []
  },
  "intent_signals": {
    "current_intent": "looking_for_dinner",
    "confidence": 0.78,
    "purchase_probability": 0.65
  },
  "behavior": {
    "frequency": "weekly",
    "avg_order_value": 450,
    "engagement_level": "high"
  },
  "segments": ["foodies", "deal_seekers"],
  "lifetime_value": 15000,
  "churn_risk": "low"
}
```

#### Merchant Profile (Derived Signals)
```json
{
  "merchant_id": "merchant_456",
  "demand_pattern": "weekend_spike",
  "customer_types": ["budget_minders", "foodies"],
  "pricing_behavior": "discount_sensitive",
  "segments": ["high_volume", "deal_responsive"],
  "health_score": 85,
  "growth_score": 72
}
```

### User Segments
| Segment | Criteria |
|---------|----------|
| `high_value` | Top 20% by LTV |
| `vip` | LTV > 50,000 |
| `foodies` | High frequency, variety |
| `deal_seekers` | Always discount responsive |
| `budget_minders` | Low AOV, price sensitive |
| `churned` | 30+ days inactive |
| `at_risk` | 14+ days inactive |
| `window_shoppers` | Browse, no buy |
| `new_users` | First order < 7 days |
| `power_users` | 5+ sessions/week |

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
| [rez-catalog-service](https://github.com/imrejaul007/rez-catalog-service) | 4005 | Product catalog |
| [rez-search-service](https://github.com/imrejaul007/rez-search-service) | 4006 | Search |
| [rez-gamification-service](https://github.com/imrejaul007/rez-gamification-service) | 4007 | Gamification |
| [rez-ads-service](https://github.com/imrejaul007/rez-ads-service) | 4008 | Ad management |
| [rez-automation-service](https://github.com/imrejaul007/rez-automation-service) | - | Workflows |
| [rez-finance-service](https://github.com/imrejaul007/rez-finance-service) | - | Finance |
| [rez-insights-service](https://github.com/imrejaul007/rez-insights-service) | - | Analytics |
| [rez-intent-graph](https://github.com/imrejaul007/rez-intent-graph) | - | Intent tracking |
| [rez-error-intelligence](https://github.com/imrejaul007/rez-error-intelligence) | - | Error tracking |

### REZ Mind - Intelligence Layer
| Repo | Port | Description |
|------|------|-------------|
| [rez-event-platform](https://github.com/imrejaul007/rez-event-platform) | 4008 | Event ingestion |
| [rez-action-engine](https://github.com/imrejaul007/rez-action-engine) | 4009 | Decision engine |
| [rez-feedback-service](https://github.com/imrejaul007/rez-feedback-service) | 4010 | Learning loop |
| [rez-user-intelligence](https://github.com/imrejaul007/REZ-user-intelligence-service) | 3004 | User profiles |
| [rez-merchant-intelligence](https://github.com/imrejaul007/REZ-merchant-intelligence-service) | 4012 | Merchant profiles |
| [rez-intent-predictor](https://github.com/imrejaul007/REZ-intent-predictor) | 4018 | Intent prediction |
| [rez-intelligence-hub](https://github.com/imrejaul007/REZ-intelligence-hub) | 4020 | Unified profiles |
| [rez-ad-copilot](https://github.com/imrejaul007/REZ-ad-copilot) | 4021 | Ad intelligence |
| [rez-merchant-copilot](https://github.com/imrejaul007/REZ-merchant-copilot) | 4022 | Merchant insights |

### Targeting & Delivery
| Repo | Port | Description |
|------|------|-------------|
| [rez-targeting-engine](https://github.com/imrejaul007/REZ-targeting-engine) | 3003 | Campaign targeting |
| [rez-recommendation-engine](https://github.com/imrejaul007/REZ-recommendation-engine) | 3001 | Product recommendations |
| [rez-personalization-engine](https://github.com/imrejaul007/REZ-personalization-engine) | 4017 | Content ranking |
| [rez-push-service](https://github.com/imrejaul007/REZ-push-service) | 4013 | Notifications |

### Supporting
| Repo | Description |
|------|-------------|
| [rez-devops-config](https://github.com/imrejaul007/rez-devops-config) | DevOps configs |
| [rez-contracts](https://github.com/imrejaul007/rez-contracts) | Smart contracts |
| [rez-corpperks-service](https://github.com/imrejaul007/rez-corpperks-service) | Corporate perks |
| [rez-hotel-service](https://github.com/imrejaul007/rez-hotel-service) | Hotel integration |

---

## Service Ports

| Port | Service | Status |
|------|---------|--------|
| 4001 | Auth Service | Live |
| 4002 | Wallet Service | Live |
| 4003 | Payment Service | Live |
| 4004 | Order Service | Live |
| 4005 | Catalog Service | Live |
| 4006 | Search Service | Live |
| 4007 | Gamification | Live |
| 3001 | Recommendation Engine | Ready |
| 3003 | Targeting Engine | Ready |
| 3004 | User Intelligence | Ready |
| 4008 | Event Platform | Running |
| 4009 | Action Engine | Running |
| 4010 | Feedback Service | Running |
| 4012 | Merchant Intelligence | Ready |
| 4013 | Push Service | Ready |
| 4017 | Personalization | Ready |
| 4018 | Intent Predictor | Ready |
| 4020 | Intelligence Hub | Ready |
| 4021 | Ad Copilot | Ready |
| 4022 | Merchant Copilot | Ready |

---

## Data Flow

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│ DATA SOURCES                                                                        │
├─────────────────────────────────────────────────────────────────────────────────────┤
│ Consumer Apps                    Merchant Apps                                     │
│ ├── ReZ App                      ├── Merchant OS                                    │
│ ├── ReZ Now                      ├── RestoPapa                                     │
│ ├── Web Menu                     └── PMS                                           │
│ ├── rendez                                                                        │
│ └── Karma                                                                           │
└─────────────────────────────────────────────────────────────────────────────────────┘
                                      ↓
┌─────────────────────────────────────────────────────────────────────────────────────┐
│ EVENT LAYER - REZ MIND                                                             │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│ Events (correlation_id) → Event Platform → Action Engine → Feedback                  │
│                                                                                      │
│ USER INTELLIGENCE          MERCHANT INTELLIGENCE       INTENT PREDICTOR            │
│ ├── preferences            ├── demand_pattern         ├── current_intent           │
│ ├── behavior              ├── insights               ├── confidence                │
│ ├── segments              ├── trends                 ├── urgency                   │
│ ├── LTV                   ├── competitors           ├── mood                      │
│ └── churn_risk            └── recommendations       └── exit_intent              │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
                                      ↓
┌─────────────────────────────────────────────────────────────────────────────────────┐
│ TARGETING & DELIVERY                                                                 │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│ TARGETING ENGINE               PERSONALIZATION              PUSH SERVICE              │
│ ├── segments                   ├── collaborative           ├── FCM                    │
│ ├── campaigns                  ├── content_based          ├── APNs                   │
│ ├── frequency_caps             ├── contextual             ├── SMS                    │
│ └── budget_pacing             └── diversity              ├── Email                  │
│                                                                   └── WhatsApp       │
└─────────────────────────────────────────────────────────────────────────────────────┘
                                      ↓
┌─────────────────────────────────────────────────────────────────────────────────────┐
│ DELIVERY CHANNELS                                                                   │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│ AdBazaar → Targeted Ads        Push → Notifications      In-App → Content          │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

---

## MongoDB Atlas

Primary Cluster: `mongodb+srv://work_db_user:ZAFYAYH1zK0C74Ap@rez-intent-graph.a8ilqgi.mongodb.net`

Databases:
- `rez-events` - Event Platform
- `rez-actions` - Action Engine
- `rez-feedback` - Feedback Service
- `rez-user-intelligence` - User Profiles
- `rez-merchant-intelligence` - Merchant Profiles
- `rez-targeting` - Campaigns
- `rez-recommendations` - Recommendations

---

## Deployment

Services are deployed on **Render** with auto-scaling.

| Service | URL |
|---------|-----|
| Auth | https://rez-auth-service.onrender.com |
| Wallet | https://rez-wallet-service-36vo.onrender.com |
| Payment | https://rez-payment-service.onrender.com |
| Order | https://rez-backend-8dfu.onrender.com |
| Catalog | https://rez-catalog-service-1.onrender.com |
| Search | https://rez-search-service.onrender.com |
| Gamification | https://rez-gamification-service-3b5d.onrender.com |
| Intent Graph | https://rez-intent-graph.onrender.com |
| Merchant | https://rez-merchant-service-n3q2.onrender.com |
| Analytics | https://analytics-events-37yy.onrender.com |

---

## Status Summary

| Category | Count | Status |
|----------|-------|--------|
| Consumer Apps | 5 | Built |
| Merchant Apps | 3 | Built |
| Core Backend | 3 | Built |
| Core Services | 14 | Built |
| Intelligence Layer | 9 | Built |
| Targeting & Delivery | 4 | Built |
| **Total** | **38** | **Complete** |

---

Last updated: 2026-05-01
By: Claude Code
