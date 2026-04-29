# WAVE 10: Merchant Service OAuth & Build Fixes
**Date:** 2026-04-30
**Status:** COMPLETE - 4 PRs merged

---

## PRs Merged

| PR # | Title | Files Changed | Issues Fixed |
|------|-------|---------------|--------------|
| #52 | feat(MERCH-AUDIT-OAUTH): mount REZ OAuth2 routes with fetch timeouts | `src/routes/oauth.ts`, `src/index.ts` | OAuth2 flow, 10s AbortController timeouts |
| #53 | feat(MERCH-AUDIT-OAUTH): add OAuth partner env vars to Zod schema | `src/config/env.ts` | OAuth env var validation |
| #54 | fix(MERCH-AUDIT): resolve build errors and npm audit conflicts | `src/config/redis.ts`, `src/routes/teamPublic.ts`, `src/models/index.ts`, `package.json` | Build errors, npm audit |
| #55 | fix(merchant-service): harden OAuth security | (see #52, #53) | OAuth security |

---

## Issues Fixed

### OAuth2 Implementation
- Full OAuth2 partner flow via REZ Auth Service
- `GET /api/merchant/oauth/authorize` → redirects to REZ Auth Service
- `GET /api/merchant/oauth/callback` → exchanges code, creates/links Merchant, issues JWT + httpOnly cookies
- `POST /api/merchant/oauth/refresh` → refreshes OAuth2 tokens
- State CSRF protection via base64-encoded JSON state
- Auto-creates default Store on new merchant creation

### Security Hardening
- All 3 external fetch calls (userinfo, token exchange, refresh) wrapped with 10s `AbortController` timeout + `try/finally` cleanup
- `__oauth_no_password__` sentinel for SSO-only merchants

### Build Fixes
- Export `ensureRedisConnected` from `redis.ts` (was used but not exported)
- Fix `getClientIp` import in `teamPublic.ts` (from `./auth` → `./auth/shared`)
- Fix `models/index.ts` barrel: 68 models used named exports, barrel expected defaults — all converted to named export style
- Fix 3 mismatched model names: `Brand`→`MerchantBrand`, `PayOut`→`Payout`, `FeatureFlag` (default)
- Remove conflicting `crypto-js` override from `package.json`

### Environment Variables Added
- `PARTNER_REZ_MERCHANT_CLIENT_ID` - OAuth2 client ID
- `PARTNER_REZ_MERCHANT_CLIENT_SECRET` - OAuth2 client secret
- `PARTNER_REZ_MERCHANT_REDIRECT_URI` - OAuth2 redirect URI

---

## Verification

```bash
# Build succeeds
cd rez-merchant-service && npm run build

# npm audit clean
npm audit

# Route file sizes under limit
find src/routes src/routers -name "*.ts" ! -name "index.ts" -exec wc -l {} + | awk '$1 > 500 {print}'
# Should return no results

# OAuth routes mounted
grep -n "oauthRouter" src/index.ts
```

---

## Source of Truth

All changes merged to `origin/main`:
- bb5e93d fix(MERCH-AUDIT): resolve build errors and npm audit conflicts (#54)
- d181a0d feat(MERCH-AUDIT-OAUTH): add OAuth partner env vars to Zod schema (#53)
- abc0382 feat(MERCH-AUDIT-OAUTH): mount REZ OAuth2 routes with fetch timeouts (#52)
- aae191e fix(merchant-service): comprehensive audit fixes round 3 (FIX-14 to FIX-19) (#51)
- d039d5a feat: add MongoDB replica set support to rez-merchant-service
- ae01eb0 fix(audit-wave8): H3 — add IDOR protection middleware (#57)

## Additional Fixes

### Order Service Build Fixes (PR #38)
| PR # | Title | Files Changed |
|------|-------|---------------|
| #38 | fix(order-service): resolve TypeScript build errors | `src/utils/cursorPagination.ts`, `src/worker.ts` |

**Order service commit:** 2f90c30 — resolved TypeScript build errors (cursorPagination unknown type, worker bullmqRedis→workerRedis)

### Additional Build Fixes Across Services

| PR # | Service | Description |
|------|---------|-------------|
| #38 | order-service | TypeScript build errors (cursorPagination, worker) |
| #39 | auth-service | models barrel named exports, authRoutes message field |
| #40 | payment-service | models barrel named exports, razorpayService params |
| #28 | wallet-service | JSON comments removed, intentGraphConsumer stub created |

## Status Summary

| Service | Build Status | Notes |
|---------|--------------|-------|
| rez-merchant-service | ✅ Pass | OAuth2 routes, 0 vulns |
| rez-order-service | ✅ Pass | Cursor pagination, worker fixes |
| rez-auth-service | ✅ Pass | Models barrel fixed |
| rez-payment-service | ✅ Pass | Models barrel fixed, razorpayService fixed |
| rez-wallet-service | ✅ Pass | Package.json fixed, intentGraphConsumer stub |
| rez-catalog-service | ✅ Pass | - |
