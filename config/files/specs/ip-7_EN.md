# Technical Specification: IP 7 (FEGR)

**Date:** 16 November 2025
**Version:** 1.0
**Author:** Dr. Lena Rossi
**Status:** Draft

---

## 1. Title of the Invention

**System and Method for Multimodal Analysis of Non-Verbal Signals for the Dynamic Control of AI Agents in Group Interactions**

**Short Title:** Facial and Gestic Recognition (FEGR)

---

## 2. Problem Statement

A large part of human communication is non-verbal. AI agents that respond only to text or speech miss crucial signals such as facial expressions, gestures and body posture. This limits their ability to understand the emotional state, engagement or intentions of a human counterpart. Particularly in group interactions (e.g., workshops, presentations), it is impossible for an AI agent to detect who is speaking, who is raising their hand, or whether the group as a whole is losing interest. Existing facial recognition systems are mostly limited to individual persons or simple emotion detection and provide no integrated solution for controlling agents in a business context.

---

## 3. Solution: The FEGR Architecture

The FEGR system is a multimodal analysis engine that captures, interprets and converts non-verbal signals from video streams in real time into actionable commands for AI agents. It enables more natural and effective human–AI collaboration, particularly in multi-participant scenarios.

The architecture consists of three core modules:

### 3.1. Module 1: Real-Time Non-Verbal Analysis

This module analyses the video stream and extracts fundamental non-verbal data points.

- **Facial Analysis:** Detects basic emotions (e.g., joy, confusion, surprise) and gaze direction using Convolutional Neural Networks (CNNs).
- **Gesture Analysis:** Detects specific hand gestures (e.g., hand raise, thumbs up) and body postures (e.g., crossed arms, nodding) using pose estimation (e.g., MediaPipe).
- **Action Recommendation:** The extracted data is sent to a higher-level logic engine (e.g., ACI), which derives a contextual action recommendation for the acting AI agent (e.g., "Client appears confused, please explain the point more simply.").

### 3.2. Module 2: Multi-Speaker and Identity Management (Seminar Room Mode)

This module is optimised for interactions with multiple persons.

- **Person Tracking:** Identifies and tracks multiple persons in the camera's field of view and assigns a temporary, anonymous ID to each person.
- **Dynamic Name Assignment:** When a person is addressed by name in conversation (e.g., "Ms. Meier, did you have a question?"), the system captures the name via speech-to-text and links it to the corresponding person ID in a temporary database.
- **Hand-Raise Trigger:** Detects the hand-raising gesture and links it to the identified person. The system sends a precise trigger to the AI agent (e.g., "Trigger: Person 'Ms. Meier' has raised their hand."), enabling the agent to address that person directly.

### 3.3. Module 3: Group Engagement Analysis

This module aggregates the non-verbal signals of the entire group to assess the overall engagement level.

- **Fatigue Detection:** Analyses aggregated metrics such as eyelid closure rate (PERCLOS) and head posture across all participants.
- **Disengagement Detection:** Detects patterns such as simultaneous looking away, repeated yawning or a predominantly passive body posture.
- **Group Action Recommendation:** When a predefined threshold for fatigue or disengagement in the group is exceeded, the system generates a proactive recommendation for the agent (e.g., "Recommendation: Suggest a short break." or "Recommendation: Ask an interactive question to re-engage the group.").

---

## 4. Patentable Core Features

1.  **The Combination of the Three Modules:** The integrated system that connects individual non-verbal analysis, multi-speaker identity management and group engagement analysis into a coherent whole to control AI agents.
2.  **Dynamic Name Assignment in Seminar Room Mode:** The method whereby a temporary but named identification of participants for the duration of an interaction is achieved through the combination of person tracking and speech-to-text.
3.  **The Hand-Raise Trigger:** The specific mechanism that assigns the hand-raising gesture to an identified person and generates a precise, actionable trigger for the AI agent.
4.  **Aggregated Group Engagement Analysis:** The method for deriving an action recommendation for the agent based on analysis of the collective non-verbal signals of a group.

---

## 5. Distinction from the State of the Art

- **Standard Facial Recognition APIs (e.g., Amazon Rekognition, Microsoft Face API):** These provide generic emotion detection for individuals. FEGR goes far beyond this by placing this data in an action and group context, identifying multiple persons by name and evaluating collective engagement.
- **Pose Estimation Libraries (e.g., MediaPipe, OpenPose):** These deliver raw body posture data. The innovation of FEGR lies in the interpretation of this raw data (e.g., detection of the specific "hand-raise" gesture) and its linkage to a person ID and an agent trigger.
- **Fatigue Detection Systems in Automotive:** These focus on a single driver. FEGR applies similar principles to a group and derives social interaction strategies from them.

FEGR is the first system to propose such a deep integration of non-verbal analysis specifically for controlling AI agents in dynamic individual and group conversations in a business context.

---

## 6. Detailed Distinction from the State of the Art

The uniqueness of FEGR is demonstrated by its distinction from existing technologies and scientific works:

| Technology/Work | Nearest Relevant State of the Art | Distinction and Novelty of FEGR |
| :--- | :--- | :--- |
| **Emotion Detection** | **US Patent 8209182B2** [1] | This patent describes an emotion recognition system for human behaviour. FEGR goes further by placing emotions **in an action and group context** and generating **dynamic control signals for AI agents**. |
| **Workplace Emotion Detection** | **Snap Patent (2024)** [2] | Snap's patent focuses on emotion detection for workplace surveillance. FEGR uses the analysis for the **active control of AI agents** in business interactions, not passive surveillance. |
| **Multi-User Gesture Recognition** | **mmWave Radar System (2025)** [3] | This system detects gestures for two users with 92.80% accuracy. FEGR combines gesture recognition with **person identification** and **hand-raise trigger generation** for agents. |
| **MediaPipe Gesture Recognition** | **Google MediaPipe** [4] | MediaPipe provides gesture recognition for hands. FEGR integrates this into a larger system with **dynamic name assignment** and **group engagement analysis**. |
| **Nonverbal Group Analysis** | **Gatica-Perez et al. (2009)** [5] | This work analyses non-verbal signals in groups. FEGR applies this to the **control of AI agents** and derives **action recommendations** (e.g., "suggest a break"). |

### References

[1] US Patent 8209182B2. *Emotion recognition system*.

[2] The Daily Upside (2024). *Snap Patent Brings Emotion Detection to Workplace Surveillance*.

[3] Han, W. et al. (2025). *A Robust Real-Time Multiuser Gesture Recognition System*. IEEE.

[4] Google AI Edge (2025). *Gesture recognition task guide - MediaPipe*.

[5] Gatica-Perez, D. et al. (2009). *Automatic nonverbal analysis of social interaction in small groups*. ScienceDirect. Cited: 438 times.
