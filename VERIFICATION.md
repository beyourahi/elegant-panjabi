# Verification Report: storefront_002 Audit Implementation

**Original audit date**: 2026-03-27
**Last verification**: 2026-04-02
**Scope**: 67-item audit (AUDIT.md) across 9 implementation plans

---

## Summary

| Status | Count | Percentage |
|--------|-------|------------|
| Resolved | 62 | 92.5% |
| Not implemented (code) | 1 | 1.5% |
| Not implemented (config) | 2 | 3% |
| Deferred (merchant content) | 2 | 3% |
| **Total** | **67** | **100%** |

**Build status**: TypeScript typecheck PASS, production build PASS (both client and SSR bundles)

---

## Remaining Items

### Not Implemented — Code (1 item)

**#1 (CRITICAL)** — React Router 7.12.0 vs required 7.9.x
- `package.json` still has `"react-router": "7.12.0"`
- Dev server warns: "Hydrogen requires React Router 7.9.x"
- **Recommendation**: Audit for 7.10-7.12 API usage, then downgrade in a dedicated commit

### Not Implemented — Configuration (2 items, same root cause)

**#11 (MEDIUM)** — `PUBLIC_STOREFRONT_ID` empty in `.env`
- Requires Shopify admin app ID
- Causes "Missing shop.hydrogenSubchannelId" console error on every page

**#12 (MEDIUM)** — PerfKit storefrontId error
- Same root cause as #11
- Causes "Error initializing PerfKit" console error on every page

### Deferred — Merchant Content (2 items)

**#56 (HIGH)** — Placeholder tokens `[INSERT TRADING NAME]` etc. in Terms of Service
**#57 (MEDIUM)** — "horcrux-demo-store" references in policy content

Both are Shopify admin content, not code fixes.

---

## Previously Unresolved Items Now Fixed

The following items were listed as unresolved in the 2026-03-28 verification but have since been addressed:

| Item | Description | Resolution |
|------|-------------|------------|
| #66 | HMR crash (`useContext` null) | Fixed via Vite `resolve.dedupe` for React + HMR WebSocket config (`vite.config.ts`) |
| #67 | Missing reset.css | Documented as by-design — Tailwind v4 preflight provides equivalent normalization (`tailwind.css` base layer comment) |

---

## Verification History

- **2026-03-28**: Initial verification — 55 PASS, 4 PASS (code-only), 4 not implemented, 2 config, 2 deferred
- **2026-04-02**: Updated — #66 and #67 now resolved, bringing total to 62/67 (92.5%)

---

**Verified by**: Claude Code (automated verification)
**Last updated**: 2026-04-02
