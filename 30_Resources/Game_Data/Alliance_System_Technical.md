---
category: alliance
type: technik
confidence: high
source_type: code
game_version: "x.x.x"
tags: [alliance, api, technische_spezifikation]
related: ["[[00_MOCs/Alliance_MOC]]"]
sources: ["api"]
created: 2024-05-23
updated: 2024-05-23
---

# Alliance System (Technische Spezifikation)

Dokumentation der technischen Implementierung des Allianz-Systems, einschließlich API-Schnittstellen, Schatzkammer, Mitgliedschaft und Foren.

## Basisdaten

### Beitrittsrichtlinien (Join Policies)

| Richtlinie | Beschreibung | Aktion |
| :--- | :--- | :--- |
| PUBLIC_OPEN | Jeder kann sofort beitreten. | join |
| PUBLIC_RESTRICTED | Erfordert eine Bewerbung und ggf. eine Nachricht. | apply |
| PRIVATE_PASSWORD | Beitritt nur mit korrektem Passwort möglich. | join |
| PRIVATE_INVITE | Nur über Einladung möglich. | none |

### Spezialisierungen (Specializations)

| Typ | Fokus |
| :--- | :--- |
| PRODUCTION | Ressourcenproduktion |
| TRADE | Handelsvorteile |
| COMBAT | Militärische Stärke |
| HYBRID | Ausgewogene Mischung |

## Mechanik / Verhalten

### 1. API & Kommunikation
Die Interaktion erfolgt über den `LiveGameService` via WebSockets unter dem Namespace `WebsocketCommands.User.Alliance`.

#### A. Allianz-Protokolle (Alliance Logs)
* **Funktion:** `updateAllianceLogSettings(allianceId, enabledCategories)`
* **Beschreibung:** Festlegung der zu protokollierenden Kategorien.
* **Parameter:** `allianceId` (String), `enabledCategories` (Array of Strings).

#### B. Allianz-Radar (Alliance Radar)
* **Funktion:** `pollAllianceRadar(allianceId)`
* **Beschreibung:** Polling-Mechanismus zur Abfrage aktueller Radardaten für die Allianz. Die Antwort wird via `normalizeAllianceRadarResponse` normalisiert.

#### C. Allianz-Module (Alliance Modules)
* **Funktionen:**
    * `listAllianceModules(allianceId)`: Liste der verfügbaren/installierten Module.
    * `upgradeAllianceModule({ allianceId, moduleKey, idempotencyKey })`: Aufwertung eines Moduls.
* **Parameter:** `moduleKey` (String), `idempotencyKey` (optionaler String zur Vermeidung von Doppel-Upgrades).

### 2. Implementierungsdetails
* **Fehlerbehandlung:** Validierung der `allianceId` und Prüfung, ob `enabledCategories` ein gültiges Array ist. Fehler werden als Error-Objekte mit Codes zurückgegeben.
* **Datennormalisierung:** Transformation der Server-Payloads in konsistente Frontend-Strukturen (z. B. Radar-Daten).

### 3. UI & Darstellung
* **Zeitstempel:** Format `dd.MM.yyyy HH:mm` (Fallback: `alliances.common.placeholder`).
* **Koordinaten:** Format `x:y:z`.
* **Flottengröße:** Nutzung von i18n-Keys (`alliances.radar.fleet_size.{value}`).
* **Spieleranzeige:** Rendering des Namens via `nameStyle` und Anzeige eines Allianz-Tags als Badge.

### 4. Allianz-Schatzkammer & Spezialisierung (Treasury & Specialization)
* **Schatzkammer-Einzahlung:** Ressourcen (`metal`, `crystal`, `antimatter`) werden von Planeten in die Schatzkammer transferiert und in Alliance Points (AP) umgewandelt.
* **Spezialisierungen:** Strategische Ausrichtung via `setSpecialization` (PRODUCTION, TRADE, COMBAT, HYBRID).

### 5. Mitgliedschaft & Beitritt (Membership & Join Policies)
(Siehe Tabelle unter Basisdaten)
Die Mitglieder-Statistiken tracken: `points`, `planetCount`, `unitCount`, `unitsBuilt`, `storedResources`.

### 6. Ränge & Berechtigungen (Ranks & Permissions)
Hierarchisches System mit Attributen wie `rankId`, `name`, `priority` und `isProtected`. Zugriff wird über ein Array von Berechtigungs-Keys gesteuert.

### 7. Forum-System
Strukturierte Kommunikation:
1. **Areas (Bereiche):** Kontext (z. B. Ankündigungen).
2. **Threads (Themen):** Einzelne Diskussionen.
3. **Posts (Beiträge):** Nachrichten innerhalb eines Threads.

Zugriff wird über `accessMode`, `minRankPriority`, `allowedRankIds` sowie `allowApplicants`/`allowGuests` gesteuert.

### 8. Sichtbarkeitseinstellungen (Visibility Settings)
Administratoren können die Sichtbarkeit von Mitgliederlisten, Statistiken, Ressourcenbeständen, Einheiten und Planeten sowie den "Shared Universe"-Modus steuern.

## Strategie
* **Wirtschaftsfokus:** Nutzung der `PRODUCTION`-Spezialisierung zur Maximierung des AP-Zuflusses über die Schatzkammer.
* **Militärfokus:** Fokus auf `COMBAT` und Überwachung durch den Allianz-Radar.

## Verknüpfungen
* [[00_MOCs/Alliance_MOC]]

## Tests & Hypothesen
* (Keine dokumentierten Tests vorhanden)

## Changelog
* 2024-05-23: Datei neu erstellt und auf Standard-Template migriert.

## LLM_CONTEXT
Technische Spezifikation des Allianz-Systems. Beinhaltet WebSockets-API (LiveGameService) für Logs, Radar und Module. Schatzkammer ermöglicht Ressourcen-Konversion in Alliance Points (AP) mit Spezialisierungen (PRODUCTION, TRADE, COMBAT, HYBRID). Mitgliedschaft via Join Policies (PUBLIC_OPEN, PUBLIC_RESTRICTED, PRIVATE_PASSWORD, PRIVATE_INVITE). Hierarchisches Rangsystem mit Berechtigungen und ein strukturiertes Forum (Areas -> Threads -> Posts).
