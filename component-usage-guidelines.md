# Component Usage Guidelines

> **Purpose:** This file answers one question: *when to use which component.*
> It is design-system-agnostic: it covers behavior and decision rules only. Pair it with your own design system's visual specs and tokens for how components look.
>
> **For AI consumers:** Before generating any UI, resolve every component choice against this file. If a needed component has no entry here, say so explicitly instead of improvising.
>
> **Entry template:** What it is · Use when · Placement (optional) · Don't use when (each with "→ use X instead") · Anti-patterns
>
> **References:** Usage rules in this file are grounded in, and reconciled against:
> [W3C ARIA Authoring Practices Guide](https://www.w3.org/WAI/ARIA/apg/patterns/) ·
> [IBM Carbon Design System](https://carbondesignsystem.com/) ·
> [SAP Fiori Design System](https://www.sap.com/design-system/fiori-design-web/)
> Where these sources conflict with each other, the chosen rule is deliberate and the alternative is noted.

---

# Inputs

## Button
**What it is:** A clickable element that triggers an immediate action — never navigation.
Variants: Primary (solid brand background), Secondary (outline), Icon button (icon only).
**Use when:**
- Triggering an action: submit, upload, save, confirm, open a modal
- Primary: the single most important action on the screen — only one per screen;
  a modal or side panel counts as its own screen and may have its own primary
- A page does NOT have to have a primary button. If the page's most important
  interactions live elsewhere (a table, cards, links), a Secondary button alone is
  correct. Decide by how frequently the action is used and how central it is to
  the page's purpose.
- Secondary: supporting actions, or the negative half of a pair (Cancel / Back)
- Icon button: compact, well-understood actions (overflow menu, close)
**Placement:**
- In a Primary + Secondary group, the Primary sits closest to the nearest page or
  container edge: top-right group → [Secondary] [Primary]; bottom-left group →
  [Primary] [Secondary].
**Don't use when:**
- Navigating to another page or object → use a text link, Tabs, or Sidebar
- Toggling a persistent on/off state → use Toggle
- Choosing among options → use Radio, Checkbox, or Dropdown/Select
**Anti-patterns:**
- More than one Primary button per screen — demote the rest to Secondary
- Icon button without an accessible label (`aria-label`); non-obvious icons also need a Tooltip
- A destructive action without a confirmation step (e.g. a Modal) — if the design
  system has no danger button variant, flag the gap instead of improvising one

## Text Field
**What it is:** A single-line free-text input.
**Use when:**
- The input is unique or unpredictable — it can't be offered as a preset list
  (names, titles, free-form values)
- The data is memorable and typed faster free-hand than picked from a control
  (email, phone, URL, password)
- Picking one item from a very large set (hundreds+), paired with type-ahead
  autocomplete — a Dropdown/Select would be unusably long
**Don't use when:**
- The input spans multiple lines → use Textarea
- Valid answers are a small, known set → use Dropdown/Select or Radio — free text
  invites typos and unparseable data
- Finding or filtering existing content → use Search Box
- Entering dates or times → use a date/time picker; if the design system has
  none, flag the gap instead of improvising
**Anti-patterns:**
- Placeholder as the only label — it disappears on input; every field needs a
  visible, persistent label
- Formatted input without a format hint (helper text, e.g. "DD/MM/YYYY") —
  surface the expected format before the error, not after
- Relying on the input type alone for validation — always validate explicitly

---

# Navigation

---

# Feedback & Notifications

---

# Overlays

---

# Standalone Components

Components with no family. Their "Don't use when → use X instead" pointers carry the cross-references.
