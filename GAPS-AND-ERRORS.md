# REZ Platform — Gaps and Errors

**Last updated:** 2026-04-26
**Status:** IN PROGRESS

---

## CRITICAL GAPS (Block Launch)

### 1. API Keys Not Configured (Consumer App)

**Files affected:**
- [rez-app-consumer/eas.json](rez-app-consumer/eas.json) — Production profile

**Missing values:**
| Variable | Current Value | Required For |
|----------|---------------|--------------|
| `EXPO_PUBLIC_GOOGLE_MAPS_API_KEY` | `REQUIRED_BEFORE_LAUNCH` | Store locator, directions, map display |
| `EXPO_PUBLIC_OPENCAGE_API_KEY` | `REQUIRED_BEFORE_LAUNCH` | Geocoding, address search |
| `EXPO_PUBLIC_RAZORPAY_KEY_ID` | `REQUIRED_BEFORE_LAUNCH` | Payment processing |
| `EXPO_PUBLIC_CLOUDINARY_API_KEY` | `REQUIRED_BEFORE_LAUNCH` | Image/video uploads |
| `EXPO_PUBLIC_FIREBASE_API_KEY` | `REQUIRED_BEFORE_LAUNCH` | Push notifications |

**Action Required:**
1. Get Google Maps API key from Google Cloud Console (enable Maps SDK, Places SDK, Geocoding)
2. Get OpenCage API key from opencagedata.com
3. Get Razorpay Live Key from dashboard.razorpay.com
4. Get Cloudinary API key from cloudinary.com/console
5. Get Firebase Web API key from Firebase Console

---

### 2. Apple App Store Credentials Missing

**Files affected:**
- [rez-app-consumer/eas.json](rez-app-consumer/eas.json) — `submit.production.ios`
- [rez-app-admin/eas.json](rez-app-admin/eas.json) — `submit.production.ios`

**Missing values:**
```json
"ascAppId": "REQUIRED_BEFORE_LAUNCH"   // App Store Connect App ID
"appleTeamId": "REQUIRED_BEFORE_LAUNCH" // Apple Developer Team ID
```

**Action Required:**
1. Go to https://appstoreconnect.apple.com
2. Create apps:
   - Consumer: "REZ App", Bundle ID: `money.rez.app`
   - Admin: "Rez Admin", Bundle ID: `com.rez.admin`
3. Get App Store Connect App ID from App Information page
4. Get Team ID from https://developer.apple.com/account

---

### 3. Google Play Console Setup Incomplete

**Files affected:**
- [rez-app-consumer/eas.json](rez-app-consumer/eas.json) — `submit.production.android`
- [rez-app-admin/eas.json](rez-app-admin/eas.json) — `submit.production.android`
- [google-service-account.json.example](google-service-account.json.example)

**Missing:**
- `google-service-account.json` file in project roots

**Action Required:**
1. Go to https://play.google.com/console
2. Create apps:
   - Consumer: "REZ App", Package: `money.rez.app`
   - Admin: "Rez Admin", Package: `com.rez.admin`
3. Go to Settings > Developer account > API access
4. Create service account, download JSON key
5. Save as `google-service-account.json` in:
   - `rez-app-consumer/`
   - `rez-app-admin/`

---

## HIGH PRIORITY GAPS

### 4. Razorpay Not in Live Mode

**Current status:** Test mode active
**Required for:** Real payment processing

**Action Required:**
1. Complete KYC on Razorpay Dashboard
2. Submit documents for activation
3. Switch from Test to Live mode
4. Update `EXPO_PUBLIC_RAZORPAY_KEY_ID` with live key

---

### 5. Firebase Push Notifications Disabled

**Current value:** `"EXPO_PUBLIC_ENABLE_PUSH_NOTIFICATIONS": "false"`

**Impact:**
- Users won't receive push notifications
- Order updates, promotions won't reach users

**Action Required:**
1. Enable Firebase Cloud Messaging
2. Generate FCM server key
3. Configure Expo Push credentials
4. Update `EXPO_PUBLIC_ENABLE_PUSH_NOTIFICATIONS` to `"true"`

---

### 6. Web App Deploy URLs Not Finalized

**Apps missing production URLs:**
| App | Status | Notes |
|-----|--------|-------|
| Rendez | Deploy pending | `Rendez/` |
| AdBazaar | Deploy pending | `adBazaar/` |
| Stay Owen (Hotel OTA) | Deploy pending | `Hotel OTA/` |
| RestoPapa | Deploy pending | `Resturistan App/` |

**Action Required:**
1. Deploy each app to Vercel/Render
2. Update DNS records
3. Update SOURCE-OF-TRUTH documentation

---

## MEDIUM PRIORITY GAPS

### 7. Partner App SSO Integration Incomplete

| App | Auth Status | Integration Needed |
|-----|-------------|-------------------|
| Rendez | Standalone Supabase auth | REZ Partner SSO |
| Stay Owen | Standalone Prisma | REZ SSO for guest wallet |
| AdBazaar | Supabase auth | Future: REZ wallet for payouts |

**Action Required:**
- Define REZ Partner API for SSO
- Implement OAuth2 flow for partner apps

---

### 8. NextaBiZ Integration Not Connected

**Current status:** Standalone B2B SaaS

**Missing integrations:**
- No connection to REZ core services
- No connection to REZ Merchant App
- Inventory signals not flowing to merchants

**Action Required:**
- Define API contract for inventory signals
- Implement webhook to notify REZ merchants

---

### 9. Hotel PMS - RestoPapa Integration Not Built

**Current status:** Separate platforms

**Missing integration:**
- RestoPapa can't receive bookings from Stay Owen
- No unified dashboard for multi-property owners

**Action Required:**
- Implement booking sync API
- Create unified property management view

---

## LOW PRIORITY / FUTURE

### 10. Event Sourcing Not Implemented

**Current:** BullMQ for async processing (not true event sourcing)

**Gap:**
- No immutable event store
- No replay capability
- No time-travel debugging

**Recommendation:** Implement when scale demands it (estimated 6-12 months)

---

### 11. GraphQL Federation Not Planned

**Current:** REST-only architecture

**Gap:**
- Multiple round trips for complex queries
- Over-fetching of data

**Recommendation:** Consider if mobile performance becomes critical

---

### 12. Scoring Engine Standalone

**Current:** Scoring engine exists but not integrated into main flow

**Files:**
- `services/scoring-engine/`

**Recommendation:** Connect to inventory management for automatic reorder signals

---

## KNOWN ERRORS (Already Fixed)

| Issue | Status | Evidence |
|-------|--------|----------|
| TypeScript enum mismatches (RFQ, Signals) | ✅ Fixed | Commits to nextabizz |
| BullMQ memory leaks | ✅ Fixed | Commits to rez-backend |
| Math.random for IDs | ✅ Fixed | crypto.randomUUID in all apps |
| XSS in email templates | ✅ Fixed | escape-html in AdBazaar |
| Store ownership guard | ✅ Fixed | Merchant page ownership check |
| Karma 2x inflation | ✅ Fixed | Atomic operations in karma service |
| Campaign total_spent recalc | ✅ Fixed | AdBazaar API fix |

---

## SECURITY CHECKLIST

| Check | Status | Notes |
|-------|--------|-------|
| API keys secured | ⚠️ Partially | Some still as placeholders |
| No hardcoded secrets in code | ✅ Good | env vars used throughout |
| Webhook signature verification | ✅ Good | HMAC-SHA256 in place |
| IDOR protection | ✅ Good | Ownership checks added |
| Rate limiting | ⚠️ Partial | Some endpoints unprotected |
| Admin MFA | ✅ Good | TOTP enabled |
| Cloudinary ownership check | ✅ Fixed | Public ID prefix validation |

---

## TESTING GAPS

| Area | Status | Notes |
|------|--------|-------|
| Unit tests | ⚠️ Limited | Most services lack tests |
| Integration tests | ❌ Missing | No CI integration tests |
| E2E tests | ⚠️ Partial | Manual testing for critical flows |
| Load testing | ❌ Missing | No performance benchmarks |
| Security testing | ⚠️ Partial | Manual security reviews |

---

## DEPLOYMENT STATUS SUMMARY

| Component | Status | Notes |
|-----------|--------|-------|
| Core Services (14) | ✅ Live | All deployed on Render |
| Event Workers (3) | ✅ Live | BullMQ workers running |
| Consumer App | ⚠️ Build Ready | Needs API keys for submission |
| Merchant App | ⚠️ Build Ready | Needs API keys for submission |
| Admin App | ⚠️ Build Ready | Needs API keys for submission |
| REZ Now | ✅ Live | Vercel |
| Web Menu | ✅ Live | Vercel |
| AdBazaar | ⚠️ Deploy Needed | Local clone exists |
| Rendez | ⚠️ Deploy Needed | Local clone exists |
| Hotel OTA | ⚠️ Deploy Needed | Local clone exists |
| RestoPapa | ⚠️ Deploy Needed | Local clone exists |
| NextaBiZ | ✅ Live | Vercel |

---

## QUICK WIN CHECKLIST

Before launch, complete these items:

- [ ] **Get all API keys** (Maps, OpenCage, Razorpay, Cloudinary, Firebase)
- [ ] **Create Apple App Store apps** (Consumer + Admin)
- [ ] **Get Apple credentials** (ascAppId, appleTeamId)
- [ ] **Set up Google Play Console** (Consumer + Admin apps)
- [ ] **Download Google service account JSON**
- [ ] **Switch Razorpay to Live mode**
- [ ] **Enable Firebase push notifications**
- [ ] **Deploy partner apps** (Rendez, AdBazaar, Hotel OTA, RestoPapa)
- [ ] **Configure DNS** for partner app domains
- [ ] **Complete App Store listings** (screenshots, descriptions, keywords)
- [ ] **Complete Play Store listings** (descriptions, screenshots, content rating)
- [ ] **Add privacy policy URL** to both stores
- [ ] **Test payment flow end-to-end**
- [ ] **Set up monitoring dashboards**
- [ ] **Create runbooks** for common incidents

---

## LAST UPDATED
- 2026-04-26: Initial gap analysis
