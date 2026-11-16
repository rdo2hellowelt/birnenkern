---
name: birne
description: |-
  Birne zeichnet. Sie macht aus einem Stoff (Aufbau mit Wegen, Ablauf mit Zeitpunkten, Probe, Befund,
  Projektstand) ein technisches Blatt nach DIN, Tusche auf Weiß: Rahmen mit Zonen und Mittenmarken
  (DIN EN ISO 5457), kleines Schriftfeld unten rechts (DIN EN ISO 7200), Linienarten statt Farbe
  (DIN EN ISO 128), Beschriftung in DIN 1451, eckig, Kanten leicht überzeichnet, Texte im Blocksatz.
  Bausteine: Draufsicht, Schnitt, Detail, Explosionsansicht, Zeitachse, Tabellen. Grund ist Schwarz-Weiß;
  auf Wunsch der Modus „Bunt und in Farbe“: Copic-Akzente, Icons vor den Titeln, Tusche dick und dünn,
  Schraffur für Tiefe, Staffage, dazu Ansicht, Grundriss, Schnitt und Werkstück wie im Bauwesen. Apfel
  zeichnet seine Befunde auf demselben Blatt. Nicht für Farbdiagramme, Dashboards, Folien oder Seiten zum Lesen.
  MUST BE USED when user says: "birne", "Birne", "birne bunt", "bunt und in farbe", "werkzeichnung", "tusche",
  "tuschezeichnung", "cad-stil", "technisches blatt", "din-zeichnung", "zeichne das als blatt".
---

# Birne

Ein Blatt zeigt, wie etwas aufgebaut ist und welchen Weg es nimmt, so wie eine Maschinenbau-, Architektur- oder
Elektrozeichnung. Die Striche tragen die Bedeutung, nicht die Farbe.

Apfel prüft, Birne zeichnet. Das Plugin apfel trägt eine Kopie von Birne in sich und zeichnet seine Befunde damit.
Geändert wird nur in birnenkern, dann die Kopie nachziehen (`QUELLEN.md`).

## Wann, wann nicht

- **Ja:** ein Zusammenhang soll auf ein Blatt. Aufbau mit Wegen, Ablauf mit Zeitpunkten, Befunde an ihrer Stelle,
  Stand eines Vorhabens mit Wartepunkten.
- **Nein:** Zahlenreihen als Diagramm, Folien, Fließtext zum Lesen. Dafür gibt es andere Werkzeuge.

## Ablauf

1. **Stoff sammeln.** Jede Zahl, jede Uhrzeit, jeder Stand hat eine Fundstelle (Protokoll, Ticket, Commit). Was nicht
   belegt ist, kommt nicht aufs Blatt.
2. **Anordnen.** Erst auf Papier oder im Kopf: Was ist die Hauptansicht, welcher Weg braucht einen Schnitt, welche
   Stelle ein Detail, gibt es eine Zeitachse. Ein Blatt, nicht mehr.
3. **Bauen.** `assets/blatt-vorlage.html` nach `birne-<thema>-<JJJJ-MM-TT>.html` kopieren, im Arbeitsordner oder wo der
   Auftrag es sagt. `<title>` setzen (ein Name aus zwei bis vier Wörtern), das
   `aria-label` am `svg` anpassen, den Block ZEICHNUNG neu schreiben. Die Blöcke WERKZEUG, BLATT und BUNT bleiben, wie
   sie sind. Das Beispiel in der Vorlage, eine erfundene Probe Ende zu Ende (Ausleihe einer Stadtbibliothek), ist
   das Muster. Für den Modus bunt ist `assets/beispiel-bunt.html` das Muster: dieselbe Probe als Haus, dieselben
   Blöcke, nur der Block ZEICHNUNG ist anders.
4. **Einmal ansehen.** Das Blatt rendern (Browser oder Headless-Chrome mit Bildschirmfoto), Überlappungen und
   Überläufe suchen, einmal nachbessern. Keine Schleife.
5. **Ausliefern.** Datei öffnen (Mac `open <datei>`, Windows `start <datei>`, PowerShell `Invoke-Item <datei>`). Wo
   Artifacts zur Verfügung stehen und das Blatt gezeigt werden soll, als privates Artifact veröffentlichen.

## Das Blatt

Raster 1700 × 1060, Zeichenfläche im Rahmen von 20 bis 1680 und 20 bis 1040. Die Reihenfolge im Block ZEICHNUNG:

```js
starten(function(){
 begin('sh1'); rahmen();                       // Blattrand, Zonen 1–8 und A–F, Mittenmarken
 sprache('en');                                // nur für ein englisches Blatt, sonst weglassen
 modus('bunt');                                // nur wenn Farbe gewünscht ist, sonst weglassen
 hinweise('(Untertitel)', ['Ziel: …', 'Steht: …', 'Offen: …']);   // oben links, Blocksatz
 /* Hauptansicht in der Mitte, Details links, Zeitachse und Schnitte unten, Tabellen rechts */
 legende(1330, y, 340, [['voll','durch'],['offen','offen'],['schraffiert','Störung'],['K','Schritt']], 'Text …');
 schriftfeld({abt, quelle, art, status, titel, zusatz, nr, massstab, refLabel, ref, aend, datum});
 tusche();                                     // als Letztes: eckig, Kanten überzeichnen
});
```

- **Schriftfeld** belegt x 1320 bis 1680, y 962 bis 1040. Darüber nichts zeichnen. Die Legende braucht rund 120 darüber;
  ist der Platz rechts voll, die Linienarten als zwei Zeilen in die Hinweise oben links schreiben.
- **Sprache:** Deutsch ohne Aufruf. `sprache('en')` gleich nach `rahmen()` stellt die festen Wörter um: Hinweise,
  Allgemeine Hinweise, alle Felder im Schriftfeld. Die eigenen Texte schreibt der Block ZEICHNUNG in derselben Sprache.
- **Hinweise oben links:** was das Blatt zeigt, was steht, was offen ist. Erst was geht, dann der Vorbehalt.
- **Hauptansicht** (Draufsicht) mit Schnittlinie A–A, wenn ein Weg zählt; der Schnitt steht unten mit denselben
  Buchstaben an den Enden.
- **Details** vergrößern eine Stelle, je Detail ein Titel mit `title(x, y, 'Detail A · …', 'Untertitel')`.
- **Zeitachse** mit fester Skala (eine Stunde gleich viele Einheiten), Störungen schraffiert, Ereignisse mit Kennung.
- **Tabellen** rechts: Schritte oder Vorschläge, Befunde mit Ticket-Links, Kennwerte, Quellen.
- **Kennungen** (`nk`) sind in Zeichnung und Tabellen dieselben.

## Linien und Flächen

| Klasse | Strich | Bedeutung |
|---|---|---|
| `obj`, `obj1` | voll, Körperkante | steht, ist durch, Bauteil |
| `hug` | voll, grau gefüllt | Bedienteil, Knopf, Feld, fester Block |
| `slot` | gestrichelt | Platzhalter, Bereich ohne Inhalt |
| `vor` | Strich-Punkt | offen, Vorschlag, Soll |
| `hat()` | schraffiert | gesperrt, Störung, fehlt, überschrieben |
| `cut` | breit | Weg im Schnitt, Sperre, Zeitachse |
| `cl` | dünn Strich-Punkt | Schnittlinie, Mittellinie |
| `dl` mit Pfeil | dünn | Fluss, Maßlinie |

Linien bleiben dünn. Nur Grau, bewusst nur hell. Farbe gibt es nur im Modus bunt.

## Modus bunt

Grund ist Schwarz-Weiß. Nur wenn der Auftrag Farbe will („bunt“, „in Farbe“, „mit Leben“, „wie ein Architekt“),
steht `modus('bunt')` gleich nach `rahmen()`. Dann gilt zusätzlich:

- **Vier Ansichten wie im Bauwesen** (DIN 1356-1, siehe `references/din.md`): **Ansicht** zeigt, wie es von außen
  aussieht und wer davor steht. **Grundriss** zeigt, wie es gebaut ist, mit Nordstern und Schnittlinie A–A.
  **Schnitt A–A** zeigt den Weg durch das Haus mit den Ebenen darüber und darunter. **Werkstück** zeigt ein Teil als
  Werkzeichnung mit Maßen, Positionsnummern und Stückliste. Zeitachse und Tabellen wie gewohnt.
- **Das Haus ist ein Bild für den Aufbau**, kein Plan. Räume sind Bausteine, die Außenwand ist die Grenze nach
  außen, Türen und Fenster sind die erlaubten Wege, Keller und Dachraum liegen darunter und darüber. Das Bild muss zum
  Stoff passen: Eine Tür gibt es nur, wo es im Stoff einen Weg gibt. In der Legende steht, dass das Haus ein Bild ist.
- **Farbe ist Akzent.** Die Linienarten gelten weiter. Rot ist der Weg und die Störung, Störungen sind zusätzlich
  schraffiert. Blau steht für Glas und Prüfung, Grün für die Umgebung, Ocker für Räume und Holz. Das Blatt muss auch
  schwarz-weiß lesbar sein: Ohne `modus('bunt')` wird jede Farbe zu Grau. Die Farben stehen in einer Zeile über der
  Legende.
- **Staffage:** Figuren sind Rollen (Leser, Betrieb, Prüfung), nie Personen. Bäume, Figuren und ein Hund geben
  Maßstab und Leben, drei bis fünf je Ansicht.
- **Titel** setzt `titel()`, linksbündig unter der Ansicht: Icon statt Emoji, Copic-Streich, Doppellinie, Untertitel
  im Akzent.
- **Tusche dick und dünn:** `k3` Boden, `k2` Ansicht, `k1` Möbel und Maße, `kh` Schraffur, `ka` Achse und
  Schnittlinie im Akzent, `kd` verdeckt und Bezug. Geschnittene Wände sind schwarz gefüllt.
- **Reihenfolge je Fläche:** weiß füllen, Copic, Schraffur, zuletzt die Kontur in Tusche.
- **Pinsel** sparsam: ein Ensō, eine Skizze. Weiß hat Platz. Keine japanischen Zeichen, keine Siegel, keine senkrechte Schrift.
- **Farbige Linien nie durch die Schrift.** Markierung eines Titels nur als dicker Copic-Schwung darunter, breiter als der Titel (macht `titel()`), nie als dünner Strich.

## Schrift und Text

- Schrift-Stapel: DIN 1451 Mittelschrift (wo installiert), DIN Alternate, Bahnschrift, Barlow Semi Condensed als
  Ersatz aus Google Fonts. Großbuchstaben über die Klassen.
- Texte über mehr als eine Zeile mit `absatz()` im Blocksatz; einzelne Zeilen mit `tx()`. Kurze Hauptsätze, keine
  Gedankenstriche.
- `starten()` wartet auf die Schrift, sonst misst der Blocksatz mit der Ersatzschrift.

## Inhalt

- Keine Namen, keine Kürzel von Personen, keine Hostnamen und keine internen Pfade. Rollen statt Personen (Betrieb,
  Prüfung). Die Marke steht im Schriftfeld unter „Verantw. Abt.“ (Feld `abt`).
- Jede Zahl mit Fundstelle, die Tabelle Quellen nennt sie. Interne Unterlagen stehen dort als „intern“.
- Keine Lücken markieren, nach denen keiner fragt. Keine Selbstkorrektur auf dem Blatt: es trägt den Stand.
- Keine erfundenen Maße. Proportionen schematisch, Zahlen nur, wenn sie belegt sind.

## Werkzeug

**WERKZEUG** (nach dimensional-drawing, MIT): `begin(id)`, `mk(tag, attr, parent)`, `tx(x, y, text, klasse, attr)`,
`rr(x, y, w, h, r, klasse)`, `hat(x, y, w, h)`, `ar(x1, y1, x2, y2, klasse)`, `dimH(x1, x2, y, e1, e2, text, opt)`,
`dimV(…)`, `callout(…)`, `nb(x, y, n)`, `slotLabel(x, y, w, h, text, ausrichtung, klasse)`, `title(x, y, titel,
untertitel)`, `detailRef(…)`, `xbox(x, y, w, h)`, `notes(liste)`, `table(x, y, titel, kopf, zeilen, breiten, ausrichtung)`.

**BLATT** (Birne): `nk(x, y, kennung)` Kästchen, das mitwächst · `zwei(x, y, w, h, a, b)` zwei Zeilen im Kasten ·
`absatz(x, y, w, text, klasse, zeilenabstand)` Blocksatz, gibt das y darunter zurück · `rahmen()` ·
`hinweise(untertitel, absätze, breite)` · `legende(x, y, w, arten, text)` mit den Arten `voll`, `offen`,
`platzhalter`, `schraffiert`, `grau` oder einer Kennung · `schriftfeld(felder)` · `sprache(code)` mit `de` oder `en` ·
`tusche()` · `starten(fn)`.

**BUNT** (Birne, Modus bunt; ohne `modus('bunt')` in Grau): `modus('bunt', keim)` · `farbe(hex)` · `akzent()` ·
Töne `FARBE.rot`, `himmel`, `salbei`, `gruen`, `ocker`, `warm`, `kuehl`, `ziegel`, `rosa`. Eine Form ist
`{r:[x, y, w, h]}`, `{k:[cx, cy, r]}` oder `{d:pfad}`.
Flächen: `copic(form, farbe, {nib, op, schraeg, quer, lagen, luecke})` Marker · `schraffur(form, {winkel, abstand,
kreuz, bereich})` · `erde(x, y, w, h)` · `imClip(form, fn)`.
Staffage: `baum(x, y, h, 'rund'|'pappel'|'nadel')` · `baumPlan(x, y, r)` · `figur(x, y, h, 'steht'|'geht', farbe,
{dir})` gibt die Hand zurück · `figurOben(x, y, s, winkel, farbe)` · `hund(x, y, s, dir)` gibt das Halsband zurück ·
`leine(hand, halsband)` · `nordstern(x, y, r)`.
Bau: `fenster(x, y, w, h, {sprossen})` · `schnittlinie(x1, y1, x2, y2, buchstabe, seite)` · `weg(punkte, {strich})` ·
`massKette(xs, y, kante, texte)` · `kote(x, y, text, bis)` · `ballon(n, x, y, px, py)` · `massstab(x, y, text, teile)`,
Zahlen nur mit Beleg.
Titel und Pinsel: `icon(name, x, y, s)` mit `ansicht`, `grundriss`, `schnitt`, `draufsicht`, `detail`, `zeit`, `werk`,
`tabelle`, `nord`, `pinsel` · `titel(x, y, icon, titel, untertitel, farbe)` · `pinsel(punkte, breite, opt)` ·
`enso(cx, cy, r)`.

Eine Gruppe verschieben, ohne jede Zahl anzufassen: `{const keep=sv; sv=mk('g',{transform:'translate(0,-36)'}); … sv=keep;}`.
`tusche()` überzeichnet auch dort richtig.

## Dateien

| Datei | Inhalt |
|---|---|
| `assets/blatt-vorlage.html` | Blatt mit WERKZEUG, BLATT, BUNT und als Muster die erfundene Probe Ende zu Ende |
| `assets/beispiel-bunt.html` | Dieselben Blöcke, als Muster dieselbe Probe im Modus bunt |
| `references/din.md` | Die Normen kurz: Blatt, Schriftfeld, Linienarten, Schrift, Bauzeichnungen |
| `evals/evals.json` | Prüffälle: wann Birne greift, wann nicht |
| `QUELLEN.md` | Herkunft, Lizenzen, Änderungen |
| `LICENSE` | MIT, für Birne selbst |
| `LICENSES/` | MIT-Text des Zeichenwerkzeugs |

## Pflege

Prüffrist 90 Tage, **nächste Prüfung 11.02.2027**: Muster gegen das jüngste Blatt halten, Schrift-Stapel prüfen,
`references/din.md` gegen die Normen lesen. Die Blöcke WERKZEUG, BLATT und BUNT in Vorlage und Beispiel bunt sind
gleich (Prüfbefehl in `QUELLEN.md`).
