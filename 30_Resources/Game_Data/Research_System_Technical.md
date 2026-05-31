---
category: [technik, progression]
type: referenz
confidence: high
source_type: code
game_version: "unknown"
tags: [research, scaling, economy, api]
related: ["[[30_Resources/Game_Data/Research_&_Unlocks_Technical|Research & Unlocks]]"]
sources: ["researchCost.js", "researchEffects.js", "researchStatusApi.js"]
created: 2024-05-23
updated: 2024-05-23
---

# Research System (Technische Spezifikation) & Kurzbeschreibung
Dokumentation der mathematischen Modelle für Forschungskosten, die Berechnung von Forschungsboni und die API zur Abfrage des Forschungsstatus.

## Basisdaten

| Bereich | Kernkonzept | Implementierung / Detail |
| :--- | :--- | :--- |
| **Kosten-Modelle** | Exponentielle Skalierung | `SERVER` (Summe vorheriger Level) oder `SCALED` (Faktor-basiert) |
| **Effekte** | Bonus-Berechnung | Kombination aus Flat- und Per-Level-Boni |
| **API-Optimierung** | Performance & Datenmenge | Caching (5s) und kompaktes WebSocket-Format |

## Mechanik / Verhalten

### 1. Forschungskosten & Skalierung (`researchCost.js`)

Die Kosten für das Erreichen eines neuen Forschungslevels werden durch verschiedene Formeln bestimmt.

#### A. Kosten-Modelle
Es gibt zwei primäre Wege, wie Kosten berechnet werden:
* **Server-Formel (`SERVER`):** Wird verwendet, wenn die `formulaSource` auf "SERVER" gesetzt ist. Sie nutzt eine exponentielle Steigerung basierend auf dem Level. Die Kosten für ein Level sind die Summe aller vorherigen Level-Kosten. Multiplikator: $\text{Multiplier} = \lfloor \text{Level} \times 1.5^{\text{Level}} \rfloor$.
* **Skalierungs-Faktor (`SCALED`):** Verwendet einen festen Faktor und ein Basis-Level für die Skalierung. Formel: $\textFlatValue \times (\text{Factor}^{\max(0, \text{Level} - \text{BaseLevel})})$.

#### B. Forschungsdauer (Duration)
Die Dauer einer Forschung skaliert ebenfalls entweder über die Server-Formel (exponentiell) oder über einen Skalierungs-Faktor (exponentiell basierend auf dem Level).

### 2. Forschungs-Effekte & Boni (`researchEffects.js`)

Die Forschung bietet Vorteile in verschiedenen Bereichen des Spiels.

#### A. Unterstützte Bereiche (Scopes)
Die Forschung kann Auswirkungen auf folgende Bereiche haben:
* `production`: Erhöhung der Ressourcenproduktion.
* `storage`: Erhöhung der Lagerkapazität.
* `upkeep`: Reduzierung des Ressourcenverbrauchs/Unterhalts.

#### B. Berechnung der Boni
Ein Effekt kann zwei Arten von Werten haben, die kombiniert werden:
$$\text{Delta} = \text{Flat} + (\text{PerLevel} \times \text{CurrentLevel})$$

### 3. API & Status (`researchStatusApi.js`)

Der Forschungsfortschritt wird über den `LiveGameService` abgerufen.
* **Caching:** Um die Performance zu optimieren, nutzt der Abruf einen Cache (Standard: 5 Sekunden).
* **Komprimierung:** Die Anfrage verwendet ein "compact" Format, um die Datenmenge im WebSocket-Payload zu minimieren.

#### A. Kosten-Skalierung (`ResearchCostScaling`)
Für fortgeschrittene Skalierungen wird die Klasse `ResearchCostScaling` verwendet, die Parameter wie `type`, `factor`, `baseLevel` sowie mathematische Konstanten (`a`, `b`, `k`) unterstützt.

## Verknüpfungen
- [[30_Resources/Game_Data/Research_&_Unlocks_Technical|Research & Unlocks Technical]]

## Changelog
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Technische Spezifikation des Research Systems: Kostenmodelle (SERVER vs. SCALED), exponentielle Skalierung von Kosten und Dauer, Bonusberechnung ($\text{Flat} + \text{PerLevel} \times \text{Level}$) sowie API-Optimierungen (Caching & Kompression).
