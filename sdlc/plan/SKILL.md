---
name: sdlc-plan
description: Use when an approved spec.md exists and an engineer wants an implementation plan (plan.md, Stage 3 Build of the AI-native SDLC). Run in plan mode, read intent.md, spec.md, and CLAUDE.md, write a plan naming the files that change, the order of work, risks, and the tests that prove it. Do not write code until the plan is approved.
---

# sdlc-plan — Produce `plan.md` in plan mode

`plan.md` is the written implementation plan created **before any code is generated**. Design review happens on this document, when changing course is still a matter of editing text. Once approved and committed, it joins the audit trail, and PR review checks the eventual diff against it.

Repository conventions for the template and the storage location win over this skill.

## Workflow

1. **Work in plan mode.** Switch to it if the session is not already there.
2. **Read the inputs:** `spec.md`, `intent.md` if it exists, and every `CLAUDE.md` that applies to the affected directories. Approval lives in git history: a committed spec is an approved spec. If `spec.md` is only a working-tree change, say so and ask whether to continue.
3. **Explore the code the spec touches:** the named modules, their tests, and their call sites. Confirm that every path you will name exists, or mark it as new.
4. **Write the plan** using the template below.
5. **Invite interrogation.** Ask the engineer about risks and alternatives, and revise after each round. Stop when an engineer who has never seen the conversation could implement the change from the plan alone.
6. **Commit the approved plan as `plan.md`** in the feature folder (see Storage). Routine changes need the engineer's approval; higher-risk changes need a tech lead or architect review first.
7. **Implement after approval.** Follow the order of work. Whenever the implementation deviates from the plan, record the deviation in `plan.md` in the same pull request, so the merged diff and the committed plan match.

## Template

```markdown
# Plan: <same title as spec.md>

## Files that change
<One line per file with a short note. Mark new files with (new).>

## Order of work
<Numbered steps. Each step leaves the system working and testable, and names the files it touches.>

## Risks
<Concrete things that can break and the mitigation for each: rate limits, migrations, shared code, feature flags, rollbacks.>

## Proof
<The tests that prove the change and what each covers. Include manual checks where automation is not possible.>

## Deviations
<Empty at approval. During implementation, record every change from the plan with the reason.>
```

## Example

```markdown
# Plan: claims status self-service

## Files that change
portal/src/claims/StatusPanel.tsx (new), claims-api/routes/status.py, claims-api/tests/test_status.py

## Order of work
1. Add the status endpoint behind existing auth.
2. Panel against the endpoint.
3. Wire into the portal nav.

## Risks
The claims-core API rate-limits at 50 rps; the panel must cache.

## Proof
test_status.py covers the four claim states; screenshot matches the approved mock.
```

## Content rules

- **Every requirement in `spec.md` maps to at least one step and one proof.** A step that serves no requirement is dropped.
- **Every step is verifiable.** A step ends with something a reviewer can run or look at.
- **Risks come from the code.** Name the specific constraint you found: the rate limit, the migration, the shared helper with many callers.
- **Say when a `CLAUDE.md` convention shaped a decision.**
- **Same names** as `spec.md` and `intent.md` for features, users, and systems.
- **No code in the plan.** A short signature or a schema line is fine when it removes ambiguity.

## Storage

Store the plan in the feature folder, next to `intent.md`, `spec.md`, and any other material about the feature:

```
features/<feature-slug>/
  intent.md
  spec.md
  plan.md
```
