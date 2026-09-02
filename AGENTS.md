# AGENTS.md

Pure-Harn Duffel connector for flight research and test-mode booking.

Shared connector authoring rules live in the Harn guide:

- [Connector authoring guide](https://github.com/burin-labs/harn/blob/main/docs/src/connectors/authoring.md)

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

## Pull request titles

Use `[Area] Sentence case`. The area is one of `Connector`, `CI`, or `Docs`.

- `[Connector] Reject webhook deliveries with a stale timestamp`
- `[CI] Repin the shared Harn package workflow`
- `[Docs] Describe the poll cursor contract`

Keep the title on one line, under about 70 characters. Say what changed, not
which files moved. Capitalize the first word after the bracket and leave the
rest in sentence case.

`CONTRIBUTING.md` states the contribution policy for this repository.

<!-- BEGIN HARN SHARED AGENT CONTRACT: managed by harn-bump-fleet -->

## Ecosystem working agreement

- Pursue the ambitious product outcome; make the seams boring with small typed
  interfaces, explicit invariants, and deterministic projections.
- Give each behavior one semantic owner. Generate or parity-test other surfaces
  instead of maintaining competing implementations.
- Work autonomously inside approved scope. Pause for destructive, production,
  high-spend, ambiguous, or authority-expanding actions—not routine reversible work.
- Treat stop, wait, stand down, and pivot as control events for long-lived work.
- Match evidence to the claim: exercise the canonical user path, state the
  falsifier, verify liveness and recovery, and record residual blind spots.
- "Ship" means landed on main with required deploy and post-merge checks complete.

<!-- END HARN SHARED AGENT CONTRACT -->
