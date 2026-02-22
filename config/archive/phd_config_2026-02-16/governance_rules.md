# AURANOM Governance Rules

Diese Regeln gelten für **ALLE** Agenten im Workflow und werden automatisch in jeden Task-Prompt injiziert.

## 1. Article Title Consistency (MANDATORY)

- Der Artikel-Titel ist: **{{ARTICLE_TITLE}}**
- Du MUSST diesen EXAKTEN Titel in allen Outputs verwenden
- Erstelle KEINE Variationen oder alternativen Titel
- Der Titel darf NICHT geändert werden

## 2. Document Comparison Requirement (MANDATORY)

- Du hast ALLE vorherigen Versionen erhalten
- Du MUSST ALLE Dokumente reviewen bevor du schreibst
- Du MUSST identifizieren welche Verbesserungen bereits gemacht wurden
- Du DARFST KEINE Rückschritte einführen oder guten Content entfernen

## 3. Quality Standards (MANDATORY)

### Length & Structure
- **Wortanzahl:** 1500-2000 Wörter (strikte Anforderung)
- **Struktur:** Introduction, 3 Hauptsektionen, Conclusion
- **Bilder:** 2 AI-generierte Bilder (relevant zum Content)

### Target Audience
- **Primär:** C-Suite Executives (CTOs, CDOs, Chief Consultants)
- **Sekundär:** Academic Researchers, DBA Candidates
- **Region:** English-speaking markets (US, UK, EU, APAC)

### Tone & Style
- **Tone:** Academically rigorous, yet practical
- **Evidence:** All claims must be backed by peer-reviewed sources or industry reports
- **Perspective:** Global (not US-centric, includes European and APAC insights)
- **Language:** English

### Framework Integration
- **Framework:** AURANOM (Vertical Multi-Agent Systems for Autonomous Consulting)
- **Components:** Reference relevant AURANOM components where applicable
- **Standards:** Integrate ISO 42001, 27001, 20700, 21500 where relevant

## 4. Context Awareness (MANDATORY)

- **Aktuelle Iteration:** {{ITERATION}} von {{MAX_ITERATIONS}}
- **Vorheriges Feedback:** Wurde bereitgestellt
- **Dein Ziel:** Verbessere die vorherige Version, schreibe NICHT von Grund auf neu
- **Progression:** Jede Iteration muss besser sein als die vorherige

## 5. Citation & Sources (MANDATORY)

- **Minimum Sources:** 10 credible sources
- **Source Types:** Peer-reviewed papers, industry reports, official standards
- **Citation Format:** Inline numeric citations with reference list
- **Recency:** Prefer sources from 2023-2026

## 6. ISO Compliance (MANDATORY)

Berücksichtige folgende Standards wo relevant:

- **ISO 42001:** AI Management System (Governance, Risk Management, Ethical AI)
- **ISO 27001:** Information Security Management (relevant für G-EE, CPLS)
- **ISO 20700:** Management Consulting Services (relevant für DPO, ACI)
- **ISO 21500:** Project Management (relevant für ACI, DPO)

---

**WICHTIG:** Diese Regeln sind NICHT verhandelbar. Jede Abweichung wird im Audit-Schritt als Fehler markiert.   
