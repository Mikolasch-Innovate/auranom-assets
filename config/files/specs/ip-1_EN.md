# Technical Specification: IP 1 (DPO-Dual-Process Orchestration)

## 1. Title of the Invention

**System and Method for Dual-Process Orchestration of AI Agents for Integrating Sales Processes under ISO 9001 and Consulting Processes under ISO 20700**

**Short Title:** Dual-Process Multi-Agent Orchestrator

---

## 2. Problem Description

In practice, sales and consulting are often separate silos within organisations. This leads to significant problems: client context is lost during the handover from sales to consulting, manual handoffs are error-prone and time-consuming, and upselling opportunities are not systematically identified. Existing systems focus either on sales or on consulting, but not on the seamless integration of both processes.

---

## 3. Solution: The Dual-Process Orchestration Architecture

The invention solves this problem through a hierarchical multi-agent orchestration system that integrates sales processes under ISO 9001 and consulting processes under ISO 20700 in a unified system.

### 3.1. System Architecture

The system comprises 9 specialised AI agents in a two-tier hierarchy:

- **Level 1: Master Orchestrator (Orion):** Coordinates both processes (sales and consulting) and ensures dual-standard compliance.
- **Level 2a: Sales Team (3 agents):** Specialised in Lead Generation (Sales Agent A), Proposal & Negotiation (Sales Agent B) and Closing & Onboarding (Sales Agent C) under ISO 9001.
- **Level 2b: Consulting Team (5 agents):** Specialised in Contracting (Contracting Agent), Analysis & Strategy (Analysis Agent), Implementation (Implementation Agent), Quality Assurance (QA Agent) and Closure (Closure Agent) under ISO 20700.

### 3.2. Dual-Process Integration

The system implements automated, context-preserving handoffs between the sales team and the consulting team. A structured context package is transferred during the handoff from Sales Agent C (sales) to the Contracting Agent (consulting), containing all relevant client information, expectations and agreements.

### 3.3. Bidirectional Transitions and Upselling

A key feature is the bidirectional transition: not only Sales → Consulting, but also Consulting → Sales. The Closure Agent identifies new opportunities during project closure and forwards these to Sales Agent B (sales) to initiate upselling processes.

---

## 4. Differentiating Features

1.  **Dual-Process Integration:** The specific integration of transactional (sales) and knowledge-based (consulting) processes in a unified multi-agent system.
2.  **Automated Sales-to-Consulting Handoffs:** The mechanism for automatically transferring structured context packages between the sales team and the consulting team.
3.  **Bidirectional Transitions with Upselling Mechanism:** The system's ability to identify upselling opportunities during consulting and automatically route them back to sales.
4.  **Dual-Standard Compliance:** The simultaneous monitoring and enforcement of ISO 9001 (sales) and ISO 20700 (consulting) by a single Master Orchestrator.

---

## 5. Distinction from the State of the Art

The uniqueness of Dual-Process Orchestration is demonstrated by its distinction from existing technologies and scientific works:

| Technology/Work | Nearest Relevant State of the Art | Distinction and Novelty |
| :--- | :--- | :--- |
| **Consulting MAS** | **IP 1 (Auranom) - Multi-Agent Orchestration for Consulting** [1] | IP 1 focuses exclusively on consulting processes under ISO 20700. IP 5 **additionally integrates sales processes** under ISO 9001 and enables **automated handoffs** and **upselling** between both processes. |
| **CRM Systems** | **Salesforce Agentforce (2024)** [2] | Salesforce Agentforce is designed for CRM and sales, but without integration of **knowledge-based consulting processes** or ISO 20700 compliance. |
| **Multi-Agent Systems** | **C3 AI – US IP 12,111,859** [3] | C3 AI is designed for general business functions. IP 5 is specifically for the **dual-process integration** of sales and consulting with **dual-standard compliance**. |

### References

[1] IP 1 (Auranom). *Multi-Agent Orchestration for Consulting Processes under ISO 20700*.

[2] Salesforce (2024). *Salesforce Agentforce Whitepaper*.

[3] US IP 12,111,859. *Multi-agent orchestration for business functions*.
