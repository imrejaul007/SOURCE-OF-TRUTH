# REZ Mind - Remaining Gaps & Implementation Plan

**Version:** 1.0.0
**Date:** 2026-05-02

---

## Architecture Decision: KEEP 16 SEPARATE SERVICES

After analysis, **keeping 16 services separate** is recommended because:
- Better isolation (failure doesn't cascade)
- Independent scaling per service
- Clear separation of concerns
- Easier to debug specific issues
- Industry best practice for microservices

---

## Current Status: WHAT'S DONE

### Integrated with REZ Mind (7 services)
| Service | Status | Webhooks |
|---------|--------|----------|
| rez-order-service | ✅ Done | order.completed, order.placed |
| rez-search-service | ✅ Done | search.query |
| rez-payment-service | ✅ Done | payment.success |
| rez-app-consumer | ✅ Done | orders, searches, views |
| rez-app-merchant | ✅ Done | orders, inventory, payments |
| rendez | ✅ Done | meetup.book |
| rez-now | ✅ Done | orders, scans, searches |

### REZ Mind Services (16 total)
| Service | Port | Status |
|---------|------|--------|
| Event Platform | 4008 | ✅ Ready |
| Action Engine | 4009 | ✅ Ready |
| Feedback Service | 4010 | ✅ Ready |
| User Intelligence | 3004 | ✅ Ready |
| Merchant Intelligence | 4012 | ✅ Ready |
| Intent Predictor | 4018 | ✅ Ready |
| Intelligence Hub | 4020 | ✅ Ready |
| Targeting Engine | 3003 | ✅ Ready |
| Recommendation Engine | 3001 | ✅ Ready |
| Personalization Engine | 4017 | ✅ Ready |
| Push Service | 4013 | ✅ Ready |
| Merchant Copilot | 4022 | ✅ Ready |
| Consumer Copilot | 4021 | ✅ Ready |
| AdBazaar | 4025 | ✅ Ready |
| Feature Flags | 4030 | ✅ Ready |
| Observability | 4031 | ✅ Ready |

---

## GAPS: WHAT'S MISSING

### 1. Missing Webhooks in Event Platform

```
❌ /webhook/auth/signup          - User registration
❌ /webhook/auth/login           - User login
❌ /webhook/auth/logout          - User logout
❌ /webhook/wallet/topup         - Wallet top-up
❌ /webhook/wallet/withdraw      - Wallet withdrawal
❌ /webhook/catalog/view         - Catalog/menu view
❌ /webhook/catalog/search       - Catalog search
❌ /webhook/merchant/signup      - Merchant registration
❌ /webhook/merchant/profile      - Merchant profile update
❌ /webhook/gamification/earn    - Points earned
❌ /webhook/gamification/redeem   - Points redeemed
❌ /webhook/support/ticket        - Support ticket
❌ /webhook/support/message       - Support message
❌ /webhook/chat/message         - Chat message
❌ /webhook/loyalty/signup       - Loyalty signup
❌ /webhook/referral/made        - Referral made
```

### 2. Services Needing REZ Mind Integration

```
❌ rez-api-gateway        - Aggregate events from all services
❌ rez-auth-service       - User auth events (signup, login, logout)
❌ rez-wallet-service     - Wallet transaction events
❌ rez-catalog-service    - Menu/catalog view events
❌ rez-merchant-service   - Merchant profile events
❌ rez-gamification-service - Points/loyalty events
```

### 3. Chat & Support Intelligence

```
❌ Support tickets not linked to user intelligence
❌ Chat messages not analyzed for sentiment
❌ Support Copilot not built
❌ Response time predictions not built
❌ Smart routing based on user history not built
```

---

## IMPLEMENTATION PLAN

### Phase 1: Add Missing Webhooks to Event Platform

Add these webhooks to Event Platform:

```typescript
// src/events/webhooks/auth.ts
router.post('/webhook/auth/signup', handleAuthSignup);
router.post('/webhook/auth/login', handleAuthLogin);
router.post('/webhook/auth/logout', handleAuthLogout);

// src/events/webhooks/wallet.ts
router.post('/webhook/wallet/topup', handleWalletTopup);
router.post('/webhook/wallet/withdraw', handleWalletWithdraw);

// src/events/webhooks/catalog.ts
router.post('/webhook/catalog/view', handleCatalogView);
router.post('/webhook/catalog/search', handleCatalogSearch);

// src/events/webhooks/merchant.ts
router.post('/webhook/merchant/signup', handleMerchantSignup);
router.post('/webhook/merchant/profile', handleMerchantProfile);

// src/events/webhooks/gamification.ts
router.post('/webhook/gamification/earn', handleGamificationEarn);
router.post('/webhook/gamification/redeem', handleGamificationRedeem);

// src/events/webhooks/support.ts
router.post('/webhook/support/ticket', handleSupportTicket);
router.post('/webhook/support/message', handleSupportMessage);

// src/events/webhooks/chat.ts
router.post('/webhook/chat/message', handleChatMessage);
```

### Phase 2: Integrate Services

| Service | Events to Send | Priority |
|---------|----------------|----------|
| rez-auth-service | signup, login, logout | HIGH |
| rez-wallet-service | topup, withdraw | HIGH |
| rez-catalog-service | view, search | MEDIUM |
| rez-merchant-service | signup, profile | MEDIUM |
| rez-gamification-service | earn, redeem | LOW |

### Phase 3: Build Support Intelligence

```
1. Add support/chat webhooks to Event Platform
2. Create Support Intelligence service
3. Build Support Copilot dashboard
4. Add sentiment analysis
```

---

## WEBHOOK SCHEMAS

### Auth Events
```typescript
interface AuthSignupEvent {
  event_type: 'auth.signup';
  user_id: string;
  method: 'email' | 'google' | 'phone';
  timestamp: string;
}

interface AuthLoginEvent {
  event_type: 'auth.login';
  user_id: string;
  method: 'email' | 'google' | 'phone';
  success: boolean;
  timestamp: string;
}
```

### Wallet Events
```typescript
interface WalletTopupEvent {
  event_type: 'wallet.topup';
  user_id: string;
  amount: number;
  payment_method: string;
  balance_after: number;
  timestamp: string;
}

interface WalletWithdrawEvent {
  event_type: 'wallet.withdraw';
  user_id: string;
  amount: number;
  status: 'pending' | 'success' | 'failed';
  timestamp: string;
}
```

### Support Events
```typescript
interface SupportTicketEvent {
  event_type: 'support.ticket';
  ticket_id: string;
  user_id: string;
  category: string;
  priority: 'low' | 'medium' | 'high' | 'urgent';
  timestamp: string;
}

interface SupportMessageEvent {
  event_type: 'support.message';
  ticket_id: string;
  sender_id: string;
  sender_type: 'user' | 'agent';
  content_preview: string;
  sentiment?: 'positive' | 'neutral' | 'negative';
  timestamp: string;
}
```

### Chat Events
```typescript
interface ChatMessageEvent {
  event_type: 'chat.message';
  message_id: string;
  conversation_id: string;
  sender_id: string;
  sender_type: 'user' | 'merchant';
  context?: 'order' | 'general';
  content_preview: string;
  sentiment?: 'positive' | 'neutral' | 'negative';
  timestamp: string;
}
```

---

## PRIORITY IMPLEMENTATION

### HIGH PRIORITY (Deploy This Week)

1. **Event Platform:** Add missing webhooks
2. **rez-auth-service:** Integrate signup/login events
3. **rez-wallet-service:** Integrate topup/withdraw events

### MEDIUM PRIORITY (Deploy Next Week)

4. **rez-catalog-service:** Integrate view/search events
5. **rez-merchant-service:** Integrate signup/profile events
6. **Support webhooks:** Add to Event Platform

### LOW PRIORITY (Deploy Later)

7. **rez-gamification-service:** Integrate earn/redeem events
8. **Support Copilot:** Build dashboard
9. **Sentiment Analysis:** Add AI analysis

---

## EFFORT ESTIMATE

| Task | Effort | Dependencies |
|------|--------|--------------|
| Add 12 webhooks to Event Platform | 2 hours | None |
| Integrate rez-auth-service | 1 hour | Event Platform |
| Integrate rez-wallet-service | 1 hour | Event Platform |
| Integrate rez-catalog-service | 1 hour | Event Platform |
| Integrate rez-merchant-service | 1 hour | Event Platform |
| Integrate rez-gamification-service | 1 hour | Event Platform |
| Build Support webhooks | 2 hours | Event Platform |
| Build Support Copilot | 8 hours | All above |
| **Total** | **17 hours** | |

---

## NEXT STEPS

```
1. Add missing webhooks to Event Platform
2. Integrate auth, wallet, catalog services
3. Build support intelligence
4. Test all events flow
5. Deploy to production
```

---

**Last Updated:** 2026-05-02
