# Numeric RPC Safety

`AnyCodable.intValue` preserves the app's existing truncation behavior for
finite fractional values, but returns `nil` when a `Double` cannot be safely
converted to `Int`. This prevents malformed or unexpectedly large gateway
numbers from trapping the process.

`approval.respond` accepts the pinned Hermes count contract: an omitted
`resolved` field remains compatible with older gateways, zero means no pending
request was resolved, and a positive integer means the response was accepted.
A present negative, fractional, nonnumeric, nonfinite, or out-of-range value is
an invalid response.

The tools and approvals split depends on commit `c06ba56` for the request-ID
parameter and Boolean response contract. Validate this slice with the complete
`AnyCodableTests` and `HermesClientTests` suites; the focused regressions cover
integer boundaries, malformed counts, zero, positive, and omitted `resolved`.
