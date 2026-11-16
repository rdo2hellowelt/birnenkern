# Quellen

| Was | Herkunft | Lizenz |
|---|---|---|
| Block WERKZEUG in `assets/blatt-vorlage.html` | nach „dimensional-drawing“ von Enes Ozturk, https://github.com/enesozturk/dimensional-drawing, über den Skill apfel (Befundzeichnung seit 07.11.2026) | MIT, `LICENSES/MIT-enesozturk-dimensional-drawing.txt` |
| Block BLATT, Rahmen, Schriftfeld, Legende, Blocksatz, Tusche | eigen, 13.11.2026 | MIT, `LICENSE` |
| Block BUNT in `assets/blatt-vorlage.html`, Muster `assets/beispiel-bunt.html` | eigen, 16.11.2026 | MIT, `LICENSE` |
| Schrift Yuji Syuku für Pinselzeichen | Google Fonts, wird beim Öffnen geladen, nicht mitgeliefert | SIL Open Font License 1.1 |
| Normen in `references/din.md` | DIN EN ISO 5457, 7200, 128, 3098, DIN 1451, DIN 1356-1, nur sinngemäß | |

## Kopie in Apfel

Das Plugin apfel (https://github.com/rdo2hellowelt/apfelkern) trägt diesen Ordner als `skills/birne`, Datei für Datei
gleich. Geändert wird nur hier. Danach im Ordner apfelkern nachziehen und prüfen:

```sh
rsync -a --delete ../birnenkern/skills/birne/ skills/birne/
diff -r ../birnenkern/skills/birne skills/birne && echo gleich
```

## Vorlage und Beispiel bunt

Beide tragen dieselben Blöcke WERKZEUG, BLATT und BUNT, nur Titel, `aria-label` und Block ZEICHNUNG sind anders.
Prüfen im Ordner `assets`:

```sh
diff <(sed -e '1d' -e '/aria-label=/d' -e '/===== ZEICHNUNG/,$d' blatt-vorlage.html) \
     <(sed -e '1d' -e '/aria-label=/d' -e '/===== ZEICHNUNG/,$d' beispiel-bunt.html) && echo gleich
```

## Änderungen

- **16.11.2026, 1.2.0.** Modus „Bunt und in Farbe“: `modus('bunt')` gleich nach `rahmen()`, Grund bleibt
  Schwarz-Weiß. Block BUNT mit Copic, Schraffur, Erdreich, Bäumen, Figuren als Rollen, Hund, Nordstern, zehn Icons,
  Titel mit Icon, Fenster, Schnittlinie, Weg, Maßkette, Koten, Positionsnummern, Pinsel, Ensō und Siegel. Ohne Modus
  zeichnen dieselben Bausteine in Grau. Ansicht, Grundriss, Schnitt und Werkstück nach DIN 1356-1 in
  `references/din.md`. Muster `assets/beispiel-bunt.html`, Bild `docs/beispiel-bunt.png`, Entwürfe als Kontaktabzug
  in `docs/entwuerfe/`. Zwei Prüffälle dazu.

- **13.11.2026, 1.1.0.** `sprache('en')` für englische Blätter: Hinweise, Allgemeine Hinweise und Schriftfeld.
  Prüffälle in `evals/evals.json`. Ungenutztes CSS aus Apfels früherem HTML-Kopf entfernt. Interne Unterlagen heißen
  in der Tabelle Quellen „intern“. Icon für das Plugin (`.claude-plugin/icon.png`).
- **13.11.2026, veröffentlicht als birnenkern 1.0.0.** Muster auf eine erfundene Probe umgestellt (Ausleihe einer
  Stadtbibliothek), Links auf example.org. Schriftfeld ohne voreingestellte Abteilung, die Marke kommt über `abt`.
  Apfel trägt eine Kopie und zeichnet seine Befunde damit, statt eines eigenen Blatts.
- **13.11.2026, angelegt.** Stil: keine Rundungen, Kanten leicht überzeichnet, dünne Linien, Blocksatz, Rahmen mit
  Zonen, kleines Schriftfeld unten rechts statt Kopf oben, eher Maschinenbau, Architektur, Elektro als Werkplan.
  Eigenes Paket neben Apfel.
