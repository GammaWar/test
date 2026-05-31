---
category: wirtschaft
type: strategie
confidence: high
source_type: user_instruction
game_version: "0.5.203"
tags: [mining, expansion, strategy, equilibrium]
related: ["[[30_Resources/Game_Data/Planet_Registry_Technical|Planet Registry]]"]
sources: ["user_instruction"]
created: 2026-05-30
updated: 2024-05-23
---

# Mining Expansion Strategy (Equilibrium Protocol) & Kurzbeschreibung

**WICHTIG: Dieses Protokoll ist die verbindliche Arbeitsanweisung für alle Anfragen bezüglich des Minenausbaus. Wenn nach wirtschaftlich sinnvollen Upgrades gefragt wird, muss dieses Schema angewendet werden.**

## Basisdaten
| Planet | Metall-Mine | Kristall-Mine | Antimaterie-Fabrik |
| :--- | :--- | :--- | :--- |
| **001 E** | X + 2 | X + 3 | X + 2 |
| **003 B** | X | X + 5 | X |
| **004 B** | X | X + 3 | X |
| **005 A** | X | X | X + 5 |
| **006 C** | X + 3 | X | X |
| **007 D** | X + 1 | X + 2 | X + 2 |
| **008 B** | X | X + 3 | X |
| **009 C** | X + 4 | X | X |
| **010 C** | X + 4 | X | X |
| **011 B** | X | X + 3 | X |
| **012 C** | X + 4 | X | X |
| **013 B** | X | X + 3 | X |
| **015 C** | X + 3 | X | X |
| **016 B** | X | X + 5 | X |
| **017 B** | X | X + 5 | X |
| **018 B** | X | X + 5 | X |
| **019 B** | X | X + 4 | X |
| **020 B** | X | X + 3 | X |
| **021 B** | X | X + 3 | X |
| **022 B** | X | X + 5 | X |
| **023 C** | X + 3 | X | X |
| **024 C** | X | X + 5 | X |
| **025 B** | X | X + 5 | X |
| **026 B** | X | X + 3 | X |
| **027 B** | X | X + 5 | X |

## Mechanik / Verhalten
Das Konzept basiert auf dem "Perfekten Stufen-Gleichgewicht". Anstatt Planeten isoliert zu betrachten, wird das gesamte Imperium in ein Gleichgewicht gebracht. Die Basis für alle Berechnungen ist die aktuell niedrigste Minenstufe im gesamten Imperium (**Basis-Stufe X**). Planeten mit einem Ressourcen-Vorteil erhalten einen festen Stufen-Vorsprung vor dieser Basisstufe ($X + n$).

### Anwendung des Protokolls (Schritt-für-Schritt)
1.  **Ermittlung von X:** Identifiziere die aktuell niedrigste Minenstufe im gesamten Imperium.
2.  **Berechnung der Zielstufe:** Wende den Offset aus der Tabelle auf $X$ an.
3.  **Umsetzung:** Alle Planeten, die in der Tabelle ein "X" haben, werden auf die aktuelle Basisstufe $X$ gehalten. Nur die Planeten mit einem Plus-Wert werden aktiv hochgezogen.
4.  **Skalierung:** Sobald das Gleichgewicht erreicht ist, wird $X$ für den nächsten Ausbau um 1 erhöht ($X = 31$) und der Prozess beginnt von vorn.

## Changelog
- 2024-05-23: Upgrade auf neues Standard-Template und Entfernung von Emojis.

## LLM_CONTEXT
Mining expansion protocol based on equilibrium theory. Uses a base level (X) from the lowest mine in the empire and applies specific offsets per planet/resource to maintain balanced growth. Target levels are calculated as X + offset.
