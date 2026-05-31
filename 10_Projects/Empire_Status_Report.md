---
category: [empire]
type: status
confidence: high
source_type: ingame
game_version: "unknown"
tags: [empire, economy, resource_report, status]
related: []
sources: ["ingame_json_export"]
created: 2024-05-23
updated: 2024-05-23
---

# Empire Status Report (Statusbericht) & Kurzbeschreibung
Aktueller Bericht über die globale Ressourcenproduktion, technische Kapazitäten und aktive Boni des Imperiums.

## Basisdaten

### Gesamtrohstoff-Produktion & Bestände

| Ressource | Produktion /h | Lagerbestand | Delta (Wachstum) |
| :--- | :--- | :--- | :--- |
| **Metall** | 190,613,697 | 7,203,995,881 | +51,735.91 |
| **Kristall** | 253,671,906 | 8,841,151,056 | +64,392.53 |
| **Antimaterie** | 18,586,929 | 245,488,071 | +4,895.85 |

### Bevölkerung & Militär

| Einheit | Produktion /h | Lagerbestand | Delta (Wachstum) |
| :--- | :--- | :--- | :--- |
| **Zivilisten** | 0.00 | 16,708,574,469,953.45 | +2,686,954.85 |
| **Soldaten** | 17,355,430.50 | 27,254,139,714.69 | +4,788.52 |

### Fortschritt & Kapazitäten

| Metrik | Wert |
| :--- | :--- |
| **Planeten** | 25 / 25 |
| **Gesamtpunkte** | 941,986,383 |
| **Rang** | 4 |
| **Forschungspunkte /h** | 7,749,400 |
| **Restlaufzeit Forschung** | ~2d 20h |

## Mechanik / Verhalten

### Ressourcen-Dynamik
* **Bevölkerungs-Motor:** Das massive Wachstum der Zivilisten (+2,6M/h) fungiert als primärer Treiber für die gesamte wirtschaftliche Expansion.
* **Produktions-Skalierung:** Die Produktion von Metall und Kristall korreliert stark mit dem Bevölkerungswachstum. Besonders auffällig ist das hohe Delta bei Kristall (+64k/h), was auf eine sehr effiziente Infrastruktur oder spezifische Forschungsboni hindeutet.
* **Antimaterie-Verhältnis:** Im Vergleich zu Metall und Kristall ist das Wachstum der Antimaterie (+4,8k/h) deutlich langsamer. Das Lager von Antimaterie (245M) ist im Verhältnis zu den anderen Ressourcen signifikant niedriger als zuvor.

### Wichtige Korrektur zur Einheitenverteilung
* **Einheiten-Standort:** Entgegen der Rohdaten-Interpretation befinden sich alle gelisteten militärischen Einheiten auf dem Planeten 001. Die restlichen Planeten dienen primär der Ressourcenproduktion und Infrastruktur.

## Technische Limits & Boni

### Konstruktions-Limits (Maximalwerte)

| Komponente | Maximaler Wert |
| :--- | :--- |
| **Rumpfgröße (Hull)** | 2,097,152 |
| **Chassigröße (Chassis)** | 1,048,576 |

### Aktive Produktions-Boni

| Ressource | Bonus |
| :--- | :--- |
| **Metall** | +15% |
| **Kristall** | +15% |
| **Antimaterie** | +15% |

## Strategie
* **Wirtschaftlicher Fokus:** Die aktuelle Wachstumsrate der Zivilisten ermöglicht eine aggressive Expansion der Produktionskapazitäten.
* **Engpass-Management:** Das Antimaterie-Lager ist im Vergleich zu Metall/Kristall relativ klein (245M vs 7B+). Es sollte geprüft werden, ob die Antimaterie-Produktion durch gezielte Forschung (z. B. `research.economy.industrial_automation`) oder zusätzliche Fabriken angehoben werden muss.
* **Militärische Bereitschaft:** Das Soldaten-Delta ist im Verhältnis zur Bevölkerung stabil, aber moderat. Eine verstärkte Produktion von Einheiten könnte notwendig sein, falls die Expansion in feindliche Gebiete geplant ist.

## Verknüpfungen
(Keine spezifischen technischen Dokumente verknüpft)

## Tests & Hypothesen
* **Hypothese:** Das Bevölkerungswachstum wird in der nächsten Phase leicht abflachen, sobald die Planetenkapazitäten (Housing/Wohngebäude) an ihre Grenzen stoßen.

## Changelog
- 2024-05-23: Erster Statusbericht basierend auf Rohdaten der Imperium-Übersicht erstellt.
- 2024-05-23: Erweiterung um technische Limits (Hull/Chassis), Forschungsrate und aktive Ressourcen-Boni.
- 2024-05-23: Korrektur der Einheitenverteilung (Alle Einheiten auf Planet 001).
- 2026-05-30: Update basierend auf neuem JSON-Export. Fokus auf Antimaterie-Lagerbestand und aktualisierte Produktionswerte.
- 2024-05-23: Upgrade auf neues Standard-Template und Entfernung von Emojis.

## LLM_CONTEXT
Imperiums-Statusbericht. Fokus auf Ressourcenproduktion (Metall, Kristall, Antimaterie) und Bevölkerungswachstum. Zivilisten wachsen massiv (+2,6M/h). Technische Limits: Rumpf 2,09M, Chassis 1,04M. Aktive Boni: +15% auf alle Primärressourcen. WICHTIG: Alle Einheiten befinden sich auf Planet 001. Antimaterie-Lager ist im Vergleich zu Metall/Kristall kritisch niedrig (245M).
