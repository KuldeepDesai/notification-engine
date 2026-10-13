# Notifier

Notifier is the organisation's unified notification system. Enterprise systems use it to deliver notifications to people's Mac and Windows machines, and it records what happened to every delivery.

## Language

### Notifications

**Notification**:
A single piece of communication triggered through Notifier, with a type, content, an audience, an activation time, and an expiry. Each notification stands alone. A reminder or follow-up is a separate notification.
_Avoid_: Message, alert, event, campaign

**Notification Type**:
The category of a notification (info, task or announcement), chosen by the origin from a fixed set that Notifier owns. Each type determines the notification's appearance, sound, how intrusive it is, which content it allows, and which actions it may carry.
_Avoid_: Kind, category, template, priority

**Info**:
A notification type for general information. It has its own look and sound, and it respects the recipient's operating-system do-not-disturb settings.

**Task**:
A notification type for asking the recipient to do something. It has its own look and sound, and it respects the recipient's operating-system do-not-disturb settings.
_Avoid_: To-do, request, assignment

**Announcement**:
The most intrusive notification type, for organisation-wide messages. It has its own look and sound, and it ignores do-not-disturb settings.
_Avoid_: Broadcast, alert, bulletin

**Body**:
The main text of a notification, which may use text formatting such as bold, italics and underline but no images or video.
_Avoid_: Message, content, payload

**Action**:
A button on a notification, or a link in its body, that opens a URL when the recipient clicks it. A notification of any type may have none, one or several. An action is identified by its label: the button text or the link text. Dismissing is not an action. Notifier does not track anything that happens after the URL opens (e.g. whether a task gets completed).
_Avoid_: CTA, button, hyperlink

**Immediate Notification**:
A notification whose activation time is the moment it is triggered.
_Avoid_: Instant, real-time, live

**Staged Notification**:
A notification triggered with a future activation time. It stays staged until that time arrives, and only a staged notification can be withdrawn.
_Avoid_: Scheduled, queued, pending, draft

**Activation Time**:
The moment a notification becomes eligible for delivery.
_Avoid_: Send time, schedule, start time, "active"

**Activated**:
The state of a notification whose activation time has arrived and whose expiry has not yet passed. It is deliverable during this period.
_Avoid_: Active, live, sent

**Past Expiry**:
The state of an activated notification after its expiry. It gets no new deliveries, but notifications already on screen can still change status.
_Avoid_: Expired, closed, finished

**Lifetime**:
How long a notification stays deliverable once it activates (e.g. 60 seconds, 1 day), set by the origin for each notification.
_Avoid_: TTL, duration, timeout

**Expiry**:
The moment a notification stops being deliverable: its activation time plus its lifetime. Expiry only prevents new deliveries. A notification already on screen stays there, and its status can still move forward after expiry, e.g. from Displayed to Delivered to Actioned.
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
One person in the expanded audience of a notification. A recipient's outcome is the furthest status reached by any of their deliveries, in the order Actioned, Dismissed, Delivered, Displayed, Received, Queued, Not Delivered.
_Avoid_: User (when meaning the addressee), subscriber, target

### Delivery

**Origin**:
The enterprise system that triggered a notification. Any enterprise system can be an origin, and it may address any audience with any notification type. Each origin has its own credential, so Notifier always knows which origin made a request. Its registered name appears on every notification it triggers, and the origin cannot change it per notification. An origin may be made up of several services that share one credential, and Notifier treats them as a single origin.
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
The state of a recipient who is logged in to a machine with an unlocked, active screen and, for info and task notifications, without do-not-disturb turned on. This is when the agent can present a notification.
_Avoid_: Active, online, present

**Delivery**:
One notification going to one recipient on one machine. A recipient with several machines has a separate delivery on each, and people who share a machine each have their own delivery on it.
_Avoid_: Send, dispatch, message

**Queued**:
A delivery that has been created but that the agent has not yet picked up.
_Avoid_: Pending, waiting, created

**Received**:
The agent has the notification but has not yet presented it.

**Displayed**:
The agent has put the notification on the recipient's screen, but the operating system did not let it take focus. It becomes delivered as soon as the recipient clicks on it.
_Avoid_: Shown, rendered

**Delivered**:
The agent has put the notification on the recipient's screen and it has taken focus. This is the point that counts as delivery.
_Avoid_: Sent, shown, seen

**Open**:
A delivered notification that is still on screen because the recipient has neither dismissed it nor clicked an action. Whenever an open notification leaves the screen without the recipient's doing (for example a restart or a logout), the agent shows it again, up until its expiry. Showing it again is not recorded, but if a displayed notification takes focus when shown again, it becomes delivered.
_Avoid_: Active, pending, unread

**Dismissed**:
The recipient closed a delivered notification without clicking an action. Every notification can be dismissed.

**Actioned**:
The recipient clicked one of a delivered notification's actions.
_Avoid_: Clicked, completed, acted on

**Not Delivered**:
The final status of a delivery, or the outcome of a recipient, that never reached the screen (Displayed or further) before expiry. It carries a reason where one is known, such as the recipient never being available or having no machine with an agent.
_Avoid_: Failed, expired, undelivered

### Reporting

**Notification Report**:
The account of what happened to one notification: overall totals, rates, and timings, together with each recipient's outcome and the status of each of their deliveries. Anyone who presents the notification's identifier may read it. Because statuses can still change after expiry, a report is never permanently final.
_Avoid_: Campaign report, analytics, stats

**Delivery Rate**:
The share of a notification's recipients whose outcome is Delivered or further.
_Avoid_: Reach, open rate

**Action Rate**:
The share of delivered recipients whose outcome is Actioned.
_Avoid_: Click-through rate, CTR, engagement rate
