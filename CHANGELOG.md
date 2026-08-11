# Changelog

## Unreleased

- Record definite Duffel order 4xx responses as dispatched rejections so
  callers do not mistake them for preflight failures and retry blindly.
- Preserve each offer's Duffel passenger reference for valid order creation.
- Declare the supported Duffel test credential environment source in the typed
  connector manifest.
- Add normalized Duffel flight/place research with paginated offers and
  mandatory pre-booking offer refresh.
- Add a test-only external-action adapter with exact spend validation,
  at-most-once order creation, bounded receipts, and read-only reconciliation.
- Install a default-deny network policy for direct connector calls so research
  works without requiring another network tool to run first.
- Give Duffel sandbox searches an explicit 30-second request budget instead of
  inheriting Harn's shorter generic HTTP default.
