---
category: wirtschaft, technik
type: bug
confidence: high
source_type: discord
game_version: "unknown"
tags: [klontank, produktion, zivilisten]
related: []
sources: ["discord"]
created: 2026-05-22
updated: 2026-05-22
---

# Bugreport: Fehler in der Klontank-Produktionslogik

## Basisdaten

| Parameter | Details |
| --- | --- |
| Betroffener Planet | Colony (Koordinaten: 03-07-07) |
| Symptom | Wohnraum wurde sofort nach Erweiterung als voll gemeldet |
| Erwartetes Verhalten | Bei einer Produktion von 13.000 Zivilisten/Std. sollte das Lager erst nach ca. 11 Tagen gefüllt sein |

## Mechanik / Verhalten

Nach der Deaktivierung des Klontanks, dem Ausbau des Wohnraums und der anschließenden Reaktivierung auf "Zivilisten", war der neue Wohnraum sofort vollständig belegt. Die berechnete Produktionsrate korreliert nicht mit der Füllgeschwindigkeit des Lagers/Wohnraums.

## Verknüpfungen

- [[20_Areas/Gameplay_Mechaniken|Gameplay & Mechaniken]]

## Tests & Hypothesen

- Möglicher Fehler in der Berechnung der Kapazität vs. aktueller Bestand bei Statuswechseln (Deaktiviert -> Zivilisten).
- Die Produktionsrate wird zwar korrekt angezeigt, aber die Logik zur Füllung des Wohnraums scheint den aktuellen Stand nicht korrekt zu berücksichtigen oder einen Sprung zu machen.

## Changelog

- 2026-05-22: Erstmals erstellt basierend auf Discord-Chatverlauf (User `xearox`).

## LLM_CONTEXT

Produktionsfehler Klontank: Wohnraum wird nach Erweiterung und Umstellung auf Zivilisten sofort als voll gemeldet, obwohl die Produktionsrate (13k/h) eine viel längere Füllzeit impliziert. Planet Colony (03-07-07).