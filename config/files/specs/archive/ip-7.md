# Technische Spezifikation: Patent 8 (FEGR)

**Datum:** 16. November 2025
**Version:** 1.0
**Autor:** Dr. Lena Rossi
**Status:** Entwurf

---

## 1. Titel der Erfindung

**System und Verfahren zur multimodalen Analyse nonverbaler Signale zur dynamischen Steuerung von KI-Agenten in Gruppeninteraktionen**

**Kurztitel:** Facial and Gestic Recognition (FEGR)

---

## 2. Problemstellung

Die Kommunikation zwischen Menschen ist zu einem großen Teil nonverbal. KI-Agenten, die nur auf Text oder Sprache reagieren, verpassen entscheidende Signale wie Mimik, Gestik und Körperhaltung. Dies schränkt ihre Fähigkeit ein, die emotionale Verfassung, das Engagement oder die Absichten eines menschlichen Gegenübers zu verstehen. Besonders in Gruppeninteraktionen (z.B. Workshops, Präsentationen) ist es für einen KI-Agenten unmöglich zu erkennen, welche Person spricht, wer aufzeigt oder ob die Gruppe als Ganzes das Interesse verliert. Bestehende Gesichtserkennungssysteme sind meist auf einzelne Personen oder einfache Emotionserkennung beschränkt und bieten keine integrierte Lösung zur Steuerung von Agenten in einem Geschäftskontext.

---

## 3. Lösung: Die FEGR-Architektur

Das FEGR-System ist eine multimodale Analyse-Engine, die nonverbale Signale aus Videoströmen in Echtzeit erfasst, interpretiert und in handlungsrelevante Befehle für KI-Agenten umwandelt. Es ermöglicht eine natürlichere und effektivere Mensch-KI-Kollaboration, insbesondere in Szenarien mit mehreren Teilnehmern.

Die Architektur besteht aus drei Kernmodulen:

### 3.1. Modul 1: Nonverbale Echtzeit-Analyse

Dieses Modul analysiert den Videostream und extrahiert grundlegende nonverbale Datenpunkte.

- **Gesichtsanalyse:** Erkennt Basisemotionen (z.B. Freude, Verwirrung, Überraschung) und die Blickrichtung (Gaze) mittels Convolutional Neural Networks (CNNs).
- **Gesten-Analyse:** Erkennt spezifische Handgesten (z.B. Hand heben, Daumen hoch) und Körperhaltungen (z.B. Arme verschränken, Nicken) mittels Pose Estimation (z.B. MediaPipe).
- **Handlungsempfehlung:** Die extrahierten Daten werden an eine übergeordnete Logik-Engine (z.B. ACI) gesendet, die eine kontextbezogene Handlungsempfehlung für den agierenden KI-Agenten ableitet (z.B. "Kunde scheint verwirrt, bitte den Punkt einfacher erklären.").

### 3.2. Modul 2: Multisprecher- und Identitätsmanagement (Seminarraum-Modus)

Dieses Modul ist für Interaktionen mit mehreren Personen optimiert.

- **Personen-Tracking:** Identifiziert und verfolgt mehrere Personen im Sichtfeld der Kamera und weist jeder Person eine temporäre, anonyme ID zu.
- **Dynamische Namenszuordnung:** Wenn eine Person im Gespräch mit Namen genannt wird (z.B. "Frau Meier, Sie hatten eine Frage?"), erfasst das System den Namen über Speech-to-Text und verknüpft ihn mit der entsprechenden Personen-ID in einer temporären Datenbank.
- **Aufzeige-Trigger:** Erkennt die Geste "Hand heben" und verknüpft sie mit der identifizierten Person. Das System sendet einen präzisen Trigger an den KI-Agenten (z.B. "Trigger: Person 'Frau Meier' hat aufgezeigt."), der daraufhin die Person direkt ansprechen kann.

### 3.3. Modul 3: Gruppen-Engagement-Analyse

Dieses Modul aggregiert die nonverbalen Signale der gesamten Gruppe, um das allgemeine Engagement-Level zu bewerten.

- **Müdigkeits-Erkennung:** Analysiert aggregierte Metriken wie die Lidschlussrate (PERCLOS) und die Kopfhaltung über alle Teilnehmer hinweg.
- **Desinteresse-Erkennung:** Erkennt Muster wie gleichzeitiges Wegsehen, wiederholtes Gähnen oder eine mehrheitlich passive Körperhaltung.
- **Gruppen-Handlungsempfehlung:** Wenn ein vordefinierter Schwellenwert für Müdigkeit oder Desinteresse in der Gruppe überschritten wird, generiert das System eine proaktive Empfehlung für den Agenten (z.B. "Empfehlung: Schlage eine kurze Pause vor." oder "Empfehlung: Stelle eine interaktive Frage, um die Gruppe zu aktivieren.").

---

## 4. Patentierbare Kernmerkmale

1.  **Die Kombination der drei Module:** Das integrierte System, das individuelle nonverbale Analyse, Multisprecher-Identitätsmanagement und Gruppen-Engagement-Analyse zu einem kohärenten Ganzen verbindet, um KI-Agenten zu steuern.
2.  **Die dynamische Namenszuordnung im Seminarraum-Modus:** Das Verfahren, bei dem durch die Kombination von Personen-Tracking und Speech-to-Text eine temporäre, aber namentliche Identifizierung von Teilnehmern für die Dauer einer Interaktion erfolgt.
3.  **Der Aufzeige-Trigger:** Der spezifische Mechanismus, der die Geste des Handhebens einer identifizierten Person zuordnet und einen präzisen, handlungsrelevanten Trigger für den KI-Agenten generiert.
4.  **Die aggregierte Gruppen-Engagement-Analyse:** Das Verfahren zur Ableitung einer Handlungsempfehlung für den Agenten basierend auf der Analyse der kollektiven nonverbalen Signale einer Gruppe.

---

## 5. Abgrenzung zum Stand der Technik

- **Standard-Gesichtserkennungs-APIs (z.B. Amazon Rekognition, Microsoft Face API):** Diese bieten generische Emotionserkennung für Einzelpersonen. FEGR geht weit darüber hinaus, indem es diese Daten in einen Handlungs- und Gruppenkontext stellt, mehrere Personen namentlich identifiziert und das kollektive Engagement bewertet.
- **Pose Estimation Bibliotheken (z.B. MediaPipe, OpenPose):** Diese liefern die Rohdaten der Körperhaltung. Die Innovation von FEGR liegt in der Interpretation dieser Rohdaten (z.B. Erkennung der spezifischen "Aufzeigen"-Geste) und deren Verknüpfung mit einer Personen-ID und einem Agenten-Trigger.
- **Systeme zur Müdigkeitserkennung im Automobilbereich:** Diese sind auf einen einzelnen Fahrer fokussiert. FEGR wendet ähnliche Prinzipien auf eine Gruppe an und leitet daraus soziale Interaktionsstrategien ab.

FEGR ist das erste System, das eine derart tiefe Integration von nonverbaler Analyse speziell für die Steuerung von KI-Agenten in dynamischen Einzel- und Gruppengesprächen im Geschäftsumfeld vorschlägt.

---

## 6. Detaillierte Abgrenzung zum Stand der Technik

Die Einzigartigkeit von FEGR wird durch die Abgrenzung zu bestehenden Technologien und wissenschaftlichen Arbeiten deutlich:

| Technologie/Arbeit | Nächster relevanter Stand der Technik | Abgrenzung und Neuheit von FEGR |
| :--- | :--- | :--- |
| **Emotionserkennung** | **US Patent 8209182B2** [1] | Dieses Patent beschreibt ein Emotionserkennungssystem für menschliches Verhalten. FEGR geht weiter, indem es Emotionen **in einen Handlungs- und Gruppenkontext** stellt und **dynamische Steuerungssignale für KI-Agenten** generiert. |
| **Workplace Emotion Detection** | **Snap Patent (2024)** [2] | Snap's Patent fokussiert auf Emotion Detection für Workplace Surveillance. FEGR nutzt die Analyse für die **aktive Steuerung von KI-Agenten** in Geschäftsinteraktionen, nicht für passive Überwachung. |
| **Multi-User Gesture Recognition** | **mmWave Radar System (2025)** [3] | Dieses System erkennt Gesten für zwei Nutzer mit 92,80% Genauigkeit. FEGR kombiniert Gestenerkennung mit **Personen-Identifikation** und **Aufzeige-Trigger-Generierung** für Agenten. |
| **MediaPipe Gesture Recognition** | **Google MediaPipe** [4] | MediaPipe bietet Gestenerkennung für Hände. FEGR integriert dies in ein größeres System mit **dynamischer Namenszuordnung** und **Gruppen-Engagement-Analyse**. |
| **Nonverbal Group Analysis** | **Gatica-Perez et al. (2009)** [5] | Diese Arbeit analysiert nonverbale Signale in Gruppen. FEGR wendet dies auf die **Steuerung von KI-Agenten** an und leitet **Handlungsempfehlungen** ab (z.B. "Pause vorschlagen"). |

### Referenzen

[1] US Patent 8209182B2. *Emotion recognition system*.

[2] The Daily Upside (2024). *Snap Patent Brings Emotion Detection to Workplace Surveillance*.

[3] Han, W. et al. (2025). *A Robust Real-Time Multiuser Gesture Recognition System*. IEEE.

[4] Google AI Edge (2025). *Gesture recognition task guide - MediaPipe*.

[5] Gatica-Perez, D. et al. (2009). *Automatic nonverbal analysis of social interaction in small groups*. ScienceDirect. Zitiert: 438 Mal.
