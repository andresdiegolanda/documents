# Example: A Well-Formed Epic

> This is the repaired version of the flawed notification-preferences epic.
> It passes every check in **Skill: Epic Quality Evaluation**.
> Use it as the answer key after running the flawed version through the skill,
> and as a reference exemplar for granularity and structure.
>
> Note what "perfect" means here: not zero open decisions — zero HIDDEN ones.

---

## EPIC: Notification Preferences Center

As a **retail customer**, I want to control which notifications I receive and
through which channel, so that I stop receiving communications I don't want
without losing the ones I need.

**Problem today:** all notifications are sent by email to every customer, with
no opt-out and no channel choice. Support logs ~400 complaints/month tagged
"notification volume", and marketing-email unsubscribe requests currently
require a support ticket.

### Scope

- Customer can view all notification categories and their current channel settings
  on a preferences page reached from account settings
- Customer can set the delivery channel per **optional** category
  (account activity, marketing, service updates): email, SMS, or push
- Customer can opt out entirely of any **optional** category
- **Mandatory categories (security alerts, legal/regulatory notices) are always
  delivered and appear as read-only on the preferences page, with a short
  explanation of why they cannot be disabled**
- SMS is selectable only when the account has a verified mobile number;
  push only when at least one registered device exists. Unavailable channels
  are shown disabled, with a link to the existing verification/registration flows
- Customer can define one quiet-hours window (start/end, account timezone)
  during which **optional** notifications are held and delivered when the
  window closes; mandatory notifications ignore quiet hours
- A saved change applies to all notifications **generated after** the save;
  notifications already queued for delivery are unaffected
- Every preference change is recorded in the account audit history

### Out of scope

- In-app notification inbox and notification history views
- Per-notification granularity below category level
- Marketing consent management beyond channel/opt-out (owned by the consent platform)
- New notification categories or new content

### Default state and migration

- Existing customers: all optional categories default to **email on**,
  matching today's behavior. No notification stops until the customer acts.
- New customers: same defaults, set at account creation.
- No historical data migration is required.

### Unhappy paths (defined)

- Verified mobile is later removed → SMS-configured categories fall back to
  email; customer is notified once of the fallback
- Preferences service unavailable at send time → notification is delivered
  using last-known preferences; if none are readable, mandatory categories
  send, optional categories are held and retried

### Success signal

- "Notification volume" support complaints drop ≥50% within two months of full rollout
- ≥20% of active customers modify at least one preference within the first month

### Open decisions (visible, owned by product)

- [ ] Marketing category: does channel opt-out here need to synchronize with the
      consent platform, or are they independent records? (compliance to confirm)
- [ ] Quiet-hours maximum length: unlimited, or capped (e.g. 12h) to prevent
      permanent deferral of service updates?

---

## Why this passes — mapped to the evaluation skill

| Skill check | How this epic satisfies it |
|---|---|
| 1. Intent | One problem, real actor (retail customer), outcome-based value clause, evidence (~400 complaints/month) |
| 2. Scope boundaries | Explicit testable list, one capability per line; SMS/email/push split visible; explicit out-of-scope |
| 3. Contradictions / absolutes | The "any category" absolute is resolved: optional vs. mandatory categories distinguished; mandatory behavior stated |
| 4. Hidden dependencies | Verified mobile and registered device named as prerequisites, with UI behavior when absent |
| 5. State and transitions | Default state, migration, and "applies after save / queued unaffected" timing all defined |
| 6. Unhappy paths | Channel loss fallback and service-down behavior specified; mandatory vs. optional failure handling differs |
| 7. Measurability | Two numeric success signals with time windows |
| 8. Decomposability | Implies ~7–9 stories (preferences page, per-channel delivery ×3, quiet hours, mandatory read-only handling, defaults/migration, audit); page + email channel is a shippable walking skeleton |

---

## The one lesson to take from this file

The flawed version and this version describe the **same feature**.
The difference is not ambition or length — it is that every decision the flawed
version left implicit is here either **made** (in scope), **excluded** (out of scope),
or **visibly open** (open decisions).

A perfect epic is not one with no open questions.
It is one where every open question is on the page instead of in the refinement meeting.
