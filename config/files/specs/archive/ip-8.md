# Technische Spezifikation: IP 8 (G-EE)

**Datum:** 16. November 2025
**Version:** 1.0
**Autor:** Dr. Lena Rossi
**Status:** Entwurf

---

## 1. Titel der Erfindung

**System und Verfahren zur dualen, ereignisgesteuerten Governance-Durchsetzung in Multi-Agenten-Systemen mit konfigurierbarer, projektspezifischer Regelebene**

**Kurztitel:** Governance & Execution Engine (G-EE)

---

## 2. Problemstellung

Multi-Agenten-Systeme, die in regulierten oder komplexen Geschäftsumgebungen operieren, stehen vor einer dualen Herausforderung: Sie müssen sowohl die **konstanten, unveränderlichen Governance-Regeln des Anbieters** (z.B. Sicherheitsstandards, Datenschutzgesetze) als auch die **dynamischen, projektspezifischen Regeln des Kunden** (z.B. interne Genehmigungsprozesse, Budgetgrenzen, Kommunikationswege) einhalten. Bestehende Orchestrierungs-Tools sind nicht in der Lage, diese beiden unterschiedlichen Regelebenen gleichzeitig und in Echtzeit durchzusetzen. Sie sind entweder auf eine feste System-Governance beschränkt oder erfordern manuelle Eingriffe, um kundenspezifische Anforderungen zu erfüllen. Dies führt zu Compliance-Risiken, Ineffizienz und mangelnder Anpassungsfähigkeit.

---

## 3. Lösung: Die G-EE Architektur

Die Governance & Execution Engine (G-EE) ist eine zentrale Laufzeit-Governance-Komponente, die als übergeordnete Kontrollinstanz für alle Subsysteme (wie SABEE, ACI, ACHP) agiert. Ihre Kerninnovation ist die Fähigkeit, zwei separate, aber hierarchisch geordnete Regelwerke in Echtzeit zu überwachen und durchzusetzen.

### 3.1. Die duale Governance-Architektur

Die G-EE implementiert eine klare Trennung zwischen System- und Projekt-Governance:

| Ebene | Name | Scope | Änderbarkeit | Beispielregel |
| :--- | :--- | :--- | :--- | :--- |
| **Ebene 1** | **System-Governance (ISMS)** | Das Auranom-System als Ganzes | **Konstant** (vom Anbieter definiert) | "Alle Daten im PPLS müssen vor der Verarbeitung anonymisiert werden." |
| **Ebene 2** | **Projekt-Governance** | Das spezifische Kundenprojekt | **Dynamisch** (vom Kunden konfigurierbar) | "Jede Ausgabe über 10.000€ muss vom CFO des Kunden genehmigt werden." |

### 3.2. Funktionsweise: Event Sourcing und Echtzeit-Validierung

Die G-EE operiert auf Basis einer Event-Sourcing-Architektur. Jede Aktion, die von einem Agenten oder Subsystem ausgeführt wird, wird als "Event" an die G-EE gesendet, **bevor** sie ausgeführt wird.

1.  **Event-Erfassung:** Ein Agent (z.B. ACI) will eine Aktion ausführen (z.B. "Neues Projekt-Team mit 5 Beratern erstellen"). Er sendet ein `action_request` Event an die G-EE.
2.  **Duale Regel-Validierung:** Die G-EE validiert das Event gegen **beide** Regelwerke:
    *   **Prüfung gegen System-Governance:** "Verstößt die Erstellung von 5 Agenten gegen eine System-Ressourcengrenze?" (ISMS-Regel)
    *   **Prüfung gegen Projekt-Governance:** "Überschreiten die Kosten für 5 Berater das vom Kunden definierte Projektbudget?" (Projekt-Regel)
3.  **Enforcement (Durchsetzung):**
    *   **Bei Konformität:** Die G-EE genehmigt das Event und leitet es zur Ausführung weiter. Das Ergebnis wird im Audit-Trail protokolliert.
    *   **Bei Verletzung:** Die G-EE blockiert die Aktion und löst einen vordefinierten Prozess aus (z.B. "Sende Eskalations-Nachricht an Agent Veritas" oder "Informiere den menschlichen Direktor").

### 3.3. Konfigurierbare Projekt-Governance

Ein wesentliches Merkmal der G-EE ist die Fähigkeit, kundenspezifische Regeln zur Laufzeit zu laden und anzuwenden. Dies geschieht über eine Konfigurationsschnittstelle, über die ein Kunde oder Projektmanager Regeln im Format "Wenn-Dann" definieren kann. Diese Regeln werden in einer separaten, projektspezifischen Datenbank gespeichert und von der G-EE für die Validierung auf Ebene 2 herangezogen.

### 3.4. Fehler-Counter und Audit-Trail

-   **Fehler-Counter:** Die G-EE führt pro Agent und pro Subsystem einen Zähler für Governance-Verletzungen. Bei wiederholten Verstößen kann ein Agent automatisch in einen "Quarantäne"-Modus versetzt werden, in dem er nur noch unter erhöhter Aufsicht agieren darf.
-   **Umfassender Audit-Trail:** Da jede Aktion als Event protokolliert wird, erstellt die G-EE einen lückenlosen, unveränderlichen Audit-Trail, der für Compliance-Prüfungen (z.B. nach ISO 27001) unerlässlich ist.

---

## 4. Patentierbare Kernmerkmale

1.  **Das duale Governance-Modell:** Das System zur gleichzeitigen Verarbeitung und Durchsetzung von zwei hierarchisch geordneten Regelwerken (konstante System-Governance und dynamische Projekt-Governance).
2.  **Die ereignisgesteuerte Echtzeit-Validierung:** Das Verfahren, bei dem jede Agenten-Aktion vor der Ausführung als Event erfasst und gegen beide Regelwerke validiert wird.
3.  **Die konfigurierbare Projekt-Regelebene:** Die Architektur, die es ermöglicht, kundenspezifische Governance-Regeln zur Laufzeit zu laden und anzuwenden, ohne die Kern-System-Governance zu verändern.
4.  **Der integrierte Fehler-Counter- und Eskalationsmechanismus:** Das System zur automatisierten Überwachung von Regelverstößen und zur Einleitung vordefinierter Korrekturmaßnahmen.

---

## 5. Abgrenzung zum Stand der Technik

-   **Traditionelle BPM-Engines:** Diese führen starre, vordefinierte Prozesse aus. Die G-EE hingegen überwacht und steuert flexible, von KI-Agenten ausgeführte Aktionen basierend auf dynamischen Regeln.
-   **API-Gateways:** Diese kontrollieren den *Zugriff* auf Systeme, aber nicht die *Logik* der Aktionen, die innerhalb der Systeme ausgeführt werden.
-   **Cloud-Security-Tools (z.B. AWS Config):** Diese überwachen die Konformität der *Infrastruktur*, aber nicht die Konformität der *Geschäftsprozesse*, die auf dieser Infrastruktur laufen.

Die G-EE ist das erste System, das eine aktive, duale und konfigurierbare Laufzeit-Governance speziell für die komplexen Anforderungen von Multi-Agenten-Systemen im Geschäftsumfeld bietet.

---

## 6. Detaillierte Abgrenzung zum Stand der Technik

Die Einzigartigkeit der G-EE wird durch die Abgrenzung zu bestehenden Technologien und wissenschaftlichen Arbeiten deutlich:

| Technologie/Arbeit | Nächster relevanter Stand der Technik | Abgrenzung und Neuheit der G-EE |
| :--- | :--- | :--- |
| **Governance-Systeme** | **Governance-as-a-Service (GaaS)** [1] | GaaS operiert auf einer einzigen, statischen Regelebene und validiert Agenten-Outputs reaktiv. Die G-EE hingegen implementiert eine **duale Governance-Architektur** mit einer konstanten System- und einer dynamischen Projekt-Regelebene und validiert Aktionen **proaktiv vor der Ausführung**. |
| **Runtime Verification** | **RV4JaCa** [2] und **Shields** [3] | Diese Systeme fokussieren auf die formale Verifikation der Systemkorrektheit (z.B. nach temporalen Logiken). Die G-EE fokussiert auf die Durchsetzung von **flexiblen, konfigurierbaren Business- und Governance-Regeln**, nicht auf formale Korrektheit. |
| **Access Control** | **Policy-Based Access Control (PBAC)** [4] | PBAC-Systeme kontrollieren den **Zugriff auf Ressourcen** (z.B. "Darf Agent A auf Datenbank B zugreifen?"). Die G-EE kontrolliert die **Logik und Konformität von Aktionen** (z.B. "Ist die von Agent A vorgeschlagene Transaktion konform mit den Projekt-Budget-Regeln?"). |
| **Event Sourcing** | **Standard Event Sourcing Patterns** [5] | Bestehende Patterns nutzen Event Sourcing für State-Management und Audits. Die G-EE **integriert Event Sourcing direkt in den Governance-Prozess**, indem sie Events als Trigger für die Echtzeit-Validierung nutzt, was eine neuartige Anwendung des Patterns darstellt. |
| **Agenten-Plattformen** | **US Patent 20250232029** [6] | Bestehende Patente für Agenten-Laufzeitumgebungen fokussieren auf Deployment und Management, nicht auf eine granulare, duale Governance-Durchsetzung zur Laufzeit. |

### Referenzen

[1] Pervez, H. et al. (2025). *Governance-as-a-Service: A Multi-Agent Framework for AI System Compliance and Policy Enforcement*. arXiv:2508.18765v1.

[2] Engelmann, D. C. et al. (2023). *RV4JaCa—Towards Runtime Verification of Multi-Agent Systems*. MDPI.

[3] (Anonym). *Synthesis of minimum-cost shields for multi-agent systems*. IEEE.

[4] Cerbos (2025). *PBAC Is Back. Why Policy-Based Access Control is a Must-Have for Enterprise Security*.

[5] Microsoft Azure Architecture Center. *Event Sourcing pattern*.

[6] US Patent 20250232029. *Runtime environment for execution of autonomous agents*.
