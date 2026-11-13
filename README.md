# birnenkern

**English** · [Deutsch](README.de.md)

![Example sheet: an invented end-to-end test of a city library's lending system](docs/beispiel-probe.png)

![License MIT](https://img.shields.io/badge/License-MIT-111?style=flat-square)
![Claude Code Skill](https://img.shields.io/badge/Claude_Code-Skill-111?style=flat-square)
![Browser only](https://img.shields.io/badge/Runs_in-a_browser-111?style=flat-square)
![Dependencies 0](https://img.shields.io/badge/Dependencies-0-111?style=flat-square)

**Birne is a Claude Code skill that draws.** It turns a subject into a technical sheet after DIN:
ink on white, a frame with zones and centring marks, a small title block bottom right, line types
instead of colour, lettering in DIN 1451, square corners with slightly overdrawn edges, justified text.

| Building block | Shows |
|---|---|
| **Plan view** | how something is built, with section line A–A where a path matters |
| **Section** | the path a request or a step takes, end to end |
| **Detail** | one spot, enlarged |
| **Exploded view** | layers that sit on top of each other |
| **Timeline** | a day or a project on a fixed scale, faults hatched |
| **Tables** | steps, findings with tickets, figures, sources |

Every number on the sheet has a source. Roles instead of names. No invented dimensions.

Birne speaks German. Sheets and commands are in German.

## Install

```text
/plugin marketplace add rdo2hellowelt/birnenkern
/plugin install birne@birnenkern
```

Then type `birne` and say what goes on the sheet and where the material comes from. The sheet lands as
`birne-<topic>-<date>.html` in the working folder and opens in the browser.

## Birne and Apfel

[Apfel](https://github.com/rdo2hellowelt/apfelkern) reviews work dialogs and draws its findings on the
same sheet. The Apfel plugin carries a copy of Birne, so installing Apfel is enough for both. Birne is
changed here only; the copy in Apfel is synced from this repo.

## Credits

The drawing toolkit follows [dimensional-drawing](https://github.com/enesozturk/dimensional-drawing)
by Enes Ozturk (MIT). Details in [`skills/birne/QUELLEN.md`](skills/birne/QUELLEN.md).

## License

MIT, see [LICENSE](LICENSE).
