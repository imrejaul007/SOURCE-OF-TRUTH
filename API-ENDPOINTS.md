# REZ Platform — API Endpoints

## Production Gateway

| Service | Production URL |
|---------|---------------|
| **API Gateway** | https://rez-api-gateway.onrender.com |
| **Backend (monolith)** | https://rez-backend-8dfu.onrender.com |
| **Auth Service** | https://rez-auth-service.onrender.com |

## Gateway Routes (rez-api-gateway)

The gateway proxies requests to microservices based on nginx location blocks:

```
/api/user/auth/*   → Auth microservice (OTP, login, session) — rewrites to bare paths
/api/auth/*        → Auth microservice (legacy alias) — rewrites to bare paths
/api/merchant/auth/* → Monolith (merchant auth)
/api/admin/*      → Monolith (admin APIs)
/api/orders/*     → Order microservice
/api/wallet/*     → Wallet microservice
/api/payment/*    → Payment microservice
/api/cashback/*   → Cashback forecast/claim
/api/qr-checkin/* → QR scan check-in
```

**Path rewrite**: Gateway uses `rewrite ^/api/user/auth(/.*)?$ $1 break;` — strips the
`/api/user/auth` prefix before proxying to auth service. Auth service has legacy aliases
at `/user/auth/*` to match.

## Consumer Auth (rez-auth-service) ← Primary

Consumer apps (rez-app, rez-now, web menu) use the auth microservice.
Monolith consumer auth routes at `/api/user/auth/*` are legacy dead code (never reached via gateway).

```
POST /auth/otp/send             → Send OTP via BullMQ
POST /auth/otp/verify           → Verify OTP, get JWT
POST /auth/refresh              → Refresh access token
POST /auth/token/refresh        → Token rotation (invalidate old refresh)
POST /auth/logout               → Invalidate session
GET  /auth/me                  → Get current user
PATCH /auth/profile             → Update profile
POST /auth/complete-onboarding  → Complete onboarding
DELETE /auth/account            → Delete account
POST /auth/login-pin           → PIN login (returning users)
GET  /auth/has-pin             → Check if PIN is set
POST /auth/set-pin             → Set/update PIN
POST /auth/guest               → Guest token (web menu)
POST /auth/change-phone/request → Change phone step 1
POST /auth/change-phone/verify  → Change phone step 2
POST /auth/otp/send-whatsapp   → WhatsApp OTP channel
POST /auth/email/verify/request → Request email verification
GET  /auth/email/verify/:token → Confirm email verification
GET  /auth/validate            → Validate JWT (internal only — requires X-Internal-Token)
POST /auth/admin/login         → Admin email/password + TOTP MFA
```

### Gateway legacy aliases (auth service handles rewritten paths)
```
POST /user/auth/send-otp           → /auth/otp/send
POST /user/auth/verify-otp         → /auth/otp/verify
POST /user/auth/logout             → /auth/logout
GET  /user/auth/me                 → /auth/me
PATCH /user/auth/profile           → /auth/profile
POST /user/auth/complete-onboarding → /auth/complete-onboarding
DELETE /user/auth/account         → /auth/account
POST /user/auth/login-pin          → /auth/login-pin
POST /user/auth/refresh-token     → /auth/refresh
POST /refresh-token               → /auth/refresh (bare path from gateway rewrite)
```

## Internal Service Endpoints (from rez-backend monolith)

### Merchant Auth
```
POST /api/merchant/auth/register  → Register merchant
POST /api/merchant/auth/login     → Merchant login
POST /api/merchant/auth/verify    → Verify merchant
```

### Admin Auth
```
POST /api/admin/auth/login          → Admin login (email + password)
POST /api/admin/auth/refresh-token → Refresh token
POST /api/admin/auth/logout-all-devices → Logout all devices
POST /api/admin/auth/change-password → Change password
```

### Wallet
```
GET  /api/wallet/balance           → Get balance
GET  /api/wallet/transactions     → List transactions
POST /api/wallet/credit           → Credit (admin/system)
POST /api/wallet/debit            → Debit (admin/system)
GET  /api/wallet/history           → Full history
```

### Orders
```
POST /api/orders/create            → Create order
GET  /api/orders/:id              → Get order
PUT  /api/orders/:id/status       → Update status
GET  /api/orders/history           → Order history
```

### Payments
```
POST /api/payment/initiate         → Create Razorpay order
POST /api/payment/verify          → Verify payment
POST /api/payment/refund           → Request refund
GET  /api/payment/status/:id       → Get payment status
```

### QR / Check-in
```
POST /api/qr-checkin/scan          → Scan QR, earn coins
POST /api/qr-checkin/self-report  → Self-report amount
GET  /api/qr-checkin/history       → Check-in history
```

### Cashback
```
GET  /api/cashback/forecast        → Forecast earnings
POST /api/cashback/claim          → Claim available cashback
```

## Microservice Endpoints (direct URLs)

### rez-auth-service
```
POST /auth/otp/send              → Send OTP (BullMQ)
/auth/otp/verify             → Verify OTP, get JWT
POST /auth/refresh             → Refresh access token
POST /auth/token/refresh      → Token rotation
POST /auth/logout             → Invalidate session
GET  /auth/me                 → Get current user
PATCH /auth/profile            → Update profile
POST /auth/complete-onboarding → Complete onboarding
DELETE /auth/account          → Delete account
POST /auth/login-pin          → PIN login
GET  /auth/has-pin           → Check PIN
POST /auth/set-pin           → Set/update PIN
POST /auth/guest             → Guest token
POST /auth/change-phone/request → Change phone step 1
POST /auth/change-phone/verify  → Change phone step 2
POST /auth/otp/send-whatsapp → WhatsApp OTP
POST /auth/email/verify/request → Request email verification
GET  /auth/email/verify/:token → Confirm email
GET  /auth/validate          → Validate JWT (internal)
POST /auth/admin/login       → Admin email+password login
```

### rez-auth-service — Legacy aliases (gateway-rewritten paths)
```
POST /user/auth/send-otp
POST /user/auth/verify-otp
POST /user/auth/logout
GET  /user/auth/me
PATCH /user/auth/profile
POST /user/auth/complete-onboarding
DELETE /user/auth/account
POST /user/auth/login-pin
POST /user/auth/refresh-token
POST /refresh-token           (bare path — gateway strips /api/user/auth/)
```

### rez-merchant-service
```
POST /merchant/register
POST /merchant/login
GET  /merchant/profile
PUT  /merchant/profile
GET  /merchant/stores
POST /merchant/stores
GET  /merchant/stores/:id
PUT  /merchant/stores/:id
```

### rez-wallet-service
```
GET  /wallet/:userId/balance
GET  /wallet/:userId/transactions
POST /wallet/credit
POST /wallet/debit
GET  /wallet/:userId/history
GET  /merchant-wallet/:merchantId/balance
GET  /merchant-wallet/:merchantId/transactions
POST /merchant-wallet/credit
POST /merchant-wallet/debit
POST /internal/referral/verify
GET  /internal/credit-score/:userId
```

### rez-payment-service
```
POST /payments/initiate
POST /payments/verify
POST /payments/refund
GET  /payments/:id
GET  /payments/user/:userId
```

### rez-order-service
```
GET  /orders                        → List orders (authenticated user's)
GET  /orders/:id                    → Get order
POST /orders/:id/cancel             → Cancel order
GET  /orders/stream                 → SSE live order updates
GET  /internal/orders/summary/:userId → Internal: per-user summary
```
Note: order *creation* (`POST /api/orders`) is currently served by the monolith
(`rezbackend`). The rez-order-service does not expose a creation endpoint — the
gateway's `/api/orders` route would need to change (or this service would need a
handler added) to fully strangle the monolith.

### rez-catalog-service
```
GET  /products
POST /products
GET  /products/:id
PUT  /products/:id
DELETE /products/:id
GET  /categories
POST /categories
GET  /search
```

### rez-search-service
```
GET  /search?q=...
GET  /search/products?q=...
GET  /search/merchants?q=...
```

### rez-gamification-service
```
GET  /gamification/points/:userId
POST /gamification/earn
POST /gamification/redeem
GET  /gamification/leaderboard
GET  /gamification/missions
```

### analytics-events
```
POST /events/track
POST /events/batch
GET  /events/user/:userId
```

## Service-to-Service Auth

All internal service calls require header:
```
X-Internal-Token: <INTERNAL_SERVICE_TOKEN>
```

## Correlation / Tracing

```
X-Correlation-ID: <uuid>   → propagated across all services
X-Request-ID: <uuid>        → per-request ID
```
