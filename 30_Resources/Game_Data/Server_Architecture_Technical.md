---
category: [technik, server]
type: referenz
confidence: high
source_type: code_analysis
game_version: "unknown"
tags: [server, architecture, mysql, plugin_system]
related: ["[[30_Resources/Game_Data/Server_Communication_Technical|Server Communication]]", "[[30_Resources/Game_Data/Universe_API_Technical|Universe API]]"]
sources: ["SpacewarCore logs"]
created: 2024-05-23
updated: 2024-05-23
---

# Server Architecture (Technische Spezifikation) & Kurzbeschreibung
Beschreibung der technischen Struktur des Spacewar-Backends, einschließlich Datenbankintegration und dem modularen Plugin-System.

## Basisdaten

| Komponente | Technologie / Detail |
| :--- | :--- |
| **Datenbank** | MySQL (persistente Speicherung aller Spielzustände) |
| **Kernsystem** | SpacewarCore (v0.0.1) |
| **Architekturtyp** | Modulares Plugin-System |

## Mechanik / Verhalten

### 1. Datenhaltung & Initialisierung
Der Gameserver nutzt eine persistente MySQL-Datenbank zur Verwaltung aller Spielzustände. Der Boot-Prozess des `SpacewarCore` folgt diesem Ablauf:
1. **Config Loading:** Laden der Server-Konfiguration.
2. **Database Setup:** Erstellung und Validierung der MySQL-Tabellen.
3. **Resource & User Loading:** Laden der Spielressourcen und Benutzerdaten aus der Datenbank.
4. **Universe Creation:** Instanziierung einer neuen Galaxie/Universums-Instanz.

### 2. Modulares Plugin-System
Um die Wartbarkeit zu erhöhen, wurde das System von einem monolithischen Ansatz auf ein modulares Plugin-System umgestellt.
* **Modularer Neustart:** Einzelne Server-Module können neu gestartet werden, ohne den gesamten Gameserver herunterfahren zu müssen. Dies minimiert die Downtime für Spieler erheblich.
* **Erhöhte Stabilität:** Fehler in einem Modul können isoliert und behoben werden.

### 3. Monitoring & Benachrichtigungen
Die Erweiterung der Überwachungskapazitäten ermöglicht proaktive Kommunikation:
* **Benachrichtigungssystem:** Integration von Benachrichtigungen für Browser oder mobile Apps (Android).
* **Zweck:** Spieler werden informiert, sobald ein Modul-Update oder ein Neustart eines spezifischen Dienstes erfolgt, sodass sie während des Updates eingeloggt bleiben können.

## Verknüpfungen
- [[30_Resources/Game_Data/Server_Communication_Technical|Server Communication]]
- [[30_Resources/Game_Data/Universe_API_Technical|Universe API]]

## Changelog
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Technische Spezifikation der Server-Architektur. Fokus auf MySQL-Integration, dem modularen Plugin-System (v0.0.1 SpacewarCore), Hot-Reloads von Modulen und proaktiven Monitoring-Benachrichtigungen für Spieler.
