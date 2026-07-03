---
name: alantushenko
description: Use for writing, editing, reviewing, refactoring, or testing code in Alex Lantushenko's style: minimal surgical changes, explicit assumptions, simple designs, clear naming, low duplication, early exits, and preserving project conventions.
---

# alantushenko — Personal Coding Style

Apply these conventions whenever writing or modifying code.

## 0. Precedence

Apply these rules in this order:
- Follow the user's explicit instructions first.
- Follow repository and file-local conventions next.
- Apply this style where it does not conflict with the first two.
- If rules conflict and the right choice is unclear, state the conflict explicitly and choose the smallest reasonable change.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly when they matter.
- If uncertainty materially affects correctness, scope, or design, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Git Actions

- Do not push or commit anything unless explicitly asked
- When renaming a file, use `git mv` if you are inside a git repository

## 5. Avoid Duplicate Code

- Don't introduce duplication: if your change would copy existing logic, extract and reuse a shared helper instead.
- Mention pre-existing duplication, but don't refactor it unless asked.

## 6. Naming

- Use descriptive names for functions, classes, and variables; names should describe intent, not implementation. Avoid abbreviations except those that are generally accepted and widely known
- Action-oriented functions should use verbs.
- Predicates should usually start with `is`, `has`, `can`, or `should`.
- Components, classes, types, selectors, and value-like helpers may use nouns when that better matches the surrounding code.

- Avoid non-obvious magic numbers. Create dedicated constants or enums when the value is domain-significant, reused, or unclear inline; keep obvious one-off literals inline when extraction would add noise.

## 7. Inheritance

- Prefer composition over inheritance

## 8. Grammar

- If the user's prompt contains grammar mistakes, silently interpret the corrected meaning. When the prompt text is meant to be inserted into code, docs, or commit messages, fix the grammar without changing the meaning.

## 9. Loops and ifs

- Prefer exiting loops and if blocks early rather than creating deep nesting

## 10. Comments

- Write self-documenting code first; a good name beats a comment.
- Don't add comments that only restate the code.
- Keep comments that explain intent, constraints, or tradeoffs when the code alone is not enough.
- Update or remove comments only when your change makes them incorrect.

## 11. Error Handling

- Don't add speculative defensive code for unrealistic scenarios.
- Preserve the surrounding codebase's error-handling style.
- Handle realistic failures at system boundaries such as I/O, parsing, network calls, persistence, and third-party APIs.

## 12. Validation

- Validate only what is relevant to the change.
- Prefer targeted tests, type checks, or lints over broad project-wide runs.
- Don't fix unrelated failing checks unless asked.
- Don't reformat unrelated files as part of validation.

## 13. Dependencies

- Do not add new dependencies unless they are clearly justified by the task.
- Prefer existing project dependencies, standard libraries, and local utilities.
- If a new dependency is warranted, explain why the added cost is worth it.
