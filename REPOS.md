# REZ Platform - All Repositories (Verified 2026-05-01)

GitHub org: `imrejaul007`
Last updated: 2026-05-01
Audit Status: COMPLETE

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
│  │ AI LAYER - ReZ Mind                                           │   │
│  │                                                               │   │
│  │ - Intent Graph (8 autonomous agents)                         │   │
│  │ - Insights Service                                           │   │
│  │ - Automation Service                                         │   │
│  │ - RTMN Commerce Memory                                        │   │
│  └──────────────────────────────────────────────────────────────┘   │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

---

## CORE PROJECTS (Source of Truth)

| # | App | Local Path | Git Remote | Tech Stack | Deploy | Status |
|---|-----|------------|------------|------------|--------|--------|
| 1 | **rez-app-consumer** | `rez-app-consumer/` | imrejaul007/rez-app-consumer | Expo SDK 53, React Native 0.79, TypeScript | EAS Build | Active |
| 2 | **rez-app-merchant** | `rez-app-merchant/` | imrejaul007/rez-app-marchant | Expo SDK 55, React Native 0.76, TypeScript | EAS Build | **BROKEN** |
| 3 | **rez-app-admin** | `rez-app-admin/` | imrejaul007/rez-app-admin | Expo SDK 53, React Native 0.79, TypeScript | EAS Build | Active |
| 4 | **rez-backend** | `rezbackend/` | imrejaul007/rez-backend | Node.js, Express, TypeScript, MongoDB | Render | Active |

---

## WEB APPS

| # | App | Local Path | Git Remote | Tech Stack | Deploy | Status |
|---|-----|------------|------------|------------|--------|--------|
| 1 | **REZ Now** | `rez-now/` | imrejaul007/rez-now | Next.js 16, React 19, Tailwind, Zustand | Vercel | Active |
| 2 | **REZ Web Menu** | N/A | N/A | Services are in rez-web-menu folder | N/A | **Not Found** |

---

## CORE SERVICES (14 microservices)

| # | Service | Local Path | Git Remote | Port | TypeScript | MongoDB | Redis | BullMQ | Status |
|---|---------|------------|------------|------|-----------|---------|-------|--------|--------|
| 1 | rez-auth-service | `rez-auth-service/` | imrejaul007/rez-auth-service | 4002 | Yes | Yes | Yes | Yes | Active |
| 2 | rez-wallet-service | `rez-wallet-service/` | imrejaul007/rez-wallet-service | 4004 | Yes | Yes | Yes | Yes | Active |
| 3 | rez-order-service | `rez-order-service/` | imrejaul007/rez-order-service | 3006 | Yes | Yes | Yes | Yes | Active |
| 4 | rez-payment-service | `rez-payment-service/` | imrejaul007/rez-payment-service | 4001 | Yes | Yes | Yes | Yes | Active |
| 5 | rez-merchant-service | `rez-merchant-service/` | imrejaul007/rez-merchant-service | 4005 | Yes | Yes | Yes | No | Active |
| 6 | rez-catalog-service | `rez-catalog-service/` | imrejaul007/rez-catalog-service | 3005 | Yes | Yes | Yes | Yes | Active |
| 7 | rez-search-service | `rez-search-service/` | imrejaul007/rez-search-service | 4003 | Yes | Yes | Yes | No | Active |
| 8 | rez-gamification-service | `rez-gamification-service/` | imrejaul007/rez-gamification-service | 3001 | Yes | Yes | Yes | Yes | Active |
| 9 | rez-ads-service | `rez-ads-service/` | imrejaul007/rez-ads-service | 4007 | Yes | Yes | Yes | No | Active |
| 10 | rez-marketing-service | `rez-marketing-service/` | imrejaul007/rez-marketing-service | 4000 | Yes | Yes | Yes | Yes | Active |
| 11 | rez-scheduler-service | `rez-scheduler-service/` | imrejaul007/rez-scheduler-service | 3012 | Yes | Yes | Yes | Yes | Active |
| 12 | rez-finance-service | `rez-finance-service/` | imrejaul007/rez-finance-service | 4006 | Yes | Yes | Yes | Yes | Active |
| 13 | rez-karma-service | `rez-karma-service/` | imrejaul007/rez-karma-service | 3009 | Yes | Yes | Yes | Yes | Active |
| 14 | rez-corpperks-service | `rez-corpperks-service/` | Built-in | 4013 | No | Yes | Yes | No | Active |

---

## BUSINESS SERVICES (3 microservices)

| # | Service | Local Path | Git Remote | Port | TypeScript | MongoDB | Redis | BullMQ | Status |
|---|---------|------------|------------|------|-----------|---------|-------|--------|--------|
| 1 | rez-hotel-service | `rez-hotel-service/` | Built-in | 4015 | No | Yes | No | No | Active |
| 2 | rez-procurement-service | `rez-procurement-service/` | Built-in | 4012 | No | Yes | No | No | Active |

---

## EVENT WORKERS (3 services)

| # | Service | Local Path | Git Remote | Port | Status |
|---|---------|------------|------------|------|--------|
| 1 | analytics-events | `analytics-events/` | imrejaul007/analytics-events | 3006 | Active |
| 2 | rez-notification-events | `rez-notification-events/` | imrejaul007/rez-notification-events | 3005 | Active |
| 3 | rez-media-events | `rez-media-events/` | imrejaul007/rez-media-events | 3008 | Active |

---

## AI LAYER - ReZ Mind (Separate Repo)

**Location:** `/Users/rejaulkarim/Documents/rez-intent-graph`
**Git:** `imrejaul007/rez-intent-graph`
**Render:** `rez-intent-graph` service

### Components

| # | Component | Port | AI Agents | Purpose |
|---|-----------|------|----------|---------|
| 1 | rez-intent-graph | 3001/3005 | 8 | Intent tracking, RTMN Commerce Memory |
| 2 | rez-insights-service | Configurable | 0 | Insights storage |
| 3 | rez-automation-service | Configurable | 0 | Rule engine |

### 8 Autonomous AI Agents

| Agent | Interval | Purpose |
|-------|----------|---------|
| DemandSignalAgent | 5 min | Demand aggregation per merchant/category |
| ScarcityAgent | 1 min | Supply/demand ratios, urgency alerts |
| PersonalizationAgent | 1 min | User response profiling, A/B testing |
| AttributionAgent | 30 min | Multi-touch conversion attribution |
| AdaptiveScoringAgent | 1 hour | ML retraining of intent scoring |
| FeedbackLoopAgent | 1 hour | Closed-loop optimization, drift detection |
| NetworkEffectAgent | 24 hours | Collaborative filtering, user similarity |
| RevenueAttributionAgent | 15 min | GMV tracking, ROI per agent/nudge |

---

## VERTICAL APPS

| # | App | Local Path | Git Remote | Tech Stack | Deploy | ReZ Integration |
|---|-----|------------|------------|------------|--------|-----------------|
| 1 | **Rendez** | `Rendez/` | imrejaul007/Rendez | React Native, Node.js, Prisma, PostgreSQL | Render + Vercel | Wallet, Catalog, Merchant |
| 2 | **AdBazaar** | `adBazaar/` | imrejaul007/adBazaar | Next.js 16, Supabase, Upstash Redis | Vercel | OAuth, Wallet, Payment, Intent |
| 3 | **NextaBiZ** | `nextabizz/` | imrejaul007/nextabizz | Next.js 15, Turborepo, Supabase | Vercel | OAuth, Merchant, Intent |
| 4 | **CorpPerks** | `CorpPerks/` | imrejaul007/CorpPerks | Node.js, MongoDB, React Native | Render, Docker | Finance, Karma, Wallet |

---

## HOTEL STACK - StayOwn (Hotel OTA)

**Brand:** StayOwn - India's First Hotel-Owned OTA
**Git:** `imrejaul007/hotel-ota`
**Location:** `Hotel OTA/`

### Apps

| # | App | Local Path | Purpose | Tech Stack |
|---|-----|------------|---------|------------|
| 1 | **OTA Web** | `apps/ota-web/` | Customer booking website | Next.js 16 |
| 2 | **Mobile** | `apps/mobile/` | StayOwn Mobile (iOS + Android) | React Native, Expo 49 |
| 3 | **Admin** | `apps/admin/` | StayOwn Admin Dashboard | Next.js 16 |
| 4 | **Hotel Panel** | `apps/hotel-panel/` | Hotel staff management | Next.js 16 |
| 5 | **Corporate Panel** | `apps/corporate-panel/` | Corporate account management | Next.js 16 |
| 6 | **API** | `apps/api/` | Backend API (includes Room QR) | Node.js, Express, Prisma |
| 7 | **Hotel PMS** | `hotel-pms/` | Property Management System | Node.js, Prisma, React |

### Room QR Feature

- **Location:** `Hotel OTA/apps/api/src/routes/room-qr.routes.ts`
- **Purpose:** Guest services when scanning room QR code
- **Intent:** `guest_services_scan`

### Deployment

| Service | Render Name | URL |
|---------|-------------|-----|
| API | hotel-ota-api | https://hotel-ota-api.onrender.com |
| OTA Web | hotel-ota-web | https://hotel-ota-web.onrender.com |
| Hotel Panel | hotel-ota-hotel-panel | https://hotel-ota-hotel-panel.onrender.com |
| Admin | hotel-ota-admin | https://hotel-ota-admin.onrender.com |

---

## KARMA APPS

| # | App | Local Path | Git Remote | Tech Stack |
|---|-----|------------|------------|------------|
| 1 | **rez-karma-app** | `rez-karma-app/` | imrejaul007/rez-karma-app | Next.js |
| 2 | **rez-karma-mobile** | `rez-karma-mobile/` | imrejaul007/rez-karma-mobile | React Native |

---

## SHARED PACKAGES

| # | Package | Local Path | Version | Purpose | Published | Status |
|---|---------|------------|---------|---------|-----------|--------|
| 1 | rez-shared | `rez-shared/` | 2.0.0 | Core utilities, types, schemas | Yes | Active |
| 2 | @rez/shared-types | `packages/shared-types/` | 2.0.0 | TypeScript interfaces, zod schemas | Yes | Active |
| 3 | @rez/service-core | `packages/service-core/` | 1.0.1 | Microservice infrastructure | No | Incomplete |
| 4 | @rez/ui | `packages/ui/` | 1.0.0 | UI components (5) | No | Minimal |
| 5 | @rez/metrics | `packages/metrics/` | 1.0.0 | Prometheus middleware | No | **Empty** |
| 6 | @rez/agent-memory | `packages/agent-memory/` | 1.0.0 | Agent memory | No | Active |
| 7 | @rez/intent-capture-sdk | `packages/intent-capture-sdk/` | 1.0.0 | Intent Capture SDK | No | Active |
| 8 | @rez/intent-graph | `packages/intent-graph/` | 0.1.0 | AI platform | No | Active |
| 9 | @rez/chat | `packages/rez-chat-service/` | 1.0.0 | Real-time chat | No | Active |
| 10 | @rez/chat-ai | `packages/rez-chat-ai/` | 1.0.0 | AI chat (Anthropic) | No | Active |
| 11 | @rez/chat-integration | `packages/rez-chat-integration/` | 1.0.0 | Chat integration | No | Active |
| 12 | @rez/chat-rn | `packages/rez-chat-rn/` | 1.0.0 | React Native chat | No | Active |
| 13 | @rez/eslint-plugin | `packages/eslint-plugin/` | 1.0.0 | ESLint rules | No | **Empty** |
| 14 | rez-contracts | `rez-contracts/` | 1.0.1 | API contracts | No | **Broken** |

### Infrastructure Packages (Not npm)

| # | Package | Local Path | Purpose |
|---|---------|------------|---------|
| 1 | rez-devops-config | `rez-devops-config/` | CI/CD (GitHub Actions) |
| 2 | rez-error-intelligence | `rez-error-intelligence/` | Error tracking docs |

---

## DUPLICATE PACKAGES (NEEDS CONSOLIDATION)

| Package | Location | Version | Issue |
|---------|----------|---------|-------|
| @rez/shared | `rez-shared/` | 2.0.0 | Canonical |
| @rez/shared | `packages/rez-shared/` | 1.0.0 | DUPLICATE - needs deprecation |

---

## KNOWN ISSUES

| # | Issue | Severity | Status | Fix |
|---|-------|----------|--------|-----|
| 1 | Merge conflict in rez-app-merchant/package.json | CRITICAL | **BROKEN** | Resolve conflict |
| 2 | Duplicate @rez/shared packages | HIGH | Needs action | Deprecate one |
| 3 | rez-contracts has no src/ directory | HIGH | **BROKEN** | Create or remove |
| 4 | @rez/metrics empty (no implementation) | MEDIUM | Dead code | Implement or remove |
| 5 | @rez/eslint-plugin empty (no rules) | MEDIUM | Dead code | Implement or remove |
| 6 | MongoDB AUTH not enabled | CRITICAL | Security Risk | Enable auth |
| 7 | Redis AUTH not enabled | CRITICAL | Security Risk | Enable auth |
| 8 | Hotel OTA has 18 remaining bugs | HIGH | Bug | Fix bugs |
| 9 | Search service needs Typesense | MEDIUM | Performance | Migrate |

---

## SERVICE PORTS REFERENCE

| Service | Port | Metrics |
|---------|------|---------|
| rez-auth-service | 4002 | 4102 |
| rez-wallet-service | 4004 | - |
| rez-order-service | 3006 | - |
| rez-payment-service | 4001 | - |
| rez-merchant-service | 4005 | - |
| rez-catalog-service | 3005 | - |
| rez-search-service | 4003 | - |
| rez-gamification-service | 3001 | 3004 (worker) |
| rez-ads-service | 4007 | - |
| rez-marketing-service | 4000 | - |
| rez-scheduler-service | 3012 | - |
| rez-finance-service | 4006 | - |
| rez-karma-service | 3009 | - |
| rez-corpperks-service | 4013 | - |
| rez-hotel-service | 4015 | - |
| rez-procurement-service | 4012 | - |
| rez-intent-graph | 3001 | 3005 (agent) |
| rez-insights-service | Configurable | - |
| rez-automation-service | Configurable | - |

---

## Last Updated

- 2026-05-01: Full ecosystem audit complete
  - All 17 services documented with verified tech stacks
  - All apps documented with API connections
  - All packages inventoried with status
  - ReZ Mind AI layer documented with 8 agents
  - Known issues catalogued
  - Source: COMPREHENSIVE-AUDIT-2026-05-01-FULL.md
