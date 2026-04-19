# REZ Platform — API Endpoints

## Production Gateway

| Service | Production URL |
|---------|---------------|
| **API Gateway** | https://rez-api-gateway.onrender.com |
| **Backend (monolith)** | https://rez-backend-8dfu.onrender.com |

## Gateway Routes (rez-api-gateway)

The gateway proxies requests to microservices. Routes are defined in `src/routes/`.

```
/api/auth/*          → Consumer auth (OTP)
/api/merchant/auth/* → Merchant auth
/api/admin/*         → Admin APIs
/api/orders/*        → Order lifecycle
/api/wallet/*       → Wallet operations
/api/cashback/*      → Cashback forecast/claim
/api/qr-checkin/*    → QR scan check-in
```

## Internal Service Endpoints (from rez-backend monolith)

### Auth
```
POST /api/auth/request-otp       → Send OTP to phone
POST /api/auth/verify-otp        → Verify OTP, get JWT
POST /api/auth/refresh-token     → Refresh access token
POST /api/auth/logout             → Invalidate session
```

### Merchant Auth
```
POST /api/merchant/auth/register  → Register merchant
POST /api/merchant/auth/login     → Merchant login
POST /api/merchant/auth/verify    → Verify merchant
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
POST /auth/otp/send
POST /auth/otp/verify
POST /auth/token/refresh
POST /auth/logout
GET  /auth/me
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
