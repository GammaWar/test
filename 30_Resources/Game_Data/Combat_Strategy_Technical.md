---
category: [schiffe, technik]
type: referenz
confidence: high
source_type: code_analysis
game_version: "unknown"
tags: [combat, strategy, targeting, weapon_groups]
related: []
sources: ["blueprintStrategy.js"]
created: 2024-05-23
updated: 2024-05-23
---

# Combat Strategy (Technische Spezifikation) & Kurzbeschreibung
Beschreibung der technischen Implementierung von Kampfstrategien für Blueprints und Spieler, einschließlich Zielauswahl (Targeting) und Feuerbefehlen (Fire Order).

## Basisdaten

| Strategie-Typ | Fokus | Kern-Mechanik |
| :--- | :--- | :--- |
| **Blueprint Strategy** | Einheitenverhalten | `startCycle`, `defaultTargeting`, `weaponGroups` |
| **Player Strategy** | Globale Priorisierung | `fireOrder` (RuleSet) |

## Mechanik / Verhalten

### 1. Blueprint Combat Strategy
Jeder Bauplan kann eine spezifische Kampfstrategie besitzen, um sein Verhalten im Gefecht zu steuern.

#### A. Datenstruktur (`combatStrategy`)
* **startCycle:** Der Zyklus (Runde), in dem die Einheit mit dem Feuer beginnt (Bereich: 1 bis 10).
* **defaultTargeting:** Die Standard-Zielauswahl (`RuleSet`), falls keine spezifische Gruppen-Strategie greift.
* **weaponGroups:** Eine Liste von spezialisierten Waffen-Gruppen mit eigenen Regeln.

#### B. Weapon Groups (`weaponGroups`)
Waffen können in Gruppen organisiert werden, um unterschiedliche Zielprioritäten für verschiedene Modultypen zu setzen.
* **Eigenschaften:** `groupId`, `displayName`, `weaponModuleIds` (Liste der Modul-IDs), `targeting` (spezifische `RuleSet`).

#### C. Constraints & Validierung
* **Start Cycle:** Muss zwischen 1 und 10 liegen.
* **Criteria Limit:** Eine Regel (Targeting oder Fire Order) darf maximal **3 Kriterien** enthalten.
* **Group ID:** Die `groupId` muss gültig sein und darf nicht `DEFAULT` sein.
* **Modul-Integrität:** Innerhalb einer Gruppe dürfen keine Modul-IDs doppelt vorkommen; alle Module müssen im Blueprint vorhanden sein.

### 2. Player Combat Strategy
Spieler können eine globale Strategie festlegen, die das allgemeine Feuerverhalten ihrer Einheiten beeinflusst.
* **fireOrder:** Eine Priorisierung der Feuerbefehle (z. B. "Zuerst die stärksten Angriffe").

### 3. Regel-System (`RuleSet`)
Ein `RuleSet` besteht aus einer Liste von Kriterien, die in ihrer Reihenfolge eine Priorität darstellen (Index 0 = höchste Priorität). Es können maximal 3 Kriterien definiert werden.

#### Verfügbare Kriterien (Sortier-IDs)
| ID | Beschreibung |
| :--- | :--- |
| `LOWEST_ATTACK` / `HIGHEST_ATTACK` | Angriffskraft (niedrig/hoch) |
| `LOWEST_ARMOR` / `HIGHEST_ARMOR` | Panzerung (niedrig/hoch) |
| `LOWEST_SHIELD` / `HIGHEST_SHIELD` | Schilde (niedrig/hoch) |
| `LOWEST_HIT_POINTS` / `HIGHEST_HIT_POINTS` | Trefferpunkte (niedrig/hoch) |
| `SMALLEST_UNITS` / `LARGEST_UNITS` | Einheitsgröße (klein/groß) |
| `LOWEST_COUNT` / `HIGHEST_COUNT` | Anzahl der Einheiten (niedrig/hoch) |
| `FEWEST_WEAPONS` / `MOST_WEAPONS` | Anzahl der Waffen (wenig/viel) |
| `SPACE_UNITS` / `GROUND_UNITS` | Einheitentyp (Weltraum/Boden) |
| `MOBILE_UNITS` / `STATIONARY_UNITS` | Mobilität (mobil/stationär) |
| `LOWEST_AGILITY` / `HIGHEST_AGILITY` | Agilität (niedrig/hoch) |

### 4. Technische Implementierung & Normalisierung
Das System nutzt Funktionen (`blueprintStrategy.js`), um Datenkonsistenz zu gewährleisten:
* **String-Normalisierung:** Bereinigung von Whitespace und Behandlung von Null-Werten.
* **Integer-Clamping:** `startCycle` wird automatisch in den Bereich [1, 10] gezwungen.
* **Deduplizierung:** Prüfung auf eindeutige Modul-IDs innerhalb einer Gruppe.
* **Fallback-Logik:** Bei fehlender Strategie werden Standardwerte verwendet (`DEFAULT_START_CYCLE: 1`, `DEFAULT_TARGETING_CRITERIA: ["LOWEST_HIT_POINTS"]`, `DEFAULT_GLOBAL_FIRE_ORDER_CRITERIA: ["HIGHEST_ATTACK"]`).

## Verknüpfungen
- [[30_Resources/Game_Data/Noob_Protection_Technical|Noob Protection]]
- [[30_Resources/Game_Data/Blueprints_Technical|Blueprint System]]

## Changelog
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Technische Spezifikation der Kampfstrategie (Targeting & Fire Order). Beinhaltet Datenstrukturen für Blueprints (`combatStrategy`, `weaponGroups`) und Spieler (`fireOrder`), das `RuleSet`-System mit Sortier-IDs sowie Validierungsregeln (Max 3 Kriterien, Start Cycle 1-10) und Normalisierungslogik.
