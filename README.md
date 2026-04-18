# REZ Platform — Source of Truth

Single place to find everything about the REZ platform. Read this before solving any issue, building any feature, or debugging anything.

## What's Inside

| File | Contents |
|------|----------|
| [REPOS.md](REPOS.md) | All 20 repo names, GitHub URLs, deploy URLs, current HEAD |
| [LOCAL-PORTS.md](LOCAL-PORTS.md) | Local dev ports for every service |
| [API-ENDPOINTS.md](API-ENDPOINTS.md) | Service endpoints, gateway routes, internal APIs |
| [ENV-VARS.md](ENV-VARS.md) | All env var names (NO values — never commit secrets) |
| [DATA-TYPES.md](DATA-TYPES.md) | Canonical types from shared-types and unified types |
| [DEPLOY-STATUS.md](DEPLOY-STATUS.md) | Which services are live on Render/Vercel |
| [ARCHITECTURE.md](ARCHITECTURE.md) | Monolith → microservice mapping, data flow |

## Quick Links

- **API Gateway**: https://rez-api-gateway.onrender.com
- **Backend**: https://rez-backend-8dfu.onrender.com
- **GitHub**: https://github.com/imrejaul007

## Bug Tracking & Gap Analysis

Gap docs are in `docs/Gaps/` (relative to project root):

| Folder | Scope | Status |
|--------|-------|--------|
| `docs/Gaps/10-REZ-NOW/` | ReZ Now (rez-now/) — 14 CRITICAL + 15 HIGH issues | **13 fixed, 1 partial, 0 open** CRITICAL |
| `docs/Gaps/09-CROSS-SERVICE-2026/` | Cross-service inconsistencies | Various |
| `docs/Gaps/11-CROSS-SERVICE-CONNECTIONS/` | Cross-repo connection issues | Various |

Always check the gap docs before starting new work — many issues are already fixed.

## Key Rules

1. **NEVER commit env values** — use placeholder names only in this folder
2. **Local dev**: always run services on their local ports from LOCAL-PORTS.md
3. **Cross-service calls**: use `*_SERVICE_URL` env vars (point to Render prod)
4. **Types**: always import from `rez-shared` or local `types/` — never duplicate
5. **Auth**: internal service calls require `X-Internal-Token` header
