---
category: [fraktion, spielmechanik]
type: technik
confidence: high
source_type: code_analysis
game_version: "unknown"
tags: [faction, api, outlaw, gameplay_effects]
related: ["[[30_Resources/Alliance_System_Technical|Alliance System]]", "[[30_Resources/Game_Data/Blueprints_Technical|Blueprint System]]"]
sources: ["factionsApi.js", "factionPresentation.js"]
created: 2026-05-22
updated: 2024-05-23
---

# Faction System (Technische Spezifikation) & Kurzbeschreibung
Beschreibung der Implementierung der Fraktionsverwaltung, einschließlich API-Kommunikation, UI-Präsentation und spielmechanischer Auswirkungen wie dem Outlaw-Risiko.

## Basisdaten

| Bereich | Kernfunktion / Effekt |
| :--- | :--- |
| **API** | `fetchFactionCatalog()`, `changeFaction(factionId)` |
| **Gameplay-Effekte** | Cargo Multiplier, Speed Multiplier |
| **Outlaw-System** | Risiko-Management mit zeitlich begrenztem Status |

## Mechanik / Verhalten

### 1. API & Kommunikation
Die Interaktion erfolgt über den `LiveGameService` via WebSockets.
* **Funktionen (`factionsApi.js`):**
    * `fetchFactionCatalog()`: Ruft die Liste aller verfügbaren Fraktionen vom Server ab (mit Normalisierung für die UI).
    * `changeFaction(factionId)`: Sendet eine Anfrage zur Änderung der aktuellen Fraktion.
* **Fehlerbehandlung:** Spezialisierte Logik (`mapFactionChangeError`) übersetzt technische API-Fehler in verständliche Benutzer-Nachrichten.

### 2. Datenmodell & Präsentation
Die UI-Präsentation wird durch Normalisierungsschichten (`factionPresentation.js`) vorbereitet:
* **Catalog Response:** Transformation der Serverdaten für effizientes Rendering von Listen und Auswahlmenüs.
* **Faction State:** Verarbeitung des aktuellen Spielerstatus zur korrekten Anzeige von Bannern oder Modifikatoren.

### 3. Fraktions-Effekte (Gameplay)
Fraktionen beeinflussen die Spielmechanik direkt über Multiplikatoren:
* **Cargo Multiplier:** Beeinflusst die Frachtkapazität der Einheiten einer Fraktion.
* **Speed Multiplier:** Beeinflusst die maximale Geschwindigkeit der Flotten einer Fraktion.

### 4. Outlaw-Status & Risiko
Ein Mechanismus zur Visualisierung und Verwaltung des "Outlaw"-Risikos (`OutlawRiskDialog`).
* **Gameplay-Mechanik:** Spieler können einen zeitlich begrenzten Status erlangen (berechnet via `outlawDurationDays` und `outlawExpiresAtPreview`).
* **UI-Feedback:** Das Interface warnt vor Aktionen, die zum Outlaw-Status führen, und erfordert eine explizite Bestätigung über ein `AlertDialog`.

## Verknüpfungen
- [[30_Resources/Alliance_System_Technical|Alliance System]]
- [[30_Resources/Game_Data/Blueprints_Technical|Blueprint System]]

## Changelog
- 2026-05-22: Erstmals erstellt.
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Technische Spezifikation des Fraktionssystems: API-Funktionen (Catalog, Change), UI-Normalisierung, spielmechanische Multiplikatoren (Cargo, Speed) und das Outlaw-Risiko-System mit Warnmechanismen.
