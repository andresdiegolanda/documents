# Skill: Epic Quality Evaluation

> Use this skill to review an epic BEFORE decomposition.
> Apply every check. Report findings as a numbered list: **check → finding → severity (blocker / gap / polish)**.
> Do not rewrite the epic. Do not be polite. An unflagged defect becomes a refinement meeting.

---

## 1. Intent

- [ ] There is exactly ONE problem being solved. If two or more, flag: candidate for splitting into separate epics.
- [ ] The user-story sentence names a real actor (not "the system", not "the business").
- [ ] The value clause ("so that...") states an outcome, not a feature restated.
- [ ] The problem evidence is present: what happens today, why it hurts, who reported it.

## 2. Scope boundaries

- [ ] Scope is an explicit list, not prose from which scope must be inferred.
- [ ] Out-of-scope is explicitly stated. An epic with no out-of-scope section has not decided what it is not.
- [ ] Every scope item is testable — a reviewer could answer "is this done?" with yes/no.
- [ ] No scope item hides multiple stories behind one line (e.g. "supports email, SMS and push" = three integrations, not one item).

## 3. Contradictions and absolutes

- [ ] Hunt absolute words: *any, all, every, always, never, immediately, entirely*. For each, ask: is there a category, case, or regulation where this cannot hold?
- [ ] Check scope items against each other: does item A make item B impossible or partially false?
- [ ] Check scope against the domain: are there mandatory behaviors (legal, regulatory, security) that user preference or configuration must NOT override?

## 4. Hidden dependencies

- [ ] For every capability, ask: what must already exist for this to work? (verified contact data, permissions, upstream services, device registration, feature flags)
- [ ] For every integration named or implied, ask: does the epic assume it exists, and is that assumption stated?
- [ ] Are there other teams or systems whose participation this epic silently requires?

## 5. State and transitions

- [ ] Does the epic define the DEFAULT state — what happens for users/records that never interact with the new capability?
- [ ] Is there a migration story: what happens to existing data/users on day one?
- [ ] Timing words ("immediately", "in real time", "on next login"): are edge cases defined — queued items, sessions in flight, timezones?

## 6. Unhappy paths

- [ ] For each capability, is failure behavior defined? (service down, invalid input, missing prerequisite)
- [ ] Are permission/eligibility boundaries stated — who can NOT do this?
- [ ] Is there an abuse or misuse case worth naming? (rate limits, spam, opt-out of mandatory messages)

## 7. Measurability

- [ ] Is there a success signal — a number or observable change that says the epic worked? (complaint volume, adoption, task completion)
- [ ] Could a demo of the finished epic be described in two sentences? If not, the epic is not concrete enough.

## 8. Decomposability

- [ ] Estimate the story count implied by scope. Fewer than 3: this is a story wearing an epic label. More than ~12: flag as candidate for splitting.
- [ ] Is there an obvious first story that delivers value alone (walking skeleton)? If nothing can ship independently, sequencing is undefined.

---

## Output format

```
EPIC EVALUATION — <epic title>

BLOCKERS (must fix before decomposition)
1. <check> — <finding>

GAPS (will surface as questions in refinement)
2. <check> — <finding>

POLISH (improves clarity, not correctness)
3. <check> — <finding>

VERDICT: READY TO DECOMPOSE / FIX BLOCKERS FIRST
Estimated story count: <n>
```

---

## Prompt to use with this skill

```
Attached: an epic and this evaluation skill.
Apply every check in the skill to the epic.
Report using the skill's output format.
Do not rewrite the epic. Flag only — I decide what to fix.
```
