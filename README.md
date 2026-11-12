# KVR II

Trainer für die **Kollisionsverhütungsregeln (KVR)** als Vorbereitung auf die
Prüfung zum Sportseeschifferschein (SSS). Die App fragt Regelnamen, Teile und
Nummern ab. Falsche Antworten kommen in derselben Runde nochmals, höchstens
zweimal.

Die App läuft ohne Server, ohne Anmeldung und nach dem ersten Aufruf auch
ohne Netz. Gestaltung übernommen aus dem SSS-Trainer Seemannschaft.

---

## Auf GitHub veröffentlichen

1. Auf GitHub ein neues Repository anlegen, z. B. `kvr-ii`.
2. **Add file → Upload files** wählen und den **Inhalt** dieses Ordners
   hineinziehen: `index.html`, `manifest.webmanifest`, `sw.js`, `README.md`,
   `.nojekyll` und den Ordner `icons`. Dann **Commit changes**.
   Hinweis: `.nojekyll` ist eine versteckte Datei. Auf dem Mac blendet
   **Cmd + Shift + .** sie im Finder ein. Fehlt sie, läuft die App trotzdem.
3. Im Repository **Settings → Pages** öffnen. Unter **Build and deployment**
   als Quelle **Deploy from a branch** wählen, Branch **main**, Ordner
   **/ (root)**, speichern.
4. Nach ein bis zwei Minuten ist die App erreichbar unter
   `https://<benutzername>.github.io/kvr-ii/`.

Alle Pfade sind relativ, die App läuft deshalb auch in einem Unterordner.

## Als App installieren

- **iPhone/iPad**: Adresse in Safari öffnen → Teilen → „Zum Home-Bildschirm“.
- **Android**: in Chrome öffnen → Menü ⋮ → „App installieren“.
- **Desktop (Chrome/Edge)**: Installations-Symbol rechts in der Adresszeile.

Nach dem ersten Aufruf liegt alles auf dem Gerät. Die App startet dann auch
im Flugmodus.

## Örtlich ausprobieren

`index.html` doppelklicken. Die Datei ist in sich geschlossen: Stylesheet,
Programm und alle Regeln stecken darin. Installation und Offlinebetrieb
funktionieren erst über eine Webadresse (GitHub Pages oder z. B.
`python3 -m http.server 8080` in diesem Ordner).

---

## Übungen

| Übungsart                 | Angezeigt                                   | Eingabe                                            |
| ------------------------- | ------------------------------------------- | -------------------------------------------------- |
| Name eingeben             | Teil (mit Namen, bei Teil B mit Abschnitt) und Nummer | Name der Regel (Freitext)                |
| Teil und Nummer bestimmen | Name der Regel                              | Teil aus Liste (A–F) und Nummer                    |
| Gemischt                  | pro Frage zufällig eine der beiden Arten    | Wiederholungen behalten die Art des Fehlversuchs   |

**Bereich**: Teil A, Teil B, Teil C (Auswahl), Teil D (Auswahl) oder alle
gemischt. **Anzahl**: 10, 15, 20, 25 oder alle. Anzahlen, die grösser als der
gewählte Bereich sind, sind ausgegraut.

**Fragenset (27 Regeln)**: alle Regeln aus Teil A (1–3) und Teil B (4–19),
dazu Regel 23, 24, 25, 26, 27, 30, 35 und 36.

**Sonderfälle**, zusätzlich zur normalen Eingabe:

- **Regel 5 Ausguck**: vollständiger Regeltext.
- **Regel 6 Sichere Geschwindigkeit**: erster Absatz („Jedes Fahrzeug … Bedingungen entspricht.“).
- **Regel 12 Segelfahrzeuge**: Buchstabe a mit den Ziffern i, ii, iii in Stichworten.
- **Regel 17 Maßnahmen des Kurshalters**: Prüfungsfrage „Erklären Sie den Begriff
  Kurshalter und wie Sie sich verhalten, wenn ein anderes Fahrzeug seiner
  Ausweichpflicht nicht nachkommt“. Fünf Felder in fester Reihenfolge:
  Begriff, dann 1) Kurs und Geschwindigkeit beibehalten, 2) mindestens 5 kurze
  Töne, 3) darf selbst manövrieren, 4) muss manövrieren, um den Zusammenstoß
  zu vermeiden.

## Bewertung

| Eingabe                | Richtig, wenn …                                                                                   |
| ---------------------- | ------------------------------------------------------------------------------------------------- |
| Regelname              | gleich bis auf Gross/Klein, Umlaute, ß/ss, Satz- und Leerzeichen; 1 Tippfehler (bis 10 Zeichen), sonst 2 |
| Teil + Nummer          | beide stimmen. „Anwendung“: Regel 1, 4, 11 sowie 20 und 40 gelten alle                              |
| Regeltext (Regel 5, 6) | Wortübereinstimmung ≥ 90 % (2 · gemeinsame Wörter / Wörter Soll + Eingabe), muß/muss gleich        |
| Stichworte (Regel 12)  | je Ziffer alle Schlüsselbegriffe erkannt                                                           |
| Stichworte (Regel 17)  | je Feld alle Schlüsselbegriffe erkannt; jedes Feld wird für sich geprüft, die Reihenfolge zählt    |

Alle Teile einer Frage müssen stimmen. Mit „Doch richtig“ lässt sich die
Automatik überstimmen.

**Hinweis** zeigt einen kurzen Tipp (Übung 1: Stichwort aus der Regel,
Übung 2: Nummernbereich, Regel 5/6: Textanfang, Regel 12/17: Tipp je Feld).
**Lösen** zeigt die Lösung. Nach jeder Antwort öffnet **i** die ganze Regel.

**Wiederholung**: Falsch, gelöst oder übersprungen: Die Frage wird frühestens
nach drei anderen Fragen wieder gestellt, höchstens zweimal. Danach bleibt sie
offen und erscheint im Ergebnis. „Fehler nochmals üben“ startet eine Runde nur
mit diesen Regeln.

---

## Lernstand und Auswahl

Die App speichert im Browser (`localStorage`, Schlüssel `kvr2.lernstand`) für
jede Regel **getrennt nach Übungsart** („r5:1“ Name, „r5:2“ Teil und Nummer),
wie oft und in welcher Runde sie zuletzt gefragt wurde, und die Ergebnisse der
letzten fünf **ersten** Versuche je Runde (richtig und „Doch richtig“ 1,
falsch, gelöst und übersprungen 0).

Ist die Anzahl kleiner als der Bereich, wird gewichtet ausgewählt:

- Noch nie gefragte Regeln kommen zuerst.
- Danach: Priorität = Runden seit dem letzten Abfragen × Gewicht (1 bei
  zuletzt immer richtig bis 4 bei immer falsch). Schwache Regeln kommen
  dadurch etwa dreimal so oft wie sichere.
- Keine Regel setzt länger als 3 × (Bereich ÷ Anzahl, aufgerundet) Runden aus.
- **Gemischt**: Je Regel wird die Übungsart mit der höheren Priorität gestellt,
  also die schwächere oder länger nicht geübte. Das gilt auch bei „Alle“.
- „Fehler nochmals üben“ stellt jede Regel in der Übungsart des Fehlversuchs.

Das Balkensymbol oben rechts öffnet die Ansicht **Fortschritt** mit je einem
Kachelraster pro Übungsart (grün sicher ab 80 %, gelb ab 40 %, rot darunter,
grau neu). Darunter: Lernstand ausgeben, einlesen und nach Rückfrage löschen.
Auf der Startseite steht eine Kurzübersicht je Übungsart.

## Aufbau

```
index.html             Die ganze App: Stylesheet, Programm, Regeldaten (JSON-Block)
manifest.webmanifest   Angaben für die Installation als App
sw.js                  Offlinebetrieb
icons/                 App-Symbole (192, 512, maskable, Apple) und Vorlage icon.svg
.nojekyll              GitHub soll die Dateien unverändert ausliefern
```

## Regeln bearbeiten

Die Regeln stehen in `index.html` im Block
`<script id="kvr-daten" type="application/json">`. Je Regel:

```json
{
  "id": "r5", "nr": 5, "name": "Ausguck", "teil": "B", "abschnitt": "I",
  "text": [[0, "", "Jedes Fahrzeug muss jederzeit …"]],
  "hinweisName": "Sehen und Hören",
  "hinweisNr": "Regelnummer zwischen 4 und 10",
  "volltext": { "art": "ganz", "auftrag": "…", "soll": "Jedes Fahrzeug …" }
}
```

- **`text`**: Blöcke `[Ebene, Marke, Text]`. Ebene 0 = Absatz, 1 = Buchstabe
  (`a)`), 2 = Ziffer (`i)`). Ein Buchstabe ohne eigenen Text (`["f)", ""]`)
  wird mit der folgenden Ziffer zusammen angezeigt.
- **`volltext`** (Regel 5, 6) und **`stichpunkte`** (Regel 12, 17) steuern die
  Sonderfälle. Bei `stichpunkte` hat jedes Feld `elemente` mit `treffer`
  (Wörter oder Wortfolgen; `^wort` = Wortanfang, `=wort` = ganzes Wort).
  Freiwillig: `titel` (Überschrift der Lösung), je Feld `label`
  (Beschriftung des Eingabefelds) und `ebene` (1 oder 2, Einzug in der Lösung).

Nach einer Änderung in `sw.js` die Zeile `const BESTAND = "kvr2-v3";`
hochzählen (`v3`, `v4` …), damit installierte Apps die neue Fassung laden.

## Datengrundlage

Kollisionsverhütungsregeln (KVR), Anlage zu § 1 der Verordnung zu den
Internationalen Regeln von 1972 zur Verhütung von Zusammenstößen auf See.
Fassung ELWIS, Wasserstraßen- und Schifffahrtsverwaltung des Bundes,
Stand 17. Dezember 2021 (zuletzt geändert durch Art. 1 der Verordnung vom
7. Dezember 2021, BGBl. I S. 5188). Regelnamen und Texte sind wörtlich
übernommen, mit zwei korrigierten Tippfehlern der Vorlage:

- **Regel 12 a**: „auweichen“ → „ausweichen“
- **Regel 25 c**: „Buchtabe“ → „Buchstabe“

## Datenschutz

Keine Übertragung, kein Tracking. Gespeichert werden nur die zuletzt gewählten
Einstellungen (Übungsart, Bereich, Anzahl) und der Lernstand im `localStorage`
des Browsers.
