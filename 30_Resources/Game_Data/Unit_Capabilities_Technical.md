---
category: [schiffe, technik]
type: referenz
confidence: high
source_type: code_analysis
game_version: "unknown"
tags: [fleet_math, unit_capabilities, carrier_logic, speed, antimatter]
related: ["[[30_Resources/Game_Data/Blueprints_Technical|Blueprint System]]", "[[30_Resources/Game_Data/Combat_Strategy_Technical|Combat Strategy Technical]]"]
sources: ["code analysis"]
created: 2026-05-22
updated: 2024-05-23
---

# Unit Capabilities & Fleet Math (Technische Spezifikation) & Kurzbeschreibung
Mathematische Modelle zur Berechnung der Fähigkeiten von Einheiten und Flotten, einschließlich Trägerlogik, Geschwindigkeit, Reichweite und Ressourcenverbrauch.

## Basisdaten

| Bereich | Kernkonzept | Mathematischer Fokus |
| :--- | :--- | :--- |
| **Trägerschiffe** | Flugdeck-Kapazität | Bucket-basierte Sortierung nach Rumpfgröße |
| **Bewegung** | Effektive Geschwindigkeit | Lineare Skalierung mit Speed-Multiplikator (max. 150%) |
| **Reichweite** | Proportionale Reichweite | Anpassung an die aktuelle Missionsgeschwindigkeit |
| **Ressourcen** | Antimaterie-Verbrauch | Quadratische Skalierung zur Geschwindigkeit |

## Mechanik / Verhalten

### 1. Carrier & Flight Deck Logik (Trägerschiffe)
Das System berechnet die Kapazität eines Trägers basierend auf dem verfügbaren Platz auf dem Flugdeck (`computeFlightDeckUsage`).
* **Transport Profile:** Definieren `Capacity` und `Max Hull Size Tier`.
* **Berechnungsprozess:** 
    1. Erstellung von "Buckets" für verschiedene Transportkapazitäten.
    2. Sortierung der Buckets nach `maxHullSizeTier`, um die effizienteste Nutzung zu gewährleisten.
    3. Befüllen der Buckets; Einheiten, deren `hullSizeTier` den Bucket überschreitet, werden übersprungen.
* **Metriken:** Liefert `maxCapacity`, `loadedCapacity`, `overCapacity` und `usagePercent`.

### 2. Bewegung & Ressourcen (Speed, Range, Antimatter)
Die Flottenbewegung ist dynamisch und wird durch die langsamste Einheit bestimmt (`minSpeed`).

* **Effektive Geschwindigkeit (`computeSpeed`):**
  $EffectiveSpeed = minSpeed \times (\frac{SpeedPercent + OverdriveExtra}{100})$
  *(Limit: maximal 150%)*

* **Effektive Reichweite (`computeRange`):**
  Um sicherzustellen, dass eine schnellere Flotte nicht über das Ziel hinausschießt, wird die Reichweite proportional zur Geschwindigkeit skaliert:
  $AdjustedRange = BaseRange \times (\frac{UnitSpeed}{MissionSpeed})$

* **Antimaterie-Verbrauch (`computeAntimatter`):**
  Der Verbrauch steigt **quadratisch** mit der Geschwindigkeit an, was ein entscheidender Balancing-Faktor ist:
  $TotalConsumption = \sum (BaseConsumption \times (\frac{EffectiveSpeed}{BaseSpeed})^2 \times Count)$

### 3. Fähigkeits-Analyse (`computeCapabilities`)
Das System scannt Einheiten und Module auf spezifische Fähigkeiten mittels Pattern-Matching:
* **Colonizer:** Erkennt `COLONIZE_MODULE_PATTERNS`.
* **Geo-Probe:** Erkennt `GEO_MODULE_PATTERNS`.
* **Recon:** Erkennt `RECON_ABILITY_PATTERNS`.
* **Recycle:** Erkennt die explizite Fähigkeit `RECYCLE`.
* **Sensor-Anzahl:** Zählt Module gemäß `SENSOR_MODULE_PATTERNS`.
* **Mission Blocked:** Prüft auf Fähigkeiten, die Missionen blockieren (`MISSION_BLOCKED_ABILITY_PATTERNS`).

### 4. Jumpgate-Anforderungen
Der Zugang zu Jumpgates ist an die Rumpfgröße der größten Einheit in der Flotte gekoppelt. Die benötigte `shipyardLevel` wird aus dem `maxHullSizeTier` abgeleitet. Ein niedrigeres Level blockiert die Bewegung.

## Verknüpfungen
- [[30_Resources/Game_Data/Blueprints_Technical|Blueprint System]]
- [[30_Resources/Game_Data/Combat_Strategy_Technical|Combat Strategy Technical]]

## Changelog
- 2026-05-22: Erstmals erstellt basierend auf Code-Analyse.
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Mathematische Modelle für Flottenberechnungen: Trägerkapazität (Bucket-System), effektive Geschwindigkeit (linear, max 150%), Reichweite (proportional) und quadratischer Antimaterie-Verbrauch. Fähigkeiten-Erkennung via Pattern-Matching und Jumpgate-Zugangsbeschränkung basierend auf Rumpfgröße.
