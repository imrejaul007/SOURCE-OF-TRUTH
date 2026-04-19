# REZ Platform — All Repositories

GitHub org: `imrejaul007`
Total: 55 repos (verified via `gh repo list imrejaul007 --limit 100`)
- REZ Platform: ~23 core repos
- Partner / Standalone Apps: 4
- Internal / Other: 4 (vesper, rez-app, ReZ-Hotel-pms, hotel)
- Unrelated personal projects: 21 (see bottom section)

## Recent Updates (2026-04-19)

### Backend P0 Fixes (MASTER-PLAN-2026-04-19 B1-B12)

All merged to `main`. Render auto-deploys on push.

| Item | Fix | Service | PR |
|------|-----|---------|----|
| B1 | Remove duplicate `startPaymentWorker()` | `rez-payment-service` | #14 |
| B2 | Move atomic `findOneAndUpdate` inside MongoDB transaction for wallet credit (TOCTOU race fix) | `rez-payment-service` | #15 |
| B4 | Add IDOR protection to `PATCH /orders/:id/status` (merchant can only update own orders) | `rez-order-service` | #17 |
| B6 | Magic byte MIME sniffing (JPEG/PNG/WebP) prevents MIME spoofing on file uploads | `rez-media-events` | #4 |
| B8 | Replace in-memory Map with Redis INCR+EXPIRE rate limiter for distributed correctness | `analytics-events` | #6 |
| B9 | Replace `cors()` with explicit CORS_ORIGIN whitelist (was wide-open) | `rez-ads-service` | #11 |
| B10 | Add nginx routes for `/api/homepage` and `/api/recommendations` to search_backend | `rez-api-gateway` | #7 |
| B12 | Remove silent 10,000-coin cap on wallet recharge (net-zero economics: 1 coin = ₹1) | `rez-payment-service` | #15 |

Not addressed:
- **B3**: SSE endpoint already fixed (BAK-CROSS-002 in previous session)
- **B5**: Ephemeral disk uploads — requires Cloudinary/S3 migration (complex infra change)
- **B11**: Gateway + SOT contract drift — no specific drift identified in codebase

### P1 Backend Fixes (2026-04-19)

| Fix | Service | PR |
|-----|---------|----|
| Add `trust proxy` to 7 Express services so `req.ip` reflects real client IP behind nginx/Render LB | `rez-auth-service` | #7 |
| Add `trust proxy` to 7 Express services so `req.ip` reflects real client IP behind nginx/Render LB | `rez-payment-service` | #16 |
| Add `trust proxy` to 7 Express services so `req.ip` reflects real client IP behind nginx/Render LB | `rez-wallet-service` | #14 |
| Add `trust proxy` to 7 Express services so `req.ip` reflects real client IP behind nginx/Render LB | `rez-search-service` | #7 |
| Add `trust proxy` to 7 Express services so `req.ip` reflects real client IP behind nginx/Render LB | `rez-ads-service` | #12 |
| Add `trust proxy` to 7 Express services so `req.ip` reflects real client IP behind nginx/Render LB | `analytics-events` | #7 |
| Add `trust proxy` to 7 Express services so `req.ip` reflects real client IP behind nginx/Render LB | `rez-marketing-service` | #5 |
| Tighten CORS regex in `rez-merchant-service` (MA-BACK-007: removed wildcard `vercel.app` subdomain allow) | `rez-merchant-service` | prior |

Already done prior:
- Merchant deep-link handler (F7): `Linking.getInitialURL` + `Linking.addEventListener` with route allowlist
- Admin deep-link handler (F8): same pattern — already committed to git HEAD

- `rez-backend` — All PRs merged. Zero open. TypeScript build clean.

| Item | Fix | Service | PR |
|------|-----|---------|----|
| B1 | Remove duplicate `startPaymentWorker()` | `rez-payment-service` | #14 |
| B2 | Move atomic `findOneAndUpdate` inside MongoDB transaction for wallet credit (TOCTOU race fix) | `rez-payment-service` | #15 |
| B4 | Add IDOR protection to `PATCH /orders/:id/status` (merchant can only update own orders) | `rez-order-service` | #17 |
| B6 | Magic byte MIME sniffing (JPEG/PNG/WebP) prevents MIME spoofing on file uploads | `rez-media-events` | #4 |
| B8 | Replace in-memory Map with Redis INCR+EXPIRE rate limiter for distributed correctness | `analytics-events` | #6 |
| B9 | Replace `cors()` with explicit CORS_ORIGIN whitelist (was wide-open) | `rez-ads-service` | #11 |
| B10 | Add nginx routes for `/api/homepage` and `/api/recommendations` to search_backend | `rez-api-gateway` | #7 |
| B12 | Remove silent 10,000-coin cap on wallet recharge (net-zero economics: 1 coin = ₹1) | `rez-payment-service` | #15 |

Not addressed:
- **B3**: SSE endpoint already fixed (BAK-CROSS-002 in previous session)
- **B5**: Ephemeral disk uploads — requires Cloudinary/S3 migration (complex infra change)
- **B11**: Gateway + SOT contract drift — no specific drift identified in codebase

- `rez-backend` — All PRs merged. Zero open. TypeScript build clean.
  - **#118** (2026-04-18): Home services booking (HomeServiceCategory, HomeService, HomeServiceBooking)
  - **#119** (2026-04-18): Loyalty stamps audit trail (StampEvent, StampRedemption)
  - **#120** (2026-04-18): Claude AI assistant + WhatsApp + catalog + appointments
  - **#125** (2026-04-18): BULL-002/004/005/006 — BullMQ timeout and clean loop fixes
  - **#126** (2026-04-18): Wallet types refactor, cart API, bill upload
  - **#127** (2026-04-18): BULL-004 — lockDuration + per-job timeout for BullMQ
  - **#130-#137** (2026-04-18): TypeScript build fixes, CRITICAL-013/016, @karim4987498/shared removal, Math.random → crypto.randomUUID
- `rez-shared` v1.0.2: net-zero coin economics (1 coin = ₹1), coinsEarned(), COIN_TO_RUPEE_RATE
- `adBazaar` — All PRs merged. Zero open.
  - **#17** (2026-04-19): AB2-C5 payout silent-fail fix + AB3-C3 campaign booking updates
- Coin economics: net-zero model (earn 1 coin/₹1, spend 1 coin = ₹1)
- Ad monetization: CPA + CPM + fixed daily charge model

### REZ Now Gap Audit (2026-04-19) — `rez-now/`
- **CRITICAL**: 13/14 fixed. 1 partial (NW-CRIT-011 CAPTCHA — needs backend). 0 open.
- **HIGH**: 11/15 fixed. 2 partial (NW-HIGH-006 unit, NW-HIGH-008 coupon re-val — need backend). 2 open (NW-HIGH-001 catalog placeholders, NW-HIGH-009 price manipulation).
- Key fixes: idempotency key UUID-only, AES-GCM token encryption, httpOnly cookies, Socket.IO store-room join for UPI, offline queue error events, canonical PaymentStatus/OrderHistoryItem types, merchant store-ownership guard, coupon server re-validation at checkout, price guard in `createRazorpayOrder`, catalog gated behind `NEXT_PUBLIC_FEATURE_CATALOG_V2`.

---

## Frontend Apps

| # | Service | Repo URL | Deploy | Status |
|---|---------|----------|--------|--------|
| 1 | **Consumer App** | https://github.com/imrejaul007/rez-app-consumer | EAS Build | Private |
| 2 | **Merchant App** | https://github.com/imrejaul007/rez-app-marchant | Vercel / Expo | Private |
| 3 | **Admin App** | https://github.com/imrejaul007/rez-app-admin | Vercel | Private |
| 4 | **Web Menu (QR)** | https://github.com/imrejaul007/rez-web-menu | vercel.app | Private |
| 5 | **REZ Now** | https://github.com/imrejaul007/rez-now | Vercel | Private | Gap audit: **13/14 CRITICAL fixed**, **11/15 HIGH fixed** |

## Backend / Infrastructure

| # | Service | Repo URL | Render Deploy URL | Local Port | Status |
|---|---------|----------|-------------------|------------|--------|
| 6 | **API Gateway** | https://github.com/imrejaul007/rez-api-gateway | rez-api-gateway.onrender.com | 5002 | ✅ Live |
| 7 | **rez-backend** | https://github.com/imrejaul007/rez-backend | rez-backend-8dfu.onrender.com | 5001 | ✅ Live (2026-04-19: TS clean, all PRs merged, home services, stamps, AI/WhatsApp) |
| 8 | **rez-auth-service** | https://github.com/imrejaul007/rez-auth-service | rez-auth-service.onrender.com | 5003 | ✅ Live |
| 9 | **rez-merchant-service** | https://github.com/imrejaul007/rez-merchant-service | rez-merchant-service-n3q2.onrender.com | 3004 | ✅ Live |
| 10 | **rez-wallet-service** | https://github.com/imrejaul007/rez-wallet-service | rez-wallet-service-36vo.onrender.com | 5006 | ✅ Live |
| 11 | **rez-payment-service** | https://github.com/imrejaul007/rez-payment-service | rez-payment-service.onrender.com | 5005 | ✅ Live |
| 12 | **rez-order-service** | https://github.com/imrejaul007/rez-order-service | rez-order-service-hz18.onrender.com | 3006 | ✅ Live |
| 13 | **rez-catalog-service** | https://github.com/imrejaul007/rez-catalog-service | rez-catalog-service-1.onrender.com | 5007 | ✅ Live |
| 14 | **rez-search-service** | https://github.com/imrejaul007/rez-search-service | rez-search-service.onrender.com | 5008 | ✅ Live |
| 15 | **rez-gamification-service** | https://github.com/imrejaul007/rez-gamification-service | rez-gamification-service-3b5d.onrender.com | 4003 | ✅ Live |
| 16 | **rez-ads-service** | https://github.com/imrejaul007/rez-ads-service | rez-ads-service.onrender.com | — | ✅ Live |
| 17 | **rez-marketing-service** | https://github.com/imrejaul007/rez-marketing-service | rez-marketing-service.onrender.com | — | ✅ Live |
| 18 | **analytics-events** | https://github.com/imrejaul007/analytics-events | analytics-events-37yy.onrender.com | 5011 | ✅ Live |
| 19 | **rez-notification-events** | https://github.com/imrejaul007/rez-notification-events | rez-notification-events-mwdz.onrender.com | — | ✅ Live (worker) |
| 20 | **rez-media-events** | https://github.com/imrejaul007/rez-media-events | rez-media-events-lfym.onrender.com | — | ✅ Live |
| 21 | **rez-shared** | https://github.com/imrejaul007/rez-shared | npm package v1.0.2 | — | Public |
| 22 | **rez-finance-service** | https://github.com/imrejaul007/rez-finance-service | TBD | — | ⚠️ In flight |
| 23 | **rez-karma-service** | https://github.com/imrejaul007/Karma | TBD | — | ⚠️ In flight |

## Supporting Services

| # | Service | Repo URL | Notes |
|---|---------|----------|-------|
| 24 | **rez-contracts** | https://github.com/imrejaul007/rez-contracts | Smart contracts / legal |
| 25 | **rez-devops-config** | https://github.com/imrejaul007/rez-devops-config | CI/CD, infra config |
| 26 | **rez-error-intelligence** | https://github.com/imrejaul007/rez-error-intelligence | Error tracking / intelligence |

## Internal / Other REZ Projects (no local clone)

| # | Service | Repo URL | Notes |
|---|---------|----------|-------|
| 27 | **vesper** | https://github.com/imrejaul007/vesper | Private — no local clone |
| 28 | **rez-app** | https://github.com/imrejaul007/rez-app | Private — no local clone (legacy consumer app?) |
| 29 | **ReZ-Hotel-pms** | https://github.com/imrejaul007/ReZ-Hotel-pms | Private — local clone exists |
| 30 | **hotel** | https://github.com/imrejaul007/hotel | Public — no local clone |

## Standalone / Partner Apps

| App | Repo URL | Notes |
|-----|----------|-------|
| **Resturistan** | https://github.com/imrejaul007/restaurantapp | RestaurantHub |
| **Rendez** | https://github.com/imrejaul007/Rendez | Social dating, v1.0.0 |
| **AdBazaar** | https://github.com/imrejaul007/adBazaar | Next.js + Supabase |
| **Hotel OTA** | https://github.com/imrejaul007/hotel-ota | Hotel + PMS integration |
| **Pentouz** | https://github.com/imrejaul007/Pentouz | Public — no local clone |

---

## Duplicate Clones / Legacy

| Local Folder | Same As | Notes |
|-------------|---------|-------|
| `rezmerchant/rez-merchant-master` | `rez-app-marchant/` | Submodule: `rezmerchant/rez-merchant-master` → imrejaul007/rez-app-marchant |
| `rezadmin/rez-admin-main` | `rez-app-admin/` | Submodule: `rezadmin/rez-admin-main` → imrejaul007/rez-app-admin |
| `rezbackend/rez-backend-master` | `rez-backend/` | Submodule: `rezbackend/rez-backend-master` → imrejaul007/rez-backend |
| `Resturistan App/` | `restaurantapp/` | Submodule → imrejaul007/restaurantapp |
| `packages/rez-shared` | `rez-shared/` | Submodule at `packages/rez-shared` → imrejaul007/rez-shared (also at root as `rez-shared/`) |
| `ReZ-Hotel-pms/` | `hotel-ota/` | Separate clone — check if duplicate or variant |
| `rezapp/` | `rez-app/` (GitHub only) | Legacy — no real git repo |
| `rezbackend/` (root) | `rez-backend/` | Legacy partial clone — no real git repo |

## Excluded / Unrelated Personal Projects

These are on GitHub under imrejaul007 but are not REZ platform projects:

| Repo | Visibility | Notes |
|------|-----------|-------|
| `luxurydrop` | public | Unrelated |
| `Homeservice` | public | Unrelated |
| `nuqtaapp` | public | Unrelated |
| `shifaalhind` | public | Unrelated |
| `thickfiberdeck` | public | Unrelated |
| `burhan` | public | Unrelated |
| `Rez_v-2` | public | Unrelated |
| `rezprive` | public | Unrelated |
| `ownly` | public | Unrelated |
| `aromasouq` | public | Unrelated |
| `stock` | public | Unrelated |
| `erp` | public | Unrelated |
| `shifa` | public | Unrelated |
| `pentouz_pms` | public | Unrelated |
| `pentouz_pms_frontend` | public | Unrelated |

## Excluded (not REZ platform)

- `docs/`, `scripts/`, `archives/`, `config/`, `dist/` — non-git directories
- `rez-scheduler-service/` — confirmed not part of REZ Full App

---

## Local Dev Note

`ReZ Full App/` has **no git repo**. Each service is a standalone repo cloned locally.
Render auto-deploys on push to `main`.
