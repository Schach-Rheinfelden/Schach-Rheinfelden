# ♟️ Schachverein Rheinfelden – Dokumentation & CSV-Handbuch

Dieses Handbuch erklärt ausführlich die Architektur der Website sowie alle Formatierungen, Typen und Besonderheiten für die Eingabe in die CSV-Dateien im Ordner `/data/`.

---

## 📋 Inhaltsverzeichnis
1. [Allgemeine Regeln für CSV-Dateien](#1-allgemeine-regeln-für-csv-dateien)
2. [Texte & Neuigkeiten schreiben (Ohne HTML-Tags)](#2-texte--neuigkeiten-schreiben-ohne-html-tags)
3. [Mediathek (`data/media.csv`) – Typen & Icons](#3-mediathek-datamediacsv--typen--icons)
4. [Hero-Banner & Hintergrund-Slideshow (`data/info.csv`)](#4-hero-banner--hintergrund-slideshow-datainfocsv)
5. [Bildergalerien mit Beschriftungen](#5-bildergalerien-mit-beschriftungen)
6. [Vereinsinfos, Footer & Copyright (`data/info.csv`)](#6-vereinsinfos-footer--copyright-datainfocsv)
7. [Neuigkeiten & Berichte (`data/news.csv`)](#7-neuigkeiten--berichte-datanewscsv)
8. [Termine & Kalender (`data/events.csv`)](#8-termine--kalender-dataeventscsv)
9. [Mannschaften & Spieler (`data/teams.csv` & `players.csv`)](#9-mannschaften--spieler-datateamscsv--playerscsv)
10. [Externe CSV-Quellen verknüpfen (`data/sources.csv`)](#10-externe-csv-quellen-verknüpfen-datasourcescsv)

---

## 1. Allgemeine Regeln für CSV-Dateien
* **Trennzeichen:** Das Semikolon (`;`) trennt die Spalten.
* **Leere Felder:** Wenn ein Feld leer bleiben soll, einfach nichts zwischen die Semikolons schreiben (`;;`).
* **Mehrzeilige Texte & Semikolons im Text:** Wenn ein Text Semikolons oder Zeilenumbrüche enthält, muss der gesamte Text in doppelte Anführungszeichen gesetzt werden (`"..."`).
* **Datumsangaben:** Am besten im Format `TT.MM.JJJJ` eingeben (z. B. `15.04.2026`).

---

## 2. Texte & Neuigkeiten schreiben (Ohne HTML-Tags)
Du musst **keine HTML-Tags** kennen oder schreiben! Die Website formatiert deine Texte automatisch:

* **Absätze:** Drücke einfach **zweimal Enter** (zwei Zeilenumbrüche im Textfeld/in der CSV), um einen neuen Absatz zu beginnen. Die Website macht daraus automatisch saubere Absätze mit Abstand (`<p>`).
* **Einfache Zeilenumbrüche:** Ein einzelner Zeilenumbruch (einmal Enter) wird automatisch als Zeilenumbruch (`<br>`) angezeigt.
* **Links (URLs):** Wenn du eine Internetadresse wie `https://www.schachbund.de` oder `www.lichess.org` in den Text schreibst, verwandelt die Website diese automatisch in einen klickbaren Link!
* *(Optional)* **HTML-Tags:** Wer möchte, *kann* trotzdem HTML-Tags wie `<b>fett</b>` oder `<i>kursiv</i>` verwenden – die Website erkennt und unterstützt auch das problemlos.

---

## 3. Mediathek (`data/media.csv`) – Typen & Icons
Spaltenstruktur:
```csv
id;title;date;category;type;color;url;description;thumbnail;author;emoji
```

### Unterstützte Typen in der Spalte `type`
Der eingetragene Typ bestimmt automatisch das Icon und was beim Klick passiert:

| Typ (`type`) | Icon | Verhalten beim Klick |
| :--- | :--- | :--- |
| `webseite`, `website`, `link`, `extern`, `tool` | 🌐 Webseite | Öffnet die Webseite direkt in einem **neuen Browser-Tab**. |
| `youtube` | ▶️ YouTube | Öffnet den YouTube-Player direkt im **Video-Modal** auf der Seite. |
| `vimeo` | 🟦 Vimeo | Öffnet den Vimeo-Player direkt im **Modal**. |
| `bild`, `image`, `foto` | 🖼️ Bild | Öffnet eine Großansicht (**Lightbox-Modal**) des Bildes. |
| `galerie`, `gallery`, `bilder` | 🖼️ Galerie | Öffnet ein Album-Modal mit allen Bildern zum Durchblättern. |
| `pdf`, `dokument`, `doc` | 📄 Dokument | Öffnet das PDF-Dokument in einem neuen Tab. |
| `taktik`, `puzzle`, `training` | ♟️ Taktik | Spezielles Badge für Schach-Taktiken und Trainingsseiten. |
| `lichess` | ♘ Lichess | Für Lichess-Studien oder Partien. |

---

## 4. Hero-Banner & Hintergrund-Slideshow (`data/info.csv`)
Das Feld `heroMedia` in `info.csv` steuert den großen Hintergrund ganz oben auf der Startseite:

* **Option A – Video:** Link zu `.mp4`, YouTube oder Vimeo.
* **Option B – Einzelbild:** Link zu einer Bilddatei (z. B. `img/hero.jpg`).
* **Option C – Automatische Slideshow (Mehrere Bilder):**
  Trage einfach mehrere Bild-URLs getrennt durch ein Komma (`,`) ein:
  ```csv
  heroMedia;img/turnier1.jpg, img/turnier2.jpg, img/turnier3.jpg
  ```
  👉 Die Website wechselt automatisch **alle 5 Sekunden sanft überblendend** zum nächsten Bild!

---

## 5. Bildergalerien mit Beschriftungen
In der Mediathek (`media.csv`), bei Artikeln (`news.csv`) und bei Terminen (`events.csv`) können Fotoalben hinterlegt werden.

* Trenne die Bilder mit einem Doppel-Pipe-Symbol: `||`
* Hinter jeder Bild-URL kann optional mit einem einzelnen Pipe-Symbol (`|`) eine **Bildunterschrift** stehen.

**Beispiel:**
```
https://example.com/saal.jpg | Turniersaal vor Runde 1 || https://example.com/sieger.jpg | Siegerehrung 2026
```

---

## 6. Vereinsinfos, Footer & Copyright (`data/info.csv`)
Die Datei `info.csv` hat die Spalten `keyPath;value`.

Wichtige Schlüssel:
* `clubName` – Name des Vereins (`Schach Rheinfelden`)
* `slogan` – Untertitel
* `announcement` – Banner oben auf der Seite
* `footer.copyright` – Überschreibt den Copyright-Text im Footer (z. B. `© 2027 Schach Rheinfelden. Alle Rechte vorbehalten.`)

---

## 7. Neuigkeiten & Berichte (`data/news.csv`)
Spalten:
```csv
id;title;date;category;teaser;content;author;image;gallery
```
* `teaser`: Kurzer Text für die Übersichtskarten.
* `content`: Vollständiger Artikel. Du kannst einfach normalen Text schreiben – Absätze durch doppelte Zeilenumbrüche werden automatisch formatiert!

---

## 8. Termine & Kalender (`data/events.csv`)
Spalten:
```csv
id;title;date;time;location;category;description;report;resultsUrl;gallery
```
* Termine in der Zukunft erscheinen automatisch unter **Kommende Termine**, vergangene Termine unter **Vergangene Termine**.
* `report`: Nachbericht zum Turnier.
* `resultsUrl`: Link zu offiziellen Ergebnissen (z. B. Chess-Results).

---

## 9. Mannschaften & Spieler (`data/teams.csv` & `players.csv`)
* Die `teamId` in `players.csv` verknüpft den Spieler mit der passenden Mannschaft in `teams.csv`.
* ELO, DWZ und Titel (`GM`, `IM`, `FM`) werden auf den Mannschaftsseiten elegant dargestellt.

---

## 10. Externe CSV-Quellen verknüpfen (`data/sources.csv`)
Möchtest du eine Datei extern hosten (z. B. über eine Online-URL), kannst du den Link in `data/sources.csv` eintragen:
```csv
filename;source
media.csv;https://example.com/meine-mediathek.csv
```
Bleibt `source` leer, wird die lokale CSV-Datei aus dem `/data/`-Ordner geladen.
