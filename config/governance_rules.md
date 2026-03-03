# Governance Rules (DBA Scholar-Practitioner Edition)

These rules apply to **ALL** agents in the workflow and are automatically injected into every task prompt.

## 1. Publication Title Consistency (MANDATORY)

- The publication title is provided by configuration for this run (dynamic).
- You MUST use the EXACT configured title in all outputs.
- DO NOT create variations or alternative titles unless the HITL explicitly requests a change.

## 2. Document Comparison Requirement (MANDATORY)

- You have received ALL previous versions.
- You MUST review ALL documents before writing.
- You MUST identify which improvements have already been made.
- You MUST NOT introduce regressions or remove good content.

## 3. Quality Standards (MANDATORY - DBA FOCUS)

### Length & Structure
- **Word Count:** MUST comply with the word-count limits provided by the workflow configuration for this run (dynamic). If violated: **revision required** (not an automatic rejection by itself).
- **Structure (minimum):**
  - Executive Summary (C-Suite focused)
  - Introduction (explicit business problem + why now)
  - Main Body (theory-to-practice translation)
  - Implications for the C-Suite (actionable takeaways)
  - Conclusion (business impact)
  - References (numbered list; clickable URLs/DOIs; no placeholders)
- **Images:** Provide 2 AI-image prompts aligned to the business case (unless the workflow step explicitly excludes images).

### Target Audience
- **Primary:** C-Suite Executives (CTOs, CDOs, Chief Consultants).
- **Secondary:** Management Consultants, Business Leaders, DBA Candidates.
- **Region:** English-speaking markets (US, UK, EU, APAC).

### Tone & Style (DBA Scholar-Practitioner)
- **Tone:** Academically rigorous, yet **practical and decisive**.
- **Business Value First:** Every section must answer: "So
