# Component Usage Guidelines

An AI-first guideline answering one question: **when to use which UI component.**

Most design systems document how components *look*. This project documents how to *choose* between them — decision rules, anti-patterns, and comparisons between commonly-confused components (toast vs. inline alert vs. modal; tabs vs. segmented control; radio vs. checkbox vs. toggle...).

## Intended use

- **AI-driven UI generation:** load `component-usage-guidelines.md` into an LLM's context (e.g. reference it from a `CLAUDE.md`) so generated interfaces make correct component choices instead of improvising.
- **Human reference:** terse, rule-based reading for designers and developers.

This guideline is **design-system-agnostic** — it defines behavior and decision rules only. Pair it with your own design system's tokens and visual specs.

## Structure

- [`component-usage-guidelines.md`](component-usage-guidelines.md) — the deliverable: ~21 component entries in 4 families (Inputs, Navigation, Feedback & Notifications, Overlays) plus standalone components; each family closes with a comparison table + rule of thumb
- [`docs/specs/`](docs/specs/) — approved design spec
- [`docs/plans/`](docs/plans/) — implementation plan with per-component drafts and workflow

## Method

Every entry is grounded in and reconciled against three authoritative references:

1. [W3C ARIA Authoring Practices Guide](https://www.w3.org/WAI/ARIA/apg/patterns/)
2. [IBM Carbon Design System](https://carbondesignsystem.com/) — per-component usage pages
3. [SAP Fiori Design System](https://www.sap.com/design-system/fiori-design-web/) — per-component usage pages

Workflow per component: research references → reconcile draft → human review and confirmation → write. Family comparison blocks are written only after every entry in the family is confirmed.

## Status

🚧 Work in progress. Skeleton and workflow are in place; component entries are being written family by family (Inputs first).
