# Technische Spezifikation: IP 6 V2 (ACI)

**Datum:** 16. November 2025
**Version:** 1.0
**Autor:** Dr. Lena Rossi
**Status:** Entwurf

---

## 1. Titel der Erfindung

**System und Verfahren zur adaptiven, kontextsensitiven Konfiguration von Multi-Agenten-Prozessen**

**Kurztitel:** Adaptive Consulting Intelligence (ACI) V2

---

## 2. Problemstellung

Bestehende Multi-Agenten-Systeme operieren mit starren, vordefinierten Workflows. Sie können ihre Vorgehensweise nicht an den spezifischen Kontext eines Projekts (z.B. Branche, Unternehmensgröße, Problemstellung, Dringlichkeit) anpassen. Dies führt zu einem "One-size-fits-all"-Ansatz, der ineffizient ist und oft zu suboptimalen Ergebnissen führt. Insbesondere im komplexen Umfeld der Unternehmensberatung ist die Fähigkeit, die richtige Methodik (z.B. agil vs. linear, Expertenberatung vs. Prozessberatung) dynamisch auszuwählen und den Prozess entsprechend zu konfigurieren, entscheidend für den Erfolg.

---

## 3. Lösung: Die ACI V2 Architektur

Die Adaptive Consulting Intelligence (ACI) ist ein KI-gestütztes System, das diese Lücke schließt. Es analysiert die initialen Projektparameter und konfiguriert autonom einen maßgeschneiderten, rollenbasierten Beratungsprozess. Die Architektur basiert auf zwei Kerninnovationen: der 9-Ebenen-Prozesshierarchie und der ACI-Entscheidungslogik zur Generierung von fünf Designelementen. Die Ausführung wird durch die übergeordnete Governance & Execution Engine (G-EE, IP 9) gesteuert.

### 3.1. Die 9-Ebenen-Prozesshierarchie

Die ACI strukturiert den gesamten Beratungsprozess in eine neunschichtige Hierarchie, die von der strategischen Direktive bis zur finalen Kundeninteraktion reicht. Diese Struktur ermöglicht eine klare Trennung von Verantwortlichkeiten und eine präzise Steuerung.

### 3.2. ACI-Entscheidungslogik & die 5 Designelemente

Das Herzstück der ACI ist eine zweistufige Entscheidungslogik, die von zwei spezialisierten Agenten ausgeführt wird:

1.  **Agent Orion (Strategische Steuerung):** Wählt auf Basis der Projektparameter das übergeordnete **Projektmanagement-Modell** (z.B. Wasserfall, Scrum) und die **Projektphasen** aus.
2.  **Operational Agent (Operative Generierung & QA):** Wählt für jede Phase die optimale **Beratungsmethode** aus einer Wissensdatenbank (RAG3) aus und generiert darauf basierend **fünf konkrete Designelemente**, die den ausführenden Agenten als verbindliche Spezifikation dienen.

Diese **fünf Designelemente** sind eine proprietäre Kerninnovation und umfassen typischerweise:
- **Ziel der Phase**
- **Einzusetzende Tools & Techniken**
- **Rollen und Verantwortlichkeiten der Agenten**
- **Erwartete Deliverables**
- **KPIs zur Erfolgsmessung**



---

## 4. Differenzierungsmerkmale

1.  **Die ACI-Entscheidungslogik:** Die spezifische zweistufige Logik zur dynamischen Auswahl von PM-Modell und Beratungsmethode, ausgeführt durch die spezialisierten Agenten Strategic Agent (Orion) und Operational Agent.
2.  **Die Generierung der 5 Designelemente:** Das Konzept, eine Beratungsmethode in fünf konkrete, maschinenlesbare Spezifikationen zu zerlegen, die als verbindliche Anleitung für ausführende Agenten dienen.

4.  **Die Integration der 9-Ebenen-Hierarchie:** Die Abbildung der ACI-Entscheidungslogik auf eine spezifische, neunschichtige Prozesshierarchie zur präzisen Steuerung.

---

## 5. Abgrenzung zum Stand der Technik

- **Business Process Management (BPM) Tools:** Diese Systeme führen starre, vordefinierte Prozesse aus. Die ACI hingegen *generiert* den Prozess dynamisch basierend auf dem Kontext.
- **Generische Agenten-Orchestratoren (z.B. Microsoft AutoGen):** Diese bieten Frameworks zur Kommunikation zwischen Agenten, enthalten aber keine Logik zur adaptiven Prozesskonfiguration oder eine aktive Governance-Durchsetzung.
- **Bestehende RAG-Systeme:** Diese beantworten Fragen. Die ACI nutzt RAG nicht nur zur Informationsgewinnung, sondern als Basis für eine komplexe, mehrstufige Entscheidungslogik zur Prozessgestaltung.

Die ACI V2 ist das erste System, das die dynamische, kontextsensitive Generierung von komplexen, wissensbasierten Prozessen für Multi-Agenten-Systeme ermöglicht. Die Durchsetzung der Governance wird durch die übergeordnete Governance & Execution Engine (G-EE, IP 9) sichergestellt.

---

## 6. Detaillierte Abgrenzung zum Stand der Technik

Die Einzigartigkeit der ACI V2 wird durch die Abgrenzung zu bestehenden Technologien und wissenschaftlichen Arbeiten deutlich:

| Technologie/Arbeit | Nächster relevanter Stand der Technik | Abgrenzung und Neuheit der ACI V2 |
| :--- | :--- | :--- |
| **Workflow-Systeme** | **US IP 20110022435A1** [1] | Dieses IP beschreibt adaptive Workflow-Automation. Die ACI hingegen **generiert** den Prozess dynamisch basierend auf Kontext und nutzt **RAG zur Methodik-Auswahl** aus einer Wissensdatenbank. |
| **AI in Consulting** | **Cognitive Automation in Business Consulting (2025)** [2] | Diese Arbeit diskutiert Gen AI für Insight Discovery. Die ACI fokussiert auf die **dynamische Konfiguration des Beratungsprozesses selbst** durch die Generierung von **5 Designelementen**. |
| **Context-Aware Systems** | **Context-Aware Decision Support for XAI Methods (2025)** [3] | Diese Arbeit beschreibt kontextabhängige Auswahl von Erklärbarkeitsmethoden. Die ACI wendet dieses Prinzip auf die **Prozesskonfiguration** an und generiert **maschinenlesbare Spezifikationen** für Agenten. |
| **BPM Tools** | **Standard Business Process Management Tools** | Diese führen starre, vordefinierte Prozesse aus. Die ACI **generiert** den Prozess dynamisch basierend auf dem Kontext. |
| **Agenten-Orchestratoren** | **Microsoft AutoGen** [4] | AutoGen bietet Frameworks zur Kommunikation zwischen Agenten, enthält aber keine Logik zur **adaptiven Prozesskonfiguration** oder RAG-basierte Methodik-Auswahl. |

### Referenzen

[1] US IP 20110022435A1. *Systems and Methods for Workflow Automation, Adaptation*.

[2] James, L. (2025). *Cognitive Automation and Generative AI Agents in Business Consulting: From Insight Discovery to Continuous Strategy Execution*. ResearchGate.

[3] Reis, M. I. et al. (2025). *A context-aware decision support system for selecting XAI methods*. ScienceDirect.

[4] Microsoft (2023). *AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation*.
