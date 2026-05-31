---
category: technik, server
type: bug
confidence: high
source_type: discord
game_version: "unknown"
tags: [pollingtransport, token, connection, error]
related: []
sources: ["discord"]
created: 2026-05-22
updated: 2026-05-22
---

# Bugreport: PollingTransport Token Registration Error

## Basisdaten

| Fehlertyp | Details |
| --- | --- |
| Exception | `ERROR | PollingTransport` |
| Message | `[ID] is not registered. Closing connection.` |
| Symptom | Flotten oder Gebäude können nicht geladen werden |

## Mechanik / Verhalten

Der Server wirft periodisch Fehler im `PollingTransport`. Ein Token wird während einer Anfrage plötzlich als "nicht registriert" gemeldet, was zum Schließen der Verbindung führt. Dies äußert sich beim Client in Fehlermeldungen wie "Flotten konnten nicht geladen werden".

**Server Log Auszug:**
```
| 2026-04-26 11:15:30 | ERROR | PollingTransport | 194 | d1dd829c-9545-46fb-bd57-bd8e3bc32af5 is not registered. Closing connection.
```

## Verknüpfungen

- [[30_Resources/BugReports/Ticket_Creation_Error|Frontend Bug: Ticket System]]

## Tests & Hypothesen

- Möglicher Fehler beim Token-Management oder bei der Session-Validierung während des Polling-Intervalls.
- Ein Wechsel auf ein neueres Protokoll wurde als mögliche Lösung diskutiert.

## Changelog

- 2026-05-22: Erstmals erstellt basierend auf Discord-Chatverlauf (User `xearox`).

## LLM_CONTEXT

Server-Fehler im PollingTransport: Token wird während der Anfrage als "not registered" gemeldet, was Verbindungsabbrüche und Ladefehler bei Flotten/Gebäuden verursacht.