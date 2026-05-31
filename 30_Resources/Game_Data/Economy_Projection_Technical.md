---
category: [wirtschaft, technik]
type: referenz
confidence: high
source_type: code_analysis
game_version: "unknown"
tags: [resource_projection, economy_rates, civilian_growth, resource_management]
related: ["[[30_Resources/Game_Data/Resource_Production_Technical|Resource Production]]", "[[30_Resources/Game_Data/Planet_Model_Technical|Planet Model Technical]]"]
sources: ["resourceProjection.js", "resourceRates.js"]
created: 2024-05-23
updated: 2024-05-23
---

# Economy Projection & Resource Rates (Technische Spezifikation) & Kurzbeschreibung
Dokumentation der mathematischen Modelle zur Vorhersage der Ressourcenentwicklung und die Logik zur Berechnung der Produktionsraten auf Planeten.

## Basisdaten

| Bereich | Kernkonzept | Implementierung / Detail |
| :--- | :--- | :--- |
| **Ressourcen-Projektion** | Lineare Entwicklung | $\text{ProjectedAmount} = \min(\max(0, \text{Start} + (\text{RatePerHour} \times \text{Hours})), \text{Capacity})$ |
| **Zivilisten-Wachstum** | Komplexes Modell | Basierend auf Fertilität und Kapazitätsgrenze (`civCap`) |
| **Netto-Rate** | $\text{Net} = \text{Production} - \text{Consumption}$ | Berücksichtigt Serverdaten oder lokale Fallbacks |

## Mechanik / Verhalten

### 1. Ressourcen-Projektion (`resourceProjection.js`)
Das System berechnet, wie sich die Ressourcenbestände eines Planeten über einen Zeitraum hinweg entwickeln (Lineare Projektion).

#### A. Lineare Projektion
Für die primären Ressourcen (IDs: 1=Metal, 2=Crystal, 3=Antimatter, 5=Soldiers) wird eine lineare Formel verwendet. Wenn der Startwert bereits die Kapazität (`cap`) erreicht hat, stoppt die Produktion, aber der Verbrauch kann weiterhin den Bestand senken.

#### B. Zivilisten-Wachstum (Civilians)
Das Wachstum der Zivilisten (ID: 4) folgt einer komplexeren Logik als rein lineare Ressourcen:
* **Fertilität:** Basierend auf dem Planetenwert (`fertility`), kombiniert mit Boni oder Ressourcen-Vorkommen.
* **Wachstumsmodell:** Nutzt die Funktion `projectCivilianAmount`, welche Produktion (Geburten) und Konsum (Sterberate/Verbrauch) über die Zeit berechnet.
* **Kapazitätslimit:** Auch Zivilisten unterliegen einer Kapazitätsgrenze (`civCap`).

### 2. Ressourcen-Raten & Dynamik (`resourceRates.js`)
Die Berechnung der Netto-Rate ist entscheidend für die Wirtschaftssimulation.

#### A. Produktions- und Konsumlogik
* **Server-Daten:** Wenn vom Server explizite Produktions- oder Konsumwerte geliefert werden, haben diese Priorität.
* **Lokale Berechnung (Fallback):** Falls keine Serverdaten vorliegen, berechnet das System die Rate basierend auf dem aktuellen Bestand und der Fertilität (bei Zivilisten).

#### B. Spezialeffekte & Boni
Das System unterstützt dynamische Modifikatoren:
* **Clone Tanks Effekt:** 
    * **Fertility Mode:** Erhöht die Zivilisten-Produktion über einen `fertilityBonus`.
    * **Soldier Mode:** Erhöht die Produktion von Soldaten (`SOLDIER_RESOURCE_ID`) durch einen spezifischen Bonus.
* **Fraktions-Multiplikatoren:** Die Raten können durch Fraktions-Effekte (Cargo/Speed) beeinflusst werden.

### 3. Technische Implementierungshinweise
* **Timestamp-Handling:** Das System erkennt automatisch, ob Server-Timestamps in Sekunden oder Millisekunden vorliegen und normalisiert diese auf Millisekunden.
* **Immutability (Klonen):** Bei der Projektion wird ein tiefer Klon des Planeten-Objekts erstellt (`Object.create(Planet.prototype)`), um Seiteneffekte im globalen State zu vermeiden (Vermeidung von exponentiellem Wachstum durch Referenzfehler).

## Verknüpfungen
- [[30_Resources/Game_Data/Resource_Production_Technical|Resource Production Technical]]

## Changelog
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Technische Spezifikation der Ressourcenprojektion (lineare Projektion für Primärressourcen, komplexes Modell für Zivilisten) und der Netto-Ratenberechnung (`resourceRates.js`). Beinhaltet Spezialeffekte wie Clone Tanks und die technische Umsetzung via Immutability/Cloning zur Vermeidung von State-Fehlern.
