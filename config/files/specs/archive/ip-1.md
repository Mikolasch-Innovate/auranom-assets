# Technische Spezifikation: Dual-Prozess-Orchestrierung

## 1. Titel der Erfindung

**System und Verfahren zur Dual-Prozess-Orchestrierung von KI-Agenten zur Integration von Vertriebsprozessen nach ISO 9001 und Beratungsprozessen nach ISO 20700**

**Kurztitel:** Dual-Prozess Multi-Agent Orchestrator

---

## 2. Problembeschreibung

In der Praxis sind Vertrieb und Beratung oft getrennte Silos innerhalb von Unternehmen. Dies führt zu erheblichen Problemen: Kundenkontext geht bei der Übergabe vom Vertrieb zur Beratung verloren, manuelle Übergaben sind fehleranfällig und zeitaufwendig, und Upselling-Möglichkeiten werden nicht systematisch identifiziert. Bestehende Systeme fokussieren entweder auf Vertrieb oder auf Beratung, aber nicht auf die nahtlose Integration beider Prozesse.

---

## 3. Lösung: Die Dual-Prozess-Orchestrierung Architektur

Die Erfindung löst dieses Problem durch ein hierarchisches Multi-Agent-Orchestrierungssystem, das Vertriebsprozesse nach ISO 9001 und Beratungsprozesse nach ISO 20700 in einem einheitlichen System integriert.

### 3.1. Systemarchitektur

Das System umfasst 9 spezialisierte KI-Agenten in einer zweistufigen Hierarchie:

- **Ebene 1: Master-Orchestrator (Orion):** Koordiniert beide Prozesse (Vertrieb und Beratung) und stellt die Dual-Standard-Konformität sicher.
- **Ebene 2a: Vertriebsteam (3 Agenten):** Spezialisiert auf Lead Generation (Sales Agent A), Proposal & Negotiation (Sales Agent B) und Closing & Onboarding (Sales Agent C) nach ISO 9001.
- **Ebene 2b: Beratungsteam (5 Agenten):** Spezialisiert auf Contracting (Contracting Agent), Analysis & Strategy (Analysis Agent), Implementation (Implementation Agent), Quality Assurance (QA Agent) und Closure (Closure Agent) nach ISO 20700.

### 3.2. Dual-Prozess-Integration

Das System implementiert automatisierte, kontexterhaltende Übergaben zwischen dem Vertriebsteam und dem Beratungsteam. Ein strukturiertes Kontext-Paket wird bei der Übergabe von Sales Agent C (Vertrieb) an Contracting Agent (Beratung) übergeben, das alle relevanten Kundeninformationen, Erwartungen und Vereinbarungen enthält.

### 3.3. Bidirektionale Transitionen und Upselling

Ein zentrales Merkmal ist die bidirektionale Transition: Nicht nur Vertrieb → Beratung, sondern auch Beratung → Vertrieb. Der Closure Agent identifiziert während des Projektabschlusses neue Opportunities und leitet diese an Sales Agent B (Vertrieb) weiter, um Upselling-Prozesse zu initiieren.

---

## 4. Differenzierungsmerkmale

1.  **Dual-Prozess-Integration:** Die spezifische Integration von transaktionalen (Vertrieb) und wissensbasierten (Beratung) Prozessen in einem einheitlichen Multi-Agenten-System.
2.  **Automatisierte Vertrieb-zu-Beratung-Übergaben:** Der Mechanismus zur automatischen Übergabe von strukturierten Kontext-Paketen zwischen dem Vertriebsteam und dem Beratungsteam.
3.  **Bidirektionale Transitionen mit Upselling-Mechanismus:** Die Fähigkeit des Systems, Upselling-Opportunities während der Beratung zu identifizieren und automatisch zurück an den Vertrieb zu leiten.
4.  **Dual-Standard-Konformität:** Die gleichzeitige Überwachung und Durchsetzung von ISO 9001 (Vertrieb) und ISO 20700 (Beratung) durch einen einzigen Master-Orchestrator.

---

## 5. Abgrenzung zum Stand der Technik

Die Einzigartigkeit der Dual-Prozess-Orchestrierung wird durch die Abgrenzung zu bestehenden Technologien und wissenschaftlichen Arbeiten deutlich:

| Technologie/Arbeit | Nächster relevanter Stand der Technik | Abgrenzung und Neuheit |
| :--- | :--- | :--- |
| **Beratungs-MAS** | **IP 1 (Auranom) - Multi-Agenten-Orchestrierung für Beratung** [1] | IP 1 fokussiert ausschließlich auf Beratungsprozesse nach ISO 20700. IP 5 integriert **zusätzlich Vertriebsprozesse** nach ISO 9001 und ermöglicht **automatisierte Übergaben** und **Upselling** zwischen beiden Prozessen. |
| **CRM-Systeme** | **Salesforce Agentforce (2024)** [2] | Salesforce Agentforce ist für CRM und Vertrieb konzipiert, aber ohne Integration von **wissensbasierten Beratungsprozessen** oder ISO 20700-Konformität. |
| **Multi-Agent-Systeme** | **C3 AI – US IP 12,111,859** [3] | C3 AI ist für allgemeine Business-Funktionen konzipiert. IP 5 ist spezifisch für die **Dual-Prozess-Integration** von Vertrieb und Beratung mit **Dual-Standard-Konformität**. |

### Referenzen

[1] IP 1 (Auranom). *Multi-Agenten-Orchestrierung für Consulting-Prozesse nach ISO 20700*.

[2] Salesforce (2024). *Salesforce Agentforce Whitepaper*.

[3] US IP 12,111,859. *Multi-agent orchestration for business functions*.
