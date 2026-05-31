---
category: [technik, universum]
type: referenz
confidence: high
source_type: code_analysis
game_version: "unknown"
tags: [universe_api, websockets, protobuf, galaxy_visibility]
related: ["[[30_Resources/Game_Data/Server_Architecture_Technical|Server Architecture]]", "[[30_Resources/Game_Data/Server_Communication_Technical|Server Communication]]"]
sources: ["universeApi.js"]
created: 2024-05-23
updated: 2024-05-23
---

# Universe API (Technische Spezifikation) & Kurzbeschreibung
Dokumentation der Schnittstellen zur Abfrage des Universums, der Galaxie-Sichtbarkeit und der Sektor-Details via WebSockets.

## Basisdaten

| Komponente | Technologie / Detail |
| :--- | :--- |
| **Kommunikation** | WebSocket-basiert (`LiveGameService`) |
| **Datenformat** | Protobuf (für effiziente Snapshots) |
| **Timeout-Management** | `UNIVERSE_PREFETCH_TIMEOUT_MS` zur UI-Optimierung |

## Mechanik / Verhalten

### 1. Kommunikation & Verbindung
Die Interaktion erfolgt über den `LiveGameService`. Die Funktion `isUniverseSocketConnected()` prüft die aktive WebSocket-Verbindung für Universums-Anfragen.

### 2. API Funktionen (`universeApi.js`)

#### A. Sichtbarkeit & Snapshots
* **`fetchUniverseVisibility()`:** Ruft die aktuelle Sichtbarkeit der Galaxie ab (welche Bereiche des Universums für den Spieler sichtbar sind).
* **`fetchUniverseSnapshot()`:** Lädt einen vollständigen Snapshot des aktuellen Universums-Zustands unter Verwendung von Protobuf zur Minimierung der Payload.

#### B. Sektor-Details
* **`fetchUniverseSectorDetails(sectorKeys)`:** Ruft detaillierte Informationen für eine Liste von Sektoren ab. Die `sectorKeys` werden intern in X/Y-Koordinaten (`posX`, `posY`) umgewandelt.

#### C. Einheiten & Missionen
* **`fetchPlanetUnits(planetId)`:** Ruft die Liste aller Einheiten auf einem spezifischen Planeten ab.
* **`checkMissionCoordinates(coordinates)`:** Validiert Zielkoordinaten für eine geplante Flottenmission.
* **`createFleetMission(payload)`:** Erstellt eine neue Mission im System.

### 3. Technische Details (Optimierung)
Um die UI-Reaktionsfähigkeit bei langsamen Verbindungen zu gewährleisten, nutzt das System einen spezifischen `UNIVERSE_PREFETCH_TIMEOUT_MS`. Für große Datenmengen (Snapshots) wird Protobuf eingesetzt, um die Payload-Größe signifikant zu reduzieren.

## Verknüpfungen
- [[30_Resources/Game_Data/Server_Architecture_Technical|Server Architecture]]
- [[30_Resources/Game_Data/Server_Communication_Technical|Server Communication]]

## Changelog
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Technische Spezifikation der Universe API: Kommunikation via WebSockets, Sichtbarkeit & Snapshots (Protobuf), Sektor-Details (X/Y Mapping) sowie Funktionen für Einheiten-Abruf und Missions-Validierung.
