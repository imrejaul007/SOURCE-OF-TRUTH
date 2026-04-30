# Fixed Issues Log
**Last Updated:** 2026-04-30

## Fixed Issues

| Date | Service | Issue | PR |
|------|---------|-------|-----|
| 2026-04-30 | notification-events | Timing-safe token comparison | #20 |
| 2026-04-30 | rez-order-service | Error logging in cache operations | #42 |
| 2026-04-30 | rez-auth-service | Error logging in Redis operations | Already fixed |

## Issues to Fix

### High Priority
- [ ] localhost fallbacks in all services (config files)
- [ ] Rate limiting gaps (search, finance, gamification)
- [ ] AsyncStorage for tokens in mobile apps

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
