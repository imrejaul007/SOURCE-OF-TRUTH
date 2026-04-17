# REZ Platform — Deployment Status

Last updated: 2026-04-18 (Gen 23: ROUTE-SEC-005 admin upload ownership, CRON-002 async onComplete, BULL-001 removeOnComplete bounded, NW-CRIT-003 store ownership)

## Production (Live on Render/Vercel)

| Service | URL | Status | Type |
|---------|-----|--------|------|
| **rez-api-gateway** | https://rez-api-gateway.onrender.com | ✅ Live | Render Web Service |
| **rez-backend** | https://rez-backend-8dfu.onrender.com | ✅ Live | Render Web Service (pending: PRs #113-120 — hotel reviews, salon booking, home services, loyalty stamps, AI/WhatsApp, JWT/dual authority fixes) |
| **rez-auth-service** | https://rez-auth-service.onrender.com | ✅ Live | Render Web Service |
| **rez-merchant-service** | https://rez-merchant-service-n3q2.onrender.com | ✅ Live | Render Web Service |
| **rez-wallet-service** | https://rez-wallet-service-36vo.onrender.com | ✅ Live | Render Web Service |
| **rez-payment-service** | https://rez-payment-service.onrender.com | ✅ Live | Render Web Service (wallet-credit BullMQ worker added — Gen 22) |
| **rez-order-service** | https://rez-order-service-hz18.onrender.com | ✅ Live | Render Web Service |
| **rez-catalog-service** | https://rez-catalog-service-1.onrender.com | ✅ Live | Render Web Service |
| **rez-search-service** | https://rez-search-service.onrender.com | ✅ Live | Render Web Service |
| **rez-gamification-service** | https://rez-gamification-service-3b5d.onrender.com | ✅ Live | Render Web Service |
| **rez-ads-service** | https://rez-ads-service.onrender.com | ✅ Live | Render Web Service |
| **rez-marketing-service** | https://rez-marketing-service.onrender.com | ✅ Live | Render Web Service |
| **analytics-events** | https://analytics-events-37yy.onrender.com | ✅ Live | Render Web Service |
| **rez-notification-events** | https://rez-notification-events-mwdz.onrender.com | ✅ Live | Render Worker |
| **rez-media-events** | https://rez-media-events-lfym.onrender.com | ✅ Live | Render Worker |
| **rez-app-admin** | https://rez-app-admin.vercel.app | ✅ Live | Vercel |
| **rez-app-consumer** | (EAS build) | ✅ Live | Expo EAS |
| **rez-app-marchant** | https://rez-app-marchant.vercel.app | ✅ Live | Vercel |
| **rez-web-menu** | https://menu.rez.money | ✅ Live | Vercel |

## Recent Updates (2026-04-18)

- `rez-payment-service`: wallet-credit BullMQ worker added (`src/worker/walletCreditWorker.ts`) — coins now correctly credited after payment capture

## Gen 23 Fixes (2026-04-18)

| Fix | File | Evidence | Repo |
|-----|------|----------|------|
| ROUTE-SEC-005: Admin Cloudinary delete ownership | `src/routes/admin/uploads.ts` | publicId prefix whitelist check on POST /delete | rez-backend |
| CRON-002: autoCheckoutWorker async onComplete | `src/workers/autoCheckoutWorker.ts` | try-catch around async CronJob callback | rez-karma-service |
| BULL-001: BullMQ removeOnComplete bounded | `src/config/jobQueues.ts` | `removeOnComplete: { count: 100 }` (was bare `true`) | rez-backend-master |
| NW-CRIT-003: Merchant page store ownership | `app/[storeSlug]/merchant/layout.tsx` | getMerchantStores() ownership check + auth error redirect | rez-now |

## Gen 29 Fixes (2026-04-18)

| Fix | File | Evidence | PR |
|-----|------|----------|-----|
| RZ-A-C2: Next.js middleware | rendez-admin/src/middleware.ts | Edge JWT verification + session cookie (12h TTL) | Rendez PR #5 |
| AB2-C1: XFF IP consistency | adBazaar/qr/scan/route.ts | XFF last-IP matches middleware exactly | AdBazaar PR #14 |
| AB3-C1: Campaign DELETE IDOR | adBazaar/campaigns/[id]/route.ts | MISJUDGMENT — ownership check existed from initial commit | — |

## Recent Updates (2026-04-17)

- `rez-shared` v1.0.2 published to npm (coin economics: net-zero 1:1, coinsEarned(), COIN_TO_RUPEE_RATE)
- `rez-backend`: 10 PRs merged (#106, #113, #114, #115, #116, #117, #118, #119, #120): JWT fix, dual authority, security fixes, hotel reviews, salon booking, home services, loyalty stamps, AI/WhatsApp
- `rez-app-consumer`: PRs #97 (auth 401 retry), #100 (Math.random → crypto.randomUUID) merged
- `rez-app-admin`: PRs #78 (admin fixes), #80 (Gen 10 audit) merged
- `rez-app-marchant`: PR #90 (Math.random → crypto.randomUUID) merged
- `Rendez`: PR #4 (auth headers + gift type mismatch) merged
- Coin economics locked: earn 1 coin/₹1, spend 1 coin = ₹1
- Ad monetization: CPA + CPM + fixed daily charge model

## Gen 24 Fixes (2026-04-17)

| Fix | File | Evidence | PR |
|-----|------|----------|-----|
| BULL-001: 5 queues bounded `{count:100}` | QueueService.ts (5 locations) | commit 79a6e723 | Direct to main |
| G-KS-C7: E11000 race → return existing record | earnRecordService.ts | Deterministic IK key + catch/return | rez-karma-service PR #17 |
| RZ-A-C1: authHeader() on 3 pages | rendez-admin/users,fraud,moderation | Bearer token in sessionStorage | Rendez PR #4 |

## Partner Apps

| App | Repo | Status |
|-----|------|--------|
| **Resturistan** | github.com/imrejaul007/restaurantapp | Local clone exists — deploy pending |
| **Rendez** | github.com/imrejaul007/Rendez | v1.0.0 — local clone exists, deploy pending |
| **AdBazaar** | github.com/imrejaul007/adBazaar | Next.js + Supabase — local clone exists, active |
| **Hotel OTA** | github.com/imrejaul007/hotel-ota | Local clone exists — deploy pending |

## In-Flight / Not Yet Deployed

| Service | Repo | Status |
|---------|------|--------|
| **rez-finance-service** | github.com/imrejaul007/rez-finance-service | In development |
| **rez-karma-service** | github.com/imrejaul007/Karma | In development |

## Internal / Undeployed (no local clone)

| Service | Repo | Notes |
|---------|------|-------|
| **vesper** | github.com/imrejaul007/vesper | Private, no local clone |
| **rez-app** | github.com/imrejaul007/rez-app | Private, no local clone (legacy?) |
| **hotel** | github.com/imrejaul007/hotel | Public, no local clone |
| **ReZ-Hotel-pms** | github.com/imrejaul007/ReZ-Hotel-pms | Private, local clone exists |

## Shared Infrastructure

| Component | Provider | Status |
|-----------|----------|--------|
| **MongoDB** | Atlas (cluster0.ku78x6g) | ✅ Live |
| **Redis** | Render Redis (red-d760rlshg0os73bd8mp0) | ✅ Live |
| **Sentry** | sentry.io (project: 4511106548301904) | ✅ Live |
| **Cloudinary** | dgqqkrsha | ✅ Live |
| **Razorpay** | Test mode active | ✅ Live |
| **SendGrid** | noreply@rez.money | ✅ Live |
| **Twilio** | SMS test mode | ✅ Live |
| **Firebase** | rez-app-e450d | ✅ Live |

## Deploy Workflow

```
Developer pushes to main
        ↓
Render auto-deploys (Webhook on push to main)
        ↓
Build → TypeScript compile → npm install → start
        ↓
Health check passes → green
Health check fails → red (auto-rollback to previous)
```

## Rollback (if needed)

If a deploy is broken:

1. Go to Render Dashboard → Service → Deploys
2. Find the last working deploy
3. Click "Redeploy" on that commit
4. Or force-revert git: `git push --force-with-lease origin <known-good-sha>:main`

## Render Auto-Deploy

All services have auto-deploy from GitHub enabled. Each push to `main` triggers a new build.
