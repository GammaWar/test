---
category: [ui, technik]
type: referenz
confidence: high
source_type: code_analysis
game_version: "unknown"
tags: [ui, react, combat_strategy, editor]
related: ["[[30_Resources/Game_Data/Blueprints_Technical|Blueprint System]]"]
sources: ["React components analysis"]
created: 2024-05-23
updated: 2024-05-23
---

# Combat Strategy Editor (UI-Spezifikation) & Kurzbeschreibung
Dokumentation der React-Komponenten und der UI-Logik zur Verwaltung der Kampfstrategien im Spacewar-Interface.

## Basisdaten

| Bereich | Beschreibung |
| :--- | :--- |
| **Hauptzweck** | Verwaltung von globalen Spieler-Strategien und spezifischen Blueprint-Kampfregeln |
| **Technologie** | React-basierte Komponenten mit Live-Synchronisation via WebSockets |
| **Validierung** | Integrierte Prüfung von Regel-Kriterien (Max. 3) und Modul-IDs |

## Mechanik / Verhalten

### Komponenten-Architektur

Die Benutzeroberfläche ist modular aufgebaut, um sowohl globale Spieler-Strategien als auch spezifische Blueprint-Strategien zu verwalten.

* **BlueprintStrategySection (Hauptkomponente):** Der zentrale Orchestrator. Verwaltet die globale `fireOrder`, die Navigation durch die `BlueprintStrategyList` und den Detail-Editor für ausgewählte Baupläne.
* **BlueprintStrategyList (Navigationskomponente):** Eine hierarchische Liste zur schnellen Auswahl von Bauplänen, unterstützt Kategorien wie Favoriten oder benutzerdefinierte Gruppen.
* **BlueprintStrategyCriteriaEditor (Regel-Editor):** Ein spezialisierter Editor für die Priorisierung von Regeln (`RuleSet`). Er bietet exakt **3 Slots**, um die technische Beschränkung (`MAX_RULE_CRITERIA`) abzubilden.
* **BlueprintStrategyDefaultGroupCard (Informationskarte):** Eine Anzeige-Komponente für die Standard-Waffengruppe eines Blueprints, inklusive Modulmengen und `orbitalFire`-Status.
* **BlueprintStrategyWeaponGroupsEditor (Gruppen-Editor):** Ermöglicht das Hinzufügen von Modulen zu Gruppen sowie die Definition gruppenspezifischer Targeting-Regeln.

### Zugriffskontrolle & Sichtbarkeit
Die Sichtbarkeit wird über die Klasse `BlueprintVisibility` gesteuert:
* **isPrivateToOwner:** Blueprint ist nur für den Besitzer sichtbar.
* **visibleToAdmins:** Steuert die Sichtbarkeit für administrative Benutzer.

### UI-Workflow & Validierung
Das Interface folgt einem strikten Workflow zur Sicherstellung der Datenintegrität:
1. **Dirty State Tracking:** Überwachung von Änderungen (`blueprintIsDirty`, `playerIsDirty`). Der "Save"-Button wird erst bei tatsächlichen Änderungen aktiviert.
2. **Feedback-Schleife:** Gelbe Banner für Regelverstöße (z. B. zu viele Kriterien) und rote Banner für Server-Fehler oder fehlgeschlagene API-Requests.
3. **Synchronisation:** Nutzung von `Reload`- und `Reset`-Funktionen zur Abstimmung des UI-States mit dem `LiveGameService`.

### Mock-Modus (Testumgebung)
Ein spezieller Modus für die Entwicklung ohne aktiven Live-Server:
* **Umschaltung:** Über einen Schalter auf der Startseite zwischen `Mock` (lokale Daten) und `Live` (Echtzeitdaten).
* **Authentifizierung:** Im Mock-Modus ist keine korrekte Anmeldung erforderlich.
* **Erweiterte Funktionen:** Ermöglicht das manuelle Hinzufügen/Löschen von Planeten sowie die Verwaltung von Ressourcen im Testmodus.

## Verknüpfungen
- [[30_Resources/Game_Data/Blueprints_Technical|Blueprint System]]
- [[30_Resources/Game_Data/Combat_Strategy_Technical|Combat Strategy Technical]]

## Changelog
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Dokumentation der React-Komponenten für den Combat Strategy Editor. Beinhaltet die Architektur (Section, List, CriteriaEditor), Validierungsregeln (Max 3 Kriterien), Dirty State Tracking und den Mock-Modus zur lokalen Entwicklung.
