---
name: alantushenko-java
description: Use whenever writing, editing, reviewing, or refactoring Java code. Alex Lantushenko's Java conventions for readable, maintainable code.
---

# alantushenko-java — Java Conventions

Apply these conventions whenever writing or modifying Java code. These are additive to the general `alantushenko` style; where they conflict, the more specific Java rule here wins.

## 1. Never assign null to a Boolean

A `Boolean` holds `true` or `false` — never set one to `null`. A third state forces every use site to guard against it. When a `Boolean` arrives from outside code you control (JSON, database, third-party API), turn `null` into `false` at that boundary with `Boolean.TRUE.equals(value)`.

```java
// Avoid
Boolean isActive = null;
if (isActive != null && isActive) { activate(); }

// Prefer
Boolean isActive = false;
if (isActive) { activate(); }
```

## 2. Treat null and empty the same for arrays and strings

For arrays and strings, `null` and empty both mean "no value". Process them in one branch, not two.

```java
// Avoid
if (name == null) { throw new IllegalArgumentException("name is missing"); }
if (name.isEmpty()) { return DEFAULT_NAME; }

// Prefer
if (name == null || name.isEmpty()) { return DEFAULT_NAME; }
```

Use `ArrayUtils.isEmpty` / `StringUtils.isEmpty` if the project already has Apache Commons; otherwise one small shared helper.
