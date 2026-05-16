---
name: uireview
description: >
  Runs autonomous Playwright-based UI exploration of a web application (local or staging).
  Tests anonymous flows (landing pages, registration, login, password reset) and authenticated
  flows (CRUD operations, navigation, settings, account management). Collects JS errors,
  network failures, and broken interactions. Scores UI quality on four dimensions
  (completeness, functional, performance, accessibility) and posts a structured
  UIREVIEW SUMMARY to the PR. Supports HITL escalation for blocked flows and optional
  FixAgent mode for proposing code fixes based on codebase analysis.
  Use when a PR changes the frontend or introduces new user flows.
license: MIT
compatibility: >
  Requires Node.js 18+, npm 9+, and UIReviewer assets installed via UIREVIEWER_HOME (fallback: ./UIReviewer).
  Requires gh CLI authenticated and Playwright Chromium installed.
  Target URL must be reachable before the run starts.
metadata:
  author: auranom
  version: "1.0"
allowed-tools: Bash(gh:*) Bash(git:*) Bash(npm:*) Bash(npx:*) Bash(node:*) Bash(curl:*)
---

# UIReview

Run autonomous UI exploration of a web application as a real user would, collect all errors, score quality, and post a structured summary to the PR.

## Inputs

- **PR number** (required): used for comment posting and label management
- **BASE_URL** (optional): target URL — defaults to `$UIREVIEWER_DIR/config/.env` value
- **UIREVIEW_TARGETS** (optional): `local` | `staging` | `both` — defaults to `local`
- **UIREVIEW_AUTOFIX** (optional): `true` | `false` — defaults to `false`

## Instructions

### 0. Resolve UIReviewer Path

Use UIREVIEWER_HOME as primary location with repo-local fallback:

```bash
UIREVIEWER_DIR="${UIREVIEWER_HOME:-./UIReviewer}"
if [[ ! -d "$UIREVIEWER_DIR" ]]; then
  UIREVIEWER_DIR="./UIReviewer"
fi
```

### 1. Parse Inputs

Extract from the trigger comment or environment:
- `PR_NUMBER`: the PR this run is for
- `BASE_URL`: resolved from argument or `$UIREVIEWER_DIR/config/.env BASE_URL`
- `TARGETS`: `local` | `staging` | `both` (default: `local`)
- `AUTOFIX`: `true` | `false` (default: `false`)

If the argument contains a `https://` or `http://` URL, use it as `BASE_URL`.
If the argument is a number, use it as `PR_NUMBER` and derive `BASE_URL` from config.
If `--staging` is in the argument, set `TARGETS=staging`.
If `--both` is in the argument, set `TARGETS=both`.
If `--autofix` is in the argument, set `AUTOFIX=true`.

### 2. Validate Prerequisites

Run these checks. On any failure, post a BLOCKED PR comment and stop.

**a. UIReviewer directory**
```bash
test -d "$UIREVIEWER_DIR" || echo "MISSING"
```
If missing: BLOCKED — "UIReviewer directory not found. Run `scripts/install-review-assets.sh --refresh-uireviewer` or set UIREVIEWER_HOME; fallback is ./UIReviewer."

**b. Node modules**
```bash
test -d "$UIREVIEWER_DIR/node_modules" || npm install --prefix "$UIREVIEWER_DIR" --silent
```

**c. Playwright Chromium**
```bash
if ! compgen -G "$HOME/Library/Caches/ms-playwright/chromium-*" >/dev/null 2>&1 && ! compgen -G "$HOME/.cache/ms-playwright/chromium-*" >/dev/null 2>&1; then npx --prefix "$UIREVIEWER_DIR" playwright install chromium 2>&1 | tail -3; fi
```
(Idempotent — safe to run every time.)

**d. Target URL reachability**
For each target URL:
```bash
HTTP_CODE=$(curl -s -o /dev/null -w "%{http_code}" --connect-timeout 10 --max-time 15 "$URL")
```
If `HTTP_CODE` is `000` (connection refused) or starts with `5`: BLOCKED — "Target `$URL` is not reachable (HTTP $HTTP_CODE). Start the dev server or verify the staging deployment before running UIReview."
If `HTTP_CODE` is `200`–`399`: proceed.

**e. Ensure labels exist on the repo**
```bash
gh label create "A_UIReview" --color "1d76db" --description "UI review in progress" --repo $REPO 2>/dev/null || true
gh label create "A_UIReview_HITL" --color "e4e669" --description "UIReview awaiting human input" --repo $REPO 2>/dev/null || true
gh label create "A_UIReview_Done" --color "0e8a16" --description "UIReview completed" --repo $REPO 2>/dev/null || true
gh label create "A_UIReview_Blocked" --color "d93f0b" --description "UIReview found critical issues" --repo $REPO 2>/dev/null || true
```

Apply `A_UIReview` to the PR:
```bash
gh pr edit $PR_NUMBER --add-label "A_UIReview" --repo $REPO
```

### 3. Configure Environment

Update `$UIREVIEWER_DIR/config/.env` with target values:
- Set `BASE_URL` to the resolved local URL if `TARGETS` includes `local`
- Set `STAGING_URL` to the staging URL if `TARGETS` includes `staging`
- Set `UIREVIEW_TARGETS=$TARGETS`
- **Do NOT overwrite** `PLAYWRIGHT_AUTH0_EMAIL` or `PLAYWRIGHT_AUTH0_PASSWORD` if they are already set in the file — preserve existing credentials.

### 4. Run Exploration

For each target in `TARGETS` (run `local` first, then `staging`):

**a. Execute the test suite:**
```bash
cd "$UIREVIEWER_DIR" && BASE_URL=<target_url> npm test 2>&1
```
Capture full stdout and stderr. Note the process exit code.

**b. Read artifacts after completion:**
- `$UIREVIEWER_DIR/artifacts/report.json` — quality score and gate (primary)
- `$UIREVIEWER_DIR/test-results/` — raw test output (fallback if report.json missing)

**c. Detect HITL triggers in output:**
- Output contains `Missing Auth0 test credentials` → trigger HITL: credentials needed
- Output contains `auth0.com` in a URL + test timeout → trigger HITL: login flow blocked
- Output contains `net::ERR_CONNECTION_REFUSED` for BASE_URL (not a sub-resource) → target went down mid-test; stop run and post BLOCKED

**d. On test failure (exit code ≠ 0), classify each failure:**
Parse Playwright output for failed test names and assertions.
For each failure record: `{ test_name, url, selector_hint, error_message, screenshot_ref }`

### 5. HITL Escalation

Trigger this phase if any HITL trigger was detected in step 4.

**Post PR comment:**
```
UIREVIEW HITL REQUEST

**UIReviewer needs human input to continue.**

**Question**: [Specific question — e.g., "Auth0 test credentials are not configured in $UIREVIEWER_DIR/config/.env. Should UIReviewer skip authenticated flows and test only anonymous flows, or should credentials be added and the run retried?"]

**Context**: [What was being tested, what state was reached, relevant error or screenshot reference]

**Options**:
- **A)** Skip this flow and continue with what can be tested anonymously
- **B)** Stop the run — I will fix the blocker and re-trigger UIReview
- **C)** Credentials are now configured in $UIREVIEWER_DIR/config/.env — retry the authenticated flow

Reply with A, B, or C (or describe your choice) to continue.
```

**Apply label:**
```bash
gh pr edit $PR_NUMBER --add-label "A_UIReview_HITL" --repo $REPO
```

**Poll for human response:**
- Poll PR comments every 60 seconds
- Maximum wait: 30 minutes
- Accept condition: any comment posted after the HITL request timestamp, from a login that does NOT end in `[bot]`, containing at least one of: `A`, `B`, `C`, `skip`, `continue`, `retry`, `yes`, `no`, `done`

**On valid response:**
- Choice **A**: continue the run, skipping the blocked flow; document as `HITL_SKIPPED` in report
- Choice **B**: stop the run; post "UIReview stopped by user request. Re-trigger with `/uireview` when ready."
- Choice **C**: re-read `$UIREVIEWER_DIR/config/.env` for new credentials; retry the blocked test section

**On timeout (30 minutes with no response):**
- Skip the blocked flow
- Document as `HITL_TIMEOUT` in the report
- Continue with remaining tests

**After HITL resolution:**
```bash
gh pr edit $PR_NUMBER --remove-label "A_UIReview_HITL" --repo $REPO
```

### 6. FixAgent (only when UIREVIEW_AUTOFIX=true and functional failures > 0)

For each failure classified as **functional** (failing click, fill, navigation, or API response — not performance or accessibility):

**a.** Extract: `{ failing_url_path, selector, action_type, error_message }`

**b.** Map URL path to source file:
- Search `app/`, `pages/`, `src/app/`, `src/pages/` for a file matching the URL path pattern
- Example: `/leads` → search for `app/leads/page.tsx`, `pages/leads.tsx`, or route definitions

**c.** Search for the failing selector or error pattern in the source:
```bash
grep -r "selector_text_or_route_pattern" --include="*.tsx" --include="*.ts" -l
```

**d.** If a clear fix exists (confidence HIGH — single obvious cause):
Post a PR comment:
```
UIREVIEW AUTOFIX PROPOSAL

**Failure**: [test name] — [error message]
**File**: [path:line]
**Root cause**: [one-sentence explanation]
**Proposed fix**:
```[language]
[code diff or replacement block]
```

Apply this fix, then re-run `/uireview` to verify.
```

**e.** If root cause is ambiguous (confidence LOW or MEDIUM): skip the fix proposal; include the failure in `UIREVIEW SUMMARY` under "Requires Manual Investigation".

**NEVER** commit, push, or edit any file. All fixes are proposals in PR comments only.

### 7. Post Final Report

Post exactly one PR comment. The comment body MUST start with `UIREVIEW SUMMARY` as the very first characters — this marker enables future pipeline polling.

**Full report template:**

```markdown
UIREVIEW SUMMARY

## Summary
[1–2 sentences: what was tested, overall gate, most significant finding]

## Target(s)
| Target | URL | Gate | Score |
|---|---|---|---|
| Local | http://localhost:3000 | PASS | 8.42/10 |

## Quality Score: X.XX/10 — [GATE: PASS / REVIEW / BLOCK]
| Dimension | Score | Weight | Contribution |
|---|---|---|---|
| Completeness | X/10 | 30% | X.XX |
| Functional | X/10 | 40% | X.XX |
| Performance | X/10 | 20% | X.XX |
| Accessibility | X/10 | 10% | X.XX |

## Critical Issues (fix before deploy)
- **[URL]** — [Error type]: [Description] *(screenshot: step-XX.png)*

## High Priority
- [selector / URL]: [Description]

## Low Priority
- [Description]

## Requires Manual Investigation
- [Failures where FixAgent could not determine root cause]

## Strengths
- [What worked well]

## Artifacts
- Screenshots: `$UIREVIEWER_DIR/artifacts/`
- Videos: `$UIREVIEWER_DIR/artifacts/videos/`
- JSON report: `$UIREVIEWER_DIR/artifacts/report.json`
- Playwright HTML report: `$UIREVIEWER_DIR/playwright-report/index.html`

## HITL Events
- [timestamp] [question asked] → [resolution] (or: none)

## Fix Proposals
- [file:line] — [description] (or: none / run with `--autofix` to enable)
```

**No-issue case**: If no actionable findings exist, post the full structure with:
- Critical Issues: none
- High Priority: none
- Low Priority: none

### 8. Finalize Labels

```bash
# Remove in-progress label
gh pr edit $PR_NUMBER --remove-label "A_UIReview" --repo $REPO

# Apply done label
gh pr edit $PR_NUMBER --add-label "A_UIReview_Done" --repo $REPO

# If Critical Issues found: also add blocked label
gh pr edit $PR_NUMBER --add-label "A_UIReview_Blocked" --repo $REPO
```

## Constraints

- Always post `UIREVIEW SUMMARY` as the final PR comment regardless of gate outcome.
- Never commit, push, or edit any file — fixes are proposals in PR comments only.
- Never echo `PLAYWRIGHT_AUTH0_PASSWORD` or any credential in PR comments.
- Do not trigger Greptile tools from this skill.
- Do not change PR state (open/closed/draft).
- If `npm test` exits with code 2 (configuration error), report BLOCKED immediately — do not attempt to interpret partial output as a quality score.
- Maximum total runtime (excluding HITL wait): 30 minutes.
- If `$UIREVIEWER_DIR/artifacts/report.json` is missing after a test run, derive the gate from exit code: 0 = green, 1 = red.
