# Technical Specification: IP 9 (LANA)

**Date:** 16 November 2025
**Version:** 1.0
**Author:** Dr. Lena Rossi
**Status:** Draft

---

## 1. Title of the Invention

**System and Method for Combined Intent and Sentiment Analysis from Multimodal Speech Data for the Dynamic Control of AI Agents**

**Short Title:** Language Analysis (LANA)

---

## 2. Problem Statement

AI agents based on speech interactions often understand only the literal meaning of what is said. They fail to capture two critical levels of human communication: the **intent** (the actual intention or goal of the speaker) and the **sentiment** (the emotional tone). A customer who sarcastically says "That's really helpful" will be incorrectly classified as satisfied by a simple system. This inability to "read between the lines" leads to inappropriate responses, frustrating user experiences and the escalation of issues that a human employee would recognise immediately.

---

## 3. Solution: The LANA Architecture

LANA is a multimodal speech analysis engine that works in parallel with the visual analysis of FEGR. It decomposes spoken communication into its core components (intent and sentiment) and synthesises the results into an actionable trigger for the overarching control system (G-EE or ACI). The architecture consists of four modules operating in a pipeline.

### 3.1. Module 1: Speech-to-Text (STT)

This module converts the raw audio input of the speaker into transcribed text. It serves as the foundation for subsequent text-based analysis.

### 3.2. Module 2: Intent Analysis

This module analyses the transcribed text to classify the underlying intention of the speaker. It uses a trained language model (LLM) to assign the text to one of several predefined intent categories.

- **Example categories:** `information_request`, `task_assignment`, `complaint`, `purchase_interest`, `agreement`, `rejection`.
- **Output:** A structured object, e.g., `{"intent": "complaint", "confidence": 0.92}`.

### 3.3. Module 3: Multimodal Sentiment Analysis

This module analyses both the **text** and the **audio track** to create a precise emotional assessment. This is a critical distinction from purely text-based systems.

- **Text Analysis:** Detects the emotional charge of the words used (positive, negative, neutral).
- **Audio Analysis:** Analyses prosodic features of the voice such as **pitch, volume, speaking speed and pauses**. A high, fast voice can indicate excitement or frustration, while a slow, quiet voice may indicate sadness or uncertainty.
- **Synthesis:** The results from text and audio analysis are combined into an overall sentiment score. This resolves the problem of sarcasm, where positive words are used with a negative tone.
- **Output:** A structured object, e.g., `{"sentiment": "frustrated", "intensity": 0.85, "source": "audio_features"}`.

### 3.4. Module 4: Actionable Trigger Generation

The core of the innovation. This module synthesises the results of intent and sentiment analysis into a single, actionable trigger for the controlling system (G-EE).

- **Input:** `{"intent": "complaint"}` and `{"sentiment": "frustrated"}`.
- **Logic:** A rule engine or small LLM combines the inputs and derives an action recommendation.
- **Output (Actionable Trigger):** An enriched JSON object that tells the system precisely what to do.
  ```json
  {
    "intent": "complaint",
    "sentiment": "frustrated",
    "urgency": "high",
    "recommended_action": "ESCALATE_TO_SENIOR_AGENT",
    "suggested_response_tone": "empathetic_and_solution_oriented"
  }
  ```

---

## 4. Patentable Core Features

1.  **Multimodal Sentiment Analysis:** The method for combining text-based analysis and prosodic audio analysis to create a robust, sarcasm-resistant sentiment score.
2.  **Synthesis into an Actionable Trigger:** The system that does not merely report the separate results of intent and sentiment analysis, but synthesises them into a single, enriched and actionable command for a higher-level control system (G-EE).
3.  **Dynamic Generation of an Action Recommendation:** The system's ability to propose a concrete next action (`recommended_action`) and a communication style (`suggested_response_tone`) based on the intent-sentiment combination.

---

## 5. Distinction from the State of the Art

-   **Standard Sentiment Analysis Tools:** These often classify text only as "positive/negative/neutral". They do not use audio features and provide no action recommendations.
-   **Chatbot Intent Detection:** These systems are typically limited to simple routing (e.g., "forward to sales"). They do not consider sentiment and do not generate complex, enriched triggers.
-   **Speech Analytics Software:** These systems can analyse tone, but are mostly passive analysis tools creating reports for human managers. They are not designed to dynamically control an AI agent system in real time.

LANA is the first system to combine intent and multimodal sentiment analysis in a pipeline to produce a single, actionable trigger specifically designed for the dynamic, real-time control of autonomous AI agents in a business context.

---

## 6. Detailed Distinction from the State of the Art

The uniqueness of LANA is demonstrated by its distinction from existing technologies and scientific works:

| Technology/Work | Nearest Relevant State of the Art | Distinction and Novelty of LANA |
| :--- | :--- | :--- |
| **Multimodal Analysis** | **US Patent 11227195B2** [1] | This patent combines video, audio and text to determine **sentiment and demographics**. LANA, by contrast, combines text and prosodic audio features to determine **intent and sentiment** and synthesises these into an **actionable trigger** for agent control. |
| **Intent & Emotion** | **MC-EIU Dataset** [2] | This work focuses on the joint understanding of emotion and intent in conversations for **passive analysis**. LANA goes a step further and generates an **actionable trigger** with concrete recommendations (`recommended_action`, `suggested_response_tone`) for the **active control** of AI agents. |
| **Text-Audio Sentiment** | **StyleBERT** [3] | StyleBERT is a framework for text-audio sentiment analysis. However, it does not detect **intent** and is not designed for agent control. |
| **Prosodic Analysis** | **Bansal et al. (2021)** [4] | This work uses prosodic features for sentiment analysis. LANA integrates this analysis into a larger pipeline that also includes **intent detection** and the **synthesis into an actionable trigger**. |
| **Commercial Systems** | **Convin.ai Voicebot** [5] | Existing voicebots combine intent and emotion for customer service. LANA differs through its **deeper multimodal analysis** (text + prosody) and the generation of a **structured, enriched trigger** designed for controlling **autonomous, task-oriented agents** beyond customer service. |

### References

[1] US Patent 11227195B2. *Multi-modal detection engine of sentiment and demographic characteristics for social media videos*.

[2] (Anonymous). *Emotion and Intent Joint Understanding in Multimodal Conversation: A Benchmarking Dataset*. arXiv:2407.02751.

[3] Lin, F. et al. (2023). *StyleBERT: Text-audio sentiment analysis with Bi-modal*. ScienceDirect.

[4] Bansal, M. et al. (2021). *A Language-Independent Speech Sentiment Analysis Using Prosodic Features*. IEEE.

[5] Convin.ai (2025). *Master Voicebot Context for Intent Recognition & Emotion*.
