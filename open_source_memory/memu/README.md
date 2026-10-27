# memU: beginner-to-production guide

The [experiment notebook](./experiment.ipynb) provides synthetic event and reminder scenarios. Consult the current memU documentation for exact runtime and provider integrations.

## 1. Beginner: memory for proactive agents

Proactive memory should help an agent surface relevant context at the right moment, not merely remember facts. Model events with time, task, and status; distinguish useful reminders from unsolicited or irrelevant interruptions.

## 2. Intermediate: event-to-action flow

- Extract event facts, deadlines, and user intent from approved interactions.
- Preserve time zones, event dates, and uncertainty.
- Retrieve context only when a new task is related.
- Ask for clarification when dates or intent are ambiguous.
- Require user confirmation before creating external reminders or taking consequential actions.
- Test unrelated queries to detect over-eager memory activation.

## 3. Advanced and production

- Store event state durably with explicit expiry and update semantics.
- Enforce user/tenant access on every read and action; keep memory service separate from action authorization.
- Use idempotency keys for reminder/action creation and reconcile changes or cancellations.
- Apply consent, retention, deletion, and correction policies to event data.
- Protect provider and calendar/tool credentials; least-privilege scopes and explicit confirmation are essential.
- Bound proactive notifications, tool calls, retries, and model budgets; provide quiet hours and user controls.
- Monitor missed/false reminders, timing correctness, action success, complaint signals, latency, and spend.

## 4. Evaluation

Test relative and absolute dates, changed/cancelled events, time zones, stale events, unrelated requests, user isolation, and tool failure. Evaluate both whether the agent remembers and whether it appropriately refrains from acting.

## 5. Common pitfalls

Do not turn every remembered event into an action. Never let a model-generated memory bypass confirmation, authorization, or calendar/task service validation. The notebook scenarios are not a live memU integration.
