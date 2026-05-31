---
category: [technik, ui]
type: referenz
confidence: high
source_type: code
game_version: "unknown"
tags: [blueprint_editor, react, state_management, frontend]
related: ["[[30_Resources/Game_Data/Blueprints_Technical|Blueprint System]]"]
sources: ["code analysis"]
created: 2024-05-23
updated: 2024-05-23
---

# Blueprint Editor Frontend (Technische Spezifikation) & Kurzbeschreibung
Dokumentation der clientseitigen Logik und des State-Managements des Blueprint-Editors. Beschreibt die Interaktion zwischen UI und Backend via React-Hooks.

## Basisdaten

| Komponente | Funktion | Implementierung / Detail |
| :--- | :--- | :--- |
| **Strategie-Management** | `useBlueprintStrategy` | Orchestriert globale Spieler- und spezifische Blueprint-Strategien |
| **Bildverarbeitung** | `useBlueprintImageUpload` | Automatische WebP-Konvertierung und Resizing ($64 \times 64$ bis $256 \times 256$) |
| **Editier-Dialog** | `useBlueprintEditDialog` | Verwaltung von Metadaten und Namensstilen (`nameStyleState`) |
| **Live-Zustand** | `useBlueprintsLiveState` | Modus-Umschaltung (List vs. Editor) und Listen-Interaktion |

## Mechanik / Verhalten

### 1. Strategie-Management (`useBlueprintStrategy`)
Der zentrale Hook für den Kampfstrategie-Editor fungiert als Brücke zwischen der UI und der `blueprintStrategyApi`.
* **State Orchestration:** Verwaltet sowohl die globale Spieler-Strategie (`playerStrategyDraft`) als auch die spezifische Blueprint-Strategie (`strategyDraft`).
* **Dirty State Tracking:** Vergleicht den aktuellen Entwurf mit dem ursprünglichen Zustand (via Serialisierung), um zu bestimmen, ob der "Save"-Button aktiviert werden soll.
* **Validierung & Fehlerbehandlung:** Transformiert technische Fehlercodes (z. B. `START_CYCLE_OUT_OF_RANGE`) in lokalisierte Benutzer-Nachrichten (`i18n`) und verarbeitet Server-Fehler im Payload.
* **Organisation:** Verwaltet die Sortierung und Gruppierung der Blueprints (Favoriten, Kategorien) basierend auf Benutzereinstellungen.

### 2. Bildverarbeitung & Upload (`useBlueprintImageUpload`)
Ein spezialisierter Hook zur Handhabung von Blueprint-Grafiken.
* **Format-Konvertierung:** Alle hochgeladenen Bilder werden automatisch in das WebP-Format konvertiert, um die Performance zu optimieren.
* **Resizing:** Implementiert strikte Größenbeschränkungen (Standard: $64 \times 64$ bis $256 \times 256$ Pixel) und eine einstellbare Qualität ($0.9$).
* **Zwei-Wege-Handling:** Unterstützt sowohl den direkten Upload von Dateien (`DataURL`) als auch die Verwendung bestehender Bild-URLs.

### 3. Editier-Dialog Logik (`useBlueprintEditDialog`)
Verwaltet den Lebenszyklus des Modals zur Bearbeitung von Blueprint-Metadaten.
* **Metadaten-Management:** Steuert die Felder für Name, Beschreibung und Bildquelle.
* **Name Style Editor:** Verwaltet das Ein- und Ausschalten sowie die Konfiguration von visuellen Namensstilen (`nameStyleState`). Dies beinhaltet eine asynchrone Synchronisation mit dem Server via `BLUEPRINT_NAME_STYLE_TOGGLE_EVENT`.
* **Zustands-Synchronisation:** Überwacht Änderungen an allen Feldern, um den "Can Save"-Status zu berechnen.

### 4. Live-Zustand & Navigation (`useBlueprintsLiveState`)
Steuert die übergeordnete Ansicht der Blueprint-Verwaltung.
* **Modus-Umschaltung:** Wechselt zwischen der Listenansicht (`list`) und dem Editor-Modus (`editor`).
* **Listen-Interaktion:** Verwaltet das Auf- und Zuklappen von Kategorien (`expanded` state) sowie das Löschen von Blueprints.
* **Editor-Integration:** Koppelt den Editier-Dialog an die Auswahl eines spezifischen Blueprints.

## Verknüpfungen
- [[30_Resources/Game_Data/Blueprints_Technical|Blueprint System]]

## Changelog
- 2024-05-23: Datei neu erstellt basierend auf Frontend-Quellcode-Analyse.
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Technische Spezifikation des Blueprint-Editors: React-Hooks für Strategie-Management (`useBlueprintStrategy`), Bildverarbeitung (WebP, Resizing), Metadaten-Editierung (`useBlueprintEditDialog`) und Live-Zustandsverwaltung (`useBlueprintsLiveState`).
