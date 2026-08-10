# AGENTS.md

Pure-Harn Duffel connector for flight research and test-mode booking.

Shared connector authoring rules live in the Harn connector authoring guide.
Keep provider transport and normalization here, reusable orchestration and
external-action semantics in Harn, product approvals and persistence in Burin,
and hosted tenancy/governance in Harn Cloud.

`CLAUDE.md` points here. Edit `AGENTS.md` only.

## Provider notes

- Allow egress only to `api.duffel.com`.
- Never log or persist Duffel bearer tokens or raw provider bodies.
- Keep test and live environments structurally distinct. The initial package
  supports Duffel test mode only.
- Order creation must use `std/external_action`; direct calls are forbidden.
- An ambiguous create is reconciled with a read-only order query and is never
  retried speculatively.

## Ecosystem working agreement

- Pursue the ambitious product outcome with small typed interfaces, explicit
  invariants, and deterministic projections.
- Give each behavior one semantic owner and parity-test every projection.
- Work autonomously inside approved scope; pause for production impact, live
  money, destructive action, exceptional spend, or new authority.
- Match evidence to the claim and exercise the canonical product path.
- Shipping means landed on main with post-merge checks complete.
