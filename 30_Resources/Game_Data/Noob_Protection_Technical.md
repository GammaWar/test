---
category: [technik, spielmechanik]
type: mechanik
confidence: high
source_type: discord_chat
game_version: "unknown"
tags: [noobschutz, outlaw, combat_rules, mechanics]
related: ["[[30_Resources/Game_Data/Combat_Strategy_Technical|Combat Strategy Technical]]"]
sources: ["discord"]
created: 2024-05-23
updated: 2024-05-23
---

# Noobschutz & Outlaw-System (Technische Spezifikation) & Kurzbeschreibung
Dokumentation des Systems zur Protektion schwächerer Spieler und der Konsequenzen bei Regelverstößen.

## Basisdaten

| Parameter | Wert / Regel | Beschreibung |
| :--- | :--- | :--- |
| **Angriffsgrenze** | $10\times$ Zielpunkte | Ein Angriff wird blockiert, wenn der Angreifer mehr als das 10-fache der Punkte des Ziels besitzt. |
| **Outlaw-Status** | Aktiv bei Verstoß | Bei einem bestätigten Angriff außerhalb der Schutzgrenzen erhält der Angreifer den Outlaw-Status. |
| **Flottenpunkt-Wert** | 1.000 Rohstoffe | Umrechnungsfaktor für die Berechnung von Flottenpunkten. |

## Mechanik / Verhalten

### 1. Noobschutz (Protection)
Das System verhindert, dass hoch entwickelte Spieler ("Whales" oder Top-Spieler) gezielt neue oder sehr schwache Spieler terrorisieren. 
* **UI-Hinweis:** Im Spiel wird ein geschützter Spieler durch ein spezielles Icon/Marker gekennzeichnet.
* **Fehlermeldung:** Versucht ein zu starker Spieler anzugreifen, wird eine Fehlermeldung ausgegeben (aktuell in der Entwicklung zur Lokalisierung).

### 2. Outlaw-System
Wenn ein Angriff die Schutzgrenzen überschreitet, greift das Outlaw-System:
* **Konsequenz:** Der Angreifer erhält einen Status, der ihn als Regelbrecher markiert.
* **Dauer:** Die Dauer des Outlaw-Status ist systemseitig festgelegt (siehe `outlaw_duration`).

### 3. Fremde Flottenpunkte (Foreign Fleet Points)
Um das Horten von Macht durch die Zerstörung anderer zu verhindern, gibt es eine Regelung für fremde Flottenpunkte:
* Ein Spieler darf nur einen maximalen Prozentsatz seiner eigenen Punkte als "fremde Flottenpunkte" (Punkte von anderen Spielern, die er kontrolliert) halten.
* **Beispiel:** Bei 50.000 Punkten und einer 10%-Regel sind höchstens 5.000 Flottenpunkte von anderen Spielern erlaubt.

## Strategie
* **Für neue Spieler:** Der Noobschutz bietet eine sichere Phase für den Aufbau der ersten Infrastruktur (Metallminen, Klontanks).
* **Für Angreifer:** Wer expandieren will, muss die Punktedifferenz im Auge behalten, um nicht in den Outlaw-Status zu geraten.

## Verknüpfungen
- [[30_Resources/Game_Data/Combat_Strategy_Technical|Combat Strategy Technical]]

## Changelog
- 2024-05-23: Datei neu erstellt basierend auf Discord-Entwickler-Diskussionen und technischen Spezifikationen.
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Technische Spezifikation des Noobschutz-Systems. Schutzgrenze bei $10\times$ Punktedifferenz. Verstöße führen zum Outlaw-Status. 1 Flottenpunkt = 1000 Rohstoffe. Regelung für maximale fremde Flottenpunkte zur Vermeidung von Machtkonzentration.
