# REZ Platform — Deployment Status
**Last Updated:** 2026-05-02 (REZ MIND deployment in progress)

## 🚨 COMMON DEPLOYMENT FIXES (Must Read!)

When deploying REZ MIND services to Render, apply these fixes BEFORE pushing to GitHub:

### Fix 1: Move @types to dependencies (ALL services)
**Problem:** TypeScript type definitions in `devDependencies` are not installed during Render build.

**Solution:** Move these from `devDependencies` to `dependencies` in `package.json`:
```json
"dependencies": {
  "@types/express": "^4.17.21",
  "@types/node": "^20.0.0",
  "@types/uuid": "^10.0.0",
  "typescript": "^5.3.2",
  // ... other dependencies
}
```

### Fix 2: Add types to tsconfig.json (ALL TypeScript services)
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

### Fix 3: Fix TypeScript 7 deprecation warnings (ALL TypeScript services)
**Problem:** `moduleResolution: "node"` and `baseUrl` are deprecated in TypeScript 7.

**Solution:** Add `"ignoreDeprecations": "5.0"` and remove deprecated options:
```json
{
  "compilerOptions": {
    "ignoreDeprecations": "5.0",
    // Remove: moduleResolution, baseUrl, paths
  }
}
```

### Fix 4: Relax strict mode (if build fails with type errors)
**Problem:** Strict TypeScript checking fails on incomplete code.

**Solution:** Set `"strict": false` in tsconfig:
```json
{
  "compilerOptions": {
    "strict": false,
    "noImplicitAny": false,
    "strictNullChecks": false
  }
}
```

### Fix 5: Remove @rez/shared dependency (rez-event-platform, rez-action-engine, etc.)
**Problem:** `@rez/shared` is not published to npm.

**Solution:** Remove from `package.json`:
```json
"dependencies": {
  // "@rez/shared": "^1.0.0", // Not published - remove
}
```

### Fix 6: Add connectRedis export (rez-event-platform, rez-action-engine, etc.)
**Problem:** Missing `connectRedis` and `disconnectRedis` exports in redis.ts.

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

### Fix 7: Use union type for event validation (rez-event-platform)
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

### Fix 8: Add missing interface properties (REZ-merchant-intelligence-service)
**Problem:** MerchantProfile interface missing intelligence properties.

**Solution:** Add to `src/types/index.ts`:
```typescript
export interface MerchantProfile {
  // ... existing properties
  revenuePatterns?: RevenuePatterns;
  orderVolume?: OrderVolume;
  popularItems?: PopularItems;
  customerDemographics?: CustomerDemographics;
  peakHoursDays?: PeakHoursDays;
  inventoryPatterns?: InventoryPatterns;
  seasonalTrends?: SeasonalTrends;
  growthMetrics?: GrowthMetrics;
  healthSignals?: HealthSignals;
}
```

### Fix 9: Make functions async (REZ-merchant-intelligence-service)
**Problem:** `await` used in non-async function.

**Solution:** Add `async` and `Promise<>` return type:
```typescript
private async calculateMarketPosition(...): Promise<MarketPosition> {
  // now await works here
}
```

---

## Service-Specific Notes

### REZ-merchant-intelligence-service
- CLAUDE.md created with deployment instructions
- Required fixes: #1, #2, #3, #4, #8, #9

### REZ-user-intelligence-service
- Required fixes: #1, #2, #3, #4

### REZ-intelligence-hub
- Required fixes: #1, #2, #3, #4

### Plain JavaScript services (no TypeScript fixes needed)
- REZ-intent-predictor
- REZ-recommendation-engine
- REZ-personalization-engine
- REZ-push-service
- REZ-adbazaar
- REZ-feature-flags

---

## REZ MIND - First Closed Loop Services

### Tier 1 - CRITICAL (Deployed ✅)
| Service | GitHub | Port | Latest Commit | Status |
|---------|--------|------|-------------|--------|
| rez-event-platform | [Link](https://github.com/imrejaul007/rez-event-platform) | 4008 | `ad857e9` | ✅ Deployed |
| rez-action-engine | [Link](https://github.com/imrejaul007/rez-action-engine) | 4009 | `34b0d0e` | ✅ Deployed |
| rez-feedback-service | [Link](https://github.com/imrejaul007/rez-feedback-service) | 4010 | `42c30e3` | ✅ Deployed |
| rez-first-loop | [Link](https://github.com/imrejaul007/rez-first-loop) | Worker | `e9b69c4` | ✅ Deployed |

### Tier 2 - Intelligence
| Service | GitHub | Port | Latest Commit | Status |
|---------|--------|------|-------------|--------|
| rez-user-intelligence | [REZ-user-intelligence-service](https://github.com/imrejaul007/REZ-user-intelligence-service) | 3004 | `dc451c5` | 🔄 Deploying |
| rez-merchant-intelligence | [REZ-merchant-intelligence-service](https://github.com/imrejaul007/REZ-merchant-intelligence-service) | 4012 | `bef714c` | 🔄 Deploying |
| rez-intent-predictor | [REZ-intent-predictor](https://github.com/imrejaul007/REZ-intent-predictor) | 4018 | - | 🔄 Deploying |
| rez-intelligence-hub | [REZ-intelligence-hub](https://github.com/imrejaul007/REZ-intelligence-hub) | 4020 | `421aeb4` | 🔄 Deploying |

### Tier 3 - Delivery
| Service | GitHub | Port | Latest Commit | Status |
|---------|--------|------|-------------|--------|
| rez-targeting-engine | [REZ-targeting-engine](https://github.com/imrejaul007/REZ-targeting-engine) | 3003 | `80cc62c` | 🔄 Deploying |
| rez-recommendation-engine | [REZ-recommendation-engine](https://github.com/imrejaul007/REZ-recommendation-engine) | 3001 | - | 🔄 Deploying |
| rez-personalization-engine | [REZ-personalization-engine](https://github.com/imrejaul007/REZ-personalization-engine) | 4017 | - | 🔄 Deploying |
| rez-push-service | [REZ-push-service](https://github.com/imrejaul007/REZ-push-service) | 4013 | - | 🔄 Deploying |

### Tier 4 - Dashboards
| Service | GitHub | Port | Latest Commit | Status |
|---------|--------|------|-------------|--------|
| rez-merchant-copilot | [REZ-merchant-copilot](https://github.com/imrejaul007/REZ-merchant-copilot) | 4022 | `37f6bb4` | 🔄 Deploying |
| rez-consumer-copilot | [REZ-consumer-copilot](https://github.com/imrejaul007/REZ-consumer-copilot) | 4021 | `f82b55e` | 🔄 Deploying |
| rez-adbazaar | [REZ-adbazaar](https://github.com/imrejaul007/REZ-adbazaar) | 4025 | - | 🔄 Deploying |
| rez-feature-flags | [REZ-feature-flags](https://github.com/imrejaul007/REZ-feature-flags) | 4030 | - | 🔄 Deploying |
| rez-observability | [REZ-observability](https://github.com/imrejaul007/REZ-observability) | 4031 | `d3d3bee` | 🔄 Deploying |

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

## Backend Services (Already Deployed ✅)

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

## Quick Links

- [Render Dashboard](https://dashboard.render.com)
- [MongoDB Atlas](https://cloud.mongodb.com)
- [GitHub Organization](https://github.com/imrejaul007)
