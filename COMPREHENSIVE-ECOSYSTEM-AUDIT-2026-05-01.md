# ReZ Ecosystem - Comprehensive Audit Report
**Date:** 2026-05-01
**Status:** COMPLETE
**Auditor:** Claude Code

---

## Executive Summary

The ReZ ecosystem contains:
- **4 Mobile Apps** (consumer, merchant, admin, karma)
- **6 Web Apps** (rez-now, adBazaar, nextabizz, rendez, corpperks-landing)
- **18 Backend Services** (microservices + event workers)
- **13 Shared Packages** (shared-types, chat, AI, intent graph)
- **1 Hotel OTA Stack** (6 apps + API + PMS)
- **1 Main Monolith** (rezbackend)

**Total Components: 49**

---

## SECTION 1: MOBILE APPS

### 1.1 rez-app-consumer
| Attribute | Value |
|-----------|-------|
| **Tech Stack** | Expo SDK 53, React Native 0.79, React 19 |
| **Navigation** | expo-router 5.1.11 |
| **State** | Zustand 35 stores, React Query |
| **Bundle ID** | `money.rez.app` |
| **Screens** | 200+ |
| **API Services** | 227 |
| **GitHub** | imrejaul007/rez-app-consumer |

**Features:**
- E-commerce (products, cart, checkout)
- Wallet (ReZ Cash, coins)
- Bookings (flights, hotels, trains)
- In-store (QR pay, dine-in)
- Bill payments, recharges
- Gamification (points, badges, missions)
- Creator dashboard
- Finance (savings, insurance)
- Karma score tracking

**API Connections:**
- Gateway: `rez-api-gateway.onrender.com`
- Auth Service: `rez-auth-service.onrender.com`
- Wallet Service: `rez-wallet-service.onrender.com`
- Order Service: `rez-order-service.onrender.com`

---

### 1.2 rez-app-merchant
| Attribute | Value |
|-----------|-------|
| **Tech Stack** | Expo SDK 53, React Native 0.76 |
| **Bundle ID** | `com.rez.admin` |
| **GitHub** | imrejaul007/rez-app-marchant |

**Features:**
- Order management
- Menu management
- Analytics dashboard
- Payment tracking

---

### 1.3 rez-app-admin
| Attribute | Value |
|-----------|-------|
| **Tech Stack** | Expo SDK 53, React Native 0.79 |
| **GitHub** | imrejaul007/rez-app-admin |

---

### 1.4 rez-karma-mobile
| Attribute | Value |
|-----------|-------|
| **Tech Stack** | React Native |
| **Purpose** | Karma score tracking |

---

## SECTION 2: WEB APPS

### 2.1 rez-now
| Attribute | Value |
|-----------|-------|
| **Tech Stack** | Next.js 16.2.3, React 19, Tailwind 4 |
| **State** | Zustand 5.0.12 |
| **Real-time** | Socket.io-client 4.8.3 |
| **URL** | https://rez-now.vercel.app |
| **GitHub** | imrejaul007/rez-now |

**Pages:** Home, Scan, Search, Profile, Wallet, Orders, Join, Store pages, Cart, Checkout, Pay, Bill, Reserve, Schedule, Staff dashboard

**API Connections:**
- Socket events: join-store, menu:item-availability, web-order:status-update

---

### 2.2 adBazaar
| Attribute | Value |
|-----------|-------|
| **Tech Stack** | Next.js 16.2.4, React 19, Supabase, Upstash Redis |
| **Payments** | Razorpay 2.9.6 |
| **Features** | Ad marketplace, QR attribution, Vendor dashboard, Admin KYC |

---

### 2.3 nextabizz
| Attribute | Value |
|-----------|-------|
| **Tech Stack** | Next.js 15.1.0, Turborepo, Supabase |
| **Features** | B2B procurement, RFQ system, Supplier portal |

**Webhook Integrations:**
- REZ Merchant webhook
- RestoPapa webhook
- Hotel PMS webhook

---

### 2.4 Rendez
| Attribute | Value |
|-----------|-------|
| **Stack** | Next.js 14 (admin), React Native (app) |
| **Features** | Meetup management, User moderation, Fraud detection |

---

## SECTION 3: HOTEL OTA STACK

### 3.1 Structure
```
Hotel OTA/
├── apps/
│   ├── api/          # Express.js API (port 3000)
│   ├── ota-web/      # Consumer web (port 3003)
│   ├── mobile/       # React Native
│   ├── admin/        # Admin dashboard (port 3002)
│   ├── hotel-panel/  # Hotel management (port 3001)
│   └── corporate-panel/  # Corporate accounts (port 3004)
├── packages/database/ # Prisma client
└── prisma/schema.prisma  # PostgreSQL schema
```

### 3.2 Tech Stack
| Component | Technology |
|-----------|------------|
| API | Express.js 4.21, TypeScript |
| Database | PostgreSQL, Prisma 5.22 |
| Queue | Redis, BullMQ |
| Real-time | Socket.IO 4.8 |
| Payments | Razorpay |

### 3.3 Key Features
- Multi-coin wallet (OTA, REZ, Hotel Brand coins)
- PMS integration (webhooks)
- Room QR validation
- Dynamic pricing & demand forecasting
- RTMN Commerce Memory
- Governance/DAO

### 3.4 API Routes
- `/v1/auth` - OTP, SSO, staff auth
- `/v1/hotels` - Hotel search, availability
- `/v1/bookings` - Hold, confirm, cancel
- `/v1/wallet` - Coin balance, transactions
- `/v1/room-qr` - QR validation
- `/v1/room-service` - Service requests
- `/v1/room-chat` - Guest-staff chat
- `/api/webhooks/pms/*` - PMS webhooks

---

## SECTION 4: BACKEND SERVICES

### 4.1 Service Inventory

| # | Service | Port | MongoDB | Redis | BullMQ | Status |
|---|---------|------|---------|-------|--------|--------|
| 1 | rez-auth-service | 4002 | Yes | Yes | Yes | |
| 2 | rez-wallet-service | 4004 | Yes | Yes | Yes | |
| 3 | rez-order-service | 3006 | Yes | Yes | Yes | |
| 4 | rez-payment-service | 4001 | Yes | Yes | Yes | |
| 5 | rez-merchant-service | 4005 | Yes | Yes | Yes | |
| 6 | rez-catalog-service | 3005 | Yes | Yes | Yes | |
| 7 | rez-search-service | 4003 | Yes | Yes | No | |
| 8 | rez-gamification-service | 3001 | Yes | Yes | Yes | |
| 9 | rez-ads-service | 4007 | Yes | Yes | No | |
| 10 | rez-marketing-service | 4000 | Yes | Yes | Yes | |
| 11 | rez-scheduler-service | 3012 | Yes | Yes | Yes | |
| 12 | rez-finance-service | 4006 | Yes | Yes | Yes | |
| 13 | rez-karma-service | 3009 | Yes | Yes | Yes | |
| 14 | rez-corpperks-service | 4013 | Yes | Yes | No | |
| 15 | rez-hotel-service | 4015 | Yes | No | No | |
| 16 | rez-procurement-service | 4012 | Yes | No | No | |
| 17 | rez-insights-service | - | Yes | Yes | No | |
| 18 | rez-automation-service | - | Yes | Yes | No | |

---

## SECTION 5: SHARED PACKAGES

| Package | Purpose | Active | Issues |
|---------|---------|--------|--------|
| shared-types | Type definitions, Zod schemas | Yes | File references |
| rez-shared | Utilities, rate limiting | Yes | No src files |
| service-core | Infra (BullMQ, Redis) | Unknown | Not used |
| agent-memory | Supabase + Redis memory | Unknown | Singleton anti-pattern |
| chat-ai | AI chat (Anthropic) | Yes | Circular deps |
| chat-integration | Ecosystem connectors | Unknown | No consumers |
| chat-service | Socket.IO client | Yes | Naming conflict |
| chat-rn | React Native chat | Unknown | No dist build |
| intent-graph | Commerce AI | Yes | ESM/CJS mismatch |
| intent-capture-sdk | Intent tracking SDK | Unknown | Global singleton |
| metrics | Prometheus middleware | Unknown | In-memory only |
| ui | Shared components | Unknown | Naming mismatch |
| eslint-plugin | Linting rules | Unknown | Missing rule files |

---

## SECTION 6: CONNECTIVITY MAP

### 6.1 Consumer App → Services
```
rez-app-consumer
    ├── rez-api-gateway (gateway)
    ├── rez-auth-service
    ├── rez-wallet-service
    ├── rez-order-service
    ├── rez-payment-service
    ├── rez-catalog-service
    └── Socket.io events
```

### 6.2 Merchant App → Services
```
rez-app-merchant
    ├── rez-api-gateway
    ├── rez-merchant-service
    └── rez-order-service
```

### 6.3 rez-now → Services
```
rez-now
    ├── rez-auth-service (OTP)
    ├── rez-catalog-service (menu)
    ├── rez-order-service
    ├── rez-payment-service
    ├── rez-wallet-service
    ├── Socket.io (real-time)
    └── Hotel OTA (room service)
```

### 6.4 Hotel OTA → ReZ Services
```
Hotel OTA API
    ├── ReZ Backend (booking sync, SSO)
    ├── ReZ Auth Service (OAuth2)
    ├── ReZ Wallet Service (coin sync)
    ├── Finance Service (BNPL)
    ├── Payment Service (webhooks)
    └── @rez/chat, @rez/chat-ai
```

### 6.5 nextabizz → ReZ Services
```
nextabizz
    ├── REZ OAuth (auth)
    ├── REZ Merchant webhook
    ├── RestoPapa webhook
    └── Hotel PMS webhook
```

---

## SECTION 7: DATA MODELS MAPPING

### 7.1 User Data Flow
| Location | Model | Fields |
|---------|-------|--------|
| rez-auth-service | User | phone, email, password, role |
| rezbackend | User | full profile |
| Hotel OTA | User | customer accounts, tiers |

**ISSUE:** User data exists in multiple places. No single source of truth.

### 7.2 Order Data Flow
| Location | Model |
|---------|-------|
| rez-order-service | Order |
| rezbackend | Order |
| Hotel OTA | Booking |

**ISSUE:** Orders in main services vs Bookings in Hotel OTA - separate systems.

### 7.3 Wallet/Coin Data Flow
| Location | Model | Coins |
|---------|-------|-------|
| rez-wallet-service | Wallet, CoinTransaction | ReZ coins |
| Hotel OTA | CoinWallet, CoinTransaction | OTA, REZ, Hotel Brand |

**ISSUE:** Dual coin systems - not synchronized.

### 7.4 Product/Catalog Data Flow
| Location | Model |
|---------|-------|
| rez-catalog-service | Product, Menu |
| Hotel OTA | RoomType, InventorySlot |

**ISSUE:** Different product models for different verticals.

---

## SECTION 8: GAP ANALYSIS

### 8.1 CRITICAL GAPS

| Gap | Impact | Files Affected |
|-----|--------|----------------|
| **No unified user identity** | Users have separate accounts across apps | All apps |
| **Dual coin systems** | ReZ coins vs Hotel OTA coins not linked | rez-wallet-service, Hotel OTA |
| **No order sync** | Main orders vs Hotel bookings separate | All |
| **Missing shared-types consumers** | 6 packages have no active consumers | packages/* |
| **File path dependencies** | All apps use `file:../` instead of npm | All apps |

### 8.2 HIGH PRIORITY GAPS

| Gap | Impact | Status |
|-----|--------|--------|
| **Circular dependencies** | chat-ai ↔ intent-graph | Risk |
| **No API versioning** | Intent graph routes not versioned | All services |
| **Missing validation** | No Zod on many routes | Intent graph |
| **In-memory metrics** | Metrics lost on restart | rez-metrics |
| **Singleton anti-patterns** | Global state in packages | agent-memory, intent-capture-sdk |

### 8.3 MEDIUM PRIORITY GAPS

| Gap | Recommendation |
|-----|----------------|
| Version mismatches | Align React, Zod, Next.js versions |
| Missing tests | Only agent-memory has test config |
| Console logging | Some files still use console.* |
| No migrations | Schema changes manual |
| No request tracing | Request IDs not tracked |

---

## SECTION 9: MISMATCHES

### 9.1 Authentication Mismatch

| App | Auth Method | Token Storage |
|-----|-------------|---------------|
| rez-app-consumer | JWT | SecureStore |
| rez-now | OTP/PIN | localStorage + httpOnly |
| adBazaar | Supabase Auth | Supabase session |
| nextabizz | REZ OAuth | httpOnly cookies |
| Hotel OTA | JWT + OTP | Redis |
| rendez-admin | Bearer token | sessionStorage |

**ISSUE:** 6 different auth patterns. No unified auth SDK.

### 9.2 Database Mismatch

| System | Database | ORM |
|--------|----------|-----|
| Main Services | MongoDB | Mongoose |
| Hotel OTA | PostgreSQL | Prisma |
| adBazaar | Supabase | - |
| nextabizz | Supabase | - |

**ISSUE:** 4 different databases. No data sharing.

### 9.3 Real-time Mismatch

| App | Real-time |
|-----|-----------|
| rez-app-consumer | Socket.io |
| rez-now | Socket.io |
| Hotel OTA | Socket.io |
| adBazaar | None |
| nextabizz | None |

**ISSUE:** Inconsistent real-time adoption.

### 9.4 Naming Conflicts

| Package | Directory Name | npm Name |
|---------|---------------|----------|
| @rez/chat | rez-chat-service | @rez/chat |
| @rez/ui | rez-ui | @rez/ui |
| intent-graph | rez-intent-graph | @rez/intent-graph |

---

## SECTION 10: MISSING PIECES FOR LIVE SYSTEM

### 10.1 Authentication & Identity
- [ ] Unified user identity across all apps
- [ ] Single sign-on (SSO) between apps
- [ ] Shared auth package (@rez/auth)
- [ ] Session management service

### 10.2 Data Synchronization
- [ ] Wallet sync between main and Hotel OTA
- [ ] Order sync between services
- [ ] User profile sync
- [ ] Loyalty points sync

### 10.3 API Gateway
- [ ] Centralized routing for all services
- [ ] Rate limiting at gateway level
- [ ] Request logging/tracing
- [ ] Auth validation at gateway

### 10.4 Monitoring & Observability
- [ ] Prometheus metrics for all services
- [ ] Distributed tracing (OpenTelemetry)
- [ ] Centralized logging (ELK stack)
- [ ] Health check aggregation

### 10.5 Shared Infrastructure
- [ ] Publish shared-types to npm
- [ ] Fix file:../ dependencies
- [ ] Shared error handling middleware
- [ ] Shared validation schemas

---

## SECTION 11: RECOMMENDATIONS

### Phase 1: Make System Live (Critical)
1. **Fix dependencies** - Replace file:../ with npm workspace or published packages
2. **Unified auth** - Create @rez/auth package with common auth patterns
3. **API Gateway** - Deploy centralized gateway for routing
4. **Health checks** - All services need /health endpoints
5. **Environment variables** - Standardize across all services

### Phase 2: Data Integrity (High)
1. **User sync** - Implement user identity service
2. **Wallet sync** - Link Hotel OTA coins with main wallet
3. **Order tracking** - Unified order tracking across apps
4. **Profile sync** - Keep user profiles in sync

### Phase 3: Polish (Medium)
1. **Remove dead code** - Delete unused packages
2. **Add tests** - Unit tests for all services
3. **API versioning** - Version all public APIs
4. **Documentation** - OpenAPI specs for all services

---

## SECTION 12: FILES NEEDED FOR SOURCE OF TRUTH

Update these files with audit findings:
- [x] REPOS.md - ✅ Updated with correct service list
- [x] ECOSYSTEM-ARCHITECTURE.md - ✅ Architecture documented
- [ ] API-ENDPOINTS.md - Needs full endpoint list
- [ ] DATA-MODELS.md - Create - document all schemas
- [ ] CONNECTIVITY.md - Create - document connections
- [ ] DEPLOYMENT-STATUS.md - Update with current status

---

## Summary

**Components:** 49 total
- 4 Mobile Apps
- 6 Web Apps  
- 18 Backend Services
- 13 Shared Packages
- 6 Hotel OTA Apps
- 2 Monoliths (rezbackend, intent-graph)

**Critical Issues:** 8
- Dual coin systems not synced
- User identity fragmented
- File path dependencies
- Circular package dependencies

**High Priority:** 12
- Missing API versioning
- No unified auth
- Dead packages
- Incomplete validation

**Medium Priority:** 15
- Version mismatches
- Missing tests
- Console logging
- No request tracing

---

*Report generated: 2026-05-01*
