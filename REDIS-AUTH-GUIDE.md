# Redis Authentication Guide
**Date:** 2026-04-30

---

## Overview

This guide shows how to enable Redis AUTH for all services.

---

## Step 1: Set Redis Password

### Option A: Redis Cloud (Redis Enterprise)

1. Go to Redis Cloud console
2. Create a new database or update existing
3. Enable "Password AUTH" in security settings
4. Copy the password

### Option B: Self-hosted Redis

Add to `redis.conf`:
```conf
requirepass YOUR_STRONG_PASSWORD_HERE
```

Then restart Redis:
```bash
sudo systemctl restart redis
```

---

## Step 2: Update Connection Strings

### Current Format:
```
redis://host:6379
```

### New Format:
```
redis://:PASSWORD@host:6379
```

---

## Step 3: Update Environment Variables

### All Services (.env)

```env
REDIS_URL=redis://:YOUR_REDIS_PASSWORD@your-redis-host:6379
```

For Redis Cloud:
```env
REDIS_URL=rediss://default:YOUR_PASSWORD@redis-cloud-host:12345
```

---

## Step 4: Update render.yaml Files

Add to each service's render.yaml:
```yaml
envVars:
  - key: REDIS_URL
    value: rediss://:YOUR_PASSWORD@your-redis-host:12345
```

---

## Verification

```bash
# Test connection
redis-cli -h your-redis-host -p 6379 -a YOUR_PASSWORD PING

# Should return: PONG
```

---

## Code Changes for TLS (Redis Cloud)

Update connection in `src/config/redis.ts`:
```typescript
export const redis = new IORedis(redisUrl, {
  // ... existing options
  tls: redisUrl.startsWith('rediss://') ? {} : undefined,
});
```

---

## Rollback

If authentication fails, temporarily set:
```env
REDIS_URL=redis://your-redis-host:6379
```

Then debug and re-enable auth.
