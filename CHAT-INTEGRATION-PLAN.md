# UNIFIED CHAT - INTEGRATION PLAN

**Date:** 2026-05-02
**Status:** Ready to Integrate

---

## CHAT SYSTEM - BOTH SIDES

```
╔═══════════════════════════════════════════════════════════════════════════════════════╗
║                                                                                   ║
║           UNIFIED CHAT FOR CONSUMERS AND MERCHANTS                        ║
║                                                                                   ║
╚═══════════════════════════════════════════════════════════════════════════════════════╝
```

---

## CONSUMER SIDE (Customer → REZ Mind)

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         CONSUMER EXPERIENCE                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  WHERE CUSTOMERS CHAT:                                                     │
│  ├── REZ NOW QR Code → Chat with restaurant                               │
│  ├── Hotel Room QR → Chat with hotel concierge                             │
│  ├── Web Menu QR → Chat with restaurant                                    │
│  ├── Consumer App → Chat for all orders/queries                          │
│  └── Ad Bazaar → Chat for ad inquiries                                   │
│                                                                             │
│  WHAT THEY CAN DO:                                                         │
│  ├── 💬 Chat - Ask questions about menu, orders, services                 │
│  ├── 📦 Order - Place orders via chat                                      │
│  ├── 📅 Book - Make reservations via chat                                 │
│  ├── ❓ Enquire - Get info about hours, location, policies                │
│  └── 😤 Complain - Report issues, get refunds                             │
│                                                                             │
│  EXAMPLES:                                                                 │
│  ├── "I'd like to order pad thai for delivery"                           │
│  ├── "Book a table for 4 at 7pm tonight"                                 │
│  ├── "What time do you close today?"                                      │
│  ├── "My food arrived cold"                                               │
│  └── "Do you have vegan options?"                                         │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## MERCHANT SIDE (Merchant → REZ Mind)

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        MERCHANT EXPERIENCE                                 │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  WHERE MERCHANTS CHAT:                                                     │
│  ├── Merchant App → AI assistant for operations                          │
│  ├── Merchant Dashboard → AI copilot for insights                         │
│  ├── Admin Panel → Full control over AI settings                         │
│  └── POS System → Quick AI assistance                                    │
│                                                                             │
│  WHAT THEY CAN DO:                                                         │
│  ├── 📊 Analytics - Get business insights & recommendations              │
│  ├── 📦 Orders - Manage & respond to orders                             │
│  ├── 📈 Marketing - Get campaign suggestions                              │
│  ├── 📚 Training - Upload menus, FAQs, policies                         │
│  └── 👥 Support - Get help with customer issues                           │
│                                                                             │
│  EXAMPLES:                                                                 │
│  ├── "What were my best selling items this week?"                         │
│  ├── "How can I improve my customer ratings?"                            │
│  ├── "Suggest a promotion for slow hours"                                │
│  ├── "Help me set up a new menu category"                                │
│  └── "What do customers complain about most?"                              │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## INTEGRATION ARCHITECTURE

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    UNIFIED CHAT INTEGRATION                              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│                         ┌─────────────────────────────────────┐           │
│                         │      REZ-SUPPORT-COPILOT             │           │
│                         │   (Central Chat Service)              │           │
│                         │                                      │           │
│                         │   Intent Detection:                  │           │
│                         │   • CUSTOMER_SUPPORT                │           │
│                         │   • MERCHANT_SUPPORT                │           │
│                         │   • ORDER_CREATE                   │           │
│                         │   • BOOKING_CREATE                 │           │
│                         │   • COMPLAINT                      │           │
│                         │   • ENQUIRY                        │           │
│                         └─────────────┬───────────────────────┘           │
│                                       │                                      │
│           ┌───────────────────────────┼───────────────────────────┐          │
│           │                           │                           │          │
│           ▼                           ▼                           ▼          │
│  ┌───────────────┐        ┌───────────────┐        ┌───────────────┐   │
│  │    USER       │        │   MERCHANT    │        │   ORDER      │   │
│  │  CONTEXT      │        │   CONTEXT     │        │   SERVICE    │   │
│  │               │        │               │        │              │   │
│  │ • Preferences │        │ • Business    │        │ • Create     │   │
│  │ • History     │        │ • Menu        │        │ • Update     │   │
│  │ • Orders      │        │ • Analytics   │        │ • Cancel     │   │
│  │ • Feedback    │        │ • Settings    │        │ • Track      │   │
│  └───────────────┘        └───────────────┘        └───────────────┘   │
│                                                                             │
│           │                           │                           │          │
│           ▼                           ▼                           ▼          │
│  ┌───────────────┐        ┌───────────────┐        ┌───────────────┐   │
│  │    REZ-       │        │    REZ-      │        │    REZ-      │   │
│  │  KNOWLEDGE-   │        │  MERCHANT-   │        │    EVENT     │   │
│  │    BASE       │        │  INTELLIGENCE │        │  PLATFORM    │   │
│  │               │        │               │        │              │   │
│  │ • Menu Data   │        │ • Insights    │        │ • Log Events │   │
│  │ • FAQs        │        │ • Trends     │        │ • Analytics  │   │
│  │ • Policies    │        │ • Predictions │        │ • Triggers   │   │
│  └───────────────┘        └───────────────┘        └───────────────┘   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## APPS TO INTEGRATE

### Consumer Apps (Chat with Customers)

| App | Platform | Integration |
|-----|----------|------------|
| **REZ NOW** | Mobile/Web | Add UnifiedChat component |
| **Hotel Room Service** | Mobile/Web | Add UnifiedChat component |
| **Web Menu** | Mobile/Web | Add UnifiedChat component |
| **rez-app-consumer** | Mobile | Add chat screen |
| **Ad Bazaar** | Web | Add chat for ad support |

### Merchant Apps (Chat with Merchants)

| App | Platform | Integration |
|-----|----------|------------|
| **REZ-merchant-copilot** | Web | Already built - Enhance |
| **rez-app-merchant** | Mobile | Add AI copilot screen |
| **Merchant Dashboard** | Web | Add chat panel |
| **Admin Panel** | Web | Full REZ Mind control |
| **POS System** | Tablet | Quick chat widget |

---

## INTEGRATION STEPS

### Step 1: Add UnifiedChat to Consumer Apps

```
CONSUMER APP INTEGRATION:

1. REZ NOW
   ├── npm install rez-unified-chat
   ├── Import UnifiedChat component
   ├── Add to QR scan screen
   └── Configure API endpoint

2. Hotel Room Service
   ├── npm install rez-unified-chat
   ├── Import to room service screen
   └── Connect to hotel-specific knowledge base

3. Web Menu
   ├── npm install rez-unified-chat
   ├── Add floating chat button
   └── Link to restaurant knowledge base

4. rez-app-consumer
   ├── Add chat tab/screen
   ├── Import UnifiedChat component
   └── Connect to REZ-support-copilot API
```

### Step 2: Add AI Copilot to Merchant Apps

```
MERCHANT APP INTEGRATION:

1. REZ-merchant-copilot (Already exists)
   ├── Enhance with unified support features
   ├── Add analytics dashboard
   └── Connect to knowledge base

2. rez-app-merchant
   ├── Add AI copilot tab
   ├── Connect to REZ-merchant-copilot API
   └── Add quick action buttons

3. Admin Panel (rez-admin-training-panel)
   ├── Deploy to Render/Vercel
   ├── Configure all integrations
   └── Add merchant management
```

### Step 3: Configure Backend Connections

```
BACKEND CONNECTIONS:

1. REZ-support-copilot
   ├── Connect to MongoDB
   ├── Connect to Redis
   ├── Connect to REZ-event-platform
   ├── Connect to rez-order-service
   └── Connect to rez-knowledge-base-service

2. Environment Variables (all services):
   ├── REZ_MIND_URL
   ├── REZ_SUPPORT_COPILOT_URL
   ├── KNOWLEDGE_BASE_URL
   ├── MONGODB_URI
   └── REDIS_*
```

---

## FILES NEEDED

### For Consumer Apps

```
src/
├── components/
│   └── UnifiedChat.tsx ← From rez-unified-chat
├── services/
│   └── chatService.ts ← API calls
└── screens/
    └── ChatScreen.tsx ← Full page chat
```

### For Merchant Apps

```
src/
├── components/
│   └── MerchantCopilot.tsx
├── pages/
│   └── Analytics.tsx
│   └── Insights.tsx
└── services/
    └── merchantApi.ts
```

---

## QUICK INTEGRATION CODE

### Consumer App (React Native)

```javascript
// In your consumer app
import { UnifiedChat } from 'rez-unified-chat';

// Add to any screen
<UnifiedChat
  merchantId="restaurant-123"
  userId={currentUser.id}
  entryPoint="REZ_NOW" // or "HOTEL", "WEB_MENU"
  onOrderCreated={(order) => handleOrder(order)}
  onBookingCreated={(booking) => handleBooking(booking)}
/>
```

### Merchant App (React Native)

```javascript
// In your merchant app
import { MerchantCopilot } from 'REZ-merchant-copilot';

// Add AI assistant tab
<MerchantCopilot
  merchantId={currentMerchant.id}
  onInsightsUpdate={(insights) => updateDashboard(insights)}
/>
```

---

## NEXT STEPS

```
1. Add UnifiedChat to REZ NOW app
2. Add UnifiedChat to Hotel Room Service
3. Add UnifiedChat to Web Menu
4. Enhance rez-app-consumer with chat
5. Add AI copilot to rez-app-merchant
6. Deploy Admin Training Panel
7. Test end-to-end flows
```

---

**Last Updated:** 2026-05-02
**Status:** Ready to integrate
