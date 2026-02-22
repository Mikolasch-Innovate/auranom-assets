# AURANOM Content Engine - Configuration

Dieses Verzeichnis enthält die Konfiguration für den automatisierten Content-Workflow.

---

## Struktur

```
config/
├── personas/                    # Rollenspezifische Personas (KEINE Projektdetails)
│   ├── mag_elias_dubois.md     # Research Assistant
│   ├── prof_critique.md         # Critical Reviewer
│   └── dr_lena_rossi.md         # Auditorin
├── project_context.md           # Projektspezifischer Kontext (für Manus Project Instructions)
└── README.md                    # Diese Datei
```

---

## Personas vs. Projekt-Kontext

### ✅ Personas (rollenspezifisch)

**Speicherort:** `personas/*.md`

**Inhalt:**
- Rolle & Expertise
- Arbeitsmethodik
- Output-Struktur
- Arbeitsstil

**KEINE Projektdetails:**
- ❌ AURANOM-Komponenten
- ❌ ISO-Standards
- ❌ Dissertationsziele
- ❌ Zielgruppe

**Vorteil:** Personas sind wiederverwendbar für andere Projekte.

### ✅ Projekt-Kontext (projektspezifisch)

**Speicherort:** `project_context.md`

**Verwendung:** Wird in **Manus Project Instructions** hinterlegt, sodass alle Tasks automatisch Zugriff haben.

**Inhalt:**
- AURANOM Framework (10 Komponenten)
- ISO-Standards (42001, 27001, 20700, 21500)
- Dissertationsziele (3 Papers, 30+ Blogs)
- Zielgruppe (C-Suite, DACH-Raum)
- Content-Strategie
- Multi-Agent Workflow

**Vorteil:** Single Source of Truth - alle Agenten arbeiten mit identischem Kontext.

---

## Verwendung in Task-Scripts

### Beispiel: Research-Ingestion

```python
# 01_ingest_research_v2.py

# Persona laden
with open("config/personas/mag_elias_dubois.md") as f:
    persona = f.read()

# System Prompt (Persona + Hinweis auf Project Instructions)
system_prompt = f"""{persona}

**Projekt-Kontext:** Siehe Manus Project Instructions für AURANOM-Komponenten, ISO-Standards und Dissertationsziele.
"""

# Perplexity API Call
response = client.chat.completions.create(
    model="sonar-deep-research",
    messages=[
        {"role": "system", "content": system_prompt},
        {"role": "user", "content": f"Research: {topic}"}
    ]
)
```

### Beispiel: Manus Task Creation

```python
# 02_create_manus_task.py

# Task-Prompt (referenziert Project Instructions)
prompt = f"""Schreibe einen Thought-Leadership-Artikel basierend auf diesem Research Report:

{research_report}

**Kontext:** Siehe Project Instructions für AURANOM-Framework, ISO-Standards und Zielgruppe.
"""

# Manus API Call mit projectId
response = requests.post(
    "https://api.manus.ai/v1/tasks",
    json={
        "projectId": "AKr8wnjgZAcN8NWmQfQQED",  # Projekt-Kontext wird automatisch injiziert
        "prompt": prompt
    }
)
```

---

## Manus Project Instructions Setup

### Schritt 1: Projekt-Kontext kopieren

Kopiere den Inhalt von `project_context.md` in die Manus Project Instructions:

1. Öffne Manus Project: "Doktorarbeit - KI-Autonomie im Consulting"
2. Gehe zu Project Settings → Instructions
3. Füge den Inhalt von `project_context.md` ein
4. Speichern

### Schritt 2: Prof. Sonderhausen Rolle hinzufügen

Die Prof. Sonderhausen Rolle ist bereits in den Project Instructions hinterlegt. Stelle sicher, dass sie NICHT in Task-Prompts wiederholt wird.

---

## Best Practices

### ✅ DO

- Personas enthalten nur Rolle und Methodik
- Projekt-Kontext wird in Manus Project Instructions hinterlegt
- Task-Prompts referenzieren Project Instructions ("Siehe Project Instructions für...")
- Personas sind wiederverwendbar für andere Projekte

### ❌ DON'T

- Projektdetails in Personas duplizieren
- Projekt-Kontext in jedem Task-Prompt wiederholen
- Prof. Sonderhausen Rolle in Task-Prompts wiederholen (bereits in Project Instructions)
- Personas direkt in Task-Prompts kopieren (nur referenzieren)

---

## Wartung

### Personas aktualisieren

Wenn sich die **Methodik** eines Agenten ändert (z.B. neue Review-Kriterien für Prof. Critique):
- Aktualisiere die entsprechende Persona-Datei
- Keine Änderungen an Project Instructions nötig

### Projekt-Kontext aktualisieren

Wenn sich **Projektdetails** ändern (z.B. neue AURANOM-Komponente, zusätzlicher ISO-Standard):
- Aktualisiere `project_context.md`
- Kopiere den neuen Inhalt in Manus Project Instructions
- Alle zukünftigen Tasks verwenden automatisch den neuen Kontext

---

## Troubleshooting

### Problem: Agent kennt AURANOM-Komponenten nicht

**Ursache:** Project Instructions nicht korrekt hinterlegt.

**Lösung:** Kopiere `project_context.md` in Manus Project Instructions.

### Problem: Task-Prompt zu lang

**Ursache:** Projekt-Kontext wird im Prompt wiederholt.

**Lösung:** Entferne Projekt-Kontext aus Prompt, referenziere nur Project Instructions.

### Problem: Persona enthält veraltete Projektdetails

**Ursache:** Projektdetails wurden fälschlicherweise in Persona gespeichert.

**Lösung:** Entferne Projektdetails aus Persona, verschiebe sie nach `project_context.md`.
