# REZ Platform — Local Development Ports

Every service listens on a specific local port. Use these when developing locally.

## Service Ports

| Service | Port | Local URL | Notes |
|---------|------|-----------|-------|
| **rez-api-gateway** | 5002 | http://localhost:5002 | Routes to all microservices |
| **rez-backend** | 5001 | http://localhost:5001 | Legacy monolith (fallback) |
| **rez-auth-service** | 5003 | http://localhost:5003 | Auth, OTP, JWT |
| **rez-merchant-service** | 3004 | http://localhost:3004 | Merchant CRUD, auth |
| **rez-wallet-service** | 5006 | http://localhost:5006 | Wallet, coins, balance |
| **rez-payment-service** | 5005 | http://localhost:5005 | Razorpay, refunds |
| **rez-order-service** | 3006 | http://localhost:3006 | Order lifecycle, BullMQ |
| **rez-catalog-service** | 5007 | http://localhost:5007 | Products, categories |
| **rez-search-service** | 5008 | http://localhost:5008 | Full-text search |
| **analytics-events** | 5011 | http://localhost:5011 | Event tracking |
| **rez-gamification-service** | 4003 | http://localhost:4003 | BullMQ + HTTP API |
| **rez-ads-service** | 4002 | http://localhost:4002 | HTTP API |
| **rez-marketing-service** | 3007 | http://localhost:3007 | BullMQ worker |
| **rez-notification-events** | 3009 | http://localhost:3009 | BullMQ worker |
| **rez-media-events** | 3008 | http://localhost:3008 | BullMQ worker |
| **rez-contracts** | 3001 | http://localhost:3001 | Smart contracts |
| **rez-finance-service** | 4005 | http://localhost:4005 | Finance service |
| **rez-karma-service** | 4006 | http://localhost:4006 | Karma service |
| **rez-hotel-service** | 4011 | http://localhost:4011 | Hotel OTA (Makcorps) |
| **rez-procurement-service** | 4012 | http://localhost:4012 | NextaBizz procurement |
| **rez-corpperks-service** | 4013 | http://localhost:4013 | CorpPerks API |
| **rez-now** | 4007 | http://localhost:4007 | REZ Now app |
| **rez-app-consumer** | — | — | Expo / EAS (mobile) |
| **rez-app-marchant** | — | — | Expo / EAS (mobile) |
| **rez-app-admin** | — | — | Vercel (web) |
| **rez-web-menu** | — | — | Vercel (web) |

## CORS Origins (for local dev)

```
https://rez-app-admin.vercel.app
https://rez-app-consumer.vercel.app
https://rez-app-marchant.vercel.app
https://www.rez.money
https://rez.money
https://menu.rez.money
https://admin.rez.money
https://merchant.rez.money
https://rez-web-menu.vercel.app
https://ad-bazaar.vercel.app
```

## Health Endpoints

| Service | Health URL |
|---------|-----------|
| rez-api-gateway | http://localhost:5002/health |
| rez-backend | http://localhost:5001/health |
| rez-auth-service | http://localhost:5003/health |
| rez-merchant-service | http://localhost:3004/health |
| rez-wallet-service | http://localhost:5006/health |
| rez-payment-service | http://localhost:5005/health |
| rez-order-service | http://localhost:3006/health |
| rez-catalog-service | http://localhost:5007/health |
| rez-search-service | http://localhost:5008/health |
| analytics-events | http://localhost:5011/health |
| rez-gamification-service | http://localhost:4003/health |
| rez-ads-service | http://localhost:4002/health |
| rez-marketing-service | http://localhost:3007/health |
| rez-notification-events | http://localhost:3009/health |
| rez-media-events | http://localhost:3008/health |
