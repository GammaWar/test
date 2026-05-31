---
category: [gameplay]
type: referenz
confidence: high
source_type: manual
game_version: "1.0.0"
tags: [gameplay, mechanics]
related: ["[[30_Resources/Game_Data/Blueprints_Technical|Blueprint System]]", "[[30_Resources/Game_Data/Resource_Production_Technical|Resource Production]]", "[[30_Resources/Game_Data/Planet_Model_Technical|Planet Model Technical]]", "[[30_Resources/Game_Data/Universe_API_Technical|Universe API Technical]]"]
sources: ["manual"]
created: 2024-05-23
updated: 2024-05-23
---

# Gameplay & Mechaniken (Übersicht) & Kurzbeschreibung
Zentrale Übersicht über die grundlegenden Spielmechaniken von Spacewar, einschließlich des Tick-Systems, der modularen Schiffskonstruktion und der wirtschaftlichen Skalierung durch HQ-Forschung.

## Basisdaten

| System | Beschreibung |
| :--- | :--- |
| **Tick-System** | Zeitbasierte Aktualisierung (empfohlen: 1s) |
| **Schiffsbau** | Modulares System aus Rümpfen und Modulen |
| **Wirtschaft** | Skalierung über HQ-Forschung & Planeten-Slots |

## Mechanik / Verhalten

### Ticks und Aktualisierung
Das Spiel basiert auf einem Tick-System. Das Aktualisierungsintervall kann in den Einstellungen angepasst werden (bis zu 0,1s; empfohlen: 1s). Dies beeinflusst die Frequenz, mit der Ressourcen berechnet und Zustände aktualisiert werden.

### Schiffbau und Konstruktion
Es gibt keine festen Schiffsklassen. Stattdessen werden Rümpfe verwendet, in die Module eingesetzt werden können. Dies ermöglicht eine nahezu unbegrenzte Vielfalt an Konstruktionen. Die maximale Größe eines Schiffes wird durch die Forschung und spezifische Rumpfgrößenbeschränkungen limitiert.
- **Technische Details:** [[30_Resources/Game_Data/Blueprints_Technical|Blueprint & Modul Spezifikationen]]

### Gebäudedaten und Abhängigkeiten
Bei der Berechnung von Gebäudedaten muss zwingend der aktuelle Stand der Forschung sowie der Betrieb von Roboterwerkstätten berücksichtigt werden, da die Rohdaten oft so vorliegen, als wären diese Faktoren nicht vorhanden.
- **Technische Details:** [[30_Resources/Game_Data/Resource_Production_Technical|Ressourcen-Produktion & Gebäude]]

### Hauptquartierforschung (HQ Research)
Die Forschung des Hauptquartiers ist von zentraler Bedeutung für die wirtschaftliche Skalierung. Ein wesentlicher Vorteil ist das Freischalten zusätzlicher Planeten-Slots, die durch Kolonisierung oder Invasion besetzt werden können.

## Strategie
(Keine spezifischen Strategien in dieser Übersicht dokumentiert)

## Verknüpfungen

### Schiffe & Bauwesen
- [[20_Areas/Gameplay_Mechaniken/Schiffsgeschwindigkeit_und_Groesse|Schiffsgeschwindigkeit & Größe]]

### Universum
- **Planetenklassen (A bis F):** [[30_Resources/Game_Data/Planet_Model_Technical|Technische Planetendaten]]
- **Sektoren & Aufklärung:** [[30_Resources/Game_Data/Universe_API_Technical|Universums-API]]

## Tests & Hypothesen
(Keine aktuellen Hypothesen dokumentiert)

## Changelog
- 2024-05-23: Upgrade auf neues Standard-Template und Entfernung von Emojis.
- 2024-05-23: Bereinigung der Struktur.

## LLM_CONTEXT
Zentrale Übersicht der Gameplay-Mechaniken. Beinhaltet das Tick-System, das modulare Schiffsbau-System (Rümpfe/Module), die Bedeutung der HQ-Forschung für die wirtschaftliche Skalierung sowie technische Referenzen zu Planeten und Universums-API.
