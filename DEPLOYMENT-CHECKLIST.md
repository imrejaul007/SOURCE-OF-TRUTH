# WEEK 4: DEPLOYMENT & TESTING

**Date:** 2026-05-02
**Status:** READY TO DEPLOY

---

## DEPLOYMENT CHECKLIST

```
╔═══════════════════════════════════════════════════════════════════════════════════════╗
║                                                                                   ║
║                    WEEK 4: TESTING & DEPLOYMENT                               ║
║                                                                                   ║
╚═══════════════════════════════════════════════════════════════════════════════════════╝
```

---

## PHASE 1: DEPLOY SERVICES

### REZ Mind Services (Render)

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ STEP 1: Deploy these services on Render                                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  1. REZ-user-intelligence-service                                        │
│     GitHub: imrejaul007/REZ-user-intelligence-service                    │
│     Port: 3004                                                             │
│                                                                             │
│  2. REZ-intent-predictor                                                │
│     GitHub: imrejaul007/REZ-intent-predictor                            │
│     Port: 4018                                                             │
│                                                                             │
│  3. REZ-support-copilot ⭐ NEW                                           │
│     GitHub: imrejaul007/REZ-support-copilot                              │
│     Port: 4033                                                             │
│                                                                             │
│  4. REZ-action-engine                                                    │
│     GitHub: imrejaul007/REZ-action-engine                                │
│     Port: 4009                                                             │
│                                                                             │
│  5. REZ-feedback-service                                                 │
│     GitHub: imrejaul007/REZ-feedback-service                             │
│     Port: 4010                                                             │
│                                                                             │
│  6. REZ-ad-copilot                                                       │
│     GitHub: imrejaul007/REZ-ad-copilot                                  │
│     Port: 4023                                                             │
│                                                                             │
│  7. REZ-merchant-intelligence-service (redeploy)                          │
│     Already fixed, just redeploy                                           │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### New Services (Render)

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ STEP 2: Deploy new services                                              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  8. rez-knowledge-base-service                                           │
│     GitHub: imrejaul007/rez-knowledge-base-service                      │
│     Port: 4005                                                             │
│                                                                             │
│  9. rez-unified-chat (optional, can be npm package)                      │
│     GitHub: imrejaul007/rez-unified-chat                                │
│                                                                             │
│  10. rez-admin-training-panel                                            │
│      GitHub: imrejaul007/rez-admin-training-panel                      │
│      Vercel recommended (React app)                                       │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Environment Variables (All Services)

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ STEP 3: Set environment variables                                         │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  REZ-SUPPORT-COPILOT:                                                     │
│  ├── MONGODB_URI=mongodb+srv://...                                       │
│  ├── SEARCH_SERVICE_URL=https://rez-search-service.onrender.com          │
│  ├── ORDER_SERVICE_URL=https://rez-order-service.onrender.com             │
│  ├── KNOWLEDGE_BASE_URL=https://rez-knowledge-base-service.onrender.com    │
│  ├── USER_INTELLIGENCE_URL=https://REZ-user-intelligence.onrender.com   │
│  ├── REZ_EVENT_PLATFORM_URL=https://REZ-event-platform.onrender.com        │
│  └── WEBHOOK_SECRET=your-secure-secret                                  │
│                                                                             │
│  REZ-KNOWLEDGE-BASE-SERVICE:                                             │
│  ├── MONGODB_URI=mongodb+srv://...                                       │
│  └── PORT=4005                                                           │
│                                                                             │
│  REZ-MERCHANT-COPILOT:                                                   │
│  ├── REZ_ORDER_SERVICE_URL=https://rez-order-service.onrender.com       │
│  ├── REZ_CATALOG_SERVICE_URL=https://rez-catalog-service.onrender.com   │
│  ├── REZ_MERCHANT_SERVICE_URL=https://rez-merchant-service.onrender.com  │
│  └── REZ_EVENT_PLATFORM_URL=https://REZ-event-platform.onrender.com      │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## PHASE 2: TEST CONSUMER CHAT

### Test Cases

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ CONSUMER CHAT TESTS                                                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  TEST 1: Basic Chat                                                    │
│  □ User sends "Hi" → AI responds with greeting                        │
│  □ User sends "I want to order food" → Intent detected as ORDER       │
│                                                                             │
│  TEST 2: Restaurant Search                                              │
│  □ User sends "Find Italian restaurants"                                 │
│  □ AI returns list of Italian restaurants from search service             │
│  □ Results include name, rating, distance                                │
│                                                                             │
│  TEST 3: Menu Search                                                   │
│  □ User selects restaurant                                               │
│  □ User sends "What do you have for vegetarian?"                        │
│  □ AI returns vegetarian menu items                                      │
│                                                                             │
│  TEST 4: Order Flow                                                    │
│  □ User says "Order biryani"                                            │
│  □ AI confirms order details                                             │
│  □ Order created in order service                                        │
│  □ Confirmation sent to user                                             │
│                                                                             │
│  TEST 5: Booking Flow                                                   │
│  □ User says "Book a table for 4 at 8pm"                              │
│  □ AI confirms details                                                   │
│  □ Booking created                                                       │
│                                                                             │
│  TEST 6: Order Tracking                                                │
│  □ User says "Track my order"                                           │
│  □ AI asks for order ID or finds latest order                           │
│  □ Returns order status                                                  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## PHASE 3: TEST MERCHANT COPILOT

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ MERCHANT COPILOT TESTS                                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  TEST 1: Insights Dashboard                                              │
│  □ Merchant logs in                                                      │
│  □ Dashboard loads with real data                                        │
│  □ Shows orders, revenue, trends                                         │
│                                                                             │
│  TEST 2: Recommendations                                                │
│  □ AI provides menu recommendations                                     │
│  □ Based on real order data                                              │
│  □ Pricing suggestions                                                   │
│                                                                             │
│  TEST 3: Health Score                                                  │
│  □ Merchant sees health score                                            │
│  □ Score based on real metrics                                          │
│  □ Alerts for low ratings/low inventory                                 │
│                                                                             │
│  TEST 4: Real-time Updates                                              │
│  □ New order comes in                                                    │
│  □ Dashboard updates automatically                                       │
│  □ AI suggests action                                                     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## PHASE 4: TEST BACKEND INTEGRATIONS

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ BACKEND INTEGRATION TESTS                                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  TEST 1: Search Service                                                 │
│  □ REZ-support-copilot calls search service                             │
│  □ Results returned and formatted                                        │
│  □ Performance < 2 seconds                                              │
│                                                                             │
│  TEST 2: Order Service                                                  │
│  □ Order created via chat                                                │
│  □ Order appears in order service                                       │
│  □ Webhook received by support copilot                                    │
│                                                                             │
│  TEST 3: Knowledge Base                                                 │
│  □ FAQ search works                                                      │
│  □ Menu items returned                                                   │
│  □ Business info available                                               │
│                                                                             │
│  TEST 4: Event Platform                                                │
│  □ Events logged from chat                                               │
│  □ Analytics available                                                   │
│                                                                             │
│  TEST 5: Health Check                                                   │
│  □ GET /api/services/health returns all services                         │
│  □ Status of each service visible                                        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## PHASE 5: VERIFICATION CHECKLIST

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ VERIFICATION CHECKLIST                                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  FRONTEND:                                                              │
│  □ REZ NOW - Chat widget visible and working                           │
│  □ rez-app-consumer - AI chat screen accessible                        │
│  □ Hotel OTA Mobile - Support screen chat working                      │
│  □ Hotel OTA Web - Chat widget visible                                  │
│                                                                             │
│  BACKEND:                                                               │
│  □ REZ-support-copilot health check passing                             │
│  □ Search returning results                                             │
│  □ Orders being created                                                 │
│  □ Knowledge base searchable                                             │
│                                                                             │
│  MERCHANT:                                                              │
│  □ REZ-merchant-copilot showing real data                              │
│  □ Recommendations based on real metrics                                 │
│  □ Dashboard updating in real-time                                       │
│                                                                             │
│  ADMIN:                                                                 │
│  □ Admin panel deployed                                                 │
│  □ Analytics showing data                                               │
│  □ Training interface accessible                                        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## DEPLOYMENT COMMANDS

### Quick Deploy (Copy-Paste for Render)

```
DEPLOY ORDER:
1. REZ-user-intelligence-service
2. REZ-intent-predictor
3. REZ-support-copilot ⭐
4. REZ-action-engine
5. REZ-feedback-service
6. REZ-ad-copilot
7. REZ-merchant-intelligence-service (redeploy)
8. rez-knowledge-base-service
```

### Render Dashboard URLs

```
https://dashboard.render.com
```

### New Service URLs (After Deploy)

```
REZ-support-copilot:        https://REZ-support-copilot.onrender.com
REZ-knowledge-base-service:  https://rez-knowledge-base-service.onrender.com
REZ-user-intelligence:      https://REZ-user-intelligence.onrender.com
REZ-intent-predictor:        https://REZ-intent-predictor.onrender.com
REZ-action-engine:            https://REZ-action-engine.onrender.com
REZ-feedback-service:         https://REZ-feedback-service.onrender.com
REZ-ad-copilot:              https://REZ-ad-copilot.onrender.com
```

---

**Last Updated:** 2026-05-02
**Status:** READY TO DEPLOY
