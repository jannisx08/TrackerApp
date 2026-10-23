# Tracker4Life

Eine einfache Web-App (PWA) für Fußball, Fitness und Ernährung. Läuft im Browser, lässt sich als App auf den Home-Bildschirm legen und funktioniert offline. Alle Daten bleiben lokal auf dem Gerät.

## Design

Glas-Design mit weichen Farbverläufen im Hintergrund, halbdurchsichtigen Karten und schwebender Menüleiste. Es gibt einen Hell- und einen Dunkelmodus, die App folgt der Einstellung des Geräts. Die Settings erreichst Du über den runden Button oben rechts.

## Funktionen

**Tageseintrag**
- Trainingsarten: Gym (Sätze, Dauer optional), Fußballtraining (Dauer, Intensität 1–5), Spiel (Dauer), Fahrrad fahren (2 von 3: Dauer, Speed, Distanz, das Dritte wird berechnet)
- Eigene Sportarten selbst anlegen
- Schlaf, Energie (1–5), Alltagsaktivität (1–5) und Notizen

**Essen**
- Lebensmittel mit Nährwerten pro Einheit (z. B. 100 g, 100 ml, 1 Stück) speichern
- Menge als Faktor eintragen (z. B. 0,783), kcal und Protein werden berechnet
- Tagessumme, Auswahl nach Datum

**Wiegen**
- Gewicht mit Zeitstempel
- Angabe, ob vorher gegessen oder getrunken wurde (dann Pflichtfeld "Was?")
- Gewichtskurve (nüchterne Messungen ausgefüllt, andere hohl)

**Gym-Tracker**
- Eigene Übungen und Workouts
- Sätze mit Wiederholungen und optional kg eintragen
- Satzpausen-Stoppuhr startet automatisch nach jedem Satz
- Pause-Button für das ganze Training, Haken "Übung fertig", Übungen im Training oder aus dem Workout entfernen
- Bei jeder Übung wird das letzte Ergebnis direkt angezeigt, egal in welchem Workout; Antippen zeigt den gesamten Verlauf
- Nach "Training beenden" werden Sätze und geschätzte Dauer ("mind. X Min") automatisch in den Tageseintrag übernommen

**Verlauf**
- Nach Tagen gruppiert, Trainings und Gym-Einheiten eingeklappt, Details beim Antippen
- Gym-Einheiten nachträglich bearbeiten: Sätze, Wdh, kg und Übungen ändern, hinzufügen oder entfernen

**Settings**
- Notizen pro Workout, Übung und Satz einzeln aktivierbar, Notizen vom letzten Mal werden beim nächsten Training angezeigt
- Wdh-Bereich (z. B. 8-9) und Teile pro Satz (mehrere Wdh/kg-Paare, z. B. Bizeps Giant)
- Gewichtstracking (Wiegen-Tab) ein- und ausblendbar

**Kalorienverbrauch (optional, Settings, mit Admin-Passwort)**
- MET-Wert pro Sportart festlegen, Verbrauch pro Training, pro Tag und in den Stats der letzten 7 Tage
- Körpergewicht = Durchschnitt der letzten bis zu 7 Tage mit Messung

**Sonstiges**
- Alles bearbeitbar und löschbar
- Auswertung der letzten 7 Tage mit regelbasierten Erkenntnissen
- Export und Import aller Daten als JSON-Datei

## Dateien

| Datei | Zweck |
|---|---|
| `index.html` | Die komplette App (HTML, CSS, JavaScript) |
| `manifest.webmanifest` | Name, Icon und Anzeige als App |
| `sw.js` | Service Worker für den Offline-Modus |
| `icon-192.png`, `icon-512.png` | App-Icons |

## Installation (GitHub Pages)

1. Öffentliches Repository erstellen und alle Dateien in den Hauptordner hochladen
2. **Settings → Pages → Deploy from a branch → `main` / `(root)` → Save**
3. Die Adresse `https://DEINNAME.github.io/REPONAME/` in Safari öffnen
4. **Teilen → Zum Home-Bildschirm**

## Updates

Neue `index.html` im Repository hochladen (gleicher Name überschreibt die alte) und committen. Die App danach ein- bis zweimal neu öffnen. Die gespeicherten Daten bleiben erhalten.

## Daten und Datenschutz

- Alle Einträge liegen im lokalen Speicher des Browsers (`localStorage`) auf dem eigenen Gerät
- Es werden keine Daten an einen Server gesendet
- Der Browser-Speicher kann in seltenen Fällen geleert werden. Deshalb regelmäßig **Verlauf → Exportieren** nutzen und die Datei sichern

## Hinweis

Die Auswertungen und Hinweise zu Training, Schlaf und Ernährung sind allgemeine Orientierungen und ersetzen keine medizinische oder ernährungswissenschaftliche Beratung.

## Ideen für später

- Verpackung als native iOS-App (z. B. mit Capacitor) mit Benachrichtigung für die Satzpause
- Schritte aus Apple Health für die Alltagsaktivität
- KI-Auswertung der Tagebuchdaten über die Claude API
