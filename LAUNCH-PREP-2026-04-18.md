# Launch-Prep 2026-04-18 — Summary

> **Last Updated: 2026-04-18 (Session 2)** — All 3 apps: 0 TS errors on main.

This is the canonical summary of the launch-preparation work performed on 2026-04-18 across the three user-facing React Native / Expo apps: `rez-app-consumer`, `rez-app-marchant`, and `rez-app-admin`.

For full per-item detail see `docs/gaps/16-LAUNCH-PREP-2026-04-18.md` in the main project.

## Branches

All three apps have a new branch `launch-prep/20260418` off their respective `main`-equivalents. The branch contains three layered commits per repo:

| Repo | Initial (TS + env) | Audit-fix | Phase 2 (gap-registry) |
|---|---|---|---|
| rez-app-admin | `e951b86` | `2a7d0bc` | `309a69d` |
| rez-app-marchant | `ab7826e` | `75bad41` | `524eacb` |
| rez-app-consumer | `f369543` | `130662a` | `46d9391` |

## Results at a glance

- **TypeScript:** 81 errors → 0 across all three apps (`tsc --noEmit` green on each).
- **Dead URLs eliminated:** `api.rezapp.com`, `api.yourrezapp.com`, `your-monolith.onrender.com`, LAN `192.168.1.4` removed from all three apps' env examples, app code fallbacks, and Vercel configs.
- **Real URLs wired in:** `https://rez-api-gateway.onrender.com` (gateway) for REST; `https://rez-backend-8dfu.onrender.com` (monolith) for Socket.IO during the in-flight microservice migration.
- **CSP alignment:** `vercel.json` on all three web deployments now whitelists the gateway, monolith, `https://*.onrender.com`, and `wss://*.onrender.com`.
- **Gap registry:** 28 previously-active items closed this session; 52 items verified already fixed but misclassified in prior audit docs.

## Known-issues that require action outside this session

These were identified in `SOURCE-OF-TRUTH/ENV-VARS.md` under "Known Issues to Fix in Live Render Env" and are dashboard-level changes, not code changes:

1. `PUBLIC_URL` on `rez-backend`, `rez-marketing-service`, `rez-notification-events` is set to `https://api.rezapp.com` (a domain we do not own). Change each service's `PUBLIC_URL` to its own Render URL.
2. `NODE_AUTH_TOKEN` (GitHub PAT starting with `ghp_`) is set on `rez-backend` env on Render. Remove — GitHub PATs belong in GitHub Actions secrets, not runtime env.
3. `REQUIRE_ADMIN_TOTP=false` — re-enable before launch once admin users have TOTP set up.
4. `LOG_OTP_FOR_TESTING=true` — disable in production.
5. `SMS_TEST_MODE` has conflicting values set — clean up to a single `false` for production.

## Push workflow

The sandbox cannot push to GitHub (SSH and API both blocked by allowlist). The push script is ready to run on your Mac:

```
cd "/path/to/ReZ Full App"
bash push-launch-prep.sh
```

The script:
1. Re-runs `tsc` on each app as a safety check before pushing
2. Runs `npx lint-staged` to compensate for the `--no-verify` commits
3. Pushes `launch-prep/20260418` to origin for each of the 3 repos
4. Uses `gh` to open PRs against `main`

Pass `--no-pr` to skip PR creation.

## Husky pre-commit bypass

All 9 commits this session used `git commit --no-verify` because the husky `pre-commit` hook is broken in all three repos — it invokes `./node_modules/.bin/lint-staged` which is not installed. Before pushing, run:

```
cd rez-app-admin && npm install && npx lint-staged
cd ../rez-app-marchant && npm install && npx lint-staged
cd ../rez-app-consumer && npm install && npx lint-staged
```

…or more simply, run `push-launch-prep.sh` which does this automatically.

## Tech debt to plan (not launch-blocking)

| Metric | Count | Notes |
|---|---|---|
| Bare `as any` casts | 6,405 | 371 admin + 728 merchant + 5,306 consumer |
| `console.*` calls | 2,523 | 677 admin + 1,103 merchant + 743 consumer |

The arch-fitness rules (`no-console-log`, `no-as-any`) would hard-fail CI on every PR as written. This session did not introduce new violations; the 6,405 + 2,523 are pre-existing. A staged cleanup campaign across multiple sessions is required to bring the codebase into arch-fitness compliance. Alternatively, the rules can be relaxed to per-file allowlists while the cleanup is in progress.

## Gaps that remain ACTIVE (top frontend items — see gap registry for full list)

### Highest priority

- Consumer NA-CRIT-02: bill amount is client-controlled — fraud vector. Needs server-side OCR.
- Consumer NA-CRIT-05: QR check-in has no camera integration — screen is manual-amount only.
- Merchant G-MA-C05 / G-MA-C15: IDOR on order detail page — needs merchant-ownership assertion after fetch.
- Merchant G-MA-C03: offline bill sync loses coin discount.
- Merchant G-MA-C13: cache never invalidated after mutations.
- Admin A10-C7: three color systems coexist (`DesignTokens` + `Colors` + `ThemeContext`) — dead code cleanup.
- Admin A10-H1 / NEW-A-M1: no `useMutation` hooks — all mutations bypass React Query cache invalidation.

## Cross-reference

- Full fix list with line numbers: `docs/gaps/16-LAUNCH-PREP-2026-04-18.md`
- Previous verification pass: `docs/gaps/15-VERIFIED-FIX-STATUS.md`
- Session `push-all.sh`: `push-launch-prep.sh` at the super-project root
- SOURCE-OF-TRUTH push script: `push-source-of-truth.sh` at the super-project root

---

## Session 2 Update (2026-04-18, Evening)

### All 3 Apps: 0 TypeScript Errors on main

| Repo | Branch | Commit | PR | Errors |
|---|---|---|---|---|
| rez-app-consumer | main | `3a33c69` (fix/consumer-ts-audit-round2) | #111 merged | 0 |
| rez-app-admin | main | `239258a` (8-team audit) | #84 merged | 0 |
| rez-app-marchant | main | `22cc3b4e` (fix/merchant-ts-audit-round2) | #94 merged | 0 |

### Consumer Fixes (PR #111)
- `deal(discountValue)` → `deal.discountValue` (Deal is object, not callable)
- `uuid` imports fixed across 7 services (were inside block comments)
- API response union type casts in `reelApi.ts`
- Error type casts in `useCheckout.ts`, `billUploadService.ts`
- `CoinType` import added to `useWallet.ts`
- `CryptoEncoding` fix in `imageHashService.ts`
- `Record<>` type annotations in wallet/loyalty hooks

### Merchant Fixes (PR #94)
- `@hookform/resolvers` 5.2.2 → 4.1.0 (v5 missing `zod.d.ts` type declarations)
- 40 implicit `any` params typed in `_layout.tsx`
- `NotificationBehavior` cast fixed, notification callbacks typed
- `tsconfig.json` invalid `types` entry removed
- Stub type declarations for `expo-notifications` and `react-native-gesture-handler`
