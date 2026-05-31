---
category: [schiffe, technik]
type: referenz
confidence: high
source_type: code_analysis
game_version: "unknown"
tags: [forces_api, unit_management, missions, recycling]
related: ["[[30_Resources/Game_Data/Blueprints_Technical|Blueprint System]]", "[[30_Resources/Game_Data/Combat_Strategy_Technical|Combat Strategy Technical]]"]
sources: ["forcesApi.js"]
created: 2024-05-23
updated: 2024-05-23
---

# Forces & Unit Management (Technische Spezifikation) & Kurzbeschreibung
Dokumentation der API-Struktur und Logik zur Verwaltung von Einheiten, Missionen sowie dem Recycling- und Upgrade-System.

## Basisdaten

| Funktion | Beschreibung |
| :--- | :--- |
| **Einheiten-Management** | Abrufen, Erstellen, Upgraden und Recyceln von Units |
| **Missions-Logik** | Erstellung und Validierung von Flottenmissionen |
| **Datenintegrität** | Batch-Optimierung, Caching und Idempotenz (Recycling) |

## Mechanik / Verhalten

### 1. Einheiten-Management (`forcesApi.js`)
Das System ermöglicht die Verwaltung von Einheiten auf Planeten.
* **Abruf-Logik:**
    * `fetchUnits(planetId)`: Ruft alle Einheiten eines Planeten ab.
    * `fetchUnitsBatch(planetIds)`: Optimierter Batch-Abruf mit Caching (`UNIT_LIST_CACHE_TTL_MS`), um Netzwerkzugriffe zu minimieren.
* **Operationen:**
    * `createMission(payload)`: Erstellt eine neue Flottenmission (z. B. Bewegung).
    * `recycleUnit({ planetId, blueprintId, amount })`: Zerstört Einheiten gegen Ressourcen. Nutzt einen `idempotencyKey`, um doppelte Recyclings bei Netzwerkfehlern zu verhindern.
    * `upgradeUnits(...)`: Transformiert eine Gruppe von Einheiten eines Blueprints in einen neuen Blueprint (Upgrade-Prozess).

### 2. Missions- & Koordinatenprüfung
Vor dem Start einer Mission erfolgt eine Validierung der Zielkoordinaten via `checkCoordinates(coordinates)`, um Erreichbarkeit und Hindernisse zu prüfen.

### 3. Workflow & Datenintegrität
* **Batch-Optimierung:** Bevorzugung von Batch-Requests für die UI (z. B. Galaxie-Übersicht) zur Latenzreduktion.
* **Caching:** Verwendung eines TTL-basierten Caches für konsistente Planeten-Einheiten-Ansichten.
* **Idempotenz:** Kritische Operationen wie das Recycling nutzen Schlüssel, um sicherzustellen, dass eine Aktion nur genau einmal ausgeführt wird.

### 4. Lokale Missions-Speicherung (Saved Missions)
Missionsdaten können via `localStorage` lokal gespeichert werden.
* **Datenstruktur:** Enthält Identität (`id`, `name`, `missionType`), Konfiguration (`target`, `cargo`, `unitSelection`), Ausführungsmodus (`direct_start` vs. `open_editor`) sowie einen statischen Snapshot und Zeitstempel.
* **Sortierung:** Automatische absteigende Sortierung nach dem Aktualisierungsdatum (`updatedAt`).

## Verknüpfungen
- [[30_Resources/Game_Data/Blueprints_Technical|Blueprint System]]
- [[30_Resources/Game_Data/Combat_Strategy_Technical|Combat Strategy Technical]]

## Changelog
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Technische Spezifikation der Forces API: Einheiten-Management (Abruf, Recycling mit Idempotenz, Upgrades), Missions-Validierung und lokale Missions-Speicherung via localStorage.
