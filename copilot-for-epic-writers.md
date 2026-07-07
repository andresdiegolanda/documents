# Copilot for Epic Writers

> A practical guide for business analysts who write epics and stories.
> The engineer's version of this method starts with an implementation guide before code.
> Yours starts earlier: **the story is the first document in the pipeline.** You own layer one.

---

## The core idea

Copilot doesn't write your epics. It drafts, reviews, and stress-tests them — you judge and decide.
Every use case below follows the same loop:

**Draft → Review against a standard → Fix gaps → Freeze.**

A frozen story is one that generates zero questions in refinement.
That is the quality bar, and it is measurable: count the questions engineering asks.

---

## 1. Epic decomposition

Give Copilot the epic draft. Ask it to propose candidate stories.

```
Here is an epic. Decompose it into candidate user stories.
For each story: title, user-story sentence, draft acceptance criteria,
dependencies on other stories, suggested sequencing.
Flag anything in the epic that is ambiguous or contradictory.
```

You cut, merge, reorder, and reject. The model proposes structure; you own the judgment.

---

## 2. The story-standard skill file (build this first)

Encode your team's definition of ready into **one markdown file**. Include:

- Required story format and fields
- Acceptance criteria house style (e.g. Given/When/Then)
- What "ready for refinement" means on your team
- The questions engineering always asks — so stories pre-answer them

Then every draft gets checked against it:

```
Review the story below against the attached story standard.
List every gap, missing field, and ambiguity. Do not rewrite it — just list.
```

This file is a living asset. It gets better every sprint (see #4).

---

## 3. The refinement pre-mortem (highest value)

Before any story goes to refinement:

```
You are a senior engineer reading this story cold.
List every question you would need answered before you could estimate it.
Do not be polite. Include edge cases, error paths, and missing context.
```

**Every question the model asks that you can't answer is a defect in the story.**
Fix it before the meeting instead of during it. This is what kills the ad-hoc
clarification calls after story creation.

---

## 4. The feedback flywheel

After each real refinement session, take the questions engineering *actually* asked
and add them to the skill file (#2) as checks.

Next sprint's stories pre-answer them automatically.
Three sprints of this and your stories stop generating meetings.
The standard improves itself — that's the flywheel.

---

## 5. Epic-level consistency check

When all child stories exist, load the epic plus every story together:

```
Here is an epic and its child stories. Check:
- Do any stories contradict each other?
- Do any overlap or duplicate scope?
- Is any part of the epic's intent not covered by any story?
- Does the sequencing create dependency problems?
```

Keeping ten stories true to one intent is hard for humans and trivial for the model.

---

## 6. Audience translation

Same content, two renders:

```
Rewrite this story as a business-facing summary for stakeholders: outcome, value, no implementation detail.
```
```
Rewrite this story in precise, testable engineering language: explicit inputs, outputs, error cases.
```

You live on the boundary between business and engineering. The model commutes across it instantly.

---

## Working setup

- Draft in **markdown files**, in an editor with Copilot alongside (e.g. VS Code).
- One folder per epic: the epic file, its stories, and the skill file.
- Paste into your tracking tool only when the story is **frozen**.
- The markdown files are the source of truth while drafting — the tool is just the destination.

If the editor is too much friction on day one: Copilot chat on a pasted draft
still covers #2, #3, and #6. Start there, move to files when ready.

---

## Session one (today)

One real epic — yours, current — through three steps:

1. **Decompose** it (#1)
2. Build the **skill file** together and review one story against it (#2)
3. Run the **pre-mortem** on that story (#3)

Stop there. You leave with a story you actually need, produced the new way,
and a skill file you own. Everything else is session two — and session two
runs without a teacher. The materials carry you. That's the design.
