# Recovery continuity

This change keeps the selected conversation and its viewport stable while
Conduit reconnects to Hermes. Automatic foreground return may select the saved
or newest conversation. Once a conversation is visible, transient transport or
catalog failures retry with `preserveCurrent` instead. A cold launch with no
visible identity retains automatic return.

When the saved conversation is temporarily absent from the catalog, Conduit
addresses its durable ID directly and stages viewport restoration for that ID.
Only Hermes error 4007 retires the saved identity. Other failures remain
retryable. If deletion invalidates pending automatic restoration, the matching
recovery purpose and queued retry are demoted together; deleting an unrelated
conversation does not affect automatic work.

The implementation depends on `ChatResumeRecoverySequence`, the coordinator's
automatic-work epoch, `ChatResumeStore`, and `ChatScrollSessionKey`. It does not
depend on tool, approval, or presentation-cache changes from the larger recovery
series.

The focused regressions cover lagging catalogs, authoritative deletion,
transient resume failures, visible and cold reconnect failures, raw initial
connection failure across background/foreground, viewport restoration for a
direct durable resume, and matching versus unrelated deletion invalidation.

This does not make transport health checks authoritative session-deletion
evidence. Network failures and catalog omissions continue to preserve saved
state until Hermes explicitly reports session-not-found.
