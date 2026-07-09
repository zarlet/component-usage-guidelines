# Design: Notessa Component Usage Guidelines

> **AMENDMENT (2026-07-09, supersedes conflicting statements below):**
> The guideline is now **design-system-agnostic** — decoupled from Notessa entirely:
> - No Notessa mentions in the deliverable; no `Status: figma/extrapolated` field
> - Visual specifics generalized (e.g. "cyan/800 bg" → "solid brand background"); Notessa-specific component names generalized (Workflow Card → Card, AI Chat Input → AI Prompt Input)
> - New optional **Placement** template field (first used by Button)
> - Confirmation is **per component**; family comparison blocks are written only after all entries in the family are confirmed
> - Tasks referencing Notessa files (visual-truth check in Task 7, CLAUDE.md pointer in Task 8) are dropped or handled outside this repo
> - The embedded entry drafts still contain Notessa specifics — generalize them during the per-component reconcile step


**Date:** 2026-07-09
**Status:** Approved pending user review
**Deliverable:** `component-usage-guidelines.md (repo root)`

## Problem

The existing `design-system-rules.md` documents how components *look* (colors, typography, spacing, per-component visual specs) but not *when to use them*. AI-driven UI generation needs decision rules — otherwise the model improvises component choices (e.g. segmented control where tabs belong, toast where a modal is required).

## Goals

- One markdown file, AI-first but human-readable, answering "which component do I use here?"
- Cover existing Figma components plus the core gaps needed to generate full screens
- Capture comparison knowledge between similar components (families)
- Publishable to GitHub later as part of the design system repo

## Non-Goals

- Visual specs (stay in `design-system-rules.md`)
- Color/token values (stay in `design-tokens.json`)
- Content/copy rules, interaction states, page-level composition recipes (possible future additions — explicitly deferred)
- GitHub repo structure and publication (later phase)
- Intent-based decision index at the top of the file (approach B/C — revisit after entries exist, distilled from the family rules of thumb)

## Document Structure

### 1. Header block

- Purpose statement
- Relationship to sibling files: visual truth = `design-system-rules.md`, color truth = `design-tokens.json`, behavioral truth = this file
- Instruction for AI consumers: "Before generating UI, resolve every component choice against this file."

### 2. Component entries (~20)

Uniform template per component:

```markdown
## Component Name
**What it is:** one sentence.
**Use when:** 2–4 bullet conditions.
**Don't use when:** 2–4 bullets, each with "→ use [X] instead."
**Anti-patterns:** observed/likely misuses, phrased as prohibitions.
**Status:** `figma` | `extrapolated`
```

**Existing components (status: `figma`):**
Button (primary / secondary / icon variants), Tabs, Segmented Control, Table, Badge/Tag, Search Box, Sidebar (nav list), AI Chat Input, Workflow Card, Breadcrumb/Header

**Core gaps (status: `extrapolated`):**
Modal/Dialog, Dropdown/Select, Text Field, Textarea, Toast, Inline Alert/Banner, Empty State, Tooltip, Radio, Checkbox, Toggle

The `status` field tells AI consumers whether a component is grounded in Figma or defined by extrapolation from tokens and existing patterns. Extrapolated components get visual specs added to `design-system-rules.md` later, when designed in Figma.

### 3. Family comparison blocks

Entries are grouped into families; after each family's entries, one comparison block: a table of differentiating dimensions plus a compressed "rule of thumb" heuristic (the part that actually drives an AI generation decision).

**Families:**

1. **Feedback & Notifications** — Toast · Inline Alert/Banner · Modal (confirmation) · Badge (status)
2. **Navigation** — Tabs · Segmented Control · Sidebar · Breadcrumb
3. **Overlays** — Modal · Tooltip · Dropdown/Popover
4. **Inputs** — Button variants · Text Field · Textarea · Dropdown/Select · Radio · Checkbox · Toggle · Search Box

A component may appear in two families when the comparisons answer different questions (e.g. Modal in Feedback = "how loud should this message be"; Modal in Overlays = "what floats above the page"). Segmented Control appears in Navigation and in the Inputs selection-control comparison.

**Comparison block format** (example, Feedback family):

```markdown
### Choosing between feedback components

| Dimension          | Toast              | Inline Alert       | Modal              | Badge             |
|--------------------|--------------------|--------------------|--------------------|-------------------|
| Interruption level | Low (auto-dismiss) | Medium (persists)  | High (blocks)      | None (ambient)    |
| User action needed | None               | Optional           | Required           | None              |
| Message lifetime   | Seconds            | Until resolved     | Until decided      | While state lasts |
| Best for           | Success confirms   | Contextual errors  | Destructive confirm| Object status     |

**Rule of thumb:** match interruption level to consequence severity.
Reversible + successful → toast. Needs fixing → inline alert.
Irreversible → modal. Not an event, just a state → badge.
```

Dimensions are chosen to differentiate, not describe — every row must distinguish at least two columns.

Components that belong to no family (Table, Workflow Card, Empty State, AI Chat Input) stand alone without a comparison block; their "Don't use when → use X instead" pointers carry the cross-references.

## Grounding Approach

- **Existing components:** usage rules derived from observed usage across the 4 Figma core pages (Projects, Document List, Ask Notessa, Workflow) and reference HTML implementations (e.g. `document-list.html`). Example: segmented control is only ever used for switching views within one page, tabs for navigating page sections — that observed distinction becomes the written rule.
- **Extrapolated components:** usage rules follow industry-standard conventions constrained by existing Notessa tokens — e.g. Toast/Inline Alert map to the `semantic.color.feedback.{error,warning,success,info}` token groups already defined in `design-tokens.json`.

## Integration

- Add one line to the Notessa section of `/Users/yuqing/Claude/CLAUDE.md`: usage rules pointer alongside the existing design-tokens / design-system-rules / reference-implementation pointers.

## Future Phases (out of scope)

1. Distill family rules of thumb into a top-of-file intent index (approach B/C)
2. Additional dimensions per entry: content/copy rules, interaction states, layout composition recipes
3. GitHub publication: README + 3 core files + reference HTML
