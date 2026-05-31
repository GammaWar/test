---
category: [technik, ui]
type: referenz
confidence: high
source_type: code
game_version: "unknown"
tags: [frontend, error-handling, analytics, posthog]
related: ["[[30_Resources/Game_Data/Alliance_System_Technical|Alliance System]]"]
sources: ["code"]
created: 2024-05-23
updated: 2024-05-23
---

# Frontend Infrastructure & Error Handling (Technische Spezifikation) & Kurzbeschreibung
Dokumentation der technischen Infrastruktur des Frontends, insbesondere in Bezug auf Analytics und das System zur Fehlererfassung.

## Basisdaten

| Tool | Zweck | Details |
| :--- | :--- | :--- |
| **PostHog** | Analytics & Tracking | Erfasst Nutzerverhalten und Events via API-Host `us.i.posthog.com`. |
| **Custom Error Buffer** | Fehlererfassung | Speichert bis zu 100 Fehlermeldungen in der `sessionStorage`. |
| **Mailto Reporting** | Fehlerbericht | Automatisiertes Senden von technischen Berichten an `info@space-war.com`. |

## Mechanik / Verhalten

### 1. Analytics (PostHog)
Das System nutzt PostHog zur Analyse des Nutzerverhaltens. Die Initialisierung erfolgt über ein integriertes Skript, das Funktionen wie `capture`, `identify` und `getFeatureFlag` bereitstellt.

### 2. Fehlerbehandlung & Crash-Management
Ein proprietäres System überwacht die Stabilität der Anwendung:

#### A. Error Buffering (`errbuf.v1`)
* **Speicherung:** Alle Fehler (Error, Window-Errors, Unhandled Rejections) werden in einem Array in der `sessionStorage` unter dem Key `errbuf.v1` zwischengespeichert.
* **Kapazität:** Der Buffer hält die letzten 100 Einträge vor (FIFO-Prinzip).
* **Inhalt:** Gespeicherte Daten enthalten Zeitstempel, Fehlertyp und den entsprechenden Stacktrace.

#### B. Crash-Fallback UI
Bei Erkennung eines kritischen Fehlers injiziert das System ein visuelles Overlay (`#crash-fallback`) in das DOM:
* **Funktionalität:** Bietet dem Nutzer die Optionen "Send error report" oder "Reload app".
* **Design:** Ein dunkles, zentriertes Modal mit hoher Z-Index-Priorität.

#### C. Reporting-Prozess
Beim Klick auf "Send error report" wird ein `mailto:` Link generiert:
* **Empfänger:** `info@space-war.com`
* **Betreff:** `[Spacewar] Crash report` (oder ähnlich).
* **Body-Inhalt:** App-URL, User-Agent, Zeitstempel des Vorfalls sowie die letzten bis zu 30 Fehler/Warnungen inklusive Stacktraces.
* **Fallback:** Falls der Body zu lang für einen Mail-Link ist (> 2000 Zeichen), wird der Inhalt in die Zwischenablage kopiert und der Nutzer informiert.

## Strategie
* **Wartung:** Die Überwachung des `errbuf.v1` in den Analytics-Daten ermöglicht eine proaktive Fehlerbehebung bei Frontend-Instabilitäten.
* **User Experience:** Das Crash-Fallback verhindert, dass Nutzer vor einer leeren oder eingefrorenen Seite stehen, ohne eine Handlungsoption zu haben.

## Verknüpfungen
- [[30_Resources/Game_Data/Alliance_System_Technical|Alliance System (Technische Spezifikation der API)]]

## Changelog
- 2024-05-23: Datei neu erstellt basierend auf Frontend-Quellcode-Analyse.
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Frontend-Infrastruktur: PostHog für Analytics; proprietäres Fehlerbehandlungssystem mit `sessionStorage`-Buffer (max. 100 Einträge); Crash-Fallback UI bei Fehlern; automatisierter Error-Reporting-Mechanismus via `mailto:` an info@space-war.com inkl. technischer Metadaten und Stacktraces.
