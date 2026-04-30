# Pre-Launch Checklist
**Date:** 2026-04-30

---

## Pre-Launch Audit Results

### Status: READY TO LAUNCH (with caveats)

| Category | Status | Notes |
|----------|--------|-------|
| Timing-safe auth | ✅ Fixed | notification-events |
| Fail-fast Redis | ✅ Fixed | All 6 core services |
| Error logging | ✅ Fixed | Core services |
| Rate limiting | ✅ Fixed | Core services |
| localhost fallbacks | ✅ Fixed | All services |

---

## Must Do Before Go-Live

### 1. Rotate Credentials (CRITICAL)

Go to each dashboard and regenerate:

| Service | What to Rotate |
|---------|---------------|
| MongoDB Atlas | Database password |
| SendGrid | API keys |
| Sentry | DSN (regenerate) |
| All services | JWT_SECRET |

### 2. Enable MongoDB AUTH

Update `MONGODB_URI` in Render dashboard:
```
mongodb+srv://admin:PASSWORD@cluster.mongodb.net/rez?authSource=admin
```

### 3. Enable Redis AUTH

Update `REDIS_URL` in Render dashboard:
```
redis://:PASSWORD@host:6379
```

---

## Quick Verification

```bash
# Check health endpoints
curl https://rez-auth-service.onrender.com/health
curl https://rez-order-service.onrender.com/health
curl https://rez-payment-service.onrender.com/health
curl https://rez-wallet-service.onrender.com/health

# Expected: {"status":"ready"}
```

---

## Post-Launch Monitoring

### Set up alerts in Sentry
- [ ] Error rate > 1%
- [ ] Response time > 2s
- [ ] Memory > 80%

### Set up Prometheus alerts
- [ ] Service down > 1m
- [ ] Error rate spike
- [ ] Queue backlog > 1000

---

## Launch Steps

1. ✅ Code audit complete
2. ⏳ Rotate credentials
3. ⏳ Enable MongoDB AUTH
4. ⏳ Enable Redis AUTH
5. ⏳ Update env vars in Render
6. ⏳ Deploy all services
7. ⏳ Verify health checks
8. ✅ GO LIVE
