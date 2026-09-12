---
name: alantushenko
description: "Use for writing, editing, reviewing, refactoring, or testing code in Alex Lantushenko's style: explicit assumptions, clear naming, low duplication, early exits, and preserving project conventions."
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

## 2. Git Actions

- When renaming a file, use `git mv` if you are inside a git repository

## 3. Avoid Duplicate Code

- Don't introduce duplication: if your change would copy existing logic, extract and reuse a shared helper instead.
- Mention pre-existing duplication, but don't refactor it unless asked.

## 4. Naming

- Use descriptive names for functions, classes, and variables; names should describe intent, not implementation. Avoid abbreviations except those that are generally accepted and widely known
- Action-oriented functions should use verbs.
- Predicates should usually start with `is`, `has`, `can`, or `should`.
- Components, classes, types, selectors, and value-like helpers may use nouns when that better matches the surrounding code.
- Do not use synonums anywhere. The same thing should always have the same name
- Avoid non-obvious magic numbers. Create dedicated constants or enums when the value is domain-significant, reused, or unclear inline; keep obvious one-off literals inline when extraction would add noise.

## 5. Inheritance

- Prefer composition over inheritance

## 6. Grammar

These rules apply to everything you write: chat replies, code, comments, docstrings, documentation, and commit messages.

- If the user's prompt contains grammar mistakes, silently interpret the corrected meaning. When the prompt text is meant to be inserted into code, docs, or commit messages, fix the grammar without changing the meaning.
- Use simple language that any non-native speaker can read. Avoid complex phrases, slang, analogies, and rarely used words
- Avoid using abbreviations and shorthands. Use only widely known ones.
- Developer jargon counts as slang even when it is common among native speakers: "in-flight", "happy path", "blast radius", "choke point", "footgun", "sane defaults", and similar. Describe the behavior in plain words instead — for example, write "requests running at the same time" instead of "in-flight requests".

## 7. Loops and ifs

- Prefer exiting loops and if blocks early rather than creating deep nesting

## 8. Comments

- Write self-documenting code first; a good name beats a comment.
- Don't add comments that only restate the code.
- Keep comments that explain intent, constraints, or tradeoffs when the code alone is not enough.
- Update or remove comments only when your change makes them incorrect.

## 9. Validation

- Validate only what is relevant to the change.
- Prefer targeted tests, type checks, or lints over broad project-wide runs.
- Don't fix unrelated failing checks unless asked.
- Don't reformat unrelated files as part of validation.

## 10. Dependencies

- Do not add new dependencies unless they are clearly justified by the task.
- Prefer existing project dependencies, standard libraries, and local utilities.
- If a new dependency is warranted, explain why the added cost is worth it.
- When adding a third-party dependency, pin an exact version instead of "latest", a range, or an unpinned entry, where the package manager allows it.
