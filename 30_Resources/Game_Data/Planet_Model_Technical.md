---
category: [planet, technik]
type: referenz
confidence: high
source_type: code_analysis
game_version: "unknown"
tags: [planet_model, data_structure, resources, fertility]
related: ["[[30_Resources/Game_Data/Universe_API_Technical|Universe API]]", "[[30_Resources/Game_Data/Resource_Production_Technical|Resource Production]]"]
sources: ["code analysis"]
created: 2024-05-23
updated: 2024-05-23
---

# Planet Model (Technik) & Kurzbeschreibung
Technische Dokumentation der Datenstruktur und des Objektmodells eines Planeten im Spacewar-System. Der Planet fungiert als zentraler Container für Ressourcen, Gebäude, Einheiten und Bevölkerung.

## Basisdaten

| Attribut | Typ | Beschreibung |
| :--- | :--- | :--- |
| **ID & Besitzer** | `id`, `ownerId` | Eindeutige Identifikation und Inhaber (Spieler/Fraktion). |
| **Name & Stil** | `name`, `nameStyleState` | Name des Planeten inklusive visueller Formatierung. |
| **Fertilität** | `fertility`, `fertilityBase`, `fertilityBonus` | Steuerung des Bevölkerungswachstums. |
| **Klassifizierung** | `planetClass` | Typ (z. B. A, B, C) mit zugehörigen Ressourcen-Vorkommen. |

## Mechanik / Verhalten

### 1. Sub-Modelle & Komplexer Zustand

Der Planet besteht aus mehreren spezialisierten Datenstrukturen:

#### A. Ressourcen (`PlanetResources`)
Die Ressourcenverwaltung ist in fünf spezialisierte Maps unterteilt:
* **storage:** Aktueller Bestand der Ressourcen.
* **deposits:** Natürliche Vorkommen auf dem Planeten (beeinflussen die Produktion).
* **capacity:** Maximale Lagerkapazität pro Ressource.
* **production:** Aktuelle Netto-Produktionsraten.
* **consumption:** Aktueller Ressourcenverbrauch.

#### B. Koordinaten (`PlanetCoordinates`)
Die Position im Universum wird durch ein 3D-Koordinatensystem definiert: `posX`, `posY`, `posZ`.

#### C. Gebäude & Warteschlangen (Queues)
Der Planet verwaltet zwei Arten von Bauprozessen:
* **buildingQueue:** Liste der aktuell in Bau befindlichen Gebäude (`PlanetBuildingQueueItem`).
* **unitQueue:** Liste der aktuell in Produktion befindlichen Einheiten (`PlanetUnitQueueItem`).

### 2. Spezialfunktionen & Erweiterungen

#### A. Clone Tanks System
Einige Planeten verfügen über die `cloneTanks`-Funktionalität, die zwei Modi unterstützt:
* **FERTILITY Mode:** Erhöht die Fertilität für das Bevölkerungswachstum.
* **SOLDIER Mode:** Erhöht die Produktionsrate von Soldaten.

#### B. Visuelle Darstellung
Die visuelle Identität wird über `imageVariant` (für Texturen) und `nameStyleState` gesteuert.

## Verknüpfungen
- [[30_Resources/Game_Data/Universe_API_Technical|Universe API]]
- [[30_Resources/Game_Data/Resource_Production_Technical|Resource Production]]

## Changelog
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Technische Spezifikation des Planet-Objektmodells: Kernattribute (ID, Besitzer, Fertilität, Klasse), Ressourcen-Management (Storage, Deposits, Capacity, Production, Consumption), Koordinaten und Warteschlangen für Gebäude/Einheiten sowie das Clone Tanks System.
