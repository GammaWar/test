---
category: ui
type: bug
confidence: high
source_type: discord
game_version: "unknown"
tags: [ticket-system, frontend, error]
related: []
sources: ["discord"]
created: 2026-05-22
updated: 2026-05-22
---

# Bugreport: Fehler beim Ticket-Erstellen

## Basisdaten

| Fehlertyp | Details |
| --- | --- |
| Exception | `NotFoundError` |
| Ursache | `insertBefore` fehlgeschlagen (Knoten ist kein Kindknoten) |
| Betroffene Komponente | Frontend / UI (Ticket-System) |
| URL/Pfad | `https://space-war.com/static/js/main.d2a13d9d.js` |

## Mechanik / Verhalten

Beim Versuch, ein Ticket zu erstellen, tritt ein JavaScript-Fehler auf. Der Fehler deutet darauf hin, dass das DOM-Management (wahrscheinlich durch ein Framework wie React) versucht, einen Knoten einzufügen, der nicht im erwarteten Kontext existiert.

**Error Message:**
`NotFoundError: Fehler beim Ausführen von 'insertBefore' für 'Node': Der Knoten, vor dem der neue Knoten eingefügt werden soll, ist kein Kindknoten dieses Knotens.`

**Stack Trace (Auszug):**
```javascript
bei gl (https://space-war.com/static/js/main.d2a13d9d.js:2:297538)
bei gl (https://space-war.com/static/js/main.d2a13d9d.js:2:297649)
...
```

## Verknüpfungen

- [[20_Areas/Gameplay_Mechaniken|Gameplay & Mechaniken]] (Falls UI-Elemente Gameplay beeinflussen)

## Tests & Hypothesen

- Der Fehler tritt bei bestimmten Browsern oder unter spezifischen Bedingungen auf (User `commander_91546` wurde nach dem Browser gefragt).
- Möglicher Konflikt zwischen DOM-Manipulation und Framework-Rendering.

## Changelog

- 2026-05-22: Erstmals erstellt basierend auf Discord-Chatverlauf.

## LLM_CONTEXT

Frontend-Bug im Ticket-System: `NotFoundError` bei `insertBefore`. Betrifft die Web-App unter `space-war.com`. Stacktrace weist auf `main.d2a13d9d.js` hin.