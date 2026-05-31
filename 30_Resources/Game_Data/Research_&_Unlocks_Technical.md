---
category: [technik, progression]
type: referenz
confidence: high
source_type: code
game_version: "unknown"
tags: [research, unlocks, requirements, debugging]
related: ["[[30_Resources/Game_Data/Blueprints_Technical|Blueprint System]]"]
sources: ["unlockRequirements.js"]
created: 2026-05-22
updated: 2024-05-23
---

# Research & Unlocks (Technische Spezifikation) & Kurzbeschreibung
Dokumentation der Logik zur Verwaltung von Forschungsfortschritten und die daraus resultierenden Freischaltungen von Gebäuden und Modulen.

## Basisdaten

| Bereich | Kernfunktion | Implementierung |
| :--- | :--- | :--- |
| **Forschungsverwaltung** | Level-Mapping & Anforderungsprüfung | `buildResearchLevelMap`, `resolveResearchRequirements` |
| **Freischaltung** | Module & Gebäude | Prüfung gegen `levelMap` und `isUnlocked`-Flags |
| **Debugging** | Manuelle Freischaltung | LocalStorage-Flag `sw_debug_unlocks` |

## Mechanik / Verhalten

### 1. Forschungsverwaltung (`unlockRequirements.js`)
Das System verwaltet den Fortschritt des Spielers durch ein Mapping von Forschungs-IDs zu erreichten Leveln.
* **Research Level Map:** Die Funktion `buildResearchLevelMap` erstellt eine konsistente Übersicht über den Forschungsstand. Sie unterstützt verschiedene Formate und nutzt das höchste gefundene Level (`setMaxLevel`) bei widersprüchlichen Daten.
* **Anforderungsprüfung (Requirements):** Die Funktion `resolveResearchRequirements` aggregiert Anforderungen aus verschiedenen Feldern (`researchRequirements`, `requiredResearch`, `constraints.requirements`), um eine einheitliche Liste zu erhalten. Diese wird gegen die aktuelle `levelMap` des Spielers geprüft.

### 2. Freischalt-Logik (Unlocks)
Die Prüfung, ob ein Objekt im Spiel nutzbar ist, erfolgt über zwei Hauptpfade:
* **Module-Freischaltung:** Ein Modul gilt als freigeschaltet, wenn alle Anforderungen erfüllt sind und kein explizites `isUnlocked: false` Flag vorliegt.
* **Gebäude-Freischaltung:** Es gibt eine Liste von Basis-IDs (`DEFAULT_UNLOCKED_BUILDING_IDS`), die ohne Forschung sofort verfügbar sind. Alle anderen Gebäude erfordern die Erfüllung spezifischer Forschungsanforderungen.

### 3. Debugging & Entwicklung
Für die Entwicklung wurde ein integriertes System implementiert:
* **Debug-Modus:** Über das LocalStorage-Flag `sw_debug_unlocks` können alle Gebäude und Module manuell freigeschaltet werden.
* **Entwickler-Logs:** Bieten Einblicke in die Größe der `levelMap` und die Anzahl der Forschungszweige.

## Verknüpfungen
- [[30_Resources/Game_Data/Blueprints_Technical|Blueprint System]]

## Changelog
- 2026-05-22: Erstmals erstellt basierend auf Code-Analyse.
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Technische Spezifikation der Forschungslogik: Management von Research Levels (`levelMap`), Auflösung komplexer Anforderungen (`resolveResearchRequirements`) und die Logik für Modul-/Gebäude-Freischaltungen sowie Debugging-Optionen.
