# Notifier

Notifier is the organisation's unified notification system. Enterprise systems use it to deliver notifications to people's Mac and Windows machines, and it records what happened to every delivery.

## Language

### Notifications

**Notification**:
A single piece of communication triggered through Notifier, with a type, content, an audience, an activation time, and an expiry.
_Avoid_: Message, alert, event

**Notification Type**:
The category of a notification (e.g. info, task, announcement). Each type determines how the notification is presented to the recipient.
_Avoid_: Kind, category, template

**Action**:
A button on a notification that opens a URL when the recipient clicks it. Dismissing is not an action. Notifier does not track anything that happens after the URL opens (e.g. whether a task gets completed).
_Avoid_: CTA, link, button

**Immediate Notification**:
A notification whose activation time is the moment it is triggered.
_Avoid_: Instant, real-time, live

**Staged Notification**:
A notification triggered with a future activation time. It stays staged until that time arrives, and only a staged notification can be withdrawn.
_Avoid_: Scheduled, queued, pending, draft

**Activation Time**:
The moment a notification becomes eligible for delivery.
_Avoid_: Send time, schedule, start time, "active"

**Lifetime**:
How long a notification stays deliverable once it activates (e.g. 60 seconds, 1 day), set by the origin for each notification.
_Avoid_: TTL, duration, timeout

**Expiry**:
The moment a notification stops being deliverable: its activation time plus its lifetime. Expiry only prevents new deliveries. A notification already delivered stays on screen until the recipient deals with it.
_Avoid_: Deadline, end time

**Withdraw**:
To cancel a staged notification before its activation time so that it never goes out. Anyone who presents the notification's identifier may withdraw it, including an origin other than the one that triggered it.
_Avoid_: Remove, delete, recall, cancel

**Withdrawn**:
The final status of a notification that was withdrawn, recorded together with the time it was withdrawn and the origin that withdrew it.

### Audience

**Audience**:
The set of people a notification is addressed to, given as any mix of individual users and Okta groups. Okta group membership is read as it stands at the notification's activation time.
_Avoid_: Targets, recipients list, distribution

**Okta Group**:
A group of users defined in Okta that can be used as part or all of an audience.
_Avoid_: Team, list, group (unqualified)

**Recipient**:
One person in the expanded audience of a notification. A recipient's outcome is taken from their deliveries: delivered if any of their machines reached Delivered, otherwise not delivered.
_Avoid_: User (when meaning the addressee), subscriber, target

### Delivery

**Origin**:
The enterprise system that triggered a notification. Any enterprise system can be an origin, and it may address any audience with any notification type. Each origin has its own credential, so Notifier always knows which origin made a request. An origin may be made up of several services that share one credential, and Notifier treats them as a single origin.
_Avoid_: Sender, source, publisher, client, service

**Agent**:
The background program on a user's machine that receives notifications and presents them. The user cannot stop or remove it.
_Avoid_: Client, daemon, app, service

**Machine**:
A Mac or Windows computer whose agent has registered with Notifier. When a notification activates, each recipient gets one delivery per machine they are linked to. That set of deliveries is final: machines or people that appear later are not added.
_Avoid_: Device, endpoint, host

**Link**:
The association between a person and a machine they use. It is created when the agent reports the person logging in with their Okta identity, or when the device-management records name them as the machine's assigned user. It is removed after the person has gone a period of time without logging in to that machine.
_Avoid_: Assignment, ownership, binding

**Connected**:
The state of a machine whose agent has recently checked in with Notifier. It says nothing about whether anyone is logged in.
_Avoid_: Online, active, alive

**Available**:
The state of a recipient who is logged in to a machine with an unlocked, active screen, which is when the agent can present a notification.
_Avoid_: Active, online, present

**Delivery**:
One notification going to one recipient on one machine. A recipient with several machines has a separate delivery on each, and people who share a machine each have their own delivery on it.
_Avoid_: Send, dispatch, message

**Received**:
The agent has the notification but has not yet presented it.

**Displayed**:
The agent has put the notification on the recipient's screen, but the operating system did not let it take focus. It becomes delivered as soon as the recipient clicks on it.
_Avoid_: Shown, rendered

**Delivered**:
The agent has put the notification on the recipient's screen and it has taken focus. This is the point that counts as delivery.
_Avoid_: Sent, shown, seen

**Open**:
A delivered notification that is still on screen because the recipient has neither dismissed it nor clicked an action. Whenever an open notification leaves the screen without the recipient's doing (for example a restart or a logout), the agent shows it again, up until its expiry. Showing them again does not change their status and is not recorded.
_Avoid_: Active, pending, unread

**Dismissed**:
The recipient closed a delivered notification without clicking an action. Every notification can be dismissed.

**Actioned**:
The recipient clicked one of a delivered notification's actions.
_Avoid_: Clicked, completed, acted on

**Not Delivered**:
The final status of a delivery, or the outcome of a recipient, that did not reach Delivered before expiry. It carries a reason where one is known, such as the recipient never being available or having no machine with an agent.
_Avoid_: Failed, expired, undelivered
