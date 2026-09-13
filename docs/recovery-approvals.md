# Approval recovery

Conduit hydrates `approval.pending` after resume and decision responses because a resume snapshot may contain only the queue head. Request IDs identify modern approval cards and responses; delayed work is fenced by client, profile, session, viewport, reconciliation, request generation, message identity, and decision identity.

A failed legacy no-ID response stays retryable when the refresh fails or returns no identified rows. A successful fresh identified snapshot replaces that ambiguous card as a group. If the target changes while the read is suspended, Conduit discards the stale result and awaits one post-transition read rather than guessing by command, description, or queue position. An expired legacy card remains terminal while later identified requests are added.

The Hermes contract is pinned at `422bc9bde9d212ab3741fbc45a871a3938436d59`: `tui_gateway/methods_prompt.py`, `tui_gateway/server.py`, and `tools/approval.py`.
