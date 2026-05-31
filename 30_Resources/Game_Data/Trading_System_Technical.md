---
category: [wirtschaft, technik]
type: referenz
confidence: high
source_type: code_analysis
game_version: "unknown"
tags: [trading, economy, api, lobby_shop]
related: ["[[30_Resources/Game_Data.md|Game Data Index]]"]
sources: ["tradeStationApi.js"]
created: 2024-05-23
updated: 2024-05-23
---

# Trading System (Technische Spezifikation) & Kurzbeschreibung
Beschreibung der API-Struktur und des Workflows für das Handelssystem (Trade Station) sowie Informationen zum kosmetischen Lobby Shop.

## Basisdaten

| Bereich | Kernfunktion | Implementierung / Details |
| :--- | :--- | :--- |
| **Handel (API)** | Preisabfrage & Order-Management | `tradeStationApi.js` via WebSockets |
| **Lobby Shop** | Kosmetische Anpassungen | Planetennamen, Blueprint-Namen (Farben) |
| **Währung** | Credits | Kaufbare Credits zur Bezahlung im Shop |

## Mechanik / Verhalten

### 1. API & Kommunikation (`tradeStationApi.js`)
Das Handelssystem nutzt den `LiveGameService`, um Transaktionen und Preisabfragen über WebSockets abzuwickeln.

#### A. Verfügbare Endpunkte
| Funktion | WebSocket Command | Beschreibung |
| :--- | :--- | :--- |
| `fetchTradingPrices` | `user.trading.price.list` | Ruft die aktuelle Preisliste aller Handelspaare ab. |
| `fetchTradingPrice` | `user.trading.price.get` | Ruft den spezifischen Preis für ein einzelnes Paar ab. |
| `fetchTradingInventory` | `user.trading.station.inventory.get` | Zeigt den aktuellen Lagerbestand der Handelsstation an. |
| `createTradingOrder` | `user.trading.order.create` | Erstellt eine neue Kauf- oder Verkaufsorder. |
| `fetchLatestOrders` | `user.trading.order.latest` | Ruft die aktuellsten offenen Orders für bestimmte Paare ab. |
| `acceptTradingOrder` | `user.trading.order.buy` | Akzeptiert eine bestehende Order (Kaufabwicklung). |

#### B. Fehlerbehandlung
Alle API-Aufrufe nutzen eine `ensureOk`-Funktion, die auf einen `status: "error"` prüft und technische Fehlercodes in aussagekräftige UI-Fehlermeldungen umwandelt.

### 2. Workflow & Validierung
* **Order-Prozess:** Preisprüfung $\rightarrow$ Order-Erstellung $\rightarrow$ Matching/Akzeptanz (`acceptTradingOrder`).
* **Handelsmechaniken:** Unterscheidung zwischen Aktion (z. B. "Purchase") und Auftragstyp; dynamische Preiskorrektur zur Marktstabilisierung.

### 3. Lobby Shop (Kosmetische Artikel)
Ein System zur Unterstützung der Projektentwicklung durch rein kosmetische Anpassungen (**kein Pay2Win**).
* **Anpassungsmöglichkeiten:** Farbgestaltung von Planeten- und Blueprint-Namen in verschiedenen Ansichten (Universum, Liste, Kampfberichte).
* **Preisgestaltung:** 
    * Einzelne Planeten: 2,50 €
    * Blueprint-Pakete: 20er Paket für 10,00 € (mit Mengenrabatt ab dem 5. Paket).
* **Credits:** Kauf von Credits möglich (z. B. 300 Credits für 3,00 €; 1000 Credits für 9,25 €).

## Verknüpfungen
- [[30_Resources/Game_Data.md|Game Data Index]]

## Changelog
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Technische Spezifikation des Trading Systems (API, Order-Workflow, Fehlerbehandlung) sowie Details zum kosmetischen Lobby Shop (Planet/Blueprint-Farben, Credit-Preise).
