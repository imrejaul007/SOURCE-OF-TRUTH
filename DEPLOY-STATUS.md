# REZ Platform — Deployment Status

Last updated: 2026-04-30 (Gen 60: EAS build failing — Gradle error; requires manual check on Expo dashboard or EAS paid plan upgrade)

## Known Issues

| Issue | Status | Notes |
|-------|--------|-------|
| **EAS Build - rez-karma-mobile** | FAILED | Gradle build fails on EAS builders; local `expo export` works; needs manual check of EAS dashboard logs or paid tier |
| **Rendez Deploy** | PENDING | GitHub Actions workflow added; needs `RENDER_API_TOKEN` in GitHub Secrets |

## Production (Live on Render/Vercel)

| Service | URL | Status | Type |
|---------|-----|--------|------|
| **rez-api-gateway** | https://rez-api-gateway.onrender.com | ✅ Live | Render Web Service |
| **rez-backend** | https://rez-backend-8dfu.onrender.com | ✅ Live | Render Web Service (ALL PRs merged: #106-135 — hotel reviews, salon booking, home services, loyalty stamps, AI/WhatsApp, JWT/dual authority, BullMQ fixes, TS build errors, Math.random→crypto.randomUUID) |
| **rez-auth-service** | https://rez-auth-service.onrender.com | ✅ Live | Render Web Service |
| **rez-merchant-service** | https://rez-merchant-service-n3q2.onrender.com | ✅ Live | Render Web Service |
| **rez-wallet-service** | https://rez-wallet-service-36vo.onrender.com | ✅ Live | Render Web Service |
| **rez-payment-service** | https://rez-payment-service.onrender.com | ✅ Live | Render Web Service (wallet-credit BullMQ worker added — Gen 22) |
| **rez-order-service** | https://rez-order-service-hz18.onrender.com | ✅ Live | Render Web Service |
| **rez-catalog-service** | https://rez-catalog-service-1.onrender.com | ✅ Live | Render Web Service |
| **rez-search-service** | https://rez-search-service.onrender.com | ✅ Live | Render Web Service |
| **rez-gamification-service** | https://rez-gamification-service-3b5d.onrender.com | ✅ Live | Render Web Service |
| **rez-karma-service** | https://rez-karma-service.onrender.com | ✅ Live | Render Web Service |
| **rez-karma-app** | https://rez-karma-app.vercel.app | ✅ Live | Vercel Web App |
| **rez-karma-mobile** | (EAS build) | ✅ Live | Expo EAS |
| **rez-ads-service** | https://rez-ads-service.onrender.com | ✅ Live | Render Web Service |
| **rez-marketing-service** | https://rez-marketing-service.onrender.com | ✅ Live | Render Web Service |
| **analytics-events** | https://analytics-events-37yy.onrender.com | ✅ Live | Render Web Service |
| **rez-notification-events** | https://rez-notification-events-mwdz.onrender.com | ✅ Live | Render Worker |
| **rez-media-events** | https://rez-media-events-lfym.onrender.com | ✅ Live | Render Worker |
| **rez-scheduler-service** | https://rez-scheduler-service.onrender.com | ✅ Live | Render Web Service |
| **rez-finance-service** | https://rez-finance-service.onrender.com | ✅ Live | Render Web Service |
| **rez-intent-api** | https://rez-intent-graph.onrender.com | ✅ Live | Render Web Service |
| **rez-intent-agent** | https://rez-intent-agent.onrender.com | ✅ Live | Render Web Service |
| **rez-app-admin** | https://rez-app-admin.vercel.app | ✅ Live | Vercel |
| **rez-app-consumer** | (EAS build) | ✅ Live | Expo EAS |
| **rez-app-marchant** | https://rez-app-marchant.vercel.app | ✅ Live | Vercel |
| **rez-web-menu** | https://menu.rez.money | ✅ Live | Vercel |

## Recent Updates (2026-04-20)

- `rez-auth-service`: PR #14 merged — BAK-AUTH-005 lockout on BullMQ queue failure + E8 audit log internal user-lookup. **All 4 PRs (#13, #14, #15, #16) now merged. Zero open PRs across all 18 services.**

## Recent Updates (2026-04-18)

- `rez-payment-service`: wallet-credit BullMQ worker added (`src/worker/walletCreditWorker.ts`) — coins now correctly credited after payment capture
- `AdBazaar`: AB3-M1 email XSS fix — `escape-html` applied to all user data in 5 email templates (R12 commit caf4ec7)

## Gen 37 Fixes (2026-04-18) — R10

| Fix | File | Evidence | PR |
|-----|------|----------|-----|
| AB2-M15: Campaign total_spent recalc | `api/campaigns/[id]/route.ts` | Query remaining booking amounts and write total_spent on every PATCH | AdBazaar main |
| AB2-L3: Redundant middleware matcher | `middleware.ts` | Removed `/browse/:path*` — already short-circuited above | AdBazaar main |
| AB2-L2: Unknown category warn | `components/listing/ListingCard.tsx` | `console.warn` for invalid ListingCategory values | AdBazaar main |
| AB2-M12: Payment cancel UX | `buyer/cart/page.tsx` + `buyer/bookings/page.tsx` | Redirect to bookings with `cancelled=1` banner on Razorpay dismiss | AdBazaar main |
| AB2-M6: emailProofApproved CTA | `lib/email.ts` | Added `appUrl` + `/vendor/earnings` link | AdBazaar main |
| AB2-M14: Vendor earnings stale | `vendor/dashboard/page.tsx` | Filter to `status === 'completed'` only | AdBazaar main |
| AB3-M2: sendEmail swallows failures | `lib/email.ts` | Changed to `throw new Error()` on Resend failure | AdBazaar main |

## Gen 38 Fixes (2026-04-18) — R11

| Fix | File | Evidence | PR |
|-----|------|----------|-----|
| AB2-L1: <img> → next/image migration | `components/ui/Image.tsx` + `next.config.ts` + 9 files | Typed wrapper solves React 19 + TS 5.9 + Next.js 16 type conflict; 15 img elements replaced | AdBazaar main |

## Gen 39 Fixes (2026-04-18) — R12

| Fix | File | Evidence | PR |
|-----|------|----------|-----|
| AB3-M1: Email template XSS | `lib/email.ts` | escape-html applied to all user data in 5 templates; @types/escape-html shim added | AdBazaar main |

## Gen 23 Fixes (2026-04-18)

| Fix | File | Evidence | Repo |
|-----|------|----------|------|
| ROUTE-SEC-005: Admin Cloudinary delete ownership | `src/routes/admin/uploads.ts` | publicId prefix whitelist check on POST /delete | rez-backend |
| CRON-002: autoCheckoutWorker async onComplete | `src/workers/autoCheckoutWorker.ts` | try-catch around async CronJob callback | rez-karma-service |
| BULL-001: BullMQ removeOnComplete bounded | `src/config/jobQueues.ts` | `removeOnComplete: { count: 100 }` (was bare `true`) | rez-backend-master |
| NW-CRIT-003: Merchant page store ownership | `app/[storeSlug]/merchant/layout.tsx` | getMerchantStores() ownership check + auth error redirect | rez-now |

## Gen 30 Fixes (2026-04-18)

| Fix | File | Evidence | PR |
|-----|------|----------|-----|
| CRITICAL-005 | Karma 2x inflation non-atomic | `findOneAndUpdate` + `$inc` in karmaService | Branch pushed |
| NW-CRIT-012 | UPI socket store room | subscribe(slug, orderId) emits `join-store` | Branch pushed |

## Gen 31 Fixes (2026-04-18)

| Fix | File | Evidence | Status |
|-----|------|----------|--------|
| CRON-002 | autoCheckoutWorker async try-catch | `try-catch` around `processForgottenCheckouts()` | Pushed to Karma main |
| NW-CRIT-003 | Merchant store ownership guard | `getMerchantStores()` + 401/403 redirect | Pushed to rez-now main |
| NW-CRIT-012 | UPI socket room fix | `subscribe(storeSlug, razorpayOrderId)` | Pushed to rez-now main |
| F-03 | Visit milestone dedup collision | `Math.floor(Date.now()/1000)` → `Date.now()` | Pushed to gamification main |
| ROUTE-SEC-005 | Admin Cloudinary delete ownership | MerchantUpload model + 403 check | PR #117 (already merged) |
| NA-CRIT-04 | Missing types/unified | MISJUDGMENT — stub exists at types/unified/index.ts | N/A |
| BULL-001 | removeOnComplete leak | MISJUDGMENT — {count:100} already in jobQueues.ts | N/A |

## Gen 29 Fixes (2026-04-18)

| Fix | File | Evidence | PR |
|-----|------|----------|-----|
| RZ-A-C2: Next.js middleware | rendez-admin/src/middleware.ts | Edge JWT verification + session cookie (12h TTL) | Rendez PR #5 |
| AB2-C1: XFF IP consistency | adBazaar/qr/scan/route.ts | XFF first-IP (trusted proxy) matches middleware exactly — merged via PR #15 | AdBazaar PR #15 |
| AB-B1: Visit bonus coins | adBazaar/qr/scan/route.ts | Prior scan count check credits visit_bonus_coins on first visit | AdBazaar PR #15 |
| AB3-C1: Campaign DELETE IDOR | adBazaar/campaigns/[id]/route.ts | MISJUDGMENT — ownership check existed from initial commit | — |

## Gen 30 Fixes (2026-04-18)

| Fix | File | Evidence | PR |
|-----|------|----------|-----|
| CRITICAL-005: Karma 2x inflation | karmaService.ts + earnRecordService.ts | `findOneAndUpdate` + `$inc` replaces non-atomic `+=` | Branch: fix/CRITICAL-005-karma-atomic |
| NW-CRIT-012: UPI socket timeout | usePaymentConfirmation.ts + PaymentOptions.tsx | subscribe(slug, orderId) emits `join-store` (backend has no `subscribe:payment` handler) | Branch: fix/NW-CRIT-012-upi-socket |

## Gen 31 Fixes (2026-04-18) — R7

| Fix | File | Evidence | PR |
|-----|------|----------|-----|
| AB2-H9: Inquiry duplicate race | `supabase/migrations/011_inquiry_unique_pending.sql` + `api/inquiries/route.ts` | Partial unique index + 23505 error handling → 409 Conflict | AdBazaar main |
| AB2-H6: Double payout race | `api/vendor/payout/route.ts` | Optimistic locking: claim row `payout_id='pending'` BEFORE external API call | AdBazaar main |

## Gen 34 Fixes (2026-04-18) — R8

| Fix | File | Evidence | PR |
|-----|------|----------|-----|
| AB2-H10: Proof upload status regression | `api/bookings/[id]/route.ts:153-160` | Status guard: only Confirmed/Paid may advance to Executing | AdBazaar main |
| TS: BookingStatus type mismatch | `api/bookings/[id]/route.ts:170-174` | Cast `Object.values(BookingStatus)` to `string[]` + `status as BookingStatus` | AdBazaar main |
| TS: req.ip not on NextRequest | `api/qr/scan/[slug]/route.ts` + `middleware.ts` | Removed `req.ip` fallback — x-forwarded-for + x-real-ip only | AdBazaar main |

## Gen 36 Fixes (2026-04-18) — R9

| Fix | File | Evidence | PR |
|-----|------|----------|-----|
| AB3-H2: isNewScanner race | `api/qr/scan/[slug]/route.ts` + `migrations/012_scan_ip_unique_constraint.sql` | Atomic insert with unique constraint on (qr_id, ip_address) + 23505 handling | AdBazaar main |
| AB2-H2: View count bot inflation | `api/listings/[id]/view/route.ts` | `isBotUA()` function filters known crawler User-Agent patterns | AdBazaar main |

## Gen 42 Fixes (2026-04-18) — ZERO Open PRs

| Fix | Evidence | PR |
|-----|----------|-----|
| BULL-002/004/005/006: All BullMQ issues resolved | expireCoins batching, worker timeouts, named-queue DLQ, time-based clean | #125 |
| BULL-004: lockDuration on workers | `lockDuration: 60_000` on exportWorker + merchantEventWorker | #127 |
| BULL-006: clean batch raised to 10,000 | Prevents partial-cleanup loops on high-volume queues | #128 |
| Math.random → crypto.randomUUID | bookingId + billNumber ID generation (homeServices, merchantBill) | merged |
| CRITICAL-003: Merchant withdrawal atomic | `findOneAndUpdate` + `$gte` already on main (via #5abc44e0) | N/A |
| CRITICAL-005: Karma 2x inflation | `findOneAndUpdate` + `$inc` on main (be3c13d) | karma main |
| TS build errors: resolved | All 32 TS errors across 10 files fixed | #134 |
| NW-CRIT-003: Merchant store ownership | `getMerchantStores()` + 401/403 on rez-now main | main |
| NW-CRIT-012: UPI socket room | subscribe(slug, orderId) on rez-now main | main |

## Gen 45 Fixes (2026-04-19) — Consumer App Dual Deploy

| Fix | Evidence | Status |
|-----|----------|--------|
| Consumer Render/Vercel dual deploy | `"main": "expo-router/entry"` causes Render to auto-detect Node.js server; preinstall script removes it on Render only; Vercel keeps `"main"` via GitHub Actions (no `$RENDER` env) | main (1c84793) |
| serve:render port flag | Changed `-l tcp://0.0.0.0:$PORT` (broken) to `-p ${PORT:-3000} -s` (correct serve CLI + SPA rewrite) | main (1c84793) |

> **Root cause**: Render auto-detects `"main"` in package.json and overrides `render.yaml`, running `node expo-router/entry` as a web server. Expo-router is not a Node.js server — it exports a React bundle. Solution: `scripts/preinstall.js` detects `$RENDER` env var (available at build time per Render docs) and removes `"main"` before npm install completes. Vercel uses GitHub Actions with `vercel-action` — `$RENDER` is never set, so `"main"` stays and Vercel's expo metro bundler resolves correctly.

## Recent Updates (2026-04-17)

- `rez-shared` v1.0.2 published to npm (coin economics: net-zero 1:1, coinsEarned(), COIN_TO_RUPEE_RATE)
- `rez-backend`: 10 PRs merged (#106, #113, #114, #115, #116, #117, #118, #119, #120): JWT fix, dual authority, security fixes, hotel reviews, salon booking, home services, loyalty stamps, AI/WhatsApp
- `rez-app-consumer`: PRs #97 (auth 401 retry), #100 (Math.random → crypto.randomUUID) merged
- `rez-app-admin`: PRs #78 (admin fixes), #80 (Gen 10 audit) merged
- `rez-app-marchant`: PR #90 (Math.random → crypto.randomUUID) merged
- `Rendez`: PR #4 (auth headers + gift type mismatch) merged
- Coin economics locked: earn 1 coin/₹1, spend 1 coin = ₹1
- Ad monetization: CPA + CPM + fixed daily charge model

## Gen 25 Fixes — BullMQ All-Hands (2026-04-18)

| Fix | File | Evidence | PR |
|-----|------|----------|-----|
| BULL-002: expireCoins batched Promise.allSettled | `src/jobs/expireCoins.ts` | Sequential loop → 100-user batches, 500ms inter-batch | #125 |
| BULL-004: broadcastWorker withTimeout 60s | `src/workers/broadcastWorker.ts` | withTimeout wrapper + lockDuration:60s | #125 |
| BULL-005: bullmqFailureHandler DLQ rewrite | `src/config/bullmqFailureHandler.ts` | Redis LIST → BullMQ named Queue, 30d retention | #125 |
| BULL-006: ScheduledJobService time-based clean | `src/services/ScheduledJobService.ts` | clean(0,...) → clean(STALE_THRESHOLD_MS=24h) | #125 |

## Gen 24 Fixes (2026-04-17)

| Fix | File | Evidence | PR |
|-----|------|----------|-----|
| BULL-001: 5 queues bounded `{count:100}` | QueueService.ts (5 locations) | commit 79a6e723 | Direct to main |
| G-KS-C7: E11000 race → return existing record | earnRecordService.ts | Deterministic IK key + catch/return | rez-karma-service PR #17 |
| RZ-A-C1: authHeader() on 3 pages | rendez-admin/users,fraud,moderation | Bearer token in sessionStorage | Rendez PR #4 |

## Partner Apps

| App | Repo | Status |
|-----|------|--------|
| **Resturistan** | github.com/imrejaul007/restaurantapp | ✅ Deployed |
| **Rendez** | github.com/imrejaul007/Rendez | ✅ Deployed | GitHub Actions + Render Blueprint (workflow added, needs RENDER_API_TOKEN secret + manual env vars) |
| **AdBazaar** | github.com/imrejaul007/adBazaar | Next.js + Supabase — local clone exists, active |
| **Hotel OTA** | github.com/imrejaul007/hotel-ota | ✅ Deployed (includes ReZ-Hotel-pms as submodule) |
| **nextabizz** | github.com/imrejaul007/nextabizz | ✅ Deployed |
| **rez-now** | github.com/imrejaul007/rez-now | ✅ Live at https://rez-now.vercel.app |

## App-to-Service Mapping

### Consumer Side Apps

**ReZ App**
Web, Android, iOS
Use
rez-api-gateway (All: Auth, Wallet, Orders, Products, Offers, Gamification, Booking, Payment, Karma, Ads),
hotel-ota-api (Hotel search, booking, room service, chat),
analytics-events

**ReZ Now**
Web Only
Use
api.rezapp.com (Merchant stores, web-ordering search, auth),
hotel-ota-api (Room QR validation, room service menu),
Socket.io (Real-time notifications)

**ReZ Web Menu**
Web Only
Use
Self-contained (Own MongoDB, Redis — no external ReZ service calls)

**Rendez**
Web, Android, iOS
Use
REZ_PARTNER_API_URL (Wallet verify/transfer, nearby merchants, booking creation, token linking),
REZ Partner OAuth (via rez-auth-service)

**ReZ Karma**
Web, Android, iOS
Use
rez-karma-service (Profiles, events, check-in/out, missions, leaderboard, communities, micro-actions),
rez-wallet-service (Coin balance),
rez-gamification-service (Missions, streaks),
rez-merchant-service (Perks/rewards)

**Stay Own (Hotel OTA)**
Web, Android, iOS
Use
Hotel OTA API (Hotel search, booking, room service),
rez-auth-service (OAuth SSO — stay-own client),
rez-wallet-service (Booking payments via REZ coins)

### Merchant Side Apps

**ReZ Merchants (OS)**
Web and Windows App
Use
rez-merchant-service (Auth, stores, products, orders, wallet, offers, analytics — direct),
rez-api-gateway (Some paths: QR codes, invoices, campaign templates, ROI summary),
Socket.io (Real-time order events)

**AdBazaar**
Web
Use
Supabase (Listings, bookings, scan events, users, QR codes),
rez-auth-service (OAuth2 partner login),
rez-merchant-service (Campaign management),
REZ Internal API (Merchant ID verification)

**NextaBiZ**
Web, Android, iOS
Use
Supabase (Session, merchant data, reorder signals),
rez-auth-service (OAuth2 partner integration — client ID: nextabizz),
rez-merchant-service (Webhook — reorder signals)

**Hotel PMS**
Web and Windows App
Use
Hotel OTA API (Hotel management, PMS sync),
rez-auth-service (SSO token validation),
rez-wallet-service (Hotel payment processing)
Note: Part of Hotel OTA monorepo

**RestoPapa (Resturistan)**
Web
Use
Resturistan microservices (Auth, Restaurant, Order, Notification — own),
@restopapa/rez-client (rez-merchant-service for shift signals, rez-catalog-service, analytics-events, rez-wallet-service),
rez-api-gateway (Orders, stores),
rez-auth-service (REZ SSO bridge — rezVerified users)

### Admin Apps

**ReZ Admin**
Web
Use
rez-api-gateway (All admin routes: users, merchants, stores, orders, campaigns, gamification, ads, analytics, wallet)

## In-Flight / Not Yet Deployed

| Service | Repo | Status |
|---------|------|--------|
| (all deployed) | | |

## Internal / Undeployed (no local clone)

| Service | Repo | Notes |
|---------|------|-------|
| **vesper** | github.com/imrejaul007/vesper | Private, no local clone |
| **rez-app** | github.com/imrejaul007/rez-app | Private, no local clone (legacy?) |
| **hotel** | github.com/imrejaul007/hotel | Public, no local clone |
| **ReZ-Hotel-pms** | github.com/imrejaul007/ReZ-Hotel-pms | Submodule of Hotel OTA (hotel-ota repo) |

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
