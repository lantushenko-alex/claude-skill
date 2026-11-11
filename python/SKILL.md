---
name: alantushenko-python
description: Use whenever writing, editing, reviewing, or refactoring Python code. Alex Lantushenko's Python conventions for readable, maintainable code.
---

# alantushenko-python — Python Conventions

Apply these conventions whenever writing or modifying Python code. These are additive to the general `alantushenko` style; where they conflict, the more specific Python rule here wins over the general style, but repository conventions still win over both.

## 1. Prefer dataclasses over loosely-typed collections

Use Python dataclasses instead of `list[str]`, `dict[int, Any]`, tuples, or nested dicts to carry structured data, because named fields provide better readability and let readers know what each value means.

```python
# Avoid: what do these positions and keys mean?
def make_user() -> dict[str, Any]:
    return {"name": "Ada", "age": 36, "active": True}

# Prefer: fields document themselves and are type-checked
from dataclasses import dataclass

@dataclass
class User:
    name: str
    age: int
    active: bool
```

Use a dataclass when a value has more than one field, when a collection's elements share a fixed shape, or when a dict is passed between functions. Keep plain lists and dicts for genuinely homogeneous, unstructured data (e.g. a set of tags, a lookup table keyed by id).

## 2. Pass every value a function uses as a parameter

A function must receive everything it reads or changes through its parameters, because the signature then shows the reader all the data the function depends on. Do not let a function use a variable from an outer scope: neither a module-level variable nor a local variable of an enclosing function.

Do not define a function inside another function. A nested function can use the local variables of the enclosing function without declaring them. Define the function at module level, so that a missing parameter becomes an error.

```python
# Avoid: the signature does not show that count_word changes word_counts
def count_words(words: list[str]) -> dict[str, int]:
    word_counts: dict[str, int] = {}

    def count_word(word: str) -> None:
        word_counts[word] = word_counts.get(word, 0) + 1


# Prefer: a module-level function that receives everything it uses
def count_word(word: str, word_counts: dict[str, int]) -> None:
    word_counts[word] = word_counts.get(word, 0) + 1
```

Module-level constants, imports, and other module-level functions and classes may be used without passing them. A decorator may define its wrapper function inside, because that is how decorators work.
