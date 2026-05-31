---
category: [ressource, technik]
type: referenz
confidence: high
source_type: code_analysis
game_version: "unknown"
tags: [resource_production, economy, clone_tanks, construction_loop]
related: ["[[30_Resources/Game_Data/Economy_Formulas_Technical|Economy Formulas]]", "[[30_Resources/Game_Data/Planet_Model_Technical|Planet Model Technical]]"]
sources: ["resourceProduction.js"]
created: 2024-05-23
updated: 2024-05-23
---

# Ressourcen-Produktion & Gebäude-Logik (Technische Spezifikation) & Kurzbeschreibung
Beschreibung der Berechnung von Produktionsraten, dem Einfluss von Clone Tanks sowie der Logik für die Bauzeitplanung.

**WICHTIGER HINWEIS zur Datenintegrität:** Bei allen Berechnungen und Dokumentationen von Gebäudedaten muss zwingend der aktuelle Stand der vorhandenen **Forschung** sowie der Betrieb von **Roboterwerkstätten** mit einbezogen werden!

## Basisdaten

| Bereich | Kernkonzept | Implementierung / Logik |
| :--- | :--- | :--- |
| **Produktionsrate** | Netto-Rate Berechnung | $\sum \text{Production} - \sum \text{Consumption}$ |
| **Offline-Produktion** | Zeitstempel-basiert | Differenz zwischen Login und letztem Speichern |
| **Bauwesen** | Construction Loop | Additiver Ansatz für kumulierte Bauzeiten |

## Mechanik / Verhalten

### 1. Ableitung der Produktionsraten (`resourceProduction.js`)
Die Netto-Produktionsrate eines Planeten ergibt sich aus der Summe aller Gebäude-Effekte:
* **Identifikation:** Ermittlung der Gebäudetypen via `buildingId`.
* **Extraktion:** Abruf der Basisproduktion (`produces`).
* **Verbrauch:** Abzug der Unterhaltskosten (`usage`) als negative Werte.
* **Spezialfall Clone Tanks:** 
    * **Fertility Mode:** Erhöht die Basis-Fertilität und die effektive Fertilität des Planeten pro Level.
    * **Soldier Mode:** Erhöht die Produktion von Soldaten (`SOLDIER_RESOURCE_ID`).

### 2. Mathematische Details & Immutability
* **Ressourcen-Identifikation:** Unterstützung von numerischen IDs, String-Keys und Mapping-Keys (`RES_KEY`).
* **Immutability:** Um "Exponential Growth"-Fehler im Store zu vermeiden, nutzt das System ein Cloning-Verfahren (`Object.create(Planet.prototype)`), anstatt direkt auf Referenzen des Original-Objekts zu schreiben.

### 3. Offline-Produktion
Die Ressourcenproduktion erfolgt nicht über kontinuierliche Ticks, sondern über eine Zeitstempel-Berechnung beim Login: Die Differenz zwischen dem aktuellen Zeitstempel und dem letzten gespeicherten Zeitstempel wird zur Berechnung der produzierten Menge genutzt.

### 4. Bauwesen & Bauschleifen (Construction Loop)
Beschreibt die Logik der Gebäudeplanung und die Anzeige der verbleibenden Zeit:
* **Additiver Ansatz:** Die Bauzeiten aller geplanten Gebäude werden aufsummiert. Wenn Gebäude A 2h benötigt und Gebäude B 3h, zeigt das System für Gebäude B eine Gesamtdauer von 5h an. Dies ermöglicht die Planung der finalen Fertigstellung des gesamten Plans.
* **Einschränkung:** Aktuell ist pro Planet nur eine einzige aktive Bauschleife möglich.

## Verknüpfungen
- [[30_Resources/Game_Data/Economy_Formulas_Technical|Economy Formulas]]
- [[30_Resources/Game_Data/Resource_Production_Technical|Resource Production (Technik)]]
- [[30_Resources/Game_Data/resourceRates.js|resourceRates.js]]
- [[30_Resources/Game_Data/resourceProjection.js|resourceProjection.js]]

## Changelog
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Technische Spezifikation der Ressourcenproduktion: Netto-Rate Berechnung ($\sum \text{Prod} - \sum \text{Cons}$), Einfluss von Clone Tanks (Fertility/Soldier Mode), Immutability durch Cloning, Offline-Produktion via Zeitstempel und die additive Bauschleifen-Logik für Bauzeiten.
