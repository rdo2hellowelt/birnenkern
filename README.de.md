# birnenkern

[English](README.md) · **Deutsch**

![Beispielblatt: erfundene Probe Ende zu Ende der Ausleihe einer Stadtbibliothek](docs/beispiel-probe.png)

**Birne ist ein Skill für Claude Code, der zeichnet.** Aus einem Stoff, etwa einem Aufbau mit seinen Wegen,
einem Ablauf mit Zeitpunkten, einer Probe oder einem Projektstand, wird ein technisches Blatt nach DIN:
Tusche auf Weiß, Rahmen mit Zonen und Mittenmarken, kleines Schriftfeld unten rechts, Linienarten statt
Farbe, Beschriftung in DIN 1451, Kanten leicht überzeichnet, Texte im Blocksatz.

Bausteine sind Draufsicht, Schnitt, Detail, Explosionsansicht, Zeitachse und Tabellen. Jede Zahl hat eine
Quelle. Rollen statt Namen. Keine erfundenen Maße.

## Einbauen

```text
/plugin marketplace add rdo2hellowelt/birnenkern
/plugin install birne@birnenkern
```

Dann `birne` tippen und dazu, was aufs Blatt soll und woher der Stoff kommt. Das Blatt landet als
`birne-<thema>-<datum>.html` im Arbeitsordner und öffnet sich im Browser. Braucht nur einen Browser; ohne
DIN 1451 lädt das Blatt Barlow Semi Condensed von Google Fonts.

## Birne und Apfel

[Apfel](https://github.com/rdo2hellowelt/apfelkern) prüft Arbeitsdialoge und zeichnet seine Befunde auf
demselben Blatt. Das Plugin apfel trägt eine Kopie von Birne, wer Apfel hat, hat beide. Geändert wird nur
hier, die Kopie in Apfel wird nachgezogen.

## Lizenz

MIT, siehe [LICENSE](LICENSE). Das Zeichenwerkzeug folgt
[dimensional-drawing](https://github.com/enesozturk/dimensional-drawing) von Enes Ozturk (MIT).
