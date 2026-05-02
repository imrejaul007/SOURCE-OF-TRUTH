# DEPLOYMENT TODO - WHAT NEEDS TO BE DONE

**Date:** 2026-05-02

---

## DUPLICATES ANALYSIS

### ❌ ACTUAL DUPLICATES (None - All Different Services)

```
Event Services:
  - rez-event-platform     → Main event ingestion bus
  - analytics-events       → Analytics/aggregations  
  - rez-media-events      → Media-specific events
  - rez-notification-events → Push/email events

Ad Services:
  - adBazaar              → Marketing site
  - adsqr                 → QR code ads
  - rez-ad-copilot        → AI copilot for ads
  - rez-adbazaar          → REZ Mind ad marketplace
  - rez-ads-service        → Backend ad serving
```

### ✅ NO REAL DUPLICATES - All serve different purposes

---

## DEPLOYMENT STATUS

```
╔═══════════════════════════════════════════════════════════════════════════════════════╗
║                         DEPLOYMENT STATUS                                 ║
╠═══════════════════════════════════════════════════════════════════════════════════════╣
║                                                                                   ║
║  RENDER:                                                                          ║
║  ├── DEPLOYED: 35 services                                                  ║
║  ├── DEPLOYING: 1 service                                                   ║
║  └── FAILED: 3 services                                                     ║
║                                                                                   ║
║  VERCEL:                                                                         ║
║  ├── DEPLOYED: 10 projects                                                 ║
║  └── ERROR: 1 project                                                       ║
║                                                                                   ║
╚═══════════════════════════════════════════════════════════════════════════════════════╝
```

---

## WHAT NEEDS TO BE DONE NOW

### ❌ RENDER - REDEPLOY FAILED (3)

```
1. REZ-merchant-intelligence-service
   Fix: Already pushed ✅
   Action: Just click "Redeploy" on Render Dashboard

2. hotel-ota
   Fix: Need to check build error
   Action: Check logs, fix, redeploy

3. rez-app-consumer-1
   Fix: Need to check build error
   Action: Check logs, fix, redeploy
```

### ❌ VERCEL - REDEPLOY FAILED (1)

```
1. rez-app-consumer
   Fix: Need to check build error
   Action: Check logs, fix, redeploy
```

---

## NOT DEPLOYED YET - REZ MIND (4)

```
1. REZ-action-engine
   Status: On GitHub ✅
   Action: Create new Web Service on Render
   Port: 4009
   Build: npm install && npm run build
   Start: npm start

2. REZ-feedback-service
   Status: On GitHub ✅
   Action: Create new Web Service on Render
   Port: 4010
   Build: npm install && npm run build
   Start: npm start

3. REZ-user-intelligence-service
   Status: On GitHub ✅
   Action: Create new Web Service on Render
   Port: 3004
   Build: npm install && npm run build
   Start: npm start

4. REZ-support-copilot
   Status: On GitHub ✅
   Port: 4033
   Action: Create new Web Service on Render
```

---

## ACTION PLAN

### STEP 1: Fix Failed (2 minutes)

```
RENDER DASHBOARD: https://dashboard.render.com

1. Click "REZ-merchant-intelligence-service" → Redeploy
2. Click "hotel-ota" → Check error → Fix → Redeploy
3. Click "rez-app-consumer-1" → Check error → Fix → Redeploy
```

### STEP 2: Deploy Missing REZ Mind (10 minutes)

```
RENDER DASHBOARD: https://dashboard.render.com

1. NEW → Web Service
   Name: REZ-action-engine
   GitHub: imrejaul007/REZ-action-engine
   Region: Singapore
   Branch: main
   Build Command: npm install && npm run build
   Start Command: npm start

2. NEW → Web Service
   Name: REZ-feedback-service
   GitHub: imrejaul007/REZ-feedback-service
   ...

3. NEW → Web Service  
   Name: REZ-user-intelligence-service
   GitHub: imrejaul007/REZ-user-intelligence-service
   ...

4. NEW → Web Service
   Name: REZ-support-copilot
   GitHub: imrejaul007/REZ-support-copilot
   ...
```

### STEP 3: Set Environment Variables

```
For all new services, add:
  MONGODB_URI=mongodb+srv://...
  REDIS_HOST=...
  REDIS_PASSWORD=...
  REZ_MIND_URL=https://REZ-event-platform.onrender.com
```

---

## SUMMARY

```
DEPLOYMENT PRIORITY:
1. Redeploy REZ-merchant-intelligence-service (already fixed)
2. Deploy REZ-action-engine (missing)
3. Deploy REZ-feedback-service (missing)
4. Deploy REZ-user-intelligence-service (missing)
5. Deploy REZ-support-copilot (missing)
6. Fix hotel-ota build error
7. Fix rez-app-consumer build error

TIME ESTIMATE: 15-20 minutes
```
