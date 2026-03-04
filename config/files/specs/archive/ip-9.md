# Technische Spezifikation: Patent 10 (LANA)

**Datum:** 16. November 2025
**Version:** 1.0
**Autor:** Dr. Lena Rossi
**Status:** Entwurf

---

## 1. Titel der Erfindung

**System und Verfahren zur kombinierten Intent- und Sentiment-Analyse aus multimodalen Sprachdaten zur dynamischen Steuerung von KI-Agenten**

**Kurztitel:** Language Analysis (LANA)

---

## 2. Problemstellung

KI-Agenten, die auf Sprachinteraktionen basieren, verstehen oft nur die wörtliche Bedeutung von dem, was gesagt wird. Sie scheitern daran, zwei entscheidende Ebenen der menschlichen Kommunikation zu erfassen: den **Intent** (die eigentliche Absicht oder das Ziel des Sprechers) und das **Sentiment** (die emotionale Tonalität). Ein Kunde, der sarkastisch "Das ist ja eine tolle Hilfe" sagt, wird von einem einfachen System fälschlicherweise als zufrieden eingestuft. Diese Unfähigkeit, "zwischen den Zeilen zu lesen", führt zu unpassenden Reaktionen, frustrierenden Benutzererfahrungen und der Eskalation von Problemen, die ein menschlicher Mitarbeiter sofort erkennen würde.

---

## 3. Lösung: Die LANA-Architektur

LANA ist eine multimodale Sprachanalyse-Engine, die parallel zur visuellen Analyse von FEGR arbeitet. Sie zerlegt die sprachliche Kommunikation in ihre Kernkomponenten (Intent und Sentiment) und synthetisiert die Ergebnisse zu einem handlungsrelevanten Trigger für die übergeordnete Steuerung (G-EE oder ACI). Die Architektur besteht aus vier Modulen, die in einer Pipeline arbeiten.

### 3.1. Modul 1: Speech-to-Text (STT)

Dieses Modul wandelt den rohen Audio-Input des Sprechers in transkribierten Text um. Es dient als Grundlage für die nachfolgende textbasierte Analyse.

### 3.2. Modul 2: Intent-Analyse

Dieses Modul analysiert den transkribierten Text, um die zugrundeliegende Absicht des Sprechers zu klassifizieren. Es nutzt ein trainiertes Sprachmodell (LLM), um den Text einer von mehreren vordefinierten Intent-Kategorien zuzuordnen.

- **Beispiel-Kategorien:** `informationsanfrage`, `aufgabenstellung`, `beschwerde`, `kaufinteresse`, `zustimmung`, `ablehnung`.
- **Output:** Ein strukturiertes Objekt, z.B. `{"intent": "beschwerde", "confidence": 0.92}`.

### 3.3. Modul 3: Multimodale Sentiment-Analyse

Dieses Modul analysiert sowohl den **Text** als auch die **Audiospur**, um eine präzise emotionale Bewertung zu erstellen. Dies ist ein entscheidender Unterschied zu rein textbasierten Systemen.

- **Text-Analyse:** Erkennt die emotionale Ladung der verwendeten Wörter (positiv, negativ, neutral).
- **Audio-Analyse:** Analysiert prosodische Merkmale der Stimme wie **Tonhöhe, Lautstärke, Sprechgeschwindigkeit und Pausen**. Eine hohe, schnelle Stimme kann auf Aufregung oder Frustration hindeuten, während eine langsame, leise Stimme auf Traurigkeit oder Unsicherheit hinweisen kann.
- **Synthese:** Die Ergebnisse aus Text- und Audio-Analyse werden zu einem Gesamt-Sentiment-Score kombiniert. Dies löst das Problem des Sarkasmus, bei dem positive Worte mit negativer Tonalität verwendet werden.
- **Output:** Ein strukturiertes Objekt, z.B. `{"sentiment": "frustriert", "intensity": 0.85, "source": "audio_features"}`.

### 3.4. Modul 4: Actionable Trigger Generation

Das Kernstück der Innovation. Dieses Modul synthetisiert die Ergebnisse aus der Intent- und Sentiment-Analyse zu einem einzigen, handlungsrelevanten Trigger für das steuernde System (G-EE).

- **Input:** `{"intent": "beschwerde"}` und `{"sentiment": "frustriert"}`.
- **Logik:** Eine Regel-Engine oder ein kleines LLM kombiniert die Inputs und leitet eine Handlungsempfehlung ab.
- **Output (Actionable Trigger):** Ein angereichertes JSON-Objekt, das dem System genau sagt, was zu tun ist.
  ```json
  {
    "intent": "beschwerde",
    "sentiment": "frustriert",
    "urgency": "hoch",
    "recommended_action": "ESCALATE_TO_SENIOR_AGENT",
    "suggested_response_tone": "empathisch_und_lösungsorientiert"
  }
  ```

---

## 4. Patentierbare Kernmerkmale

1.  **Die multimodale Sentiment-Analyse:** Das Verfahren zur Kombination von textbasierter Analyse und prosodischer Audio-Analyse zur Erstellung eines robusten, sarkasmus-resistenten Sentiment-Scores.
2.  **Die Synthese zu einem Actionable Trigger:** Das System, das die separaten Ergebnisse von Intent- und Sentiment-Analyse nicht nur berichtet, sondern zu einem einzigen, angereicherten und handlungsrelevanten Befehl für ein übergeordnetes Steuerungssystem (G-EE) synthetisiert.
3.  **Die dynamische Generierung einer Handlungsempfehlung:** Die Fähigkeit des Systems, basierend auf der Intent-Sentiment-Kombination eine konkrete nächste Aktion (`recommended_action`) und einen Kommunikationsstil (`suggested_response_tone`) vorzuschlagen.

---

## 5. Abgrenzung zum Stand der Technik

-   **Standard-Sentiment-Analyse-Tools:** Diese klassifizieren Text oft nur als "positiv/negativ/neutral". Sie nutzen keine Audio-Merkmale und liefern keine Handlungsempfehlungen.
-   **Chatbot-Intent-Erkennung:** Diese Systeme sind typischerweise auf einfaches Routing beschränkt (z.B. "Leite an den Vertrieb weiter"). Sie berücksichtigen nicht das Sentiment und generieren keine komplexen, angereicherten Trigger.
-   **Speech-Analytics-Software:** Diese Systeme können zwar die Tonalität analysieren, sind aber meist passive Analyse-Tools, die Berichte für menschliche Manager erstellen. Sie sind nicht darauf ausgelegt, in Echtzeit ein KI-Agenten-System dynamisch zu steuern.

LANA ist das erste System, das Intent- und multimodale Sentiment-Analyse in einer Pipeline kombiniert, um einen einzigen, handlungsrelevanten Trigger zu erzeugen, der speziell für die dynamische Echtzeit-Steuerung von autonomen KI-Agenten in einem Geschäftsumfeld konzipiert ist.

---

## 6. Detaillierte Abgrenzung zum Stand der Technik

Die Einzigartigkeit von LANA wird durch die Abgrenzung zu bestehenden Technologien und wissenschaftlichen Arbeiten deutlich:

| Technologie/Arbeit | Nächster relevanter Stand der Technik | Abgrenzung und Neuheit von LANA |
| :--- | :--- | :--- |
| **Multimodale Analyse** | **US Patent 11227195B2** [1] | Dieses Patent kombiniert Video, Audio und Text zur Bestimmung von **Sentiment und Demografie**. LANA hingegen kombiniert Text und prosodische Audio-Merkmale zur Bestimmung von **Intent und Sentiment** und synthetisiert diese zu einem **Actionable Trigger** zur Agenten-Steuerung. |
| **Intent & Emotion** | **MC-EIU Dataset** [2] | Diese Arbeit fokussiert auf das gemeinsame Verständnis von Emotion und Intent in Konversationen für die **passive Analyse**. LANA geht einen Schritt weiter und generiert einen **handlungsrelevanten Trigger** mit konkreten Empfehlungen (`recommended_action`, `suggested_response_tone`) für die **aktive Steuerung** von KI-Agenten. |
| **Text-Audio Sentiment** | **StyleBERT** [3] | StyleBERT ist ein Framework für die Text-Audio-Sentiment-Analyse. Es erkennt jedoch keinen **Intent** und ist nicht für die Agenten-Steuerung konzipiert. |
| **Prosodische Analyse** | **Bansal et al. (2021)** [4] | Diese Arbeit nutzt prosodische Merkmale für die Sentiment-Analyse. LANA integriert diese Analyse in eine größere Pipeline, die auch **Intent-Erkennung** und die **Synthese zu einem Actionable Trigger** umfasst. |
| **Kommerzielle Systeme** | **Convin.ai Voicebot** [5] | Bestehende Voicebots kombinieren Intent und Emotion für den Kundenservice. LANA unterscheidet sich durch die **tiefere multimodale Analyse** (Text + Prosodie) und die Generierung eines **strukturierten, angereicherten Triggers**, der für die Steuerung von **autonomen, aufgabenorientierten Agenten** über den Kundenservice hinaus konzipiert ist. |

### Referenzen

[1] US Patent 11227195B2. *Multi-modal detection engine of sentiment and demographic characteristics for social media videos*.

[2] (Anonym). *Emotion and Intent Joint Understanding in Multimodal Conversation: A Benchmarking Dataset*. arXiv:2407.02751.

[3] Lin, F. et al. (2023). *StyleBERT: Text-audio sentiment analysis with Bi-modal*. ScienceDirect.

[4] Bansal, M. et al. (2021). *A Language-Independent Speech Sentiment Analysis Using Prosodic Features*. IEEE.

[5] Convin.ai (2025). *Master Voicebot Context for Intent Recognition & Emotion*.
