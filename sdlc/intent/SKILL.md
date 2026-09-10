---
name: sdlc-intent
description: Use when a person describes an idea, problem, ticket, or incident and wants it captured as an intent.md (Stage 1 Plan of the AI-native SDLC). Brainstorm until the idea is concrete, then write the file using the organization's template.
---

# sdlc-intent — Capture an idea as `intent.md`

`intent.md` is a short, version-controlled proto-spec. It states **what is wanted, why, and under which constraints**, in the originator's own words. Committing it starts Stage 2: Design, where `spec.md` is produced from it (see the `sdlc-spec` skill).

The originator is often not an engineer. Ideas arrive by three routes: a brainstorm with Claude, a filed ticket, or an incident surfaced by an alert.

Repository conventions for the template and the storage location win over this skill.

## Workflow

1. **Listen.** The originator describes the problem in their own words. Do not ask for formal language.
2. **Brainstorm until the idea is concrete.** Concrete means: the problem is observable, the outcome is testable, the constraints are explicit, and the remaining unknowns are listed as open questions instead of guessed.
3. **Write `intent.md`** using the template below. Keep it to a page or less.
4. **Read the draft back** so the originator can correct misunderstandings.
5. **Save the file** in the feature folder (see Storage). The product owner reviews and approves the committed file before Stage 2 starts.

## Template

```markdown
# Intent: <short title>

## Problem
<What is wrong or missing today, and how you know. Observable facts, not solutions.>

## Proposed outcome
<What the world looks like when this is done. Written so someone could check if it happened.>

## Constraints
<Rules the solution must respect: security, privacy, compliance, budget, deadlines, existing systems that must not change.>

## Open questions
<Things nobody in the conversation could answer. One question per line.>
```

## Example

```markdown
# Intent: claims status self-service

## Problem
Customers phone the contact center to ask where their claim is.
Handlers spend roughly a third of call time on status-only queries.

## Proposed outcome
Customers see claim status, next step and expected date in the portal.

## Constraints
No new PII in the portal session. Existing authentication only.

## Open questions
Do third-party loss adjusters need access too?
```

## Content rules

- **Problem, not solution.** If the originator proposes a solution, record it under proposed outcome and keep the problem section factual.
- **Numbers over adjectives.** "A third of call time" beats "a lot of time". If the exact figure is unknown, write "roughly" and add the figure to open questions.
- **Every constraint is checkable.** "Existing authentication only" is checkable. "Must be secure" is not.
- **Do not resolve open questions yourself.** A listed unknown is more useful than a hidden assumption.
- **Keep the author's voice and vocabulary.** Correct grammar only.
- **No implementation details.** File names, libraries, and tables belong in `spec.md` and `plan.md`.

## Storage

Every feature has one folder under `features/` in the product repository, named with a short kebab-case slug. All information about the feature lives there: `intent.md`, later `spec.md` and `plan.md`, and any other material such as mockups, decisions, or notes. If the feature folder already exists, put `intent.md` into it.

```
features/<feature-slug>/
  intent.md
```
