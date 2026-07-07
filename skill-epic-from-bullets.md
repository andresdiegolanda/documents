# Skill: Epic Draft from Bullet List

> Use this skill to turn a bullet list of intent into a structured epic draft.
> The output is NEVER a finished epic. It is a draft plus a list of decisions the bullets did not make.
> This skill pairs with **Skill: Epic Quality Evaluation** — generation and evaluation are separate passes.

---

## The contract

The model expands bullets into house-format structure. In doing so it WILL fill gaps —
that is what language models do. The contract is: **every fill must be visible.**

Two tags, mandatory:

- `[ASSUMED: ...]` — content not traceable to any bullet, filled with a plausible default.
  The human may accept it, but must SEE it.
- `[DECISION NEEDED: ...]` — a gap only a human can settle: business rules, scope
  boundaries, regulatory behavior, defaults for existing users, success metrics.
  The model must NOT pick an answer, even a plausible one.

An untagged invention is a defect in the generation. If unsure whether something
was implied by a bullet, tag it.

---

## Epic structure to produce

```
EPIC: <title>

As a <actor>, I want <capability>, so that <outcome>.

<Problem context: what happens today, why it hurts, evidence if given.>

Scope:
- <explicit, testable items — one capability per line>

Out of scope:
- <explicit exclusions>

Success signal:
- <observable measure that says the epic worked>

Notes / open decisions:
- <every DECISION NEEDED tag, collected here as a checklist>
```

---

## Generation rules

1. **One problem per epic.** If the bullets contain two unrelated problems, produce two
   epic drafts and say so — do not merge them.
2. **Actor must be real.** If the bullets don't name who this is for, tag it:
   `[DECISION NEEDED: actor — who is this for?]`. Never default to "the user".
3. **Scope items must be testable.** Rewrite vague bullets into yes/no-verifiable lines.
   If a bullet hides multiple capabilities ("supports email, SMS and push"), split it
   into separate scope lines.
4. **Out-of-scope is mandatory.** If the bullets don't exclude anything, propose
   exclusions tagged `[ASSUMED]` — an epic that excludes nothing has not decided
   what it is.
5. **No invented absolutes.** Do not introduce *any, all, always, immediately, entirely*
   unless a bullet states them. If a bullet states one, keep it and add
   `[DECISION NEEDED: does this hold for every case, including mandatory/regulated ones?]`
6. **Default state and migration.** If the bullets are silent on what happens to
   existing users/data on day one, add
   `[DECISION NEEDED: default state for existing users]` — never assume it.
7. **Success signal.** If no bullet implies a measure, propose one tagged `[ASSUMED]`.
8. **Do not gold-plate.** No capabilities beyond the bullets, however obvious the
   adjacent feature seems. If something feels missing, that is a
   `[DECISION NEEDED]`, not a free addition.

---

## Output format

```
EPIC DRAFT — <title>

<the epic, in house structure, tags inline>

---
DECISIONS THE BULLETS DID NOT MAKE
1. <each DECISION NEEDED, one line each>

ASSUMPTIONS I MADE (accept or correct)
2. <each ASSUMED, one line each>

Bullet coverage: <n> of <m> bullets represented in scope.
Uncovered bullets: <list, if any>
```

---

## Prompt to use with this skill

```
Attached: a bullet list and this generation skill.
Produce an epic draft following the skill exactly.
Tag every assumption and every open decision — an untagged invention is a defect.
Do not resolve DECISION NEEDED items yourself, even when an answer seems obvious.
```

---

## Workflow rules (non-negotiable)

1. A generated draft NEVER goes straight to frozen. Every tag gets resolved by a human first.
2. After tags are resolved, run **Skill: Epic Quality Evaluation** as a SEPARATE, fresh pass —
   the generator does not grade its own output in the same conversation.
3. The tags are the point. If a draft comes back with zero tags, be suspicious:
   either your bullets were unusually complete, or the model invented silently. Check.
