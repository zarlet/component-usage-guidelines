# Notessa Component Usage Guidelines Implementation Plan

> **AMENDMENT (2026-07-09, supersedes conflicting statements below):**
> The guideline is now **design-system-agnostic** — decoupled from Notessa entirely:
> - No Notessa mentions in the deliverable; no `Status: figma/extrapolated` field
> - Visual specifics generalized (e.g. "cyan/800 bg" → "solid brand background"); Notessa-specific component names generalized (Workflow Card → Card, AI Chat Input → AI Prompt Input)
> - New optional **Placement** template field (first used by Button)
> - Confirmation is **per component**; family comparison blocks are written only after all entries in the family are confirmed
> - Tasks referencing Notessa files (visual-truth check in Task 7, CLAUDE.md pointer in Task 8) are dropped or handled outside this repo
> - The embedded entry drafts still contain Notessa specifics — generalize them during the per-component reconcile step


> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Write `component-usage-guidelines.md (repo root)` — an AI-first usage guideline (when to use which component) with 21 component entries organized into 4 families plus standalone components, each family closed by a comparison table + rule of thumb.

**Architecture:** Single markdown deliverable, built section-by-section: header → Inputs → Navigation → Feedback → Overlays → Standalone → consistency check → CLAUDE.md integration. Content is fully specified in this plan; the executor assembles and verifies.

**Tech Stack:** Markdown only. Verification via `grep`. **No git commits** — the Notessa folder is not a git repository; versioning is deferred to the GitHub-publication phase per the approved spec (`docs/specs/2026-07-09-component-usage-guidelines-design.md`).

**Source-of-truth files (read-only context for the executor):**
- `/Users/yuqing/Claude/Notessa/design-system-rules.md` — visual specs the entries must not contradict
- `/Users/yuqing/Claude/Notessa/design-tokens.json` — semantic feedback tokens referenced by Toast/Alert entries
- `/Users/yuqing/Claude/Notessa/docs/specs/2026-07-09-component-usage-guidelines-design.md` — approved spec

**External usage references (authoritative grounding):**
1. **W3C ARIA Authoring Practices Guide** — https://www.w3.org/WAI/ARIA/apg/patterns/ — canonical pattern definitions and interaction semantics
2. **IBM Carbon Design System** — https://carbondesignsystem.com/components/<component>/usage/ — "When to use / When not to use" per component
3. **SAP Fiori Design System** — https://www.sap.com/design-system/fiori-design-web/v1-148/ui-elements/<component> — "When to use / When not to use" per component

**Reference grounding workflow — applies to every content task (Tasks 2–6):**

The entry drafts embedded in this plan are *starting drafts*, not final content. Confirmation is **per component**; family comparison blocks are written only **after every entry in the family is confirmed**. For each task:

1. **Per component, one at a time:**
   a. **Research:** WebFetch the relevant pages from the three references (e.g. for Checkbox: APG checkbox pattern, Carbon checkbox usage, Fiori checkbox). Skip a reference only if it has no page for that component.
   b. **Reconcile:** Compare the plan's draft entry against the references. Adjust rules where references disagree with the draft; keep Notessa-specific observations (Figma usage) that references can't know. Where references conflict with each other, note the conflict and pick the rule that fits Notessa's patterns.
   c. **Confirm with user (mandatory gate):** Present the reconciled entry — highlighting what changed from the plan draft and why, with reference attribution — and wait for explicit confirmation BEFORE writing.
   d. **Write:** On confirmation, append the entry to the family's section in the deliverable. Then move to the next component.
2. **Family comparison block:** After ALL entries in the family are confirmed and written, draft the comparison table + rule of thumb from the confirmed entries (not the plan drafts), present it for confirmation, then write it.

Every rule that came from a reference keeps its provenance available on request; the deliverable itself stays terse (AI-first) and lists the three references once in its header.

---

### Task 1: File skeleton + header block

**Files:**
- Create: `component-usage-guidelines.md (repo root)`

- [ ] **Step 1: Create the file with header block and section scaffolding**

Write exactly this content:

```markdown
# Component Usage Guidelines — Notessa

> **Purpose:** This file answers one question: *when to use which component.*
> It is the behavioral counterpart to two sibling files:
> - **Visual truth:** `design-system-rules.md` — how components look (colors, typography, spacing, per-component specs)
> - **Color truth:** `design-tokens.json` — token values
>
> **For AI consumers:** Before generating any UI, resolve every component choice against this file. If a needed component has no entry here, say so explicitly instead of improvising.
>
> **Status field:** `figma` = exists in the Notessa Figma designs; usage rules derived from observed usage across the 4 core pages (Projects, Document List, Ask Notessa, Workflow). `extrapolated` = not yet designed in Figma; usage rules follow standard conventions constrained by existing Notessa tokens. Visual specs for extrapolated components will be added to `design-system-rules.md` when they are designed.
>
> **References:** Usage rules in this file are grounded in, and reconciled against:
> [W3C ARIA Authoring Practices Guide](https://www.w3.org/WAI/ARIA/apg/patterns/) ·
> [IBM Carbon Design System](https://carbondesignsystem.com/) ·
> [SAP Fiori Design System](https://www.sap.com/design-system/fiori-design-web/)
> Where these sources conflict with observed Notessa usage, Notessa's own patterns win and the deviation is deliberate.

---

# Inputs

---

# Navigation

---

# Feedback & Notifications

---

# Overlays

---

# Standalone Components

Components with no family. Their "Don't use when → use X instead" pointers carry the cross-references.
```

- [ ] **Step 2: Verify skeleton**

Run: `grep -c "^# " component-usage-guidelines.md (repo root)`
Expected: `6` (title + 5 section headings)

---

### Task 2: Inputs family (8 entries + comparison)

**Files:**
- Modify: `component-usage-guidelines.md (repo root)` (fill the `# Inputs` section)

- [ ] **Step 1: Write the 8 Inputs entries**

Insert under `# Inputs`, before the `# Navigation` heading:

```markdown
## Button
**What it is:** A clickable element that triggers an immediate action. Variants: Primary (cyan/800 bg), Secondary outline (white bg, gray/300 border), Icon button (transparent).
**Use when:**
- Triggering an action: submit, upload, save, open a modal
- Primary: the single most important action in a view region (e.g. "Upload") — at most one per region
- Secondary outline: supporting actions alongside a primary (e.g. "Collapse All")
- Icon button: compact, well-understood actions (overflow `dots-horizontal`, close `x`)
**Don't use when:**
- Navigating between pages or sections → use Tabs, Sidebar, or a text link
- Toggling a persistent on/off state → use Toggle
- Choosing among options → use Radio, Checkbox, or Dropdown/Select
**Anti-patterns:**
- More than one Primary button in the same view region — demote the rest to Secondary
- Icon button for a non-obvious icon without a Tooltip
- A destructive action as a plain button with no confirmation Modal
**Status:** `figma`

## Text Field
**What it is:** A single-line free-text input.
**Use when:**
- Short, unconstrained input: names, emails, titles, numbers
- The expected answer fits on one line
**Don't use when:**
- Input runs to multiple lines → use Textarea
- The valid answers are a known, enumerable set → use Dropdown/Select or Radio
- The user is filtering or finding items in a list → use Search Box
**Anti-patterns:**
- Free text where options are enumerable (invites typos and unparseable data)
- Placeholder text as the only label — placeholder disappears on input
**Status:** `extrapolated`

## Textarea
**What it is:** A multi-line free-text input.
**Use when:**
- Paragraph-length input: descriptions, notes, comments
**Don't use when:**
- The answer is one line → use Text Field
- The input is a conversational prompt to AI → use AI Chat Input
**Anti-patterns:**
- A fixed tiny height for content that is expected to be long
**Status:** `extrapolated`

## Dropdown/Select
**What it is:** A collapsed list that expands to let the user pick one option.
**Use when:**
- 5 or more options
- Space is constrained and a sensible default exists
**Don't use when:**
- 4 or fewer options where seeing them all helps → use Radio (pick one) or Checkbox (pick many)
- A binary setting with instant effect → use Toggle
- Switching views of the same content → use Segmented Control
**Anti-patterns:**
- A dropdown for 2 options — a Toggle or Radio pair is one click cheaper
- A dropdown as navigation between pages
**Status:** `extrapolated`

## Radio
**What it is:** A visible group of mutually exclusive options; picking one deselects the others.
**Use when:**
- 2–4 options and the user benefits from seeing all of them at once
- The choice takes effect on form submit, not instantly
**Don't use when:**
- 5+ options → use Dropdown/Select
- Multiple options can be selected at once → use Checkbox
- The choice applies instantly → use Toggle (binary) or Segmented Control (named views)
**Anti-patterns:**
- A radio group with no default selected
- A single radio by itself — it can never be unchecked
**Status:** `extrapolated`

## Checkbox
**What it is:** Independent on/off choices; any number can be selected.
**Use when:**
- Selecting multiple items from a list
- A single opt-in inside a form (takes effect on submit)
**Don't use when:**
- Options are mutually exclusive → use Radio
- The change applies instantly outside a form → use Toggle
**Anti-patterns:**
- A checkbox that triggers an immediate action on click — checkboxes declare state for a later submit
**Status:** `extrapolated`

## Toggle
**What it is:** A binary switch whose change takes effect immediately.
**Use when:**
- On/off settings that apply the moment they are flipped (e.g. a notification setting)
**Don't use when:**
- The change only applies after a Save/Submit → use Checkbox
- There are more than two states → use Segmented Control or Radio
**Anti-patterns:**
- A Toggle inside a form that ends in a Save button — users can't tell when it took effect
- A label where the on/off meaning is ambiguous (label the state, not the action)
**Status:** `extrapolated`

## Search Box
**What it is:** A text input (240px standard, in toolbars) for finding or filtering items within existing content.
**Use when:**
- Filtering rows of a Table or items in a list
- Locating an item in a set too large to scan
**Don't use when:**
- Collecting structured form data → use Text Field
- Asking questions of documents/AI → use AI Chat Input
**Anti-patterns:**
- Search as the only way to reach content that also deserves browsable structure (Tabs, Sidebar)
**Status:** `figma`

### Choosing between selection inputs

| Dimension        | Radio       | Checkbox     | Toggle        | Dropdown/Select | Segmented Control |
|------------------|-------------|--------------|---------------|-----------------|-------------------|
| Options visible  | All         | All          | 2 (implicit)  | Collapsed       | All               |
| Selections       | One         | Many         | One (binary)  | One             | One               |
| Effect timing    | On submit   | On submit    | Instant       | On submit       | Instant           |
| Option count     | 2–4         | 2–7          | 2             | 5+              | 2–4               |

**Rule of thumb:** instant + binary → Toggle. Instant + named views → Segmented Control.
Deferred + pick one of few → Radio. Deferred + pick many → Checkbox. Pick one of many → Dropdown/Select.
```

- [ ] **Step 2: Verify Inputs section**

Run: `awk '/^# Inputs/,/^# Navigation/' component-usage-guidelines.md (repo root) | grep -c "^## "`
Expected: `8`

---

### Task 3: Navigation family (4 entries + comparison)

**Files:**
- Modify: `component-usage-guidelines.md (repo root)` (fill the `# Navigation` section)

- [ ] **Step 1: Write the 4 Navigation entries**

Insert under `# Navigation`, before the `# Feedback & Notifications` heading:

```markdown
## Tabs
**What it is:** Page-level section navigation under the header (e.g. Documents · Workflow · Ask Notessa). Active tab: cyan/700 underline.
**Use when:**
- Switching between major sections of a page, each with distinct content
- 2–5 sections, one level of navigation
**Don't use when:**
- Switching how the *same* content is displayed → use Segmented Control
- Navigating a long or growing list of destinations → use Sidebar
- Stepping through a sequence → use a wizard/stepper pattern (not yet in this system — flag it)
**Anti-patterns:**
- Tabs that trigger actions instead of revealing sections
- More than 5 tabs — regroup the content instead
**Status:** `figma`

## Segmented Control
**What it is:** A compact toggle group (gray/100 container, white active segment) that switches views or modes of the same content, instantly, in place.
**Use when:**
- 2–4 alternate views of the same data (e.g. list vs. grid)
- The switch is instant and stays within the current page area
**Don't use when:**
- The sections have genuinely different content → use Tabs
- The selection is part of a form submitted later → use Radio
**Anti-patterns:**
- Segmented control as page navigation
- Segments whose content differs so much the user loses context when switching
**Status:** `figma`

## Sidebar
**What it is:** A vertical navigation list in a two-panel layout (264px, gray/100), with grouped sections (e.g. Pinned, Recents in Ask Notessa).
**Use when:**
- Navigating many parallel items of the same kind (chats, documents) while keeping content visible
- Items need grouping into labeled sections
**Don't use when:**
- There are only 2–5 fixed sections → use Tabs
**Anti-patterns:**
- Burying the page's primary action inside the sidebar
- Two sidebars on one screen
**Status:** `figma`

## Breadcrumb
**What it is:** A hierarchical location trail in the header of detail pages (e.g. / Projects / Project Name), separators in gray/500.
**Use when:**
- The page is 2+ levels deep and users need a path back up the hierarchy
**Don't use when:**
- The page is top-level → no breadcrumb
- It would be the primary navigation → use Tabs or Sidebar; breadcrumb only *shows* location
**Anti-patterns:**
- Rendering the current page as a clickable crumb
- Breadcrumbs alongside a Sidebar that already expresses the same hierarchy
**Status:** `figma`

### Choosing between navigation components

| Dimension        | Tabs                  | Segmented Control        | Sidebar                  | Breadcrumb          |
|------------------|-----------------------|--------------------------|--------------------------|---------------------|
| Switches between | Sections of a page    | Views of same content    | Many parallel items      | Levels of hierarchy |
| Content changes  | Different content     | Same data, reshaped      | Different item, same kind| Shows location only |
| Item count       | 2–5                   | 2–4                      | Unbounded, grouped       | = page depth        |
| Position         | Under header          | In content toolbar       | Left panel               | In header           |

**Rule of thumb:** different content sections → Tabs. Same content, different lens → Segmented Control.
Long or growing list of destinations → Sidebar. Showing where you are → Breadcrumb.
```

- [ ] **Step 2: Verify Navigation section**

Run: `awk '/^# Navigation/,/^# Feedback/' component-usage-guidelines.md (repo root) | grep -c "^## "`
Expected: `4`

---

### Task 4: Feedback & Notifications family (3 entries + comparison)

**Files:**
- Modify: `component-usage-guidelines.md (repo root)` (fill the `# Feedback & Notifications` section)

- [ ] **Step 1: Write the 3 Feedback entries**

Insert under `# Feedback & Notifications`, before the `# Overlays` heading. Note: Modal's own entry lives in Overlays; it appears here only in the comparison table.

```markdown
## Toast
**What it is:** A transient, auto-dismissing notification overlaid at the screen edge. Lowest interruption level.
**Use when:**
- Confirming success of a reversible or background operation (saved, uploaded, copied)
- Information that requires no response
**Don't use when:**
- An error the user must fix → use Inline Alert, next to where the fix happens
- A decision is required before continuing → use Modal
- Communicating a lasting state of an object → use Badge
**Anti-patterns:**
- A toast for an error that disappears before the user can read or act on it
- Critical links or actions available *only* inside a toast
- Stacking several toasts at once
**Status:** `extrapolated`

## Inline Alert/Banner
**What it is:** A persistent message embedded in the page or section it concerns. Colors come from the `semantic.color.feedback.{error,warning,success,info}` token groups in `design-tokens.json`.
**Use when:**
- An error or warning tied to specific content, persisting until resolved
- Page-level notices the user should see but that don't block work
**Don't use when:**
- A quick success confirmation → use Toast
- The user must decide before anything else can happen → use Modal
**Anti-patterns:**
- Auto-dismissing an alert that reports an unresolved error
- A global banner for a field-level error — place the alert next to its context
**Status:** `extrapolated`

## Badge
**What it is:** A small, ambient, non-interactive label showing an object's state or category (e.g. document type, version: Original/Amendment).
**Use when:**
- Showing status or category on rows in Tables and items in lists
- The information is a *state that lasts*, not an event
**Don't use when:**
- Announcing an event → use Toast or Inline Alert
- The element triggers an action → use Button
**Anti-patterns:**
- Clickable badges that behave like buttons
- More badge color variants than users can keep meanings for — stick to the specced set
**Status:** `figma`

### Choosing between feedback components

| Dimension          | Toast              | Inline Alert       | Modal               | Badge             |
|--------------------|--------------------|--------------------|---------------------|-------------------|
| Interruption level | Low (auto-dismiss) | Medium (persists)  | High (blocks)       | None (ambient)    |
| User action needed | None               | Optional           | Required            | None              |
| Message lifetime   | Seconds            | Until resolved     | Until decided       | While state lasts |
| Best for           | Success confirms   | Contextual errors  | Destructive confirm | Object status     |

**Rule of thumb:** match interruption level to consequence severity.
Reversible + successful → Toast. Needs fixing → Inline Alert.
Irreversible → Modal. Not an event, just a state → Badge.
```

- [ ] **Step 2: Verify Feedback section**

Run: `awk '/^# Feedback/,/^# Overlays/' component-usage-guidelines.md (repo root) | grep -c "^## "`
Expected: `3`

---

### Task 5: Overlays family (2 entries + comparison)

**Files:**
- Modify: `component-usage-guidelines.md (repo root)` (fill the `# Overlays` section)

- [ ] **Step 1: Write the 2 Overlays entries**

Insert under `# Overlays`, before the `# Standalone Components` heading. Note: Dropdown/Select's own entry lives in Inputs; it appears here only in the comparison table.

```markdown
## Modal
**What it is:** A blocking dialog over a dimmed page; nothing behind it is interactive until it's dismissed.
**Use when:**
- Confirming an irreversible or destructive action (delete, overwrite)
- A short, focused subtask that must complete before continuing (create, rename)
**Don't use when:**
- The message doesn't require an immediate decision → use Toast or Inline Alert
- The content is a complex or multi-step flow → use a dedicated page
- A passive hint on hover → use Tooltip
**Anti-patterns:**
- A modal opening another modal
- A modal with no explicit cancel/close path
- A modal for information that could sit inline
**Status:** `extrapolated`

## Tooltip
**What it is:** A small text label appearing on hover or keyboard focus.
**Use when:**
- Naming icon-only buttons
- Supplementary, non-essential hints
**Don't use when:**
- The information is essential — touch users never see tooltips → put it inline
- The overlay needs interactive content (links, buttons, options) → use Dropdown/Select or Modal
- Reporting errors → use Inline Alert
**Anti-patterns:**
- Actions or links inside a tooltip — it vanishes when the pointer moves
- Critical content readable *only* via tooltip (e.g. behind truncation)
**Status:** `extrapolated`

### Choosing between overlays

| Dimension       | Modal                 | Tooltip             | Dropdown/Select        |
|-----------------|-----------------------|---------------------|------------------------|
| Blocks the page | Yes (dimmed)          | No                  | No                     |
| Trigger         | Explicit action       | Hover / focus       | Click on trigger       |
| Contains        | Decision or subtask   | Passive text only   | Interactive options    |
| Dismissal       | User decides/cancels  | Pointer leaves      | Selection or click-out |

**Rule of thumb:** needs a decision → Modal. Passive hint text → Tooltip.
Interactive choices anchored to a trigger → Dropdown/Select.
```

- [ ] **Step 2: Verify Overlays section**

Run: `awk '/^# Overlays/,/^# Standalone/' component-usage-guidelines.md (repo root) | grep -c "^## "`
Expected: `2`

---

### Task 6: Standalone components (4 entries)

**Files:**
- Modify: `component-usage-guidelines.md (repo root)` (fill the `# Standalone Components` section)

- [ ] **Step 1: Write the 4 standalone entries**

Append under `# Standalone Components` (after its intro line):

```markdown
## Table
**What it is:** Rows and columns for structured, homogeneous data (e.g. the document list), with gray/50 header row and optional alternating gray/25 rows.
**Use when:**
- Many records share the same fields and users compare, scan, or sort them
- Rows carry per-item actions (actions column, `dots-horizontal`)
**Don't use when:**
- Items are visual and heterogeneous → use Workflow Card-style grid
- A handful of items with one field each → use a simple list
**Anti-patterns:**
- So many columns the table scrolls horizontally — cut low-value columns
- More than one actions column
**Status:** `figma`

## Workflow Card
**What it is:** A card in a 3-column grid representing a workflow: colored preview area (cyan/300 list-type, sky/200 chart-type) + white footer with title and meta.
**Use when:**
- A browsable gallery of distinct objects where visual identity aids recognition
**Don't use when:**
- Users compare items attribute-by-attribute → use Table
- Showing one item in full detail → use a dedicated page
**Anti-patterns:**
- More than two meta items in the footer (keep to e.g. "3 Extractions · Updated 2 days ago")
- Mixed card sizes within one grid
**Status:** `figma`

## Empty State
**What it is:** A placeholder shown when a view has no content: brief explanation plus the action that fills it.
**Use when:**
- First use (nothing created yet), zero search/filter results, or all content removed
**Don't use when:**
- Content is still loading → use a loading indicator, never an empty state flash
- Content failed to load → use Inline Alert with the error
**Anti-patterns:**
- A blank region with no explanation
- An empty state without a CTA when a filling action exists (e.g. "Upload")
- Error text styled as a friendly empty state — errors need the feedback tokens
**Status:** `extrapolated`

## AI Chat Input
**What it is:** The Ask Notessa prompt box: gray/100 multi-line input with stars icon, suggestion chips, and source dropdown.
**Use when:**
- Free-form conversational input to AI — questions over documents
**Don't use when:**
- Structured data collection → use form inputs (Text Field, Dropdown/Select…)
- Finding items in a list → use Search Box
**Anti-patterns:**
- Reusing it as a general Textarea outside the AI context
- Hiding the source selector when the answer's scope matters
**Status:** `figma`
```

- [ ] **Step 2: Verify standalone section and total count**

Run: `grep -c "^## " component-usage-guidelines.md (repo root)`
Expected: `21`

Run: `grep -c '\*\*Status:\*\*' component-usage-guidelines.md (repo root)`
Expected: `21`

---

### Task 7: Consistency check

**Files:**
- Modify (fixes only, if needed): `component-usage-guidelines.md (repo root)`

- [ ] **Step 1: Verify status distribution**

Run: `grep -c 'Status:\*\* \`figma\`' component-usage-guidelines.md (repo root)`
Expected: `10`

Run: `grep -c 'Status:\*\* \`extrapolated\`' component-usage-guidelines.md (repo root)`
Expected: `11`

- [ ] **Step 2: Verify every cross-reference points at a real entry**

Run: `grep -o "use [A-Z][A-Za-z /]*" component-usage-guidelines.md (repo root) | sort -u`

Check each referenced name against the 21 `## ` headings. Allowed exceptions (deliberately out-of-system, flagged in text): "wizard/stepper pattern". Every other reference must match an existing heading (or an explicit variant of it, e.g. "Workflow Card-style grid"). Fix any dangling reference by pointing it at the correct entry.

- [ ] **Step 3: Verify family comparison count**

Run: `grep -c "^### Choosing between" component-usage-guidelines.md (repo root)`
Expected: `4`

- [ ] **Step 4: Verify no contradiction with visual truth**

Read `/Users/yuqing/Claude/Notessa/design-system-rules.md` sections 4 (Components). Confirm no usage entry contradicts a visual spec (e.g. the Button entry must not claim cyan/700 backgrounds; primary is cyan/800). Fix the usage file if any conflict is found — the visual file wins.

---

### Task 8: CLAUDE.md integration

**Files:**
- Modify: `/Users/yuqing/Claude/CLAUDE.md` (Notessa Design System section)

- [ ] **Step 1: Add the usage-rules pointer**

In the bullet list under `## Notessa Design System`, after the `**Component rules:**` line, add:

```markdown
* **Usage rules:** `component-usage-guidelines.md (repo root)` — when to use which component; resolve every component choice against this file before generating UI
```

- [ ] **Step 2: Verify**

Run: `grep -c "component-usage-guidelines" /Users/yuqing/Claude/CLAUDE.md`
Expected: `1`

---

### Task 9: Final review against spec

**Files:**
- Read: `/Users/yuqing/Claude/Notessa/docs/specs/2026-07-09-component-usage-guidelines-design.md`
- Read: `component-usage-guidelines.md (repo root)`

- [ ] **Step 1: Check every spec requirement**

Confirm each is satisfied:
1. Header block with purpose, sibling-file relationships, AI-consumer instruction — Task 1
2. 21 entries, uniform template (What it is / Use when / Don't use when / Anti-patterns / Status) — Tasks 2–6
3. 4 family comparison blocks, each with table + rule of thumb — Tasks 2–5
4. Modal in both Feedback and Overlays comparisons; Segmented Control in both Navigation and Inputs comparisons; Dropdown in both Inputs and Overlays comparisons — single entry each, dual table appearance
5. CLAUDE.md pointer — Task 8

- [ ] **Step 2: Report completion**

State to the user: what was created, entry/family counts, any cross-reference fixes made in Task 7, and that the file is ready for review. No git commit (not a repo — deferred to GitHub-publication phase).
