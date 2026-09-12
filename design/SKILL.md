---
name: alantushenko-design
description: Alex Lantushenko's personal user interface design rules. Use when designing, building, or reviewing user interface elements such as buttons, forms, and controls.
---

# alantushenko-design — Personal User Interface Style

Apply these rules whenever you design, build, or review user interface elements.

## 1. Buttons

- Every button must have at least three visual states: normal, hovered, and pressed. This includes buttons that are shown only as an icon.
- The states must be clearly different from each other, so the user can see that the button reacts to the pointer.
- A submit button must become disabled right after the user clicks it, so the same data cannot be sent twice.
- A disabled button must look disabled, and it must not react to hover or press.
- Enable the submit button again when the request finishes with an error, so the user can try again. Keep it disabled when the request succeeds and the page moves on.

## 2. Animations

- Animations must not slow down the interface in a way the user can notice.
- If an animation blocks user interaction for more than 500 milliseconds, rework it: make it shorter, or let the user interact while it is still running.

## 3. Grids and Tables

- When a grid or table scrolls, keep the column headings and the pagination controls outside the scrollable area, so they stay visible while the user scrolls the rows.
- Only the rows scroll. Never place headings or pagination controls inside the scroll container.
