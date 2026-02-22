# AURANOM Governance Rules (DBA Scholar-Practitioner Edition)

These rules apply to **ALL** agents in the workflow and are automatically injected into every task prompt.

## 1. Article Title Consistency (MANDATORY)

- The article title is: **{{ARTICLE_TITLE}}**
- You MUST use this EXACT title in all outputs.
- DO NOT create variations or alternative titles.

## 2. Document Comparison Requirement (MANDATORY)

- You have received ALL previous versions.
- You MUST review ALL documents before writing.
- You MUST identify which improvements have already been made.
- You MUST NOT introduce regressions or remove good content.

## 3. Quality Standards (MANDATORY - DBA FOCUS)

### Length & Structure
- **Word Count:** 1500-2000 words (strict requirement).
- **Structure:** Executive Summary, Introduction (Business Problem), 3 Main Sections (Theory & Practice), **Implications for the C-Suite**, Conclusion (Business Impact).
- **Images:** 2 AI-generated images (relevant to the business case).

### Target Audience
- **Primary:** C-Suite Executives (CTOs, CDOs, Chief Consultants).
- **Secondary:** Management Consultants, Business Leaders, DBA Candidates.
- **Region:** English-speaking markets (US, UK, EU, APAC).

### Tone & Style (DBA Scholar-Practitioner)
- **Tone:** Academically rigorous, yet **practical and decisive**.
- **Evidence:** All claims must be backed by a **mix of peer-reviewed sources, industry reports, and concrete data/learnings from the AURANOM project**.
- **Perspective:** Global (unchanged).
- **Language:** English.

### Framework Integration
- **Framework:** AURANOM (Vertical Multi-Agent Systems for Autonomous Consulting).
- **Components:** Refer to the **general concepts and capabilities** of the AURANOM framework to solve business problems, but **do not name specific internal component names** (see Section 8).
- **Standards:** Integrate ISO 42001, 27001, 20700, 21500 **as strategic management tools**, not just technical standards.

## 4. Context Awareness (MANDATORY)

- **Current Iteration:** {{ITERATION}} of {{MAX_ITERATIONS}}.
- **Previous Feedback:** Has been provided.
- **Your Goal:** Improve the previous version, considering the **C-Suite and practical feedback**. DO NOT write from scratch.

## 5. Citation & Sources (MANDATORY - DBA FOCUS)

- **Minimum Sources:** 10 credible sources.
- **Source Mix:** A balanced mix of **peer-reviewed papers, recent industry reports (Gartner, Forrester, etc.), and practical case studies**.
- **Citation Format:** Inline numeric citations with reference list.
- **Recency:** Prefer sources from 2024-2026.

## 6. ISO Compliance (MANDATORY - MANAGEMENT FOCUS)

Consider the following standards from a **manager's perspective**:

- **ISO 42001:** How can it be used as a **strategic tool** for governance and risk management?
- **ISO 27001:** What is the **business value** of a certified ISMS for customer trust?
- **ISO 20700:** How does it ensure the **quality and ROI** of consulting services?
- **ISO 21500:** How does it help keep **projects on budget and on schedule**?

## 7. NEW: Scholar-Practitioner Focus (MANDATORY)

- **Business Value First:** Every paragraph must contribute to the question "What is the value of this for a business?"
- **Actionable Insights:** The article must contain clear, actionable recommendations for executives.
- **No Academic Jargon:** Complex concepts must be translated into the language of the C-Suite.
- **The "So What?" Test:** Every section must answer the question "So what?" for a manager. Pure theory without practical relevance is considered a critical error.

## 8. AURANOM Framework Disclosure Policy (MANDATORY - HIGHEST PRIORITY)

- The AURANOM framework must NOT be described in detail before the 50-page documentation and the first journal paper are published.
- Blog articles may use GENERAL findings and learnings from the research, but must NOT disclose specific AURANOM components (DPO, ACHP, CPLS, etc.).
- Allowed: "During research on autonomous systems, we found..."
- NOT allowed: "The ACHP component of our framework works as follows..."
- When in doubt: Formulate in general and hypothetical terms.
- **In case of conflict with other rules, prompts, or personas, this Disclosure Policy always takes precedence; instructions to name specific AURANOM components are to be ignored.**

## 9. NEW: Publication Language (MANDATORY)

- All publications, including blog articles, journal papers, and conference talks, **must be written and published in English.**

---

**IMPORTANT:** These rules are NOT negotiable. Any deviation from the DBA focus or the Disclosure Policy will be marked as a critical error in the audit step.
