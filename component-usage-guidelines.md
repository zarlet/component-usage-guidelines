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
- Choosing among options → use Radio, Checkbox, or Select Menu
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
  autocomplete — a Select Menu would be unusably long
**Don't use when:**
- The input spans multiple lines → use Textarea
- Valid answers are a small, known set → use Select Menu or Radio — free text
  invites typos and unparseable data
- Finding or filtering existing content → use Search Box
- Entering dates or times → use a date/time picker; if the design system has
  none, flag the gap instead of improvising
**Anti-patterns:**
- A field with neither a label nor a placeholder — the user has to guess what to
  enter. In most cases prefer a persistent, visible label; when the layout
  genuinely can't fit one (compact toolbars, search patterns), a placeholder is
  the minimum — pair it with an accessible label (`aria-label`), since
  placeholders disappear on input
- Formatted input without a format hint (helper text, e.g. "DD/MM/YYYY") —
  surface the expected format before the error, not after
- Relying on the input type alone for validation — always validate explicitly

## Textarea
**What it is:** A multi-line free-text input.
**Use when:**
- Expected input is more than a few words and may span multiple lines —
  comments, descriptions, notes
**Don't use when:**
- The answer fits on one line → use Text Field
- Rich formatting (bold, lists, headings) is required → use a rich text editor;
  if the design system has none, flag the gap instead of improvising
**Anti-patterns:**
- A fixed, tiny height for content expected to be long — size the field to the
  expected input, or let it auto-grow with content
- A character limit without a visible counter — if input is limited, show
  remaining characters
- Neither a label nor a placeholder — same labeling rule as Text Field (prefer
  a persistent label; placeholder as the minimum)

## Select Menu
**What it is:** A collapsed list that expands on demand to let the user pick one
option (or several, in the multi-select variant). The closed trigger always
displays the current selection.
**Use when:**
- Picking one option from a short list — roughly 4–12 items
- The options are of secondary importance and don't need to be visible until the
  user interacts — this is the key trade against Radio, which shows everything
- Space is constrained and a sensible default can be preselected
- Multi-select variant: choosing several options from such a list in compact space
**Don't use when:**
- Only 2–3 options that benefit from visibility → use Radio (on submit) or
  Toggle (binary + instant)
- All options should be visible without any interaction → use Radio
- The set is very large (hundreds+) → use Text Field with type-ahead autocomplete
- Switching views of the same content → use Segmented Control
- Navigating between pages → use Tabs, Sidebar, or links
**Anti-patterns:**
- A select menu for 2 options — a Toggle or Radio pair is one click cheaper
- A trigger that doesn't update to show what is selected — after choosing, the
  closed state must display the current selection, not the original label
- No preselected default when a clear common choice exists — make the frequent
  case zero-click

---

# Navigation

---

# Feedback & Notifications

---

# Overlays

---

# Standalone Components

Components with no family. Their "Don't use when → use X instead" pointers carry the cross-references.
