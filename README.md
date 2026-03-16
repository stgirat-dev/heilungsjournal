# 🌿 Heilungsjournal · Andreia

**Version 2.9.2** · Persönliches Heilungsjournal nach anteriorer Densschrauben-Fixation (Typ IIc)
**OP:** 19. März 2026 · Dr. med. Ladislav Mica · USZ Zürich

🔗 **Live App:** [stgirat-dev.github.io/heilungsjournal](https://stgirat-dev.github.io/heilungsjournal)

---

## Über die App

Progressive Web App (PWA) zur Begleitung des Heilungsprozesses nach HWS-Operation. Tägliches Tracking von Schmerzniveau und Medikamenteneinnahmen, Visualisierung des Heilungsfortschritts und statistische Auswertung inkl. Medikamenten-Wirkungsanalyse.

Alle Daten werden lokal im Browser gespeichert (`localStorage`). Kein Server, kein Login, keine Cloud-Abhängigkeit. Backup/Restore über JSON-Datei (Google Drive, lokaler Download).

---

## Features

### Heute
- Aktuelle Heilungsphase mit Fortschrittsbalken (Gesamt + Phase)
- Tag als erledigt abhaken (Streak-Zähler 🔥)
- Erlaubte / verbotene Aktivitäten der aktuellen Phase
- Medikation & Orthesen-Info, Meilensteine, Hinweise
- Schnell-Schmerzeintrag direkt auf der Startseite
- Tages-Zitat, Notfall-Nummern (USZ, Sanacare)

### Phasen
- Timeline aller 6 Heilungsphasen (OP-Tag bis Volle Rückkehr)
- Pro Phase: erlaubte/verbotene Aktivitäten, Hinweise, Meilensteine, Medikation, Orthese
- Aktive Phase hervorgehoben, vergangene Phasen mit ✅ markiert

### Kalender
- Monatsansicht mit Phasenfärbung pro Tag
- Tage abhaken per Tipp
- Farbige Schmerzpunkte pro Tag (Ø-Wert, Farbskala Blau→Rot)

### Schmerztracker
- Schieberegler 0–10 mit Echtzeit-Feedback (Emoji, Beschreibung, Beispiel)
- Notiz-Feld pro Eintrag
- **Medikamenten-Log:** Tramadol (Tropfen) / Paracetamol / Ibuprofen / Anderes mit Dosis
- Erinnerungen 3–5×/Tag (Browser-Benachrichtigungen)
- Heutige Einträge (Schmerz + Medikamente) in der Seitenleiste
- 7-Tage-Verlaufsdiagramm
- **Backup → Google Drive** (Android Share-Sheet) + Restore

### Auswertung
- **KPI-Karten:** Einträge gesamt, Ø Schmerz, Median, Standardabweichung σ
- **Erweiterte Statistik:** Mean, σ, Varianz, Min, Max, IQR, Vor/Nach-OP Ø
- **Verlaufskurve:** Alle Einzelmessungen chronologisch (Vor OP blau / Nach OP orange)
- **Schmerz pro Phase:** Balkendiagramm inkl. Vor-OP Referenz
- **Tageszeit-Muster:** Ø Schmerz in 6 Zeitfenstern
- **Tagesschmerzverlauf (Fullscreen):**
  - Linearer Zeitstrahl mit Zoom & Pan (Hammer.js Touch-Gesten)
  - Schmerzpunkte farbig nach Schmerzskala, gerade Verbindungslinien, Gradient-Fill
  - Medikamenten-Dreiecke (▼) als Overlay, Tooltip bei Hover/Touch
  - Zeitbereichsfilter: 3 Tage / 7 Tage / 14 Tage / Alles
- **Vorher/Nachher:** Ø Schmerz 3h vor vs. 3h nach Einnahme pro Medikament
- **Wöchentliche Statistik:** Tabelle mit Ø, Min, Max, Trend (↓↑→)
- **Tages-Statistiken:** 14-Tage-Balkendiagramm + aufklappbare Tages-Tabelle
- **Journal:** Kombinierte Tabelle aller Schmerz- und Medikamenten-Einträge
  - Filter: Datum von/bis, Phase, Schmerzstufe ≥X, Tageszeit
  - Datum/Zeit bearbeiten · Löschen pro Eintrag · CSV-Export

### Erfolge
- 12 freischaltbare Achievements (Erster Tag, Streak-Badges, Schmerzfrei, etc.)
- Fortschrittsbalken der freigeschalteten Achievements

---

## Installation (PWA)

1. [stgirat-dev.github.io/heilungsjournal](https://stgirat-dev.github.io/heilungsjournal) in **Chrome** öffnen
2. Chrome-Menü **⋮** → **«App installieren»** oder **«Zum Startbildschirm hinzufügen»**
3. Das 🌿 Icon erscheint auf dem Homescreen — öffnet im Vollbild wie eine native App

**Offline:** Nach erstem Laden funktioniert die App vollständig ohne Internet.

---

## Tech Stack

| Technologie | Version | Verwendung |
|---|---|---|
| Vanilla HTML/CSS/JS | — | Gesamte App (kein Framework, kein Build-System) |
| [Chart.js](https://www.chartjs.org/) | 4.4.1 | Alle Diagramme |
| [Hammer.js](https://hammerjs.github.io/) | 2.0.8 | Touch-Gesten (Pinch-Zoom, Pan) |
| [chartjs-plugin-zoom](https://www.chartjs.org/chartjs-plugin-zoom/) | 2.0.1 | Zoom & Pan im Fullscreen-Chart |
| Google Fonts (Lora, DM Sans) | — | Typografie |
| localStorage | — | Datenpersistenz im Browser |
| PWA (Service Worker + Manifest) | — | App-Installation, Offline-Betrieb |
| GitHub Pages | — | Hosting (kostenlos, Auto-Deploy via Actions) |

Alle externen Bibliotheken werden von `cdnjs.cloudflare.com` geladen — kein npm, kein Build-Schritt.

---

## Dateistruktur

```
heilungsjournal/
├── index.html          # Gesamte App — HTML, CSS und JS in einer Datei (~5200 Zeilen)
├── README.md           # Diese Dokumentation
└── Backups/            # Versionierte Sicherungskopien (index_vX.Y.Z_vor_vA.B.C.html)
```

Die App ist bewusst als Single-File gehalten: kein Bundler, keine Dependencies lokal, einfach per GitHub Pages deployen.

---

## Code-Architektur (`index.html`)

Die Datei ist in folgende Abschnitte gegliedert:

| Bereich | ca. Zeile | Inhalt |
|---|---|---|
| `<head>` / CDN | 1–18 | Externe Bibliotheken, Fonts, PWA-Meta |
| CSS Design System | 20–900 | CSS-Variablen, Layout, Komponenten, Dark Mode |
| HTML Markup | ~900–1250 | Navigation, Sektionen, Modal-Overlays |
| Konstanten & Phasen | ~1250–1535 | `PHASES[]`, `APP_VERSION`, `DAY`/`HOUR` etc. |
| `PAIN_INFO[]` | ~1535 | Schmerzskala 0–10: Emoji, Label, Farbe (Blau→Rot) |
| State & Helpers | ~1550–2000 | `STATE`, `saveState()`, `getPainColor()`, Datum-Utils |
| Render-Funktionen | ~2000–2450 | Heute, Phasen, Kalender, Achievements |
| Chart-Infrastruktur | ~2450–2650 | Zoom-Reset, Zoom-Config, Fullscreen-Wrapper |
| Fullscreen-Chart | ~2651–3100 | `_buildFsMedChart()`: Zeitstrahl, Plugins, Tooltip, Range-Buttons |
| Auswertungs-Charts | ~3100–3800 | KPI, Verlauf, Phasen-Balken, Tageszeit, Statistiken |
| Med-Timeline (klein) | ~3800–4200 | `renderMedCharts()`: Kategorie-Achse, Gradient-Plugins |
| Journal & Filter | ~4200–4600 | Tabellen-Render, CSV-Export, Edit/Delete |
| Event-Listener | ~4600–5000 | Navigation, Inputs, Backup/Restore, Benachrichtigungen |
| Service Worker | ~5000+ | PWA Offline-Cache |

### Wichtige Design-Entscheide

**Schmerzfarben (`PAIN_INFO[].color`):** Einziger Eintragspunkt — alle Canvas-Plugins, Kalender, Timeline und Tabellen rufen `getPainColor(level)` auf. Farbschema ändern heisst: nur `PAIN_INFO` anpassen.

**Fullscreen-Chart vs. kleines Chart:** Zwei unterschiedliche Chart-Instanzen mit unterschiedlichen x-Achsen-Typen:
- Fullscreen (`_buildFsMedChart`): `type: 'linear'`, Timestamp-Werte (ms) — ermöglicht echten Zoom
- Klein (`renderMedCharts`): `type: 'category'`, Index-basiert — schlanker, für Überblick

**Gap-Problem bei med-only Timestamps:** Das kleine Chart hat in der Schmerz-Dataserie `null`-Werte an Zeitpunkten, wo nur Medikamente (ohne Schmerzwert) eingetragen wurden. Die Custom-Gradient-Plugins (`medGradFillPlugin`, `medGradLinePlugin`) verwenden deshalb einen `prevNonNull`-Pointer statt naiver `i → i+1` Iteration, um Lücken korrekt zu überbrücken.

**Textkontrast in Schmerzkreisen:** Level 0–6 (helle Blautöne) verwenden dunklen Text (`#1a2a3a`), Level 7–10 (dunkle Rottöne) weissen Text (`#FFFFFF`). Betrifft `plugPainCircles` (Fullscreen) und `painLabelPlugin` (klein).

---

## Datenstruktur (`localStorage: heilungsjournal_v1`)

```json
{
  "checkedDays":     { "2026-03-19": true },
  "painLogs":        [{ "date": "2026-03-19", "time": "08:00", "level": 5, "note": "..." }],
  "medLogs":         [{ "date": "2026-03-19", "time": "07:30", "med": "Tramadol", "dose": "20 Tropfen", "note": "" }],
  "reminderEnabled": true,
  "reminderTimes":   ["08:00", "12:00", "16:00", "20:00"],
  "lastBackup":      "19.03.2026 10:00"
}
```

**Backup-Format:** JSON-Datei mit obiger Struktur + `version`, `exportedAt`, `appName`.

---

## Backup & Restore

| Aktion | Weg |
|---|---|
| Backup erstellen | Schmerztracker → «☁️ Backup → Google Drive» (Android Share) |
| Backup herunterladen | Schmerztracker → «⬇ Backup als Datei» |
| Daten wiederherstellen | Schmerztracker → «📂 Backup-Datei auswählen» |

---

## Changelog

| Version | Datum | Änderungen |
|---|---|---|
| **2.9.2** | März 2026 | Farbschema Blau→Rot (Schema 2, divergierend); adaptiver Textkontrast in Schmerzkreisen |
| **2.9.1** | März 2026 | Gap-Fix kleines Chart: `prevNonNull`-Iteration in Gradient-Plugins (med-only Timestamps) |
| **2.9.0** | März 2026 | Fullscreen-Chart: gerade Linien (`tension=0`), ältester Punkt linksbündig, Medikamenten-Tooltip |
| **2.8.x** | März 2026 | Fullscreen-Zoom & Pan, Medikamenten-Dreiecke, Range-Buttons |

---

## Hinweis

Diese App dient als persönliches Orientierungstool und ersetzt **nicht** die ärztlichen Anweisungen von Dr. Mica und seinem Team.

**Notfall:** USZ Zürich +41 44 255 11 11 · Europaweiter Notruf 112

---

*Entwickelt mit Claude Sonnet (Anthropic) · März 2026 · [@stgirat-dev](https://github.com/stgirat-dev)*
