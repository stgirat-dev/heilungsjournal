# 🌿 Heilungsjournal · Andreia

Persönliches Heilungsjournal nach anteriorer Densschrauben-Fixation (Typ IIc)  
**OP:** 19. März 2026 · Dr. med. Ladislav Mica · USZ Zürich

🔗 **Live App:** [stgirat-dev.github.io/heilungsjournal](https://stgirat-dev.github.io/heilungsjournal)

---

## 📋 Über die App

Eine Progressive Web App (PWA) zur Begleitung des Heilungsprozesses nach Halswirbelsäulen-Operation. Die App ermöglicht das tägliche Tracking von Schmerzniveau und Medikamenteneinnahmen, visualisiert den Heilungsfortschritt und liefert eine statistische Auswertung — inklusive Medikamenten-Wirkungsanalyse.

Alle Daten werden lokal im Browser gespeichert (localStorage). Kein Server, kein Login, keine Cloud-Abhängigkeit.

---

## ✨ Features

### 🏠 Heute
- Aktuelle Heilungsphase mit Fortschrittsbalken (Gesamt + Phase)
- Tag als erledigt abhaken (Streak-Zähler 🔥)
- Erlaubte / verbotene Aktivitäten der aktuellen Phase
- Medikation & Orthesen-Info, Meilensteine, Hinweise
- Schnell-Schmerzeintrag direkt auf der Startseite
- Tages-Zitat, Notfall-Nummern (USZ, Sanacare)

### 🗺 Phasen
- Timeline aller 6 Heilungsphasen (OP-Tag bis Volle Rückkehr)
- Pro Phase: erlaubte/verbotene Aktivitäten, Hinweise, Meilensteine, Medikation, Orthese
- Aktive Phase hervorgehoben, vergangene Phasen mit ✅ markiert

### 📅 Kalender
- Monatsansicht mit Phasenfärbung pro Tag
- Tage abhaken per Tipp
- Farbige Schmerzpunkte pro Tag (Ø-Wert)

### 📊 Schmerztracker
- Schieberegler 0–10 mit Echtzeit-Feedback (Emoji, Beschreibung, Beispiel)
- Notiz-Feld pro Eintrag
- **💊 Medikamenten-Log:** Tramadol (Tropfen) / Paracetamol / Ibuprofen / Anderes mit Dosis
- Erinnerungen 3–5×/Tag (Browser-Benachrichtigungen)
- Heutige Einträge (Schmerz + Medikamente) in der Seitenleiste
- 7-Tage-Verlaufsdiagramm
- **☁️ Backup → Google Drive** (Android Share-Sheet) + Restore

### 📈 Auswertung
- **KPI-Karten:** Einträge gesamt, Ø Schmerz, Median, Standardabweichung σ
- **Erweiterte Statistik:** Mean, σ, Varianz, Min, Max, IQR, Vor/Nach-OP Ø
- **Verlaufskurve:** Alle Einzelmessungen chronologisch (Vor OP blau / Nach OP orange)
- **Schmerz pro Phase:** Balkendiagramm inkl. Vor-OP Referenz
- **Tageszeit-Muster:** Ø Schmerz in 6 Zeitfenstern
- **Medikamenten-Wirkung:**
  - Zeitstrahl mit Schmerzpunkten + Medikamenten-Dreiecken (▼)
  - Vorher/Nachher: Ø Schmerz 3h vor vs. 3h nach Einnahme pro Medikament
- **Wöchentliche Statistik:** Tabelle mit Ø, Min, Max, Trend (↓↑→)
- **Tages-Statistiken:** 14-Tage-Balkendiagramm + aufklappbare Tages-Tabelle (Ø, Median, σ)
- **📓 Journal:** Kombinierte Tabelle aller Schmerz- und Medikamenten-Einträge
  - Filter: Datum von/bis, Phase, Schmerzstufe ≥X, Tageszeit
  - ✏️ Datum/Zeit bearbeiten · 🗑 Löschen pro Eintrag
  - ⬇ CSV-Export für Arzt / Physiotherapie

### 🏅 Erfolge
- 12 freischaltbare Achievements (Erster Tag, Streak-Badges, Schmerzfrei, Ferien Meran, etc.)
- Fortschrittsbalken der freigeschalteten Achievements

---

## 🚀 Installation (PWA auf Android)

1. [stgirat-dev.github.io/heilungsjournal](https://stgirat-dev.github.io/heilungsjournal) in **Chrome** öffnen
2. Chrome-Menü **⋮** → **«App installieren»** oder **«Zum Startbildschirm hinzufügen»**
3. Das 🌿 Icon erscheint auf dem Homescreen — öffnet im Vollbild wie eine native App

**Offline:** Nach erstem Laden funktioniert die App vollständig ohne Internet.

---

## 🛠 Tech Stack

| Technologie | Verwendung |
|---|---|
| Vanilla HTML/CSS/JS | Gesamte App (kein Framework) |
| [Chart.js 4.4.1](https://www.chartjs.org/) | Alle Diagramme |
| localStorage | Datenpersistenz im Browser |
| PWA (Service Worker + Manifest) | App-Installation, Offline |
| Google Fonts (Lora, DM Sans) | Typografie |
| GitHub Pages | Hosting (kostenlos) |

---

## 📁 Dateistruktur

```
heilungsjournal/
├── index.html    # Gesamte App — HTML, CSS und JS in einer Datei
└── README.md     # Diese Dokumentation
```

---

## 💾 Datenstruktur (localStorage: `heilungsjournal_v1`)

```json
{
  "checkedDays":     { "2026-03-19": true },
  "painLogs":        [{ "date": "2026-03-14", "time": "08:00", "level": 5, "note": "..." }],
  "medLogs":         [{ "date": "2026-03-14", "time": "07:30", "med": "Tramadol", "dose": "20 Tropfen", "note": "" }],
  "reminderEnabled": true,
  "reminderTimes":   ["08:00", "12:00", "16:00", "20:00"],
  "lastBackup":      "14.03.2026 10:00"
}
```

**Backup-Format:** JSON-Datei mit obiger Struktur + `version`, `exportedAt`, `appName`.

---

## 🔄 Backup & Restore

| Aktion | Weg |
|---|---|
| Backup erstellen | Schmerztracker → «☁️ Backup → Google Drive» (Android Share) |
| Backup herunterladen | Schmerztracker → «⬇ Backup als Datei» |
| Daten wiederherstellen | Schmerztracker → «📂 Backup-Datei auswählen» |

---

## ⚠️ Wichtiger Hinweis

Diese App dient als persönliches Orientierungstool und ersetzt **nicht** die ärztlichen Anweisungen von Dr. Mica und seinem Team.

**Notfall:** USZ Zürich +41 44 255 11 11 · Europaweiter Notruf 112

---

*Entwickelt mit Claude Sonnet (Anthropic) · März 2026 · [@stgirat-dev](https://github.com/stgirat-dev)*
