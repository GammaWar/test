---
category: [schiffe]
type: [kampf, technik]
confidence: high
source_type: discord
game_version: "unknown"
tags: [geschwindigkeit, masse, groesse]
related: ["[[20_Areas/Gameplay_Mechaniken|Gameplay & Mechaniken]]"]
sources: ["discord"]
created: 2026-05-22
updated: 2024-05-23
---

# Schiffsgeschwindigkeit und Größe (Technische Spezifikation) & Kurzbeschreibung
Dokumentation des Zusammenhangs zwischen Schiffgröße, Agilität, Masse und der resultierenden Bewegungsgeschwindigkeit.

## Basisdaten

| Faktor | Auswirkung auf Geschwindigkeit |
| :--- | :--- |
| **Schiffgröße** | Verringert den Speedbonus |
| **Agilität** | Beeinflusst die Gesamtbewegung |
| **Masse** | Beeinflusst die Geschwindigkeit (siehe EE-Formeln) |

## Mechanik / Verhalten

Die Bewegungsgeschwindigkeit eines Schiffes ist ein Zusammenspiel aus der **Größe/Agilität** des Schiffes und einem **Speedbonus**. 

Ein entscheidender Faktor ist, dass der **Speedbonus mit steigender Schiffsgröße sinkt**. Zudem gibt es Geschwindigkeitseinbußen bei höheren Schiffsmassen. Die genauen mathematischen Auswirkungen sind in den externen EE-Skripten definiert.

## Strategie
(Keine spezifischen Strategien dokumentiert)

## Verknüpfungen
- [[20_Areas/Gameplay_Mechaniken|Gameplay & Mechaniken]]

## Tests & Hypothesen
* **Hypothese:** Die genauen Produktionsformeln und die exakten mathematischen Auswirkungen der Masse auf die Geschwindigkeit sind nicht in der Ingame-Hilfe dokumentiert.
* **Hinweis:** Diese Formeln befinden sich in der JavaScript-Datei von EE (externes Tool/System).

## Changelog
- 2026-05-22: Erstmals erstellt basierend auf Discord-Chatverlauf.
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Zusammenhang zwischen Schiffgröße, Agilität und Speedbonus: Der Speedbonus sinkt mit zunehmender Schiffsgröße. Masse beeinflusst die Geschwindigkeit ebenfalls (Formeln in EE JS-Datei).
