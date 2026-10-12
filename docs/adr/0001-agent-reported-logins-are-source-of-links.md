# Agent-reported logins are the primary source of person–machine Links

A notification is delivered once per Machine a recipient is linked to, so we need to know who uses which machine. Jamf and Intune each record an assigned user, but that is only one person per device, so it misses shared machines, and it goes out of date when laptops are reassigned. We decided the agent reports each Okta-authenticated login, and that report creates the Link. The MDM assigned user is used only as a fallback, so a machine that has not seen a login yet can still receive deliveries. A Link is removed once the person has gone 30 days without logging in to that machine. This is deliberately separate from the machine's heartbeat, which only decides whether the machine is Connected.

## Considered Options

- **MDM assigned user only.** Rejected: it can't represent shared machines, and it depends on IT keeping assignment records up to date.
- **Agent-reported logins only.** Rejected: a freshly provisioned machine would get no deliveries until someone logs in on it.

## Consequences

- Login has to go through Okta so the logged-in account can be matched to a person. Local accounts break this.
- Without the unlink period, people would keep Links to machines they no longer use, and those machines would produce misleading Not Delivered records.
- The unlink period must not be tied to the heartbeat. If a Link were dropped after a short offline spell, a laptop closed overnight would get no deliveries for notifications that activate before it is opened again.
