# REZ Platform — Deployment Status
**Last Updated:** 2026-05-02 (REZ MIND deployment in progress)

## 🚨 COMMON DEPLOYMENT FIXES (Must Read!)

When deploying REZ MIND services to Render, apply these fixes before deploying:

### Fix 1: Move @types to dependencies
**Problem:** TypeScript type definitions in `devDependencies` are not installed during Render build.

**Solution:** Move these packages from `devDependencies` to `dependencies` in `package.json`:
```json
"dependencies": {
  "@types/express": "^4.17.21",
  "@types/node": "^20.0.0",
  "@types/uuid": "^10.0.0",
  "typescript": "^5.3.2",
  // ... other dependencies
}
```

### Fix 2: Add types to tsconfig.json
**Problem:** TypeScript can't find `process` or other Node types.

**Solution:** Add `"types": ["node"]` to `tsconfig.json`:
```json
{
  "compilerOptions": {
    "types": ["node"],
    // ... other options
  }
}
```

### Fix 3: Fix TypeScript 7 deprecation warnings
**Problem:** `moduleResolution: "node"` and `baseUrl` are deprecated.

**Solution:** Add `"ignoreDeprecations": "5.0"` and remove deprecated options:
```json
{
  "compilerOptions": {
    "ignoreDeprecations": "5.0",
    // Remove: moduleResolution, baseUrl, paths
  }
}
```

### Fix 4: Remove @rez/shared dependency
**Problem:** `@rez/shared` is not published to npm.

**Solution:** Remove from `package.json` or comment it out:
```json
"dependencies": {
  // "@rez/shared": "^1.0.0", // Not published - comment out
}
```

### Fix 5: Add connectRedis export
**Problem:** Missing `connectRedis` and `disconnectRedis` exports.

**Solution:** Add to `src/config/redis.ts`:
```typescript
export async function connectRedis(): Promise<void> {
  getRedis();
  logger.info('Redis connection initialized');
}

export async function disconnectRedis(): Promise<void> {
  if (redis) {
    await redis.quit();
    logger.info('Redis disconnected');
  }
}
```

### Fix 6: Use union type for event validation
**Problem:** TypeScript error with event validation return type.

**Solution:** Use union type instead of specific event type:
```typescript
export type AnyEvent = 
  | z.infer<typeof InventoryLowEventSchema>
  | z.infer<typeof OrderCompletedEventSchema>
  | z.infer<typeof PaymentSuccessEventSchema>;

export function validateEvent(payload: unknown): AnyEvent {
  // ... validation logic
}
```

---

## REZ MIND - First Closed Loop Services

### Tier 1 - CRITICAL (Deployed)
| Service | GitHub | Port | Latest Fix Commit | Status |
|---------|--------|------|------------------|--------|
| rez-event-platform | [Link](https://github.com/imrejaul007/rez-event-platform) | 4008 | `ad857e9` | ✅ Ready |
| rez-action-engine | [Link](https://github.com/imrejaul007/rez-action-engine) | 4009 | `34b0d0e` | ✅ Ready |
| rez-feedback-service | [Link](https://github.com/imrejaul007/rez-feedback-service) | 4010 | `42c30e3` | ✅ Ready |
| rez-first-loop | [Link](https://github.com/imrejaul007/rez-first-loop) | Worker | `e9b69c4` | ✅ Ready |

### Tier 2 - Intelligence
| Service | GitHub | Port | Fixes Applied | Status |
|---------|--------|------|----------------|--------|
| rez-user-intelligence | [REZ-user-intelligence-service](https://github.com/imrejaul007/REZ-user-intelligence-service) | 3004 | ✅ | 🔄 Deploying |
| rez-merchant-intelligence | [REZ-merchant-intelligence-service](https://github.com/imrejaul007/REZ-merchant-intelligence-service) | 4012 | ✅ | 🔄 Deploying |
| rez-intent-predictor | [REZ-intent-predictor](https://github.com/imrejaul007/REZ-intent-predictor) | 4018 | N/A (JS) | 🔄 Deploying |
| rez-intelligence-hub | [REZ-intelligence-hub](https://github.com/imrejaul007/REZ-intelligence-hub) | 4020 | ✅ | 🔄 Deploying |

### Tier 3 - Delivery
| Service | GitHub | Port | Fixes Applied | Status |
|---------|--------|------|----------------|--------|
| rez-targeting-engine | [REZ-targeting-engine](https://github.com/imrejaul007/REZ-targeting-engine) | 3003 | ✅ | 🔄 Deploying |
| rez-recommendation-engine | [REZ-recommendation-engine](https://github.com/imrejaul007/REZ-recommendation-engine) | 3001 | N/A (JS) | 🔄 Deploying |
| rez-personalization-engine | [REZ-personalization-engine](https://github.com/imrejaul007/REZ-personalization-engine) | 4017 | N/A (JS) | 🔄 Deploying |
| rez-push-service | [REZ-push-service](https://github.com/imrejaul007/REZ-push-service) | 4013 | N/A (JS) | 🔄 Deploying |

### Tier 4 - Dashboards
| Service | GitHub | Port | Fixes Applied | Status |
|---------|--------|------|----------------|--------|
| rez-merchant-copilot | [REZ-merchant-copilot](https://github.com/imrejaul007/REZ-merchant-copilot) | 4022 | ✅ | 🔄 Deploying |
| rez-consumer-copilot | [REZ-consumer-copilot](https://github.com/imrejaul007/REZ-consumer-copilot) | 4021 | ✅ | 🔄 Deploying |
| rez-adbazaar | [REZ-adbazaar](https://github.com/imrejaul007/REZ-adbazaar) | 4025 | N/A (JS) | 🔄 Deploying |
| rez-feature-flags | [REZ-feature-flags](https://github.com/imrejaul007/REZ-feature-flags) | 4030 | ✅ | 🔄 Deploying |
| rez-observability | [REZ-observability](https://github.com/imrejaul007/REZ-observability) | 4031 | ✅ | 🔄 Deploying |

---

## Common Environment Variables

All REZ MIND services use these shared values:

```env
# MongoDB Atlas
MONGODB_URI=mongodb+srv://work_db_user:RmptskyDLFNSJGCA@cluster0.ku78x6g.mongodb.net/{service_db}

# Redis
REDIS_URL=redis://default:EJRABXvbLsG0WYu4tmkRnwbGZodLPLeb@redis-15692.c244.us-east-1-2.ec2.redns.redis-cloud.com:15692

# Sentry
SENTRY_DSN=https://138c07c22c015d41c23626fce16be643@o4511106544369664.ingest.de.sentry.io/4511106548301904

# Service URLs
EVENT_PLATFORM_URL=https://rez-event-platform.onrender.com
```

---

## Backend Services (Already Deployed)

| Service | GitHub | Status |
|---------|--------|--------|
| rez-backend | [rez-backend](https://github.com/imrejaul007/rez-backend) | ✅ Active |
| rez-auth-service | [rez-auth-service](https://github.com/imrejaul007/rez-auth-service) | ✅ Active |
| rez-merchant-service | [rez-merchant-service](https://github.com/imrejaul007/rez-merchant-service) | ✅ Active |
| rez-order-service | [rez-order-service](https://github.com/imrejaul007/rez-order-service) | ✅ Active |
| rez-payment-service | [rez-payment-service](https://github.com/imrejaul007/rez-payment-service) | ✅ Active |
| rez-wallet-service | [rez-wallet-service](https://github.com/imrejaul007/rez-wallet-service) | ✅ Active |
| rez-catalog-service | [rez-catalog-service](https://github.com/imrejaul007/rez-catalog-service) | ✅ Active |
| rez-gamification-service | [rez-gamification-service](https://github.com/imrejaul007/rez-gamification-service) | ✅ Active |
| rez-notification-events | [rez-notification-events](https://github.com/imrejaul007/rez-notification-events) | ✅ Active |
| analytics-events | [analytics-events](https://github.com/imrejaul007/analytics-events) | ✅ Active |
| rez-api-gateway | [rez-api-gateway](https://github.com/imrejaul007/rez-api-gateway) | ✅ Active |

---

## Deploy URLs (Production)

| Service | URL |
|---------|-----|
| API Gateway | https://rez-api-gateway.onrender.com |
| Auth Service | https://rez-auth-service.onrender.com |
| Merchant Service | https://rez-merchant-service.onrender.com |
| Order Service | https://rez-order-service.onrender.com |
| Payment Service | https://rez-payment-service.onrender.com |
| Wallet Service | https://rez-wallet-service.onrender.com |

---

## Quick Links

- [Render Dashboard](https://dashboard.render.com)
- [MongoDB Atlas](https://cloud.mongodb.com)
- [GitHub Organization](https://github.com/imrejaul007)
