---
name: alantushenko
description: Alex Lantushenko's personal coding style and conventions. Use when writing or editing code.
---

# alantushenko — Personal Coding Style

Apply these conventions whenever writing or modifying code.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
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


## 4. Git actions

- Do not push or commit anything if not explicitly asked
- When rename file, use git rename if you are inside git repository

## 5. Avoid duplicate code

- Detect duplicate code and deduplicate it. 

## 6. Naming

- Use elegant and descriptive names for functions, classes, and variables. Avoid abbreviations except those that are generally accepted and widely known
- Function names should be verbs (they do some action)
- Avoid magic numbers. Create dedicated constants or enums for them

## 7. Inheritance

- Prefer composition over inheritance

## 8. Grammar

- If I make grammar mistakes in my prompts, fix them without asking me, but do not change meaning. 

## 9. Loops and ifs

- Prefer exiting loops and if blocks early rather than creating deep nesting

## 10. Comments

- Write self-documenting code first; a good name beats a comment.
