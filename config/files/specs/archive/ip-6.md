# Technische Spezifikation: IP 7 (SABEE)

**Datum:** 16. November 2025
**Version:** 1.0
**Autor:** Dr. Lena Rossi
**Status:** Entwurf

---

## 1. Titel der Erfindung

**System und Verfahren zur dynamischen Kontext-Archivierung und intelligenten Wiederherstellung in langlebigen Multi-Agenten-Systemen**

**Kurztitel:** Sandbox Execution Engine (SABEE)

---

## 2. Problemstellung

Large Language Models (LLMs), die als Gehirn für KI-Agenten dienen, haben ein begrenztes Kontextfenster (Context Window). Bei langlebigen Projekten (z.B. mehrmonatige Beratungsaufträge) übersteigt die Menge an generierten Informationen (Gespräche, Entscheidungen, Dateien) schnell die Kapazität dieses Fensters. Dies führt zu einem "Kontextverlust", bei dem der Agent wichtige, aber ältere Informationen vergisst, was zu Fehlern, Inkonsistenzen und einer schlechten Benutzererfahrung führt. Bestehende Lösungen sind unzureichend, da sie entweder den Kontext willkürlich kürzen oder auf ineffiziente, manuelle Suchen in externen Datenbanken angewiesen sind.

---

## 3. Lösung: Die SABEE-Architektur

Die Sandbox Execution Engine (SABEE) löst dieses Problem durch eine neuartige, dreistufige Hybrid-Architektur zur dynamischen Verwaltung des Kontexts. Das System archiviert und de-archiviert Informationen automatisch basierend auf ihrer Relevanz und ihrem Alter, um sicherzustellen, dass der Agent immer den relevantesten Kontext im direkten Zugriff hat, während der vollständige Projektverlauf durchsuchbar bleibt.

### 3.1. Die 3-Schichten-Kontext-Archivierung

Die Kerninnovation ist die Aufteilung des Kontexts in drei hierarchische Schichten, die unterschiedliche Speichertechnologien und Zugriffsgeschwindigkeiten nutzen:

| Schicht | Name | Speicherort | Zugriffszeit | Größe | Beschreibung |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Schicht 1** | **Aktiver Kontext** | In-Memory (RAM) & Event-Log | < 100 ms | < 128k Tokens | Enthält die Interaktionen der letzten 24 Stunden. Dieser Kontext wird direkt in das Prompt des LLM geladen. |
| **Schicht 2** | **Archivierter Kontext** | Vektor-Datenbank (z.B. Pinecone) | < 500 ms | Bis zu 5 GB | Enthält komprimierte Zusammenfassungen und semantische Vektoren von Interaktionen, die zwischen 24 Stunden und 30 Tagen alt sind. |
| **Schicht 3** | **Kalter Kontext** | Cold Storage (z.B. AWS S3 Glacier) | > 5 s | Unbegrenzt | Enthält den vollständigen, unveränderten Event-Log aller Interaktionen, die älter als 30 Tage sind. |

### 3.2. Intelligente Kontext-Wiederherstellung (Context-Reload)

Wenn ein Agent Informationen benötigt, die nicht im aktiven Kontext (Schicht 1) vorhanden sind, löst SABEE einen intelligenten Wiederherstellungsprozess aus:

1.  **Semantische Suche (RAG):** Der Agent formuliert eine interne Suchanfrage. SABEE durchsucht den **Archivierten Kontext (Schicht 2)** mittels Retrieval-Augmented Generation (RAG), um die relevantesten Informations-Chunks zu finden.
2.  **Kontext-Injektion:** Die gefundenen Chunks werden dynamisch in das Prompt des Agenten für die aktuelle Aufgabe injiziert, ohne das gesamte Kontextfenster zu überladen.
3.  **Fallback auf Kalten Kontext:** Nur wenn die semantische Suche keine Ergebnisse liefert, wird eine gezielte Suche im **Kalten Kontext (Schicht 3)** initiiert. Dies ist ein langsamerer Prozess, der für forensische Analysen oder die Rekonstruktion weit zurückliegender Ereignisse vorgesehen ist.

### 3.3. Kontext-Integritäts-Validierung

Um die Korrektheit des wiederhergestellten Kontexts zu gewährleisten, wird ein Zwei-Agenten-Validierungs-Mechanismus eingesetzt:

- **QA Agent (Qualitätssicherung):** Überprüft die vom RAG-System abgerufenen Kontext-Chunks auf semantische Korrektheit und Relevanz für die aktuelle Aufgabe.
- **Governance Agent (Veritas):** Stellt sicher, dass der wiederhergestellte Kontext nicht gegen bestehende Governance-Regeln oder Datenschutzrichtlinien verstößt.

Dieser Validierungsschritt verhindert, dass der Agent mit veralteten oder irrelevanten Informationen arbeitet.

---

## 4. Differenzierungsmerkmale

1.  **Das 3-Schichten-Hybrid-System:** Die spezifische Kombination aus In-Memory-, Vektor- und Cold-Storage zur hierarchischen Kontextverwaltung.
2.  **Der intelligente Reload-Prozess:** Der automatisierte, mehrstufige Prozess der semantischen Suche im archivierten Kontext und dem Fallback auf den kalten Kontext.
3.  **Die Zwei-Agenten-Validierung:** Der Einsatz von spezialisierten Agenten (QA Agent und Governance Agent) zur Sicherstellung der Integrität und Konformität des wiederhergestellten Kontexts.
4.  **Der automatische Archivierungs-Trigger:** Der zeitbasierte Mechanismus, der Kontext-Events nach vordefinierten Zeiträumen (24h, 30d) automatisch zwischen den Schichten verschiebt.

---

## 5. Abgrenzung zum Stand der Technik

- **Standard-RAG-Systeme:** Diese durchsuchen lediglich eine externe Wissensbasis. SABEE verwaltet den *gesamten, dynamischen Projektkontext* in einer strukturierten, hierarchischen Weise.
- **Memory-Systeme in Agenten-Frameworks (z.B. LangChain):** Diese bieten einfache In-Memory-Speicher oder Chat-Historien, aber keine intelligente, mehrschichtige Archivierung und Wiederherstellung für langlebige Kontexte.
- **Datenbank-Caching-Systeme:** Diese optimieren den Datenzugriff, führen aber keine semantische Suche oder kontext-sensitive Validierung durch KI-Agenten durch.

SABEE ist das erste System, das eine vollautomatische, intelligente und validierte Lösung für das Problem des Kontextverlusts in langlebigen Multi-Agenten-Systemen bietet.

---

## 6. Detaillierte Abgrenzung zum Stand der Technik

Die Einzigartigkeit von SABEE wird durch die Abgrenzung zu bestehenden Technologien und wissenschaftlichen Arbeiten deutlich:

| Technologie/Arbeit | Nächster relevanter Stand der Technik | Abgrenzung und Neuheit von SABEE |
| :--- | :--- | :--- |
| **LLM Context Management** | **US IP 12387050** [1] | Dieses IP beschreibt ein System für "unlimited context windows through thought abstraction and hierarchical memory management". SABEE unterscheidet sich durch die **spezifische 3-Schichten-Architektur** mit klar definierten Zeitgrenzen (24h, 30d) und die **Zwei-Agenten-Validierung** (QA Agent, Governance Agent). |
| **Memory Management** | **MongoDB: Memory Engineering for Multi-Agent Systems** [2] | Diese Arbeit identifiziert Memory als kritisches Problem, bietet aber keine detaillierte technische Lösung. SABEE implementiert eine konkrete **hierarchische Architektur** mit intelligenter Wiederherstellung. |
| **RAG-Systeme** | **Anthropic: Contextual Retrieval** [3] | Contextual Retrieval verbessert die Retrieval-Qualität in RAG-Systemen für statische Wissensbasen. SABEE hingegen verwaltet den **dynamischen, projektspezifischen Kontext** eines langlebigen Agenten mit zeitbasierten Archivierungsregeln. |
| **LangChain Memory** | **Standard Memory-Systeme in Agenten-Frameworks** [4] | Diese bieten einfache In-Memory-Speicher oder Chat-Historien ohne intelligente, mehrschichtige Archivierung für langlebige Kontexte. |
| **Datenbank-Caching** | **Standard-Caching-Systeme** | Diese optimieren Datenzugriff, führen aber keine **semantische Suche** oder **kontext-sensitive Validierung durch KI-Agenten** durch. |

### Referenzen

[1] US IP 12387050. *Multi-stage LLM with unlimited context*.

[2] MongoDB (2025). *Why Multi-Agent Systems Need Memory Engineering*.

[3] Anthropic (2024). *Contextual Retrieval in AI Systems*.

[4] Factory.ai (2025). *The Context Window Problem: Scaling Agents Beyond Token Limits*.
