---
name: alantushenko-python
description: Use whenever writing, editing, reviewing, or refactoring Python code. Alex Lantushenko's Python conventions for readable, maintainable code.
---

# alantushenko-python — Python Conventions

Apply these conventions whenever writing or modifying Python code. These are additive to the general `alantushenko` style; where they conflict, the more specific Python rule here wins.

## 1. Prefer dataclasses over loosely-typed collections

Use Python dataclasses instead of `List[str]`, `Dict[int, Any]`, tuples, or nested dicts to carry structured data, because named fields provide better readability and let readers know what each value means.

```python
# Avoid: what do these positions and keys mean?
def make_user() -> Dict[str, Any]:
    return {"name": "Ada", "age": 36, "active": True}

# Prefer: fields document themselves and are type-checked
from dataclasses import dataclass

@dataclass
class User:
    name: str
    age: int
    active: bool
```

Reach for a dataclass when a value has more than one field, when a collection's elements share a fixed shape, or when a dict is passed between functions. Keep plain lists and dicts for genuinely homogeneous, unstructured data (e.g. a set of tags, a lookup table keyed by id).
