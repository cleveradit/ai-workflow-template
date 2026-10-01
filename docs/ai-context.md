# AI Context & Development Mandates

All AI agents MUST read and follow these rules before proposing or implementing any changes.

> **Orientation (understand the project without reading code):** read in order — this document (mandates) → [architecture.md](architecture.md) (module map) → [data-model.md](data-model.md) (data structures) → [features/index.md](features/index.md) (per-feature details).

**Documentation language:** <!-- FILL IN: e.g. "English" or "Indonesian (technical terms stay in English)". If empty, ask the user before writing any docs, then fill this in. -->

---

## 1. Tech Stack (STRICT — no deviations)

<!-- FILL IN: languages, frameworks, core libraries, and version constraints that MUST NOT be violated. Example: Go 1.23, React 19, PostgreSQL 16, Redis 7. -->

---

## 2. Architecture Mandates

<!-- FILL IN: absolute architecture rules. Example: "All domain logic lives in internal/. Nothing domain-related in cmd/." -->
<!-- Example: "Cross-module reads are allowed. Cross-module writes are forbidden — call the owning module's Service instead." -->

---

## 3. Rules

<!-- FILL IN: technical rules every AI agent must follow. Format: Rule N — short title, then 1-3 sentences of explanation. -->
<!-- Example:
**Rule 1 — Naming Convention:** All service files MUST be suffixed with `_service.go`.
**Rule 2 — Error Handling:** Never panic; always return wrapped errors with context.
-->

---

## 4. Local Development Environment

<!-- FILL IN: how to run the project locally. Include:
- Prerequisites (Docker, Go version, Node version, etc.)
- How to start services
- How to rebuild
- How to clear caches
- Important notes (mounts, hot reload, etc.)
-->

---

## 5. Documentation Workflow

**Rule 0 — All documentation/context MUST live in `docs/` (versioned in git), NOT in the AI's local memory.**
Developers switch between machines, and the AI's local memory is not committed, so it is unavailable on other machines. Therefore: decisions, ticket status, analysis results, and any context that must survive across sessions/machines must be written to the appropriate `docs/` file (planning, feature, decision-log, or backlog) — not stored as local memory. AI agents must not rely on local memory as the source of truth for this project.

All documentation is written in the **Documentation language** set at the top of this file.

Never write code without going through this flow first. Do not create `implementation_plan.md` as a standalone artifact — use the official planning files below.

**Step 1 — Backlog (`docs/backlog.md`)**
New bugs/ideas go here without ticket numbers. Status: `OPEN` (ready to be planned) or `BLOCKED`. Remove the item once it becomes a planning ticket.

**Step 2 — Planning (`docs/planning/TICKET-NUMBER-NAME.md`)**
Create the plan before writing any code. Use `docs/planning/_template-implementation-plan.md`. Register in `docs/planning/index.md`. Get explicit user approval before executing.

Status lifecycle: `DRAFT` → `REVIEW` → `READY` → `DONE`.
- `DRAFT`: decisions not locked, execution blocked.
- `REVIEW`: decisions locked, waiting for user manual approval — do NOT execute.
- `READY`: user gave explicit written approval in chat — execution allowed.
- `DONE`: implementation and verification complete.

Each plan must include: Business Decision Snapshot, Non-Negotiable Technical Contract (target files, method signatures, integration points, return shapes), Acceptance Test Matrix (min. 1 boundary + 1 failure case, or `N/A — <reason>` if not relevant), and Out of Scope section.

When a ticket is DONE: move its file to `docs/planning/Ticket-Implemented/`, remove its entry from `docs/planning/index.md` (do not delete the index file itself). Check both locations when numbering new tickets to avoid duplicates.

`docs/planning/current-session.md` is updated only when the user explicitly asks. Do not create or modify it on your own initiative.

**Step 3 — Feature Docs (`docs/features/`)**
Every shipped feature needs a doc here, registered in [`docs/features/index.md`](features/index.md). Use the lean template: `# Title` → `**Status:** Live` → `## Summary` (2–4 sentences) → relevant sections (Quick Reference / catalogs as tables) → `## Gotchas` (non-obvious things only) → `## Related` (links to related docs).

Style rules (mandatory): no decorative emoji in headers; no commit hash/branch/date in Status; no motivational/marketing prose; method/field/column catalogs are always tables; every claim is verified against the actual code (anything unverified is not written); cross-links use standard Markdown links (`[name](name.md)`). Structural docs (module map, data reference) live one level up: `docs/architecture.md` and `docs/data-model.md`.

**Step 4 — Decision Log (`docs/decision-log.md`)**
Record a decision only if it meets at least one criterion:
- A technical gotcha/trap that cannot be derived from reading the code
- A business trade-off with non-obvious consequences
- A correction of a previously wrong assumption or mandate

Do not record: code cleanup, minor UI changes, or anything already documented in `ai-context.md` itself. SUPERSEDED entries must be deleted, not kept. Use the entry format in [`docs/decision-log.md`](decision-log.md).
