# harn-duffel-connector

Pure-Harn Duffel connector for flight search, offer refresh, sandbox booking,
and safe order reconciliation.

The initial package is deliberately test-only. It accepts tokens beginning
with `duffel_test_`, rejects live tokens and live action environments before
network access, and uses only `https://api.duffel.com` with `Duffel-Version:
v2`.

## Capabilities

Read/research methods are available through `call(...)`:

- `places.list`
- `offer_requests.create`
- `offer_requests.get`
- `offers.list`
- `offers.get`
- `orders.list`
- `orders.get`

Search results are normalized to stable comparison facts: exact decimal price
and currency, expiry, airline, slices, segments, stops, schedule, duration, and
aircraft. Offer pagination preserves Duffel cursors. Always call `offers.get`
before presenting a final booking preview because airline price and availability
can change after the initial search.

`orders.create` cannot be invoked through `call(...)`. It requires a
`std/external_action` intent with:

- provider `duffel`;
- capability `flights.book`;
- operation `orders.create`;
- environment `test`;
- exact offer ID, decimal amount, currency, and passenger payload;
- matching `external_spend` in ISO currency minor units.

The adapter refreshes the offer inside the at-most-once dispatch checkpoint,
checks identity, expiry, price, currency, and the granted spend, then creates
one test order using Duffel test balance. Services and live payments are not
enabled. A timeout or 5xx after creation becomes `reconciliation_required`;
reconciliation lists orders by the exact offer ID and never repeats the POST.

## Configure

Store the token as `duffel/test-access-token` through Harn/Burin connector
setup. During local Burin development, the credential resolver may consume the
existing `DUFFEL_TEST_KEY` environment entry. Never paste the token into a
prompt, committed file, CLI argument, or trace.

Duffel test mode is a sandbox: its test tokens can access only test resources,
and test orders do not spend real money or create real travel bookings. The
connector still records an external-spend amount so the same policy and receipt
path is exercised before any future live-mode work.

## Validate

```sh
harn connector check . --provider duffel
harn test tests
```

Implementation is tracked in
[issue #1](https://github.com/burin-labs/harn-duffel-connector/issues/1).
