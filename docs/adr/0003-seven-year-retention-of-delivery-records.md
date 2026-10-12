# Delivery records are kept for 7 years under internal policy

Notifications, deliveries, and every status change (including per-person actions) are kept for 7 years because an internal compliance policy requires it. Keeping less would have saved storage, but deleted records can't be recovered once an audit asks for them.

## Consequences

- Delivery records must stay meaningful after the people they refer to have left the organisation and been removed from Okta. Each delivery therefore keeps its recipient's identity as it was when the delivery was created, not just a reference to Okta.
- The per-person activity in a Notification Report has been judged not sensitive, which is why it is acceptable for anyone holding the notification's identifier to read it (ADR-0002).
