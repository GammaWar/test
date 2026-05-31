---
category: [alliance]
type: technik
confidence: high
source_type: code
game_version: "unknown"
tags: [alliance, technical, api]
related: ["[[30_Resources/Game_Data/Faction_System_Technical|Faction System]]", "[[30_Resources/Game_Data/Universe_API_Technical|Universe API Technical]]"]
sources: ["frontend API", "React hooks"]
created: 2024-05-23
updated: 2024-05-23
---

# Alliance System (Technische Spezifikation) & Kurzbeschreibung
Technische Implementierungsdetails für das Allianz-System, basierend auf der Frontend-API und React Hooks.

## Basisdaten

| Attribut | Wert / Status |
| :--- | :--- |
| **Upgrade Stats (Beispiel)** | 1087.91 AP |
| **Member Limit Level** | 1 / 38 |
| **Current Effect** | 15 |

## Mechanik / Verhalten

### Factions API
Ermöglicht das Anzeigen und Wechseln von Fraktionen.
* `fetchFactionCatalog()`: Holt die Liste via `WebsocketCommands.User.Faction.GET`.
* `changeFaction(factionId)`: Beantragt einen Fraktionswechsel via `WebsocketCommands.User.Faction.CHANGE`.

### Alliance Applications
Verwaltung von Beitrittsanfragen über den Hook `useAllianceApplications`.
* **Returns:** `{ applications, loading, error, reload, setApplications }`

### Alliance Export
Export der Allianzdaten als komprimiertes Archiv (`tar.gz` oder `zip`).
* **Polling:** Überwachung des Status via `POLL_INTERVAL_MS = 2500`.
* **Erfolgs-Status:** `ACCEPTED`, `DONE`, `COMPLETED`, `READY`, `FINISHED`.

### Alliance Description & Metadata
Verwaltung von Text und Metadaten (`description`, `version`, `updatedAt`, `updatedByUserId`).

### Filtering & Sorting
* **Join Policies:** `PUBLIC_OPEN`, `PUBLIC_RESTRICTED`, `PRIVATE_INVITE`, `PRIVATE_PASSWORD`.
* **Sorting:** Name, Members, Free Slots.

### Alliance List
Abruf der Allianzliste via Hook `useAllianceList` (`listAlliances()`).

### Alliance Forum
Kommunikationssystem mit Bereichen (Areas) und Threads.
* **Hooks:** `useAllianceForumAreas`, `useAllianceForumThreads`, `useAllianceForumPosts`, `useAllianceForumVisibility`.

### Profile & Ranks
Verwaltung des Profils und der internen Hierarchie.
* **Hooks:** `useAllianceProfile`, `useAllianceRanks` (inkl. Permissions), `useAllianceRank`.

### Radar & Visibility
* **Radar:** Echtzeit-Status via `useAllianceRadar` (Polling).
* **Visibility:** Sichtbarkeit im Spiel via `useAllianceVisibility`.

### Chat Integration (XForgeBot)
Bidirektionale Synchronisation zwischen Discord-Kanälen und dem In-Game Allianz-Chat.

### Alliance Mobility (Concept)
Vorschlag zur Bewegung von Monden oder großen Strukturen (siehe [[20_Areas/Gameplay_Mechaniken/Raumstationen|Mobile Space Station]]).

### Alliance Upgrades
Fortschritt durch Einsatz von Alliance Points (AP). Erhöht Member-Limits und bietet spezifische Effekte.

## Verknüpfungen
- [[30_Resources/Game_Data/Faction_System_Technical|Faction System Technical]]
- [[30_Resources/Game_Data/Universe_API_Technical|Universe API Technical]]
- [[20_Areas/Gameplay_Mechaniken/Raumstationen|Mobile Space Station Concept]]

## Changelog
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Technische Dokumentation des Allianz-Systems (API, Hooks, Forum, Ranks, Upgrades, Export). Beinhaltet Details zu Faction-Wechseln, Beitrittsrichtlinien und der Discord-Chat-Integration via XForgeBot.
