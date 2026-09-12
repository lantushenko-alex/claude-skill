---
name: sdlc-spec
description: Use when an approved intent.md exists and the user wants a requirements and design spec (spec.md, Stage 2 Design of the AI-native SDLC). Reads intent.md, applies organization skills and policies, writes spec.md ready to hand to engineering, and lists areas of concern.
---

# sdlc-spec — Produce `spec.md` from `intent.md`

`spec.md` compresses requirements and design into one document. It records **what was asked for and what was decided**, and it is the handoff to the engineering team. It is produced from an approved `intent.md` in a single session. Committing it starts Stage 3: Build, where `plan.md` is produced from it (see the `sdlc-plan` skill). PR review later checks the diff for compliance against this file.

Claude writes the spec; the product owner reviews it.

Repository conventions for the template and the storage location win over this skill.

## Workflow

1. **Read the committed `intent.md`.** Approval lives in git history: a committed intent is an approved intent. If the file is only a working-tree change, say so and ask whether to continue.
2. **Load organization constraints.** Apply every relevant skill and policy in the session: brand guidelines, security policies, compliance rules, UX standards, and `CLAUDE.md`. If none are available, say so under areas of concern.
3. **Study the existing codebase** where the change lands: current modules, data models, authentication, integration points. Reuse what exists over inventing new parts.
4. **Search for a mature third-party library** before designing any major piece of functionality from scratch. Major means a whole subsystem or a well-known problem that many teams have already solved: authentication, payments, scheduling, parsing, search, charting, state management, and similar. Do not search for small helpers that a few lines of code cover. Prefer libraries the project already depends on, then the standard library, then a new dependency. Offer the options to the product owner in the spec; do not pick a new dependency silently.
5. **Write `spec.md`** using the template below. Answer every open question from `intent.md` or carry it forward as still open.
6. **Describe areas of concern.** Name every place where two policies contradict each other and you cannot satisfy both. Resolving policy conflicts is the product owner's job, not yours.
7. **Save the file** in the feature folder (see Storage). The product owner reviews the spec against the intent and resolves concerns with policy owners. `intent.md` and `spec.md` are committed together, and a human approves the move to Stage 3.

## Default instruction

When the user gives no specific instruction, act as if they had asked:

> Read the attached intent.md and produce a requirements and design spec for integrating it into our existing codebase. Apply the skills available to you so the plan conforms to our brand guidelines, security policies and UX standards. Document the spec fully as spec.md, ready to hand to the engineering team. Describe clearly any areas of concern, especially where you cannot satisfy contradicting policies.

## Template

```markdown
# Spec: <same title as intent.md>

## Summary
<Two or three sentences: the problem, the chosen solution, the main tradeoff.>

## Goals
<Numbered list. Each goal is testable and maps back to the proposed outcome in intent.md.>

## Non-goals
<What this change deliberately does not do.>

## Users and scenarios
<Who uses the result and how. One short scenario per user type.>

## Functional requirements
<Numbered, one per line, with ids like FR-1. Use "must", "should", "may".>

## Non-functional requirements
<Performance, availability, security, privacy, accessibility, compliance. Ids like NFR-1.>

## Design
### Current state
<How the relevant part of the system works today. Name real modules and services.>
### Proposed change
<Components added or changed, data flow, APIs, data model changes, authentication and authorization.>
### Third-party libraries
<One block per major piece of functionality. Name the candidate libraries found, their license, maintenance state (last release, open issues, adoption), and how they fit the existing stack. State the recommendation: use the library, or build it in the project and why. Write "none needed" when the functionality is small enough to build. Leave the final decision on a new dependency to the product owner.>
### Alternatives considered
<Options rejected and why.>

## Policy compliance
<One line per applied policy or skill: what it required and how the design satisfies it.>

## Acceptance criteria
<Numbered checks an engineer or tester can run. Each maps to at least one requirement.>

## Areas of concern
<Contradicting policies, unresolved risks, missing information, dependencies on other teams.>

## Open questions
<Carried over from intent.md if still unanswered, plus new ones. Name who should answer each.>
```

## Content rules

- **Every requirement traces to a goal.** Otherwise remove it or move it to non-goals.
- **Every requirement is checkable.** Replace "fast" with a number and "secure" with the specific control.
- **Design names real code.** Real files, services, and data stores from the repository.
- **Build from scratch needs a reason.** When the spec builds a major piece of functionality that a known library already covers, write why the library was rejected: license, maintenance state, size, missing features, or a policy conflict.
- **A new dependency is an open decision.** Mark it as a recommendation and list it under open questions with the product owner as the person who answers.
- **No implementation order and no test file names.** Those belong in `plan.md`.
- **Same names as `intent.md`** for users, systems, and features.

## Storage

Store the spec in the feature folder, next to `intent.md` and any other material about the feature:

```
features/<feature-slug>/
  intent.md
  spec.md
```

When this skill runs as a non-interactive job that opens a pull request, repeat the areas of concern in the pull request description.
