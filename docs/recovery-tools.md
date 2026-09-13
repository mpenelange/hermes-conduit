# Pending tool recovery

Hermes can emit a tool start before its transcript row is durable. Conduit records a bounded presentation marker synchronously, then folds it into the normal debounced session cache. Resume restores a running card only when gateway history has no completion with the same message or stable tool-call identity.

Stable tool IDs keep concurrent calls distinct and let out-of-order completions resolve the correct card. Legacy events without IDs remain ambiguous; Conduit does not match them by name or input because identical concurrent calls are valid.

Completion and authoritative idle cleanup still rewrite the full presentation store. Replacing those writes safely requires durable resolution tombstones so a crash cannot resurrect a committed running row.
