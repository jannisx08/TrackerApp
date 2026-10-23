# Projektstand: Tracker4Life

## Ziel
Der Name der App ist **Tracker4Life** (früher "Fortschrittstagebuch"). Eine eigene Tagebuch-App für Fußball, Fitness und Ernährung (Stil ähnlich PerformAll, aber besser). Läuft als PWA auf dem iPhone, später evtl. als native iOS-App (Capacitor). Nutzer ist Anfänger, Sprache Deutsch, Anrede "Du".

## Technik
- Eine einzige Datei `index.html` (HTML, CSS, JavaScript ohne Frameworks)
- Daten im `localStorage` (Schlüssel `fortschrittstagebuch_v1` plus Suffixe `_w`, `_m`, `_f`, `_x`, `_wo`, `_s`, `_c`, `_a`, `_set`)
- Weitere Dateien: `manifest.webmanifest`, `sw.js` (Service Worker, network-first), `icon-180.png`, `icon-192.png`, `icon-512.png`, `README.md`
- Hosting: GitHub Pages (öffentliches Repository `fortschrittstagebuch`, Name im Repo bleibt wie er ist, damit die Adresse gleich bleibt)
- Die localStorage-Schlüssel behalten das alte Präfix `fortschrittstagebuch_v1`, damit bestehende Daten erhalten bleiben (nie umbenennen ohne Migration)
- Updates: neue `index.html` im Repo hochladen und committen
- Keine KI-Funktion eingebaut (Auswertung ist regelbasiert)

## Design (freigegeben): Glas / Aurora
- Dunkel (Standard bei Dunkelmodus): nachtviolett mit weichen Farbverläufen (Violett, Türkis, Rosa), halbdurchsichtige Glas-Karten (backdrop-filter), Verlauf Violett -> Türkis für Buttons, Haken und aktiven Tab; Hell: Lavendel-Hintergrund, weiße Glas-Karten
- Farben als CSS-Variablen in `:root` (`--bg --card --tx --mu --ac --acx --onac --ac2 --bd --in --g --navbg --b1..b3 --dn`), Hell/Dunkel über `prefers-color-scheme`
- Untere Leiste: schwebende Glas-Pille mit 6 Symbolen (Eintrag, Essen, Wiegen, Gym, Verlauf, Stats), nur der aktive Tab zeigt Text; Settings über den runden Button oben rechts in der Kopfzeile
- Gym-Training: Satzpause als Fortschrittsring (füllt sich über 120 Sek., dann von vorn) mit Workout-Name, Gesamtzeit und rundem Pause-Button
- App-Icon: Glas-Karte mit Checkliste und Hantel auf violett-türkisem Aurora-Hintergrund (180/192/512 px); iOS übernimmt das Icon nur beim Hinzufügen zum Home-Bildschirm
- Systemschrift statt Webfonts (Regel: alles offline in einer Datei); Icons als inline SVG; keine Emojis in der Leiste
- Frühere Varianten: Navy-Design (Sicherung `vorschau/vorschau_navy.html`, nur im Chat-Arbeitsbereich), Design-Optionen A bis J in der Design-Ansicht im Chat

## Funktionen (Stand jetzt)
- **Tageseintrag:** Training (Gym: Sätze + optional Dauer; Fußballtraining: Dauer + Intensität 1–5; Spiel: Dauer; Fahrrad: 2 von 3 aus Dauer/Speed/km; eigene Sportarten), Schlaf, Energie 1–5, Alltagsaktivität 1–5 (1 = nur liegen/sitzen, 5 = durchgehend in Bewegung), Notizen
- **Essen:** Lebensmittel mit Nährwerten pro Einheit (z. B. 100 g), Menge als Faktor (z. B. 0,783), gespeicherte Lebensmittel, Tagessumme, Auswahl nach Datum
- **Wiegen:** Zeitstempel, "schon gegessen?" mit Pflichtfeld "Was?", Gewichtskurve (nüchtern gefüllt, sonst hohl)
- **Gym-Tracker:** Übungen, Workouts, Sätze (Wdh + kg), Satzpausen-Stoppuhr (startet automatisch nach jedem Satz), letztes Ergebnis je Übung direkt sichtbar (workoutübergreifend), Antippen zeigt Verlauf, laufende Einheit bleibt gespeichert
- **Training bedienen (Patch 1.1, freigegeben):** Pause-Button (stoppt Gesamtzeit und Satzpause, übersteht Neuladen), Haken "Übung fertig" (klappt Übung auf Name + Pfeil zusammen), Übung entfernen im Training (rotes ✕ mit Rückfrage, nur dieses Training) und aus der Vorlage (✕-Chips im Workout mit Rückfrage)
- **Settings-Tab (Patch 1.2, freigegeben):** ganz rechts in der Leiste, Checkboxen: Notiz pro Workout, Notiz pro Übung (Sprechblase nach dem Dropdown-Pfeil), Notiz pro Satz, Wdh-Bereich (z. B. 8-9), Teile pro Satz, Gewichtstracking (blendet den Wiegen-Tab aus). Standard: alles aus außer Gewichtstracking
- **Notizen:** Workout-, Übungs- und Satznotiz einzeln aktivierbar; Workout- und Übungsnotizen vom letzten Training desselben Workouts werden beim Start angezeigt; Satznotizen im Verlauf sichtbar
- **Teile pro Satz:** optional 1-3 Wdh/kg-Paare pro Satz (z. B. Bizeps Giant); Auswahl nur bei aktiver Option und nur beim Anlegen/Bearbeiten einer Übung (auch im Training über "Übung bearbeiten" in der Übungskarte); bestehende mehrteilige Übungen zeigen ihre Felder auch bei ausgeschalteter Option
- **Wdh-Bereich:** Eingabe wie 8-9 wird als "8–9" gespeichert und angezeigt; Satzformat: reps, rt (Bereichstext), kg, more (weitere Teile), note, rest
- **Verlauf kompakt (Patch B, freigegeben):** nach Tagen gruppiert, neueste zuerst; Überschrift z. B. "Donnerstag 15.10.2026" mit Tageswerten (Schlaf, Energie, Alltag, kcal, Protein); darunter jedes Training/jede Gym-Einheit als eingeklappte Zeile mit Details beim Antippen; Pfeil an der Tages-Überschrift klappt Notiz sowie Eintrag bearbeiten/löschen auf; Gym-Einheiten und Tageseinträge in einer Liste (Gym-Tageseintrag mit Einheiten wird nicht doppelt angezeigt)
- **Gym-Einheiten nachträglich bearbeiten (Patch B):** Name, Dauer, Notizen, Wdh/kg je Satz inkl. Wdh-Bereich und Teile pro Satz ändern; Satz zu einer Übung hinzufügen (vorbelegt mit letztem Satz); Übung hinzufügen (auch neu anlegen); Übung entfernen (zweimal tippen); einzelne Sätze löschen; danach Sätze und "mind. X Min" im Tageseintrag neu berechnen; Löschen einer Einheit mit zweimal tippen
- **Kalorienverbrauch (Patch C, freigegeben):** in den Settings aktivierbar, nur mit Admin-Passwort (Abfrage im Tab, Passwort "admin"; das ist nur eine Sperre in der Oberfläche, kein echter Schutz, da der Code öffentlich liegt; Ausschalten geht ohne Passwort). MET-Wert je Sportart frei einstellbar (Gym, Fußballtraining, Spiel, Fahrrad, eigene Sportarten, Settings-Schlüssel `met`). Rechnung: MET x Körpergewicht x Dauer in Stunden. Körpergewicht = Durchschnitt der letzten bis zu 7 Tage mit Messung (bis zum Datum des Trainings). Gym nutzt die Dauer des Tageseintrags ("mind. X Min"). Anzeige: pro Training im Verlauf, Tagessumme als Tag, Stats (7 Tage gesamt und Ø pro Tag)
- **Gym -> Tageseintrag automatisch:** Nach "Training beenden" werden Sätze und geschätzte Dauer ("mind. X Min", 60 Sek. pro Satz, abgerundet auf 5 Min.) eingetragen
- **Bearbeiten/Löschen** fast überall (Tageseinträge, Essen, Lebensmittel, Messungen, Übungen, Workouts, Gym-Einheiten inkl. Sätze, Sätze während des Trainings)
- **Auswertung:** letzte 7 Tage, Gewichtskurve, regelbasierte Erkenntnisse
- **Export/Import** als JSON

## Bekannte Lücken / ungetestet
- Patch 1.1, 1.2, B, C und das Glas-Design nicht am echten iPhone getestet (nur im Test-Browser); backdrop-filter kann auf älteren Geräten weniger weich wirken
- Kalorien: Gym-Einheit an einem Tag mit anderem Tageseintrag (z. B. Fußball) wird nicht mitgerechnet, da nur der Tageseintrag zählt
- Nach dem Löschen der letzten Gym-Einheit eines Tages bleiben Sätze/Dauer im Tageseintrag stehen (manuell anpassen)
- Eigene Sportarten können nur gelöscht, nicht umbenannt werden
- Patch 1.2 wurde im Test-Browser (Playwright) durchgespielt, aber nicht auf einem echten iPhone
- Export-Download funktioniert in der Chat-Vorschau evtl. nicht (nur in der GitHub-Version sicher)
- Browser-Speicher kann auf iOS selten geleert werden -> regelmäßig exportieren

## Features Update 1.0
Alle geplanten Patches (1.1, 1.2, B, C) sind umgesetzt und freigegeben. Neue Wünsche: wie bisher in kleine Patches aufteilen, erst Vorschau, dann Freigabe.

## Nächste Schritte
1. GitHub-Repository fertigstellen: Dateien hochladen, Pages aktivieren, als App auf den Home-Bildschirm legen
2. App im Alltag testen, Fehler und Wünsche sammeln
3. Optional: native iOS-App mit Capacitor (Pausen-Benachrichtigung, Apple-Health-Schritte)
4. Optional: KI-Auswertung über die Claude API (braucht kleines Backend, API-Key nie im Frontend)

## Regeln für Claude
- App-Name immer **Tracker4Life** verwenden
- Antworten auf Deutsch, kurz und mobilfreundlich
- Größere Wünsche in kleine Patches aufteilen, zuerst Vorschau im Chat, erst nach "Freigeben" die fertige index.html und den aktualisierten Projektstand liefern
- Änderungen immer an der aktuellen `index.html` machen und die komplette Datei zum Hochladen bereitstellen
- Keine medizinische Beratung, nur allgemeine Hinweise
