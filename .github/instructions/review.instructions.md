---
description: "Use when: interacting with AURANOM review pipeline PR comments, stage triggers, and apply/fix requests. Enforces deterministic, parser-safe responses for Copilot and review agents."
applyTo: "**"
---

# AURANOM Pipeline Review Instructions

## Deterministic Markers

Use stable markers so pipeline parsing remains reliable.

### Stage 1 — Copilot Trigger

- Confirmation reply must include: `Copilot review triggered`

### Stage 2 — Copilot Result

- Severity summary line must be present exactly: `P1: X | P2: Y | P3: Z`
- Each finding must use a severity tag: `[P1]`, `[P2]`, or `[P3]`
- If no findings: `P1: 0 | P2: 0 | P3: 0`
- `[P1]` = blocker (security breach, data loss, complete flow broken) — must be fixed before merge
- `[P2]` = important, should fix
- `[P3]` = low / nice-to-have

### Stage 3 — Apply Copilot Fixes

- Completion line must be present exactly: `Copilot apply complete`
- List applied changes as: `[file] intent` (one per line)

### Stage 5/6 — Governance Gates

- Pre-execution evidence line must be present exactly: `AIIA: complete` or `AIIA: missing`
- Pre-execution assessment line must be present exactly: `PRE-Assessment: pass` or `PRE-Assessment: fail`

### Noop Output

- `no changes needed`
- `nothing to apply`
- `no actionable review comments`

## Compliance Evidence Requirements (Copilot)

Every finding must include the following fields:

- `[P1|P2|P3] <title>`
- `file: <path>`
- `risk: <what can fail and why>`
- `evidence: present|missing (<short proof>)`
- `fix: <specific change>`

Every finding must map to at least one governance area: AI governance, security, service quality, workflow governance.

## Terminology

- `AIIA` = AI Impact Assessment
- `PRE-Assessment` = pre-execution governance/security check
- Do not use `AICC` or `PRegate` in stage markers
