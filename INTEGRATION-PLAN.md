# REZ Ecosystem — Full Integration & Execution Plan

**Created:** 2026-04-28
**Status:** PENDING — Awaiting user approval to begin
**Scope:** Auth, Wallet, Payment integration across all ecosystem apps

---

## PART 1: AUDIT FINDINGS SUMMARY

### Canonical Services (What Should Be The Standard)

| Service | Port | Owns | Must Use |
|---------|------|------|---------|
| `rez-auth-service` | 4002 | `users` collection, OTP, JWT issuance, OAuth2 | ALL apps for identity |
| `rez-wallet-service` | 4004 | `wallets`, `ledgerentries`, `merchantwallets`, coins | ALL apps for wallet/coins |
| `rez-payment-service` | 4001 | `payments` collection, Razorpay | ALL apps for payments |
| `rez-merchant-service` | 4005 | `merchants`, `stores`, KDS, orders | ALL merchant-facing apps |

### User Types in REZ Auth

REZ Auth Service supports **two distinct user types**:

| User Type | JWT Secret | OTP Method | Scopes | Example |
|-----------|-----------|-----------|--------|---------|
| **Consumer** (`user`) | `JWT_SECRET` | Phone OTP | `profile`, `wallet:read`, `wallet:hold` | REZ App, Rendez, Stay Owen |
| **Merchant** (`merchant`) | `JWT_MERCHANT_SECRET` | Phone OTP or Password | `profile`, `wallet:read`, `wallet:hold`, `orders` | REZ Merchant App, Hotel PMS, AdBazaar |

The distinction is enforced at the **token level** — different secrets mean consumer tokens cannot access merchant endpoints and vice versa.

---

## PART 2: CURRENT STATE MATRIX

### Auth Integration Status

| App / Service | Auth Method | REZ Auth Used? | Token Storage | Risk |
|---------------|------------|----------------|---------------|------|
| **REZ App Consumer** | Own backend (rezbackend monolith) | Indirect — backend calls auth | SecureStore | MEDIUM |
| **REZ App Merchant** | Own backend (rezbackend monolith) | Indirect | SecureStore | MEDIUM |
| **REZ Now** | Own JWT via rezbackend | Indirect | httpOnly cookies | HIGH (auth bypass) |
| **REZ Web Menu** | Own backend (rezbackend monolith) | Indirect | Session/OTP | MEDIUM |
| **Rendez backend** | OAuth2 Partner SSO | YES — Full OAuth2 flow | Redis + own JWT | LOW |
| **Rendez app** | Own JWT via rendez-backend | NO — delegates to backend | SecureStore | MEDIUM |
| **Rendez admin** | Own JWT | NO | httpOnly cookies | CRITICAL (client-side signing) |
| **Hotel OTA API** | Own JWT + REZ token validation | Partial — validates tokens only | Redis + JWT | MEDIUM |
| **Hotel PMS** | Own JWT (password/bcrypt) | NO | httpOnly cookies | HIGH |
| **Hotel Panel** | Own JWT (unverified!) | NO | localStorage | CRITICAL |
| **Hotel Admin** | Own JWT (unverified!) | NO | localStorage | CRITICAL |
| **AdBazaar** | OAuth2 Partner SSO + Supabase | YES — Full OAuth2 | Supabase DB | LOW |
| **NextaBiZ** | SSO token validation + custom HMAC | Partial — validates only | Supabase auth | MEDIUM |
| **rez-merchant-service** | Own JWT (merchant secret) | NO — standalone | Redis blacklist | HIGH |
| **rez-karma-service** | Own JWT + REZ token cache | Partial — validates via HTTP | Redis cache | MEDIUM |
| **rez-auth-service** | IS THE STANDARD | — | Redis blacklist | LOW |
| **rez-wallet-service** | IS THE STANDARD | — | Redis | MEDIUM |
| **rez-payment-service** | IS THE STANDARD | — | Redis | MEDIUM |
| **rez-api-gateway** | Proxies to services | YES — validates all tokens | Redis rate-limit | MEDIUM |

### Wallet Integration Status

| App / Service | REZ Wallet? | Method |
|---------------|------------|--------|
| **REZ App Consumer** | YES | Calls rezbackend → wallet-service |
| **REZ App Merchant** | YES | Calls rezbackend → wallet-service |
| **REZ Now** | YES | Direct fallback to localhost:4005 |
| **REZ Web Menu** | YES | Via rezbackend |
| **Rendez backend** | NO | Partner API only |
| **Hotel OTA API** | YES | Direct HTTP to wallet-service `/internal/balance` |
| **AdBazaar** | NO | Scope only (`wallet:read`), no API calls |
| **NextaBiZ** | NO | None |
| **Hotel Panel** | NO | None |
| **Hotel Admin** | NO | None |
| **rez-karma-service** | YES | Direct HTTP + Redis pub/sub subscription |
| **rez-merchant-service** | PARTIAL | Reads `merchantwallets` collection directly |

### Payment Integration Status

| App / Service | Payment Method | REZ Payment Service? |
|---------------|---------------|---------------------|
| **REZ App Consumer** | Razorpay via backend | NO — routes through monolith |
| **REZ App Merchant** | Razorpay via backend | NO — routes through monolith |
| **REZ Now** | Razorpay via backend | NO — routes through monolith |
| **Hotel OTA API** | Razorpay SDK (own) | NO |
| **AdBazaar** | Razorpay SDK (own) | NO |
| **rez-payment-service** | IS THE STANDARD | YES — Razorpay integrated |
| **All others** | None | N/A |

---

## PART 3: CRITICAL SECURITY ISSUES

These must be fixed FIRST before any integration work.

### CRITICAL-1: Hotel Panel & Hotel Admin — Unverified JWTs in localStorage

**Affected:** `Hotel OTA/apps/hotel-panel`, `Hotel OTA/apps/admin`
**File:** `src/lib/api.ts` (both)
**Issue:** JWT decoded client-side with NO server-side signature verification. Token stored in localStorage (XSS-accessible).

```typescript
// CURRENT (BOTH hotel-panel and admin) — WRONG
const token = localStorage.getItem('hotel_token');
const payload = JSON.parse(atob(token.split('.')[1])); // No signature verification!
```

**Fix:** Replace with server-side JWT verification via Hotel OTA API middleware.

### CRITICAL-2: Rendez Admin — JWT Secret in Client Bundle

**Affected:** `Rendez/rendez-admin`
**File:** `src/app/login/page.tsx:16`
**Issue:** `NEXT_PUBLIC_ADMIN_JWT_SECRET` is embedded in browser JavaScript bundle. Anyone can extract it.

**Fix:** Remove `NEXT_PUBLIC_ADMIN_JWT_SECRET`. Use httpOnly cookie with server-side session only.

### CRITICAL-3: REZ Now — Auth Bypass in Middleware

**Affected:** `rez-now`
**File:** `middleware.ts:34-42`
**Issue:** Middleware only checks token PRESENCE, not validity. Any string passes the auth check.

```typescript
// CURRENT — WRONG
const token = request.cookies.get('merchant_access_token')?.value;
if (!token) return NextResponse.redirect('/login'); // Only checks presence!
```

**Fix:** Verify JWT signature server-side.

### CRITICAL-4: REZ Now — Cookie Route Validates Format, Not Signature

**Affected:** `rez-now`
**File:** `app/api/auth/set-cookies/route.ts:24-75`
**Issue:** Token format validated (3 parts, base64url) but signature is NEVER verified.

**Fix:** Add `jwt.verify()` call before setting cookies.

---

## PART 4: CROSS-SERVICE DB ACCESS (Service Boundary Violations)

These must be eliminated by replacing direct DB access with HTTP API calls.

### VIOLATION-1: rez-auth-service → `stores` collection (merchant-service owned)

**File:** `rez-auth-service/src/routes/authRoutes.ts:665`
```typescript
Stores = mongoose.connection.collection('stores'); // WRONG — merchant-service owns this
```
**Fix:** Call `REZ_MERCHANT_SERVICE_URL` via HTTP to register merchant store.

### VIOLATION-2: rez-merchant-service → `users` collection (auth-service owned)

**File:** `rez-merchant-service/src/models/User.ts`
```typescript
const UserSchema = new Schema({ /* reads auth-service's users collection */ });
```
**Fix:** Remove direct `User` model. Use `REZ_AUTH_SERVICE_URL/api/users/:id` via HTTP.

### VIOLATION-3: rez-wallet-service → `orders` collection (order-service owned)

**File:** `rez-wallet-service/src/services/merchantWalletService.ts:233`
```typescript
orders.findOne({ _id: orderId }); // Read-only, but still violates boundaries
```
**Fix:** Keep as-is (read-only for settlement), document the coupling.

### VIOLATION-4: rez-wallet-service → `payments` collection (payment-service owned)

**File:** `rez-wallet-service/src/services/merchantWalletService.ts:302`
```typescript
payments.findOne({ _id: paymentId }); // Read-only for settlement verification
```
**Fix:** Keep as-is, document the coupling.

### VIOLATION-5: rez-payment-service → `orders` collection

**File:** `rez-payment-service/src/services/paymentService.ts:233`
```typescript
orders.findOne({ razorpayOrderId }); // Read-only for amount verification
```
**Fix:** Keep as-is, document the coupling.

---

## PART 5: EXECUTION PLAN

### PHASE 1: Critical Security Fixes (Week 1) — DO FIRST

#### Step 1.1: Fix Hotel Panel & Hotel Admin Auth (CRITICAL-1)
**Files:**
- `Hotel OTA/apps/hotel-panel/src/lib/api.ts`
- `Hotel OTA/apps/admin/src/lib/api.ts`

**Action:** Replace client-side JWT decode with server-side verification via Hotel OTA API.

#### Step 1.2: Fix Rendez Admin Secret Exposure (CRITICAL-2)
**File:** `Rendez/rendez-admin/src/app/login/page.tsx`
**File:** `Rendez/rendez-admin/src/middleware.ts`

**Action:** Remove `NEXT_PUBLIC_ADMIN_JWT_SECRET`. Implement server-side session via httpOnly cookie + server-side JWT verification.

#### Step 1.3: Fix REZ Now Auth Bypass (CRITICAL-3)
**Files:**
- `rez-now/middleware.ts`
- `rez-now/app/api/auth/set-cookies/route.ts`

**Action:** Add `jwt.verify()` to middleware. Add signature verification to cookie route.

---

### PHASE 2: Canonical Auth Integration (Week 1-2) — REZ Auth as Single Source of Truth

#### Step 2.1: Register All Partner Apps in REZ Auth Service

Add these to `rez-auth-service/src/routes/oauthPartnerRoutes.ts` (`initializePartners()`):

| App | client_id | Scopes |
|-----|-----------|--------|
| `rez-now` | `rez-now` | `profile`, `wallet:read` |
| `hotel-pms` | `hotel-pms` | `profile`, `bookings` |
| `hotel-panel` | `hotel-panel` | `profile`, `hotel:manage` |
| `nextabizz` | `nextabizz` | `profile`, `merchant` |
| `rez-merchant` | `rez-merchant` | `profile`, `orders`, `inventory` |

**Files:** `rez-auth-service/src/routes/oauthPartnerRoutes.ts`

**Action:** Add environment variables for each partner's client credentials. Update `initializePartners()`.

#### Step 2.2: Update REZ Merchant Service to Use REZ Auth (Merchant Type)

**Current:** Standalone merchant JWT (`JWT_MERCHANT_SECRET`).
**Target:** OAuth2 partner flow for merchant login.

**Files to change:**
- `rez-merchant-service/src/routes/authRoutes.ts` — Replace own OTP/JWT with OAuth2 consent flow
- `rez-merchant-service/src/models/User.ts` — REMOVE direct DB access to `users` collection
- `rez-merchant-service/src/middleware/auth.ts` — Accept REZ Auth merchant tokens

**Action:**
1. Add `REZ_OAUTH_CLIENT_ID`, `REZ_OAUTH_CLIENT_SECRET`, `REZ_OAUTH_REDIRECT_URI` env vars
2. Register `rez-merchant` as OAuth2 partner in auth-service
3. Replace `User.findOne()` with `GET ${REZ_AUTH_SERVICE_URL}/api/users/:id`
4. Update `merchantAuth` middleware to verify `JWT_MERCHANT_SECRET` tokens (keep this — merchant tokens are valid)

**Note:** The `JWT_MERCHANT_SECRET` tokens issued by REZ Auth Service ARE the same tokens that `rez-merchant-service` validates. So merchant-service's `merchantAuth` middleware is already correct — it just needs the direct DB access removed.

#### Step 2.3: Update REZ Now to Use OAuth2

**Current:** Own JWT via rezbackend.
**Target:** OAuth2 partner flow to REZ Auth Service.

**Files to change:**
- `rez-now/src/app/api/auth/set-cookies/route.ts` — Replace backend token fetch with OAuth2 flow
- `rez-now/middleware.ts` — Update to verify REZ Auth tokens
- `rez-now/src/lib/auth/client.ts` — Add OAuth2 login URL construction

**Action:**
1. Register `rez-now` as OAuth2 partner
2. Replace `/api/auth/set-cookies` (fetches from backend) with OAuth2 redirect flow
3. After OAuth2 callback, exchange code → tokens → set httpOnly cookies

#### Step 2.4: Update Hotel OTA API to Use OAuth2 (Guest Login)

**Current:** Own OTP system.
**Target:** OAuth2 partner flow for guest login.

**Files to change:**
- `Hotel OTA/apps/api/src/routes/auth.ts` — Add OAuth2 initiate endpoint
- `Hotel OTA/apps/api/src/routes/oauth-callback.ts` — Add OAuth2 callback handler

**Action:**
1. Register `stay-owen` (already registered: `PARTNER_STAY_OWEN_CLIENT_ID=stay-owen`)
2. Add `/auth/oauth-login` and `/auth/oauth-callback` routes
3. Frontend redirects to REZ Auth OAuth2 flow

#### Step 2.5: Update Hotel Panel & Hotel Admin to Use OAuth2

**Current:** Own unverified JWTs.
**Target:** OAuth2 for staff login.

**Files to change:**
- `Hotel OTA/apps/hotel-panel/src/lib/api.ts`
- `Hotel OTA/apps/admin/src/lib/api.ts`
- OAuth2 routes in Hotel OTA API

**Action:** After Phase 1 security fix (Step 1.1), add OAuth2 login flow.

#### Step 2.6: Update NextaBiZ to Use OAuth2 (Merchant)

**Current:** Custom HMAC token exchange.
**Target:** OAuth2 partner flow.

**Files to change:**
- `nextabizz/apps/web/lib/auth/rez-auth.ts` — Replace token exchange with OAuth2

**Action:**
1. Register `nextabizz` as OAuth2 partner
2. Replace `exchangeCodeForToken()` with standard OAuth2 token exchange
3. Remove custom HMAC token format (JSON.stringify order issue)

---

### PHASE 3: Wallet & Payment Integration (Week 2-3)

#### Step 3.1: Add REZ Wallet to AdBazaar

**Current:** OAuth2 scope `wallet:read` requested but never used.
**Target:** Show REZ wallet balance, use coins for ad campaign credits.

**Files to change:** `adBazaar/src/app/api/wallet/` (new routes)

**Action:**
1. Call `REZ_WALLET_SERVICE_URL/internal/balance/{userId}` with `X-Internal-Token`
2. Store `rez_access_token` from OAuth2 to call `/oauth/userinfo` for userId
3. Display wallet balance in AdBazaar dashboard

#### Step 3.2: Add REZ Payment Service to AdBazaar

**Current:** Direct Razorpay integration.
**Target:** Route through `rez-payment-service`.

**Files to change:**
- `adBazaar/src/app/api/payments/` — Replace direct Razorpay with `REZ_PAYMENT_SERVICE_URL` calls

**Action:**
1. Replace `RAZORPAY_KEY_ID` / `RAZORPAY_SECRET` with `REZ_PAYMENT_SERVICE_URL`
2. Ad campaigns paid via REZ Payment Service → wallet settlement
3. Vendor payouts via wallet-service auto-settlement

#### Step 3.3: Add REZ Wallet to NextaBiZ

**Current:** No wallet integration.
**Target:** Wallet balance for merchant payouts.

**Files to change:** `nextabizz/apps/web/lib/wallet/` (new routes)

**Action:**
1. Call `REZ_WALLET_SERVICE_URL/internal/balance/{merchantId}`
2. Show merchant wallet balance
3. Future: auto-payout to wallet on PO completion

#### Step 3.4: Add REZ Payment Service to Hotel OTA

**Current:** Direct Razorpay SDK.
**Target:** Route through `rez-payment-service`.

**Files to change:** `Hotel OTA/apps/api/src/services/payment/`

**Action:**
1. Replace direct `razorpay.orders.create()` with `REZ_PAYMENT_SERVICE_URL/api/payments/initiate`
2. Replace direct `razorpay.payments.fetch()` with `REZ_PAYMENT_SERVICE_URL/api/payments/verify`
3. Wallet credit for loyalty coins on booking completion

#### Step 3.5: Update REZ Merchant Service Wallet Access

**Current:** Direct MongoDB read of `merchantwallets` collection.
**Target:** HTTP call to `REZ_WALLET_SERVICE_URL`.

**Files to change:** `rez-merchant-service/src/routes/payouts.ts`

**Action:**
1. Replace `MerchantWallet.findOne()` with `GET ${REZ_WALLET_SERVICE_URL}/internal/merchant/balance/{merchantId}`
2. Pass `X-Internal-Token` header

---

### PHASE 4: ENV Var Standardization (Week 2)

#### Step 4.1: Standardize All Env Var Names

Create a single canonical naming convention across all apps:

| Concept | Canonical Name | Used By |
|---------|--------------|---------|
| REZ Auth URL | `REZ_AUTH_SERVICE_URL` | ALL |
| REZ Wallet URL | `REZ_WALLET_SERVICE_URL` | ALL |
| REZ Payment URL | `REZ_PAYMENT_SERVICE_URL` | ALL |
| REZ Merchant URL | `REZ_MERCHANT_SERVICE_URL` | ALL |
| OAuth Client ID | `REZ_OAUTH_CLIENT_ID` | Partner apps |
| OAuth Client Secret | `REZ_OAUTH_CLIENT_SECRET` | Partner apps |
| OAuth Redirect URI | `REZ_OAUTH_REDIRECT_URI` | Partner apps |
| Internal Token | `INTERNAL_SERVICE_TOKEN` | Services |

**Current Inconsistencies to Fix:**

| Old Name | New Name | App |
|----------|----------|-----|
| `EXPO_PUBLIC_REZ_AUTH_URL` | `REZ_AUTH_SERVICE_URL` | REZ App Consumer |
| `EXPO_PUBLIC_WALLET_SERVICE_URL` | `REZ_WALLET_SERVICE_URL` | REZ App Consumer |
| `EXPO_PUBLIC_PAYMENT_SERVICE_URL` | `REZ_PAYMENT_SERVICE_URL` | REZ App Consumer |
| `NEXT_PUBLIC_API_URL` | `REZ_GATEWAY_URL` | REZ Now, Rendez |
| `WALLET_SERVICE_URL` | `REZ_WALLET_SERVICE_URL` | REZ Now |
| `localhost:4005` fallback | `REZ_WALLET_SERVICE_URL` | REZ Now |
| `https://auth.rez.money/api` | `REZ_AUTH_SERVICE_URL` | NextaBiZ |

**Files to update:**
- `rez-app-consumer/config/env.ts` and `.env.production.example`
- `rez-now/.env.example`
- `nextabizz/apps/web/.env.example`
- `Hotel OTA/apps/api/.env.example`

---

### PHASE 5: Service Boundary Cleanup (Week 3)

#### Step 5.1: Remove Cross-Service DB Writes from rez-auth-service

**File:** `rez-auth-service/src/routes/authRoutes.ts:665`
**Change:** Replace `Stores = mongoose.connection.collection('stores')` with HTTP call to `REZ_MERCHANT_SERVICE_URL/api/internal/merchants/register`.

#### Step 5.2: Remove Cross-Service DB Reads from rez-merchant-service

**File:** `rez-merchant-service/src/models/User.ts`
**Change:** Remove the `User` model entirely. Replace all `User.findOne()` calls with `GET ${REZ_AUTH_SERVICE_URL}/api/users/:id`.

#### Step 5.3: Document Shared Collections

Create `docs/SHARED-COLLECTIONS.md` documenting:
- Which service owns each collection
- Read-only access patterns (which services read which collections)
- Migration plan for HTTP-API replacement

---

## PART 6: PRIORITY MATRIX

| Priority | Step | What | Effort | Risk |
|----------|------|------|--------|------|
| P0 | 1.1 | Hotel Panel/Admin — unverified JWT | 2h | CRITICAL |
| P0 | 1.2 | Rendez Admin — secret in bundle | 2h | CRITICAL |
| P0 | 1.3 | REZ Now — auth bypass | 1h | CRITICAL |
| P1 | 2.1 | Register all partner apps in auth-service | 1h | LOW |
| P1 | 2.2 | REZ Merchant → REZ Auth (remove User model) | 4h | MEDIUM |
| P1 | 2.3 | REZ Now → OAuth2 | 4h | MEDIUM |
| P1 | 3.4 | Hotel OTA → REZ Payment Service | 3h | MEDIUM |
| P2 | 2.4 | Hotel OTA API → OAuth2 guest login | 3h | MEDIUM |
| P2 | 3.1 | AdBazaar → REZ Wallet | 3h | LOW |
| P2 | 3.2 | AdBazaar → REZ Payment Service | 3h | LOW |
| P2 | 3.3 | NextaBiZ → REZ Wallet | 3h | LOW |
| P2 | 4.1 | ENV var standardization | 2h | LOW |
| P3 | 2.5 | Hotel Panel/Admin → OAuth2 | 4h | MEDIUM |
| P3 | 2.6 | NextaBiZ → OAuth2 | 3h | MEDIUM |
| P3 | 5.1 | auth-service → remove stores write | 1h | LOW |
| P3 | 5.2 | merchant-service → remove User model | 2h | MEDIUM |
| P3 | 5.3 | Document shared collections | 2h | LOW |

---

## PART 7: DEPLOYMENT SEQUENCE

```
BEFORE ANYTHING:
  1. Fix CRITICAL security issues (Phase 1)
  2. Register all partner apps in auth-service (Step 2.1)

PHASE 1 (Week 1):
  Hotel Panel → Hotel Admin → REZ Now (security fixes)

PHASE 2 (Week 1-2):
  REZ Merchant → REZ Now → Hotel OTA → NextaBiZ (OAuth2)

PHASE 3 (Week 2-3):
  AdBazaar → NextaBiZ → Hotel OTA → REZ Merchant (Wallet/Payment)

PHASE 4 (Week 2):
  ENV var standardization across all apps

PHASE 5 (Week 3):
  Service boundary cleanup
```

---

## PART 8: BLOCKERS & DEPENDENCIES

| Blocker | Blocks | Resolution |
|---------|--------|------------|
| `PARTNER_RENDEZ_CLIENT_SECRET` not set in Render | Rendez OAuth2 | Set in Render dashboard |
| `REZ_OAUTH_CLIENT_SECRET` not generated for new partners | Phases 2-3 partner apps | Generate via `openssl rand -hex 32` |
| Hotel OTA `INTERNAL_SERVICE_TOKEN` not shared | Hotel OTA → auth-service validation | Share token between services |
| `UPSTASH_REDIS_REST_URL`/`TOKEN` not set in AdBazaar | AdBazaar OAuth2 state | Set in Vercel dashboard |
| `REZ_PAYMENT_SERVICE_URL` not set anywhere | All apps in Phase 3 | Add to env vars |

---

## PART 9: FILES TO CHANGE PER STEP

### Phase 1 — Critical Security

| Step | Files |
|------|-------|
| 1.1 | `Hotel OTA/apps/hotel-panel/src/lib/api.ts`, `Hotel OTA/apps/admin/src/lib/api.ts` |
| 1.2 | `Rendez/rendez-admin/src/app/login/page.tsx`, `Rendez/rendez-admin/src/middleware.ts` |
| 1.3 | `rez-now/middleware.ts`, `rez-now/app/api/auth/set-cookies/route.ts` |

### Phase 2 — Auth Integration

| Step | Files |
|------|-------|
| 2.1 | `rez-auth-service/src/routes/oauthPartnerRoutes.ts` |
| 2.2 | `rez-merchant-service/src/models/User.ts`, `rez-merchant-service/src/routes/authRoutes.ts`, `rez-merchant-service/src/middleware/auth.ts` |
| 2.3 | `rez-now/app/api/auth/set-cookies/route.ts`, `rez-now/middleware.ts`, `rez-now/src/lib/auth/client.ts` |
| 2.4 | `Hotel OTA/apps/api/src/routes/auth.ts`, `Hotel OTA/apps/api/src/routes/oauth-callback.ts` |
| 2.5 | `Hotel OTA/apps/hotel-panel/src/lib/api.ts`, `Hotel OTA/apps/admin/src/lib/api.ts` |
| 2.6 | `nextabizz/apps/web/lib/auth/rez-auth.ts` |

### Phase 3 — Wallet/Payment

| Step | Files |
|------|-------|
| 3.1 | `adBazaar/src/app/api/wallet/balance/route.ts` (new), `adBazaar/src/app/dashboard/page.tsx` |
| 3.2 | `adBazaar/src/app/api/payments/initiate/route.ts`, `adBazaar/src/app/api/payments/verify/route.ts` |
| 3.3 | `nextabizz/apps/web/lib/wallet/` (new) |
| 3.4 | `Hotel OTA/apps/api/src/services/payment/razorpay.ts` → replace with `REZ_PAYMENT_SERVICE_URL` calls |
| 3.5 | `rez-merchant-service/src/routes/payouts.ts` |

### Phase 4 — ENV Vars

| Step | Files |
|------|-------|
| 4.1 | All `.env.example` files across all repos |

### Phase 5 — Boundary Cleanup

| Step | Files |
|------|-------|
| 5.1 | `rez-auth-service/src/routes/authRoutes.ts:665` |
| 5.2 | `rez-merchant-service/src/models/User.ts` (delete), all files importing it |
| 5.3 | New file: `SOURCE-OF-TRUTH/SHARED-COLLECTIONS.md` |

---

*Last Updated: 2026-04-28*
