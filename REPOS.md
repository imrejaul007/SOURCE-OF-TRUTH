# REZ Platform — All Repositories

GitHub org: `imrejaul007`
Last updated: 2026-04-25

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
│  │ • Consumer   │  │ • Backend    │  │ • API Gateway             │ │
│  │ • Merchant   │  │   (Monolith) │  │ • Auth Service            │ │
│  │ • Admin      │  │              │  │ • Wallet Service          │ │
│  └──────────────┘  └──────────────┘  │ • Payment Service         │ │
│                                       │ • Order Service           │ │
│                                       │ • Catalog Service         │ │
│                                       │ • Search Service          │ │
│                                       │ • ... (14 services)       │ │
│                                       └────────────────────────────┘ │
│                                                                      │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │ USER-FACING APPS (connected via services)                    │   │
│  │                                                               │   │
│  │ • REZ Now (web ordering)  • Rendez (social)                  │   │
│  │ • REZ Web Menu           • StayOwen (hotel OTA)              │   │
│  │ • Karma (social impact)  • AdBazaar (ads platform)          │   │
│  └──────────────────────────────────────────────────────────────┘   │
│                                                                      │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │ MERCHANT PLATFORMS                                           │   │
│  │                                                               │   │
│  │ • Restaurian (Resto Papa) - restaurant management            │   │
│  │ • Hotel PMS - property management                            │   │
│  └──────────────────────────────────────────────────────────────┘   │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

---

## CORE PROJECTS (Source of Truth)

These are the main applications — changes should be made here.

| # | App | Local Path | Git Remote | Tech Stack | Deploy |
|---|-----|------------|------------|------------|--------|
| 1 | **rez-app-consumer** | `rez-app-consumer/` | imrejaul007/rez-app-consumer | Expo SDK 53, React Native 0.79, TypeScript | EAS Build |
| 2 | **rez-app-marchant** | `rez-app-marchant/` | imrejaul007/rez-app-marchant | Expo SDK 53, React Native | EAS Build |
| 3 | **rez-backend** | `rezbackend/rez-backend-master/` | imrejaul007/rez-backend | Node.js, Express, TypeScript, MongoDB | Render |

---

## SERVICES (14 microservices)

All apps connect to the ecosystem through these services.

| # | Service | Local Path | Git Remote | Port | Status |
|---|---------|------------|------------|------|--------|
| 1 | rez-api-gateway | `rez-api-gateway/` | imrejaul007/rez-api-gateway | 5002 | Live |
| 2 | rez-auth-service | `rez-auth-service/` | imrejaul007/rez-auth-service | 5003 | Live |
| 3 | rez-merchant-service | `rez-merchant-service/` | imrejaul007/rez-merchant-service | 3004 | Live |
| 4 | rez-wallet-service | `rez-wallet-service/` | imrejaul007/rez-wallet-service | 5006 | Live |
| 5 | rez-payment-service | `rez-payment-service/` | imrejaul007/rez-payment-service | 5005 | Live |
| 6 | rez-order-service | `rez-order-service/` | imrejaul007/rez-order-service | 3006 | Live |
| 7 | rez-catalog-service | `rez-catalog-service/` | imrejaul007/rez-catalog-service | 5007 | Live |
| 8 | rez-search-service | `rez-search-service/` | imrejaul007/rez-search-service | 5008 | Live |
| 9 | rez-gamification-service | `rez-gamification-service/` | imrejaul007/rez-gamification-service | 4003 | Live |
| 10 | rez-ads-service | `rez-ads-service/` | imrejaul007/rez-ads-service | - | Live |
| 11 | rez-marketing-service | `rez-marketing-service/` | imrejaul007/rez-marketing-service | - | Live |
| 12 | rez-scheduler-service | `rez-scheduler-service/` | imrejaul007/rez-scheduler-service | - | In Dev |
| 13 | rez-finance-service | `rez-finance-service/` | imrejaul007/rez-finance-service | - | In Dev |
| 14 | rez-karma-service | `rez-karma-service/` | imrejaul007/Karma | - | In Dev |

## Event Workers

| # | Service | Local Path | Git Remote | Status |
|---|---------|------------|------------|--------|
| 1 | analytics-events | `analytics-events/` | imrejaul007/analytics-events | Live |
| 2 | rez-notification-events | `rez-notification-events/` | imrejaul007/rez-notification-events | Live |
| 3 | rez-media-events | `rez-media-events/` | imrejaul007/rez-media-events | Live |

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
| 4 | **StayOwen (Hotel OTA)** | `Hotel OTA/` | imrejaul007/hotel-ota | Node.js, Prisma | Render |
| 5 | **AdBazaar** | `adBazaar/` | imrejaul007/adBazaar | Next.js, Supabase | Vercel |

---

## MERCHANT PLATFORMS

These are separate platforms for merchants (not connected to REZ core services)

| # | App | Local Path | Git Remote | Tech Stack | Status |
|---|-----|------------|------------|------------|--------|
| 1 | **Restaurian** | `Resturistan App/` | imrejaul007/restaurantapp | Node.js, monorepo | Deploy pending |
| 2 | **Hotel PMS** | `Hotel OTA/` (same as above) | imrejaul007/hotel-ota | Node.js, Prisma | Live |

---

## DUPLICATE/Legacy FOLDERS (CLEANED - 2026-04-25)

Deleted after proper audit to preserve all unpushed commits:

| Local Folder | Same As | Action |
|-------------|---------|--------|
| `hotel-ota/` | `Hotel OTA/` | ✅ Deleted (955M freed) |
| `packages/rez-shared/` | `rez-shared/` | ✅ Deleted |
| `rezapp/rez-master/` | `rez-app-consumer/` | ✅ Deleted |
| `rez-web-menu/rezbackend/` | `rez-backend/` | ✅ Deleted (empty) |
| `components/` | - | ✅ Deleted (empty) |
| `config/` | - | ✅ Deleted (empty) |
| `test/` | - | ✅ Deleted (empty) |
| `tests/` | - | ✅ Deleted (empty) |

### Note: `rezbackend/rez-backend-master/` is the CORRECT location for the backend repo - do NOT delete.

---

## ARCHITECTURE NOTES

### How Apps Connect to Services

```
User App (Consumer/Merchant/Now)
         │
         ▼
   API Gateway
         │
         ├──► rez-backend (monolith)
         │
         ├──► rez-auth-service
         ├──► rez-wallet-service
         ├──► rez-payment-service
         ├──► rez-order-service
         ├──► rez-catalog-service
         ├──► rez-search-service
         └──► ... (other services)

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

## Last Updated

- 2026-04-25: Full audit, architecture clarification, duplicate identification
