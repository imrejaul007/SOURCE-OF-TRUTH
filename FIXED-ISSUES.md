# Fixed Issues Log
**Last Updated:** 2026-04-30

## Fixed Issues

| Date | Service | Issue | PR |
|------|---------|-------|-----|
| 2026-04-30 | notification-events | Timing-safe token comparison | #20 |
| 2026-04-30 | rez-order-service | Error logging in cache operations | #42 |
| 2026-04-30 | rez-order-service | Remove localhost fallback from Redis | #43 |
| 2026-04-30 | rez-auth-service | Add fail-fast Redis validation | #32 |
| 2026-04-30 | rez-payment-service | Add fail-fast Redis validation | #44 |
| 2026-04-30 | rez-wallet-service | Add fail-fast Redis validation | #32 |

## Remaining Issues

### High Priority
- [ ] Rate limiting gaps (search, finance, gamification)
- [ ] AsyncStorage for tokens in mobile apps
- [ ] localhost fallbacks in other services (catalog, gamification, etc.)

### Medium Priority  
- [ ] Error logging in remaining services
- [ ] Type safety (reduce `any` usage)

## Verification Commands
```bash
# Check for silent catches
grep -rn "\.catch(() => {})" --include="*.ts" src/

# Check for localhost
grep -rn "localhost" --include="*.ts" src/ | grep -v process.env
```
