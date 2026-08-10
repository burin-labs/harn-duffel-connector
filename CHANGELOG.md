# Changelog

## Unreleased

- Add normalized Duffel flight/place research with paginated offers and
  mandatory pre-booking offer refresh.
- Add a test-only external-action adapter with exact spend validation,
  at-most-once order creation, bounded receipts, and read-only reconciliation.
- Install a default-deny network policy for direct connector calls so research
  works without requiring another network tool to run first.
- Give Duffel sandbox searches an explicit 30-second request budget instead of
  inheriting Harn's shorter generic HTTP default.
