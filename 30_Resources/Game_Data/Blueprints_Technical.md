---
category: [schiffe, blueprint]
type: technik
confidence: high
source_type: code_analysis
game_version: "unknown"
tags: [blueprint, module, ship_mechanics]
related: ["[[30_Resources/Game_Data/Blueprint_Strategy_UI_Technical|Strategie-Editor UI]]", "[[30_Resources/Game_Data/Unit_Capabilities_Technical|Einheiten-Fähigkeiten & Mathematik]]", "[[30_Resources/Game_Data/Faction_System_Technical|Fraktions-System]]", "[[30_Resources/Game_Data/Forces_API_Technical|Einheiten- & Missions-Management]]", "[[30_Resources/Game_Data/Blueprint_Editor_Frontend_Technical|Frontend-Editor-Logik]]"]
sources: ["constructionSpeed_analysis.md"]
created: 2024-05-23
updated: 2024-05-23
---

# Blueprint-System (Technische Spezifikation) & Kurzbeschreibung
Umfassende technische Dokumentation der Blueprint-Logik, des Modul-Systems und der Schiffbau-Mechaniken.

## Basisdaten

| Eigenschaft | Beschreibung |
| :--- | :--- |
| **Identität** | `id`, `ownerPlayerId`, `name` (inkl. `nameStyleState`) |
| **Physische Werte** | Geschwindigkeit, Reichweite, Panzerung, Schilde, Angriffskraft, Kapazitäten |
| **Modul-System** | Dynamische Liste von `BlueprintModuleEntry`-Objekten |
| **Forschungsstatus** | `researchState`, `upgradeInfo` (Verfügbarkeit/Status) |

## Mechanik / Verhalten

### 1. Datenmodell (`Blueprint` Klasse)
Ein Blueprint definiert die Identität, physischen Eigenschaften und die Organisation einer Einheit.
* **Physische Eigenschaften:** Bestimmen das Verhalten im Kampf und die Effizienz der Reise (z. B. `speedPcPerHour`, `armor`, `shieldCapacity`, `hullSizeTier`).
* **Forschung:** Überwacht den aktuellen Forschungsstand (`researchState`) und identifiziert Upgrade-Möglichkeiten.

### 2. Modul-System
Module sind die Bauteile, die in Blueprints eingesetzt werden.
* **Kern-Eigenschaften:** Identität (`id`, `code`), Kompatibilität (`unitTypeCompat`), Slot-Management (`slotsProvided` vs. `slotsUsed`) und statistische Werte (`baseStats`).
* **Einschränkungen (Constraints):** Regeln wie Einzigartigkeit (`uniquePerBlueprint`), Rumpf-Abhängigkeiten (`minHullSizeTier`, `maxHullSizeTier`) und Mengenlimits (`maxPerType`).
* **Kosten:** Normalisierte Ressourcenkosten für Metall, Kristall und Antimaterie.

### 3. Organisation & UI-Logik
* **Modul-Kategorisierung:** Interne Gruppierung zur Steuerung der Anzeige (`hull`, `defense`, `engine`, `power`, `weapons`, `tanks`, `special`).
* **Blueprint-Organisation:** Unterteilung in Favoriten, Unkategorisiert und benutzerdefinierte Kategorien.
* **Sortier-Logik:** Sortierung nach Name, Rumpfgröße, Geschwindigkeit, Kapazität oder Panzerung.

### 4. Bildverarbeitung (Image Processing)
Automatisierte Pipeline zur Optimierung von Blueprint-Bildern:
* **Format:** Konvertierung in **WebP**.
* **Parameter:** Größe ($64 \times 64$ bis $256 \times 256$ Pixel), Qualität ($0.9$).

### 5. Verwaltung & Editor (Management)
Das `BlueprintEditDialog`-Interface ermöglicht die Bearbeitung von Namen, Beschreibungen und Bildern.
* **Validierung:** Prüfung auf Slot-Überlastung (`usedSlots > totalSlots`) und ID-Integrität (`hasMissingModuleIds`).
* **Upgrade Tracking:** Markiert Module als `outdated`, wenn das aktuelle Level niedriger ist als das durch Forschung ermöglichte Level.

### 6. Schiffbau-Mechanik (Shipbuilding)
* **Größen-Skalierung:** Die maximale Größe eines Schiffes skaliert exponentiell basierend auf der Rumpfgröße und dem Ausbaulevel der Schiffswerft ($2^x$).
* **Bauzeit-Optimierung:** 
    * **Roboter-System:** Reduktion durch Roboter (exponentielle Skalierung).
    * **Schiffswerft-Forschung:** Ein System zur graduellen Optimierung. Jede Stufe erhöht die Produktionsgeschwindigkeit um ca. $0,249\%$ bezogen auf die Basis-Werft (Stufe 1).

## Verknüpfungen
- [[30_Resources/Game_Data/Blueprint_Strategy_UI_Technical|Strategie-Editor UI]]
- [[30_Resources/Game_Data/Unit_Capabilities_Technical|Einheiten-Fähigkeiten & Mathematik]]
- [[30_Resources/Game_Data/Faction_System_Technical|Fraktions-System]]
- [[30_Resources/Game_Data/Forces_API_Technical|Einheiten- & Missions-Management]]
- [[30_Resources/Game_Data/Blueprint_Editor_Frontend_Technical|Frontend-Editor-Logik]]

## Changelog
- 2024-05-23: Initialer Import.
- 2024-05-23: Erweiterung um Modul-System und Organisation.
- 2024-05-23: Update: State Management, Editor Validierung & Upgrade Tracking hinzugefügt.
- 2024-05-23: Upgrade auf neues Standard-Template und Bereinigung von Duplikaten.

## LLM_CONTEXT
Umfassende technische Spezifikation des Blueprint-Systems: Datenmodell (Identität, Physis), Modul-System (Eigenschaften, Constraints, Kosten), Organisation (Kategorien, Sortierung), Bildverarbeitung (WebP), Editor-Validierung (Slots, IDs) und Schiffbau-Mechanik (Größen-Skalierung $2^x$, Bauzeit-Optimierung).
