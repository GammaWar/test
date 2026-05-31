---
category: [technik, spielmechanik]
type: analyse
confidence: medium
source_type: code_analysis
game_version: "unknown"
tags: [bauzeit, produktion, optimierung, constructionSpeed]
related: ["[[20_Areas/Gameplay_Mechaniken/Resource_Production_Technical|Ressourcen-Produktion]]", "[[30_Resources/Game_Data/Economy_Formulas_Technical|Economy Formulas]]"]
sources: ["constructionSpeed_analysis.md"]
created: 2026-05-22
updated: 2024-05-23
---

# Analyse: constructionSpeed.js & Kurzbeschreibung
Technische Analyse der Datei `constructionSpeed.js`, welche die Dynamik der Bauzeiten im Spiel steuert.

## Basisdaten

| Parameter | Beschreibung |
| :--- | :--- |
| **Primärfunktion** | Berechnung der Baugeschwindigkeit / Bauzeitreduktion |
| **Eingabevariablen** | Gebäudestufe, Planetentyp, Forschungsboni, Allianzboni, Speedmultiplikatoren |
| **Ausgabewerte** | Finale Bauzeit, Prozentboni, dynamische Restzeit |

## Mechanik / Verhalten

Die Datei `constructionSpeed.js` ist die zentrale Komponente für die zeitliche Planung von Infrastrukturprojekten. Sie berechnet die finale Bauzeit basierend auf einer Kombination aus statischen und dynamischen Faktoren:

### Wahrscheinliche Eingabeparameter
* **Gebäudestufe:** Skalierung der Basisbauzeit.
* **Planetentyp:** Spezifische Modifikatoren je nach Planetengattung.
* **Forschungsboni:** Aktive Effekte aus dem Forschungssystem.
* **Allianzboni:** Unterstützung durch Allianz-Infrastruktur oder -Technologien.
* **Speedmultiplikatoren:** Globale oder spezifische Geschwindigkeitsfaktoren.

### Wahrscheinliche Ausgaben
Das Skript liefert Werte für:
* **Finale Bauzeit:** Die tatsächliche verbleibende Zeit in Sekunden/Minuten.
* **Prozentboni:** Die prozentuale Reduktion der Basisbauzeit.
* **Restzeit:** Dynamische Aktualisierung des Timers.

## Strategie

Die Analyse dieser Datei ist für folgende Bereiche von sehr hoher Relevanz:
1.  **Bauzeitrechner:** Entwicklung von Tools zur präzisen Planung.
2.  **Ausbauoptimierung:** Berechnung der effizientesten Reihenfolge von Bauprojekten.
3.  **ROI-Berechnung (Return on Investment):** Bestimmung, wann sich ein Gebäude durch seine Produktion gegenüber den Baukosten amortisiert.
4.  **Earlygame-Optimierung:** Minimierung der Wartezeiten in der kritischen Startphase des Spiels.

## Verknüpfungen
- [[20_Areas/Gameplay_Mechaniken|Gameplay & Mechaniken]]
- [[30_Resources/Game_Data/Economy_Formulas_Technical|Economy Formulas (Zusammenhang zwischen Kosten und Zeit)]]

## Tests & Hypothesen
(Keine aktuellen Hypothesen dokumentiert)

## Changelog
- 2026-05-22: Erstmals erstellt basierend auf Code-Analyse.
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Technische Analyse von `constructionSpeed.js`: Berechnet Bauzeitreduktion basierend auf Stufe, Planetentyp, Forschung und Allianzboni. Wichtig für ROI-Berechnungen und Earlygame-Optimierung.
