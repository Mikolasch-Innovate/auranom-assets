# Technical Specification: IP 6 V2 (ACI)

**Date:** 16 November 2025
**Version:** 1.0
**Author:** Dr. Lena Rossi
**Status:** Draft

---

## 1. Title of the Invention

**System and Method for Adaptive, Context-Sensitive Configuration of Multi-Agent Processes**

**Short Title:** Adaptive Consulting Intelligence (ACI) V2

---

## 2. Problem Statement

Existing multi-agent systems operate with rigid, predefined workflows. They cannot adapt their approach to the specific context of a project (e.g., industry, company size, problem statement, urgency). This leads to a "one-size-fits-all" approach that is inefficient and often produces suboptimal results. Particularly in the complex environment of management consulting, the ability to dynamically select the right methodology (e.g., agile vs. linear, expert consulting vs. process consulting) and configure the process accordingly is critical to success.

---

## 3. Solution: The ACI V2 Architecture

The Adaptive Consulting Intelligence (ACI) is an AI-powered system that closes this gap. It analyses the initial project parameters and autonomously configures a tailored, role-based consulting process. The architecture is based on two core innovations: the 9-layer process hierarchy and the ACI decision logic for generating five design elements. Execution is governed by the overarching Governance & Execution Engine (G-EE, IP 9).

### 3.1. The 9-Layer Process Hierarchy

ACI structures the entire consulting process into a nine-layer hierarchy, ranging from strategic directives to final client interaction. This structure enables a clear separation of responsibilities and precise control.

### 3.2. ACI Decision Logic & the 5 Design Elements

The heart of ACI is a two-stage decision logic executed by two specialised agents:

1.  **Agent Orion (Strategic Control):** Based on the project parameters, selects the overarching **project management model** (e.g., waterfall, Scrum) and **project phases**.
2.  **Operational Agent (Operative Generation & QA):** For each phase, selects the optimal **consulting method** from a knowledge database (RAG3) and generates on that basis **five concrete design elements** that serve as binding specifications for the executing agents.

These **five design elements** are a proprietary core innovation and typically include:
- **Phase objective**
- **Tools & techniques to be deployed**
- **Agent roles and responsibilities**
- **Expected deliverables**
- **KPIs for success measurement**



---

## 4. Differentiating Features

1.  **The ACI Decision Logic:** The specific two-stage logic for dynamically selecting the PM model and consulting method, executed by the specialised agents Strategic Agent (Orion) and Operational Agent.
2.  **The Generation of the 5 Design Elements:** The concept of decomposing a consulting method into five concrete, machine-readable specifications that serve as binding instructions for executing agents.

4.  **The Integration of the 9-Layer Hierarchy:** The mapping of the ACI decision logic onto a specific, nine-layer process hierarchy for precise control.

---

## 5. Distinction from the State of the Art

- **Business Process Management (BPM) Tools:** These systems execute rigid, predefined processes. ACI, by contrast, *generates* the process dynamically based on context.
- **Generic Agent Orchestrators (e.g., Microsoft AutoGen):** These offer frameworks for communication between agents but contain no logic for adaptive process configuration or active governance enforcement.
- **Existing RAG Systems:** These answer questions. ACI uses RAG not only for information retrieval but as the basis for a complex, multi-stage decision logic for process design.

ACI V2 is the first system that enables the dynamic, context-sensitive generation of complex, knowledge-based processes for multi-agent systems. Governance enforcement is ensured by the overarching Governance & Execution Engine (G-EE, IP 9).

---

## 6. Detailed Distinction from the State of the Art

The uniqueness of ACI V2 is demonstrated by its distinction from existing technologies and scientific works:

| Technology/Work | Nearest Relevant State of the Art | Distinction and Novelty of ACI V2 |
| :--- | :--- | :--- |
| **Workflow Systems** | **US IP 20110022435A1** [1] | This IP describes adaptive workflow automation. ACI, by contrast, **generates** the process dynamically based on context and uses **RAG for methodology selection** from a knowledge database. |
| **AI in Consulting** | **Cognitive Automation in Business Consulting (2025)** [2] | This work discusses Gen AI for insight discovery. ACI focuses on the **dynamic configuration of the consulting process itself** through the generation of **5 design elements**. |
| **Context-Aware Systems** | **Context-Aware Decision Support for XAI Methods (2025)** [3] | This work describes context-dependent selection of explainability methods. ACI applies this principle to **process configuration** and generates **machine-readable specifications** for agents. |
| **BPM Tools** | **Standard Business Process Management Tools** | These execute rigid, predefined processes. ACI **generates** the process dynamically based on context. |
| **Agent Orchestrators** | **Microsoft AutoGen** [4] | AutoGen provides frameworks for communication between agents but contains no logic for **adaptive process configuration** or RAG-based methodology selection. |

### References

[1] US IP 20110022435A1. *Systems and Methods for Workflow Automation, Adaptation*.

[2] James, L. (2025). *Cognitive Automation and Generative AI Agents in Business Consulting: From Insight Discovery to Continuous Strategy Execution*. ResearchGate.

[3] Reis, M. I. et al. (2025). *A context-aware decision support system for selecting XAI methods*. ScienceDirect.

[4] Microsoft (2023). *AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation*.
