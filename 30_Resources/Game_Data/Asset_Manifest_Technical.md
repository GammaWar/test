---
category: [ressource, technik]
type: referenz
confidence: high
source_type: code_analysis
game_version: "unknown"
tags: [assets, textures, webp, pattern_analysis]
related: []
sources: ["webpack build artifacts"]
created: 2024-05-23
updated: 2024-05-23
---

# Asset & Texture Manifest (Technische Analyse) & Kurzbeschreibung
Dokumentation der visuellen Assets (Texturen/Bilder), extrahiert aus den Webpack-Build-Artefakten. Dient als Referenz für die Benennung und Organisation von Grafiken.

## Basisdaten

| Bereich | Beschreibung |
| :--- | :--- |
| **Format** | Primär `.webp` (optimiert für Performance) |
| **Struktur** | Kategorisiert nach Objekttyp und Varianten (A-F) |
| **Ladesystem** | Dynamisches Laden basierend auf Pfad-Mustern |

## Mechanik / Verhalten

### 1. Identifizierte Einzel-Assets
Spezifische Dateien, die wichtige Spielobjekte oder UI-Elemente darstellen:
* `clonetanks.webp`: Textur für Clone Tanks.
* `metalmine_v1.webp`: Textur für Metallminen/Gebäude.
* `sensortower.webp` / `sensortower2.webp`: Texturen für Sensortürme (Überwachung/Aufklärung).

### 2. Identifizierte Schiffstypen
Schiffsklassen und deren Pfad-Muster zur Texturzuordnung:
* **Carrier Ship:** `./carrier-ship/carrier-ship*.webp`
* **Colony Ship:** `./colony-ship/colony-ship*.webp`
* **Fighter Bomber:** `./fighter-bomber/fighter-bomber*.webp`
* **Fighter:** `./fighter/fighter*.webp`
* **Geography Probe:** `./geography-probe/geography-probe*.webp`
* **Large Transporter:** `./large-transporter/large-transporter*.webp`
* **Recon Fighter:** `./recon-fighter/recon-fighter*.webp`
* **Recon Probe:** `./recon-probe/recon-probe*.webp`
* **Small Transporter:** `./small-transporter/small-transporter*.webp`
* **Spy Probe:** `./spy-probe/spy-probe*.webp`

### 3. Texture-Varianten System (Pattern Analysis)
Das Spiel nutzt ein strukturiertes Muster für die Bereitstellung von Varianten, um Objekten unterschiedliches Aussehen zu geben (z. B. Planetenoberflächen oder Skins).

| Kategorie | Pfad-Muster | Anzahl Varianten | Möglicher Bezug im Spiel |
| :--- | :--- | :--- | :--- |
| **A** | `./A/variant[1-5].webp` | 5 | Planetentyp A (Antimaterie) |
| **B** | `./B/variant[1-4].webp` | 4 | Planetentyp B (Kristall) |
| **C** | `./C/variant[1-4].webp` | 4 | Planetentyp C (Eisen) |
| **D** | `./D/variant[1-4].webp` | 4 | Planetentyp D (Mixed) |
| **E** | `./E/variant[1-4].webp` | 4 | Planetentyp E (Mixed) |
| **F** | `./F/variant[1-4].webp` | 4 | Planetentyp F (Mixed) |

## Verknüpfungen
- [[30_Resources/Game_Data.md|Game Data Index]]

## Changelog
- 2024-05-23: Datei neu erstellt basierend auf Build-Artefakten.
- 2024-05-23: Upgrade auf neues Standard-Template.

## LLM_CONTEXT
Technische Analyse der Asset-Struktur: Identifizierte Schiffstypen, Einzel-Assets und das systematische Varianten-Pattern (Kategorien A-F) für dynamisches Textur-Loading.
