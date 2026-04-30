# REZ Platform - All Repositories

GitHub org: `imrejaul007`
Last updated: 2026-04-30

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────┐
│                        REZ ECOSYSTEM                                 │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────────────┐ │
│  │ CORE APPS    │  │ CORE BACKEND │  │ CORE SERVICES             │ │
│  │              │  │              │  │                           │ │
│  │ - Consumer   │  │ - Backend    │  │ - API Gateway             │ │
│  │ - Merchant   │  │   (Monolith) │  │ - Auth Service            │ │
│  │ - Admin      │  │              │  │ - Wallet Service          │ │
│  └──────────────┘  └──────────────┘  │ - Payment Service         │ │
│                                       │ - Order Service           │ │
│                                       │ - Catalog Service         │ │
│                                       │ - Search Service          │ │
│                                       │ - Gamification Service    │ │
│                                       │ - Ads Service             │ │
│                                       │ - Marketing Service       │ │
│                                       │ - Scheduler Service       │ │
│                                       │ - Finance Service         │ │
│                                       │ - Karma Service           │ │
│                                       │ - CorpPerks Service       │ │
│                                       │ - Hotel Service           │ │
│                                       │ - Procurement Service     │ │
│                                       └────────────────────────────┘ │
│                                                                      │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │ USER-FACING APPS                                             │   │
│  │                                                               │   │
│  │ - REZ Now (web ordering)  - Rendez (social)                  │   │
│  │ - REZ Web Menu           - Karma (social impact)              │   │
│  │ - AdBazaar (ads platform)                                    │   │
│  └──────────────────────────────────────────────────────────────┘   │
│                                                                      │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │ HOTEL STACK - StayOwn                                        │   │
│  │                                                               │   │
│  │ - OTA Web (booking)  - Mobile (iOS/Android)                   │   │
│  │ - Admin Dashboard   - Hotel Panel (staff)                   │   │
│  │ - Corporate Panel    - API (includes Room QR)                │   │
│  │ - Hotel PMS (property management)                             │   │
│  └──────────────────────────────────────────────────────────────┘   │
│                                                                      │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │ MERCHANT PLATFORMS                                           │   │
│  │                                                               │   │
│  │ - REZ Merchant App (POS) - INTEGRATED                      │   │
│  │ - RestoPapa (restaurant) - STANDALONE, NOT integrated     │   │
│  └──────────────────────────────────────────────────────────────┘   │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

---

## CORE PROJECTS (Source of Truth)

These are the main applications - changes should be made here.

| # | App | Local Path | Git Remote | Tech Stack | Deploy |
|---|-----|------------|------------|------------|--------|
| 1 | **rez-app-consumer** | `rez-app-consumer/` | imrejaul007/rez-app-consumer | Expo SDK 53, React Native 0.79, TypeScript | EAS Build |
| 2 | **rez-app-marchant** | `rez-app-marchant/` | imrejaul007/rez-app-marchant | Expo SDK 53, React Native | EAS Build |
| 3 | **rez-backend** | `rezbackend/rez-backend-master/` | imrejaul007/rez-backend | Node.js, Express, TypeScript, MongoDB | Render |

---

## CORE SERVICES (9 microservices)

| # | Service | Local Path | Git Remote | Port | Status | README |
|---|---------|------------|------------|------|--------|--------|
| 1 | rez-api-gateway | `rez-api-gateway/` | imrejaul007/rez-api-gateway | 5002 | Live | YES |
| 2 | rez-auth-service | `rez-auth-service/` | imrejaul007/rez-auth-service | 4002 | Live | YES |
| 3 | rez-wallet-service | `rez-wallet-service/` | imrejaul007/rez-wallet-service | 3010 | Live | YES |
| 4 | rez-payment-service | `rez-payment-service/` | imrejaul007/rez-payment-service | 4001 | Live | YES |
| 5 | rez-order-service | `rez-order-service/` | imrejaul007/rez-order-service | 3008 | Live | YES |
| 6 | rez-catalog-service | `rez-catalog-service/` | imrejaul007/rez-catalog-service | 3005 | Live | YES |
| 7 | rez-search-service | `rez-search-service/` | imrejaul007/rez-search-service | 4003 | Live | YES |
| 8 | rez-gamification-service | `rez-gamification-service/` | imrejaul007/rez-gamification-service | 3001 | Live | YES |
| 9 | rez-merchant-service | `rez-merchant-service/` | imrejaul007/rez-merchant-service | 4005 | Live | YES |

---

## SUPPORTING SERVICES (5 microservices)

| # | Service | Local Path | Git Remote | Port | Status | README |
|---|---------|------------|------------|------|--------|--------|
| 1 | rez-ads-service | `rez-ads-service/` | imrejaul007/rez-ads-service | 4007 | Live | YES |
| 2 | rez-marketing-service | `rez-marketing-service/` | imrejaul007/rez-marketing-service | 4000 | Live | YES |
| 3 | rez-scheduler-service | `rez-scheduler-service/` | imrejaul007/rez-scheduler-service | 3012 | Live | YES |
| 4 | rez-finance-service | `rez-finance-service/` | imrejaul007/rez-finance-service | 4005 | Live | YES |
| 5 | rez-karma-service | `rez-karma-service/` | imrejaul007/Karma | 3009 | Live | YES |

---

## EVENT WORKERS (3 services)

| # | Service | Local Path | Git Remote | Port | Status |
|---|---------|------------|------------|------|--------|
| 1 | analytics-events | `analytics-events/` | imrejaul007/analytics-events | 3006 | Live |
| 2 | rez-notification-events | `rez-notification-events/` | imrejaul007/rez-notification-events | 3005 | Live |
| 3 | rez-media-events | `rez-media-events/` | imrejaul007/rez-media-events | 3008 | Live |

---

## CORPPERKS SERVICES (4 microservices)

| # | Service | Local Path | Git Remote | Port | Status | README |
|---|---------|------------|------------|------|--------|--------|
| 1 | rez-corpperks-service | `rez-corpperks-service/` | Built-in | 4013 | Live | YES |
| 2 | rez-hotel-service | `rez-hotel-service/` | Built-in | 4011 | Live | YES |
| 3 | rez-procurement-service | `rez-procurement-service/` | Built-in | 4012 | Live | YES |
| 4 | rez-karma-service | `rez-karma-service/` | imrejaul007/Karma | 3009 | Live | YES |

### CorpPerks SDK

```bash
npm install @rez/corpperks-sdk
```

```typescript
import { CorpPerksClient } from '@rez/corpperks-sdk';

const corp = new CorpPerksClient({
  apiBaseUrl: 'https://api.rez.money',
  token: userToken,
});

const benefits = await corp.getMyBenefits();
const booking = await corp.createBooking({...});
await corp.redeemReward('R001');
```

### CorpPerks Deploy Files

| File | Purpose |
|------|---------|
| `CorpPerks/docker-compose.yml` | Docker + MongoDB |
| `CorpPerks/render.yaml` | Render one-click deploy |
| `CorpPerks/DEPLOY.md` | Deployment guide |
| `CorpPerks/sdk/` | JS SDK |
| `CorpPerks/CorpPerks.postman_collection.json` | API testing |

---

## ReZ Mind - AI Intelligence Layer

**Location:** `/Users/rejaulkarim/Documents/rez-intent-graph` (separate repo)
**Git:** `imrejaul007/rez-intent-graph`
**Render:** `rez-intent-graph` service

ReZ Mind is the **AI-powered commerce intelligence platform** combining:
- **RTMN Commerce Memory** - Tracks user intent across all apps
- **8 Autonomous AI Agents** - Self-operating agents for commerce
- **Intent Graph** - Dormant intent detection and revival

### 8 Autonomous Agents
| Agent | Schedule | Purpose |
|-------|----------|---------|
| DemandSignalAgent | Every 5 min | Aggregate demand per merchant/category |
| ScarcityAgent | Every 1 min | Supply/demand ratios, urgency alerts |
| PersonalizationAgent | Event-driven | User response profiling, A/B testing |
| AttributionAgent | Event-driven | Multi-touch conversion attribution |
| AdaptiveScoringAgent | Hourly | ML retraining of intent scoring |
| FeedbackLoopAgent | Event-driven | Closed-loop optimization, drift detection |
| NetworkEffectAgent | Daily | Collaborative filtering, user similarity |
| RevenueAttributionAgent | Every 15 min | GMV tracking, ROI per agent/nudge |

### Ports
| Server | Port | Purpose |
|--------|------|---------|
| API Server | 3001 | Intent capture, commerce memory |
| Agent Server | 3005 | Autonomous agent swarm |

---

## Shared Packages

| # | Package | Local Path | Git Remote | Notes |
|---|---------|------------|------------|-------|
| 1 | rez-shared | `rez-shared/` | imrejaul007/rez-shared | npm: @rez/shared |
| 2 | shared-types | `packages/shared-types/` | imrejaul007/shared-types | Shared TypeScript types |
| 3 | rez-contracts | `rez-contracts/` | imrejaul007/rez-contracts | Smart contracts |
| 4 | rez-devops-config | `rez-devops-config/` | imrejaul007/rez-devops-config | CI/CD config |
| 5 | rez-error-intelligence | `rez-error-intelligence/` | imrejaul007/rez-error-intelligence | Error tracking |

---

## USER-FACING APPS (Connected via Services)

These apps use the core services (auth, wallet, orders, etc.)

| # | App | Local Path | Git Remote | Tech Stack | Deploy |
|---|-----|------------|------------|------------|--------|
| 1 | **REZ Now** | `rez-now/` | imrejaul007/rez-now | Next.js, React | Vercel |
| 2 | **REZ Web Menu** | `rez-web-menu/` | imrejaul007/rez-web-menu | Next.js | Vercel |
| 3 | **Rendez** | `Rendez/` | imrejaul007/Rendez | React Native, Node.js, Prisma | Render + Vercel |
| 4 | **AdBazaar** | `adBazaar/` | imrejaul007/adBazaar | Next.js, Supabase | Vercel |

---

## HOTEL STACK - StayOwn (Hotel OTA)

**Brand:** StayOwn - India's First Hotel-Owned OTA

| # | App | Local Path | Purpose | Tech Stack |
|---|-----|------------|---------|------------|
| 1 | **OTA Web** | `Hotel OTA/apps/ota-web/` | Customer booking website | Next.js |
| 2 | **Mobile** | `Hotel OTA/apps/mobile/` | StayOwn Mobile (iOS + Android) | React Native |
| 3 | **Admin** | `Hotel OTA/apps/admin/` | StayOwn Admin Dashboard | Next.js |
| 4 | **Hotel Panel** | `Hotel OTA/apps/hotel-panel/` | Hotel staff management | Next.js |
| 5 | **Corporate Panel** | `Hotel OTA/apps/corporate-panel/` | Corporate account management | Next.js |
| 6 | **API** | `Hotel OTA/apps/api/` | Backend API (includes Room QR) | Node.js, Prisma |
| 7 | **Hotel PMS** | `Hotel OTA/hotel-pms/` | Property Management System | Node.js, Prisma |

### Room QR - Guest Services

- **Location:** `Hotel OTA/apps/api/src/routes/room-qr.routes.ts`
- **Purpose:** Guest services when scanning room QR code
- **Intent:** `guest_services_scan`

---

## MERCHANT PLATFORMS

| # | App | Local Path | Git Remote | Tech Stack | Status |
|---|-----|------------|------------|------------|--------|
| 1 | **RestoPapa** | `Resturistan App/` | imrejaul007/restaurantapp | Node.js, monorepo | STANDALONE - NOT integrated |
| 2 | **REZ Merchant App** | `rez-app-marchant/` | imrejaul007/rez-app-marchant | Expo, React Native | INTEGRATED |
| 3 | **REZ Admin App** | `rez-app-admin/` | imrejaul007/rez-app-admin | Expo, React Native | INTEGRATED |

---

## Cleanup Commands

```bash
# Remove duplicate clones (after confirming they match above)
rm -rf "hotel-ota"
rm -rf "packages/rez-shared"
rm -rf "rezapp"
rm -rf "rezbackend"
rm -rf "rez-web-menu/rezbackend"
rm -rf "components"
rm -rf "config"
rm -rf "test"
rm -rf "tests"
```

---

## Architecture Notes

### How Apps Connect to Services

```
User App (Consumer/Merchant/Now)
         |
         v
   API Gateway
         |
         +-- rez-backend (monolith)
         |
         +-- rez-auth-service
         +-- rez-wallet-service
         +-- rez-payment-service
         +-- rez-order-service
         +-- rez-catalog-service
         +-- rez-search-service
         +-- rez-gamification-service
         +-- rez-ads-service
         +-- rez-marketing-service
         +-- rez-scheduler-service
         +-- rez-finance-service
         +-- rez-karma-service

Event Queue: BullMQ + Redis
```

### Partner Apps (Standalone)

| App | Connection to REZ | Auth |
|-----|-------------------|------|
| Rendez | REZ wallet (hold/release), SSO | REZ partner API |
| StayOwen | REZ wallet, SSO | REZ SSO |
| AdBazaar | None | Supabase auth |
| Restaurian | REZ wallet (future) | TBD |

---

## Last Updated

- 2026-04-30: Phase 0 Documentation complete
  - Created comprehensive README.md for all 17 services
  - Updated SERVICE ports in LOCAL-PORTS.md
  - Updated REPOS.md with correct paths and README status

---

## Known Issues (Audit Findings)

| Issue | Severity | Status |
|-------|----------|--------|
| Git conflict markers in 3 services | CRITICAL | To Fix |
| Wrong package name (rez-workspace) | CRITICAL | To Fix |
| Missing source for 2 packages | CRITICAL | To Fix |
| Typo: rez-app-marchant | HIGH | To Fix |
| Nested duplicate packages | HIGH | To Fix |
| MongoDB/Redis AUTH not enabled | CRITICAL | Security Risk |
