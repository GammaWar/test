---
category: [wirtschaft, referenz]
type: [technik, konstanten]
confidence: high
source_type: code
game_version: "0.5.203"
tags: [economy, constants, reference]
related: ["[[30_Resources/Game_Data|Game Data Index]]"]
sources: ["economy.constants.js"]
created: 2024-05-23
updated: 2026-05-30
---

# Economy Constants & ID Mappings (Referenz) & Kurzbeschreibung
Zentrale Referenz für die numerischen IDs und Schlüssel, die im gesamten Spacewar-System verwendet werden. Beinhaltet Ressourcen-Mappings, Gebäude-IDs sowie Basiswerte für Kosten, Bauzeiten, Produktion und Lagerkapazitäten.

## Basisdaten

| Bereich | Inhalt |
| :--- | :--- |
| **Ressourcen** | Metall, Kristall, Antimaterie, Zivilisten, Soldaten, Forschung |
| **Gebäude** | 40+ definierte IDs (inkl. Synonyme) |
| **Planeten-Klassen** | A bis F mit spezifischen Ressourcen-Multiplikatoren |

## Mechanik / Verhalten

### 1. Ressourcen-Mapping (RES_KEY / RES_NAME)

| ID | Key | Name |
| :--- | :--- | :--- |
| 1 | `metal` | Metall |
| 2 | `crystal` | Kristall |
| 3 | `antimatter` | Antimaterie |
| 4 | `civilians` | Zivilisten |
| 5 | `soldiers` | Soldaten |
| 6 | `research` | Forschungspunkte |

### 2. Gebäude-ID Mapping (BUILDING_ID)

| ID | Name / Synonyme |
| :--- | :--- |
| 0 | Metal Mine |
| 1 | Crystal Mine |
| 2 | Antimatter Factory |
| 3 | Metal Storage |
| 4 | Crystal Storage |
| 5 | Antimatter Tank |
| 6 | Residential Building |
| 7 | Barracks |
| 8 | Research Center |
| 28 | Clone Tanks (Clone Tank, Clonetanks, Klontanks) |
| 29 | Sensor Tower |
| 30 | Robot Factory (Roboter Workshop, Roboterwerkstatt) |
| 31 | Shipyard (Schiffwerft) |
| 32 | Armory (Rüstungswerke) |
| 40 | Jumpgate (Sprungtor) |

### 3. Basis-Werte (Base Tables)

#### A. Baukosten (BASE_COSTS)
*Kosten pro Gebäude-ID und Ressourcen-ID (RID)*

| ID | Metall (1) | Kristall (2) | Antimaterie (3) | Zivilisten (4) | Soldaten (5) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **0** | 125 | 12 | - | 50 | - |
| **1** | 10 | 100 | - | 75 | - |
| **2** | 25 | 125 | - | 100 | - |
| **3** | 25 | 12 | - | 12 | - |
| **4** | 25 | 12 | - | 12 | - |
| **5** | 25 | 37 | - | 25 | - |
| **6** | 75 | 25 | - | 12 | - |
| **7** | 250 | 100 | - | 125 | - |
| **8** | 125 | 400 | - | 250 | - |
| **28** | 375 | 500 | - | 125 | - |
| **29** | 2500 | 7500 | - | 2500 | 1250 |
| **30** | 3750 | 7500 | - | 2500 | - |
| **31** | 375 | 250 | - | 100 | 37 |
| **32** | 250 | 125 | - | 125 | 50 |
| **40** | 50 | 250 | - | 125 | 25 |

#### B. Basis-Bauzeit (BASE_BUILD_TIME)
*Sekunden pro Gebäude-ID*

| ID | Bauzeit (s) | ID | Bauzeit (s) |
| :--- | :--- | :--- | :--- |
| **0** | 137 | **28** | 875 |
| **1** | 110 | **29** | 10000 |
| **2** | 150 | **30** | 11250 |
| **3** | 37 | **31** | 625 |
| **4** | 37 | **32** | 375 |
| **5** | 62 | **40** | 750 |
| **6** | 100 | | |
| **7** | 350 | | |
| **8** | 525 | | |

#### C. Basis-Produktion (BASE_PRODUCTION)
*Produktion pro Stunde bei Level 1*

| ID | Ressource (RID) | Menge /h |
| :--- | :--- | :--- |
| **0** | 1 (Metall) | 800 |
| **1** | 2 (Kristall) | 500 |
| **2** | 3 (Antimaterie) | 300 |
| **7** | 5 (Soldaten) | 250 |
| **8** | 6 (Forschung) | 100 |

#### D. Basis-Lagerkapazität (BASE_STORAGE)
*Kapazität bei Level 1*

| ID | Ressource (RID) | Kapazität |
| :--- | :--- | :--- |
| **3** | 1 (Metall) | 5000 |
| **4** | 2 (Kristall) | 5000 |
| **5** | 3 (Antimaterie) | 5000 |
| **6** | 4 (Zivilisten) | 5000 |
| **7** | 5 (Soldaten) | 500 |

#### E. Basis-Verbrauch (BASE_USAGE)
*Verbrauch pro Stunde*

| ID | Ressource (RID) | Verbrauch /h |
| :--- | :--- | :--- |
| **7** | 4 (Zivilisten) | 500 |
| **28** | 3 (Antimaterie) | 200 |

### 4. Planeten-Klassen & Depots (CLASS_DEPOSITS)

*Multiplikator-Bereiche [Min, Max] pro Klasse und Ressource*

| Klasse | Metall (1) | Kristall (2) | Antimaterie (3) | Zivilisten (4) | Soldaten (5) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **A (1)** | [0.05, 0.3] | [0.05, 0.25] | [0.8, 2.0] | [0, 0] | [0.75, 0.85] |
| **B (2)** | [0.1, 0.4] | [0.8, 2.0] | [0.05, 0.2] | [0, 0.1] | [0.9, 1.1] |
| **C (3)** | [0.8, 2.0] | [0.05, 0.2] | [0.1, 0.3] | [0, 0] | [0.75, 0.85] |
| **D (4)** | [0.4, 0.8] | [0.4, 0.8] | [0.4, 0.8] | [0.1, 0.2] | [1.0, 1.2] |
| **E (5)** | [0.3, 0.6] | [0.3, 0.6] | [0.3, 0.6] | [0.2, 0.3] | [1.25, 1.5] |
| **F (6)** | [0.1, 0.4] | [0.1, 0.4] | [0.05, 0.2] | [0.3, 0.6] | [1.3, 1.8] |

**Klassen-Mapping:** `A:1, B:2, C:3, D:4, E:5, F:6`

## Verknüpfungen
- [[30_Resources/Game_Data|Game Data Index]]

## Changelog
- 2024-05-23: Erstmals erstellt basierend auf `economy.constants.js`.
- 2024-05-23: Upgrade auf neues Standard-Template.
- 2026-05-30: Bidirektionale Verknüpfung zum Game Data MOC hinzugefügt.

## LLM_CONTEXT
Zentrale Wirtschaftskonstanten für Spacewar. Enthält Mappings für Ressourcen (Metall, Kristall, Antimaterie, Zivilisten, Soldaten, Forschung), Gebäude-IDs (inkl. Synonyme) sowie Basiswerte für Kosten, Bauzeiten, Produktionsraten, Lagerkapazitäten und Verbrauch. Beinhaltet zudem Multiplikator-Bereiche der Planetenklassen [Min, Max].
