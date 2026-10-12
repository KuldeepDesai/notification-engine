# Withdrawing a notification is authorised by its identifier, not by which origin triggered it

Any authenticated origin that presents a staged notification's identifier may withdraw it, even if a different origin triggered it. This lets one enterprise system (e.g. an orchestration tool) cancel notifications that another system staged, without Notifier keeping track of which origins are allowed to manage each other's notifications. The obvious alternative, "only the triggering origin may withdraw", was rejected for that reason.

## Consequences

- The identifier works as a bearer token. It must be unguessable, and it must never be exposed to recipients (e.g. in action URLs or the notification UI).
- Every withdrawal records which origin withdrew the notification and when, because the origin that withdrew it may not be the one that triggered it.
