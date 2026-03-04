# Whitepaper: Adaptive Consulting Intelligence (ACI)

**Version:** 2.0 (Public Version)
**Date:** 29 November 2025
**Classification:** Public / Investor Relations

---

## 1. Executive Summary
ACI is the strategic brain of the autonomous enterprise. It replaces static workflow templates with dynamic process generation. By analysing 22 project parameters (e.g., client industry, budget, risk), ACI autonomously designs a tailored project plan, selects the right methodologies and instructs the executing agents on exactly what to do.

## 2. The Challenge
Consulting is not "one size fits all". A startup needs a different approach than a bank. Standard workflow tools require humans to manually model every step. When the project context changes, the model breaks. Agents without clear instructions hallucinate or produce generic, low-value work.

## 3. The Solution: Dynamic Process Generation
ACI uses a 2-stage decision engine:
1.  **Strategy Layer:** Selects the project management model (e.g., "Agile Scrum" vs. "Regulatory Waterfall").
2.  **Methodology Layer:** Retrieves expert methods from a vector database (RAG3) and generates **5 specific Design Elements** for each individual task: *Objective, Role, Input Data, Deliverable, KPI*.

## 4. Key Innovations
*   **The 5 Design Elements:** A proprietary format that translates vague business goals into machine-executable agent instructions.
*   **RAG3 Knowledge Base:** A specialised library of thousands of consulting methods, indexed by industry and complexity, allowing ACI to act like a senior partner with 30 years of experience.
*   **Feedback Loop:** ACI presents its plan to the human user for validation *before* execution and learns from every correction.

## 5. Market Differentiation
| Feature | BPM Tools (e.g., Camunda) | ACI Architecture |
| :--- | :--- | :--- |
| **Creation** | Manual modelling | Autonomous generation |
| **Adaptability** | Static (requires re-deployment) | Dynamic (recalculates immediately) |
| **Knowledge** | Empty shell | Pre-loaded with expert methods |

## 6. Use Cases
*   **Project Kickoff:** Instant generation of a 3-month project plan for a digital transformation initiative.
*   **Crisis Management:** Automatic replanning of a project when the budget is cut by 50%.
