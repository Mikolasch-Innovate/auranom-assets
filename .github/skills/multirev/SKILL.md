---
name: multirev
description: >
  Runs a structured multi-perspective pull request review (correctness, quality,
  security, architecture), then posts a concise findings summary with priorities and
  concrete recommendations. Use when the pipeline asks for "multirev" on a PR.
license: MIT
compatibility: Requires gh authenticated and repository pull-request access.
metadata:
  author: auranom
  version: "1.1"
allowed-tools: Bash(gh:*) Bash(git:*)
---

# MultiRev

Review a PR through four independent perspectives and produce one actionable summary.

## Inputs

- PR number (required)

## Instructions

### 1. Load PR Context

- Fetch PR details, changed files, commits, comments, and reviews.
- Identify the exact scope of change.

### 2. Analyze in Four Lenses (Independent)

Run these lenses independently. Do not let one lens bias another.

- Correctness: logic errors, edge cases, boundary conditions, null handling, regressions
- Code Quality: readability, naming clarity, duplication, maintainability, complexity
- Security: validation gaps, injection risks, auth/authz flaws, data exposure
- Architecture: design consistency, separation of concerns, dependency direction

### 3. Synthesize Findings

- Merge overlapping issues from different lenses.
- Categorize by severity: Critical, High Priority, Low Priority.
- Include concrete remediation guidance per issue.
- Add strengths (good practices) explicitly.

### 4. Post Structured Summary

Post one PR comment containing these exact headings:

- Summary
- Critical Issues
- High Priority
- Low Priority
- Strengths
- Recommendations

Include the marker phrase MULTIREV SUMMARY in the first paragraph so pipeline marker detection is stable.

### 5. No-issue Case

If no actionable findings exist, still post the same structure and state:

- Critical Issues: none
- High Priority: none
- Low Priority: none

## Constraints

- Do not run sequentially by perspective; keep the four lenses independent in analysis.
- Do not over-focus on style; prioritize correctness, security, architecture.
- Do not trigger Greptile tools from this skill.
- Keep recommendations concrete and actionable.
