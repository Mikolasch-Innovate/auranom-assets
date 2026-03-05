# Whitepaper: Sandbox Execution Engine (SABEE)

**Version:** 3.0 (Public Version)
**Date:** 29 November 2025
**Classification:** Public / Investor Relations

---

## 1. Executive Summary
SABEE is the long-term memory and execution environment for AI agents. It overcomes the "context window" limitation of large language models (LLMs) by introducing a hierarchical 3-layer memory system. This enables agents to "remember" unlimited amounts of project history without slowing down or incurring massive API costs.

## 2. The Challenge
LLMs have limited memory capacity (context window). In long-running projects this fills up quickly. Agents begin to "forget" early instructions or must re-read thousands of documents for every simple task, which is slow and expensive.

## 3. The Solution: 3-Layer Memory Architecture
SABEE mimics human memory organisation:
1.  **Layer 1 (Active Memory):** Ultra-fast RAM for the current task (last 24 hours).
2.  **Layer 2 (Archived Memory):** Vector databases for semantic search of the recent past (last 30 days).
3.  **Layer 3 (Cold Storage):** Low-cost storage for the complete, immutable audit trail (years).

SABEE intelligently moves data between these layers. When an agent needs old information, SABEE retrieves only relevant "chunks" from Layer 2 or 3 and injects them into Layer 1.

## 4. Key Innovations
*   **Automated Session Handoff:** When Layer 1 becomes full, SABEE automatically archives the session and starts a fresh one, retaining only the essential summary. This creates an infinite continuous workflow.
*   **CPLS Integration:** SABEE serves as the local training ground for federated learning, enabling the system to learn without exposing raw data.
*   **Context Validation:** Retrieved memories are checked for relevance and compliance before being given to the agent, preventing hallucinations based on outdated data.

## 5. Market Differentiation
| Feature | Standard RAG (Retrieval Augmented Generation) | SABEE Memory Engine |
| :--- | :--- | :--- |
| **Structure** | Flat (all data is equal) | Hierarchical (hot/warm/cold) |
| **Limit Management** | Truncation (delete old text) | Smart summarisation & handoff |
| **Security** | Passive storage | Active compliance filtering |

## 6. Use Cases
*   **Long-Term Consulting:** An AI agent recalls a strategic decision made 6 months ago.
*   **Legal Tech:** Analysis of case files that exceed the token limit of all current LLMs.
