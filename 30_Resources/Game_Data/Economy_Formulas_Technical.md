---
category: [wirtschaft, technik]
type: referenz
confidence: high
source_type: code
game_version: "unknown"
tags: [economy_formulas, math, scaling, growth]
related: ["[[30_Resources/Game_Data/Resource_Production_Technical|Resource Production]]", "[[30_Resources/Game_Data/Planet_Model_Technical|Planet Model Technical]]"]
sources: ["economy.formulas.js"]
created: 2024-05-23
updated: 2024-05-23
---

# Economy Formulas (Technische Spezifikation) & Kurzbeschreibung
Dokumentation der mathematischen Formeln für die Simulation der Wirtschaft, des Wachstums und der Bauprozesse im Spacewar-System.

## Basisdaten

| Bereich | Fokus | Skalierungsmuster |
| :--- | :--- | :--- |
| **Gebäude** | Kosten, Zeit, Kapazität | Exponentiell ($1.5^{\text{Level}}$) |
| **Produktion** | Netto-Rate | Kumulativ über Level hinweg |
| **Bevölkerung** | Zivilisten-Wachstum | Exponentielles Wachstum basierend auf Fertilität |

## Mechanik / Verhalten

### 1. Gebäude-Ökonomie

Die Kosten und Zeiten für Gebäude skalieren exponentiell mit dem Level.

#### A. Baukosten (`computeNextCostByLevel`)
Die Kosten für das nächste Level eines Gebäudes berechnen sich wie folgt:
$$\text{Cost} = \lfloor \text{BaseCost} \times \lfloor (\text{Level} + 1) \times 1.5^{\text{Level}} \rfloor \rfloor$$

#### B. Bauzeit (`computeNextConstructionTimeSeconds`)
Die Zeit bis zur Fertigstellung folgt demselben Skalierungsmuster wie die Kosten:
$$\text{Time} = \lfloor \text{BaseBuildTime} \times \lfloor (\text{Level} + 1) \times 1.5^{\text{Level}} \rfloor \rfloor$$

#### C. Lagerkapazität (`computeStorageCapacity`)
Die kumulative Lagerkapazität eines Gebäudes steigt mit jedem Level:
$$\text{TotalCapacity} = \sum_{i=1}^{\text{Level}} \lfloor \text{BaseStorage} \times (i \times 1.5^i) \rfloor$$

### 2. Produktions- & Verbrauchsdynamik

#### A. Gebäude-Produktion (`computeProductionPerHour`)
Die Produktion ist kumulativ über alle Level des Gebäudes hinweg berechnet:
$$\text{TotalProduction} = \sum_{i=1}^{\text{Level}} \lfloor \text{BaseAmount} \times \text{Bonus} \times (i \times 1.1^i) \rfloor$$
* **Multiplikatoren:** Die Produktion wird durch Server-Geschwindigkeit, Ressourcen-Vorkommen (`deposits`) und spezifische Ressourcen-Boni beeinflusst.

#### B. Gebäude-Verbrauch (`computeUsagePerHour`)
Der Verbrauch pro Stunde skaliert mit dem Level:
$$\text{Consumption} = \lfloor \text{BaseUsage} \times (\text{Level} \times 1.5^{\text{Level}-1}) \rfloor$$

### 3. Bevölkerungswachstum (Civilians)

Das Wachstum der Zivilisten folgt einer exponentiellen Wachstumsformel basierend auf der Fertilität und der aktuellen Manpower.

#### A. Wachstumsformel (`computeCiviliansSpecial`)
Die Berechnung des Wachstums über eine vergangene Zeitspanne ($t$ in Sekunden) lautet:
$$\text{Total} = \text{Manpower} \times (1 + \frac{\text{Fertility}}{3600})^t$$
* **Delta:** Die Differenz zwischen dem neuen Total und der ursprünglichen Manpower ($\text{Total} - \text{Manpower}$).
* **Limitierung:** Das Wachstum wird durch die Kapazität des Planeten (`civCap`) begrenzt.

## Verknüpfungen
- [[30_Resources/Game_Data/Resource_Production_Technical|Resource Production Technical]]
- [[20_Areas/Gameplay_Mechaniken/Baugeschwindigkeit_und_Optimierung.md|Baugeschwindigkeit & Optimierung]]

## Changelog
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Mathematische Formeln für die Wirtschaftssimulation: Exponentielle Skalierung von Baukosten, Bauzeit und Lagerkapazität ($1.5^{\text{Level}}$). Kumulative Produktionsberechnung und exponentielles Bevölkerungswachstum basierend auf Fertilität.
