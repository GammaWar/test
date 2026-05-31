---
category: [technik, server]
type: referenz
confidence: medium
source_type: code_analysis
game_version: "unknown"
tags: [websocket, network, communication, engine.io]
related: ["[[30_Resources/Server_Architecture_Technical|Server Architecture]]"]
sources: ["citation_4"]
created: 2026-05-22
updated: 2024-05-23
---

# Netzwerk & Websocket Kommunikation (Technische Spezifikation) & Kurzbeschreibung
Beschreibung der technischen Basis der Echtzeit-Netzwerkkommunikation zwischen Client und Server.

## Basisdaten

| Bibliothek | Verwendungszweck |
| :--- | :--- |
| `engine.io-client` | WebSocket-Kommunikation und Transport-Layer |
| `date-fns` | Zeitstempel-Management & Differenzberechnungen (Offline-Produktion) |
| `decimal.js-light` | Präzise mathematische Berechnungen (Vermeidung von Floating-Point-Fehlern) |

## Mechanik / Verhalten

### Kommunikationsprotokoll
Das System nutzt eine WebSocket-basierte Architektur für die Echtzeit-Kommunikation zwischen Client und Server.

* **Websocket Layer:** Basierend auf dem `engine.io-client`. Dies ermöglicht bidirektionale, eventgesteuerte Kommunikation.
* **Netzwerk-Typ:** WebSocket-basiertes Netzwerk (`# Websocket_Network`).

## Verknüpfungen
- [[30_Resources/Server_Architecture_Technical|Server Architecture]]
- [[30_Resources/Game_Data/Universe_API_Technical|Universe API Technical]]

## Changelog
- 2026-05-22: Erstmals erstellt basierend auf Code-Analyse.
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Netzwerk-Infrastruktur: WebSocket-Kommunikation via `engine.io-client`. Wichtige Abhängigkeiten für Zeitberechnungen (`date-fns`) und präzise Wirtschaftsberechnungen (`decimal.js-light`).
