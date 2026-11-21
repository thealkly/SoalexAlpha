# Changelog — Soalex Add-on

Dieses Changelog betrifft nur das HA-Add-on-Artefakt (Container + Manifest).
Repo-weites Changelog: `/CHANGELOG.md`.

## 0.1.191.216

_Alpha vom 21.11.2026 · 97777b8 · enthält alles seit Beta 0.1.190_

### Für die nächste Beta beschrieben

#### Verbessert

- **„Günstig laden“ läuft jetzt auch ohne Solaranlage.** Ist bei allen deinen Akkus (und Wechselrichtern) „Keine eigenen Module an diesem Gerät“ angehakt und nirgends eine Solar-Prognose, ein Solar-Eingang oder eine „Dach-PV ohne Soalex“ eingetragen, rechnet Soalex mit 0 kWh Sonne und plant das Laden nur nach Preis und Verbrauch, über alle bekannten Preise (höchstens 48 Stunden). Bisher blieb „Günstig laden“ dann mit „Prognose fehlt“ stehen. Der Haken heißt jetzt „Keine Solaranlage eingetragen — Soalex rechnet ohne Sonne.“ **Das gilt sofort auch für bestehende Einrichtungen:** Hast du doch eine Solaranlage, die Soalex nicht kennt, trag ihre Prognose unter Einstellungen → Anlage ein — sonst rechnet Soalex ohne Sonne und lädt mehr aus dem Netz als nötig. → [Ohne Solaranlage](https://soalex.de/funktionen/guenstig-laden/#ohne-solaranlage)
- **Ist dein Akku leer und keine Solaranlage eingetragen, steht auf der Startseite „Akku ist leer — Soalex entlädt ihn nicht weiter“ statt „… wartet auf Sonne“** (mit mehreren Akkus „Deine Akkus sind leer — Soalex entlädt sie nicht weiter“). Ist eine Preisquelle gewählt und „Günstig laden“ aus, sagt die Zeile darunter „„Günstig laden“ ist aus.“; fehlt „Günstig laden“ noch etwas, nennt sie den ersten offenen Haken. Mit Solaranlage bleibt der Satz wie bisher. → [Akku leer](https://soalex.de/hilfe/status/#akku-leer)

#### Behoben

- **Tippst du auf „Sofort“, nennt die Geräte-Zeile den richtigen Grund fürs Umschalten auf drei Phasen.** Bisher stand dort „Seit 5 min sind mehr als … übrig“, obwohl nicht die Sonne, sondern deine Wahl den Wechsel ausgelöst hat. Jetzt steht „Du hast „Sofort“ gewählt, dafür lädt dein Auto auf drei Phasen.“, bei „Günstig“ entsprechend „Jetzt ist eine günstige Zeit“. Der nächste Satz sagt, wie es weitergeht („Gleich lädt dein Auto mit 6 A auf drei Phasen weiter, danach mit 16 A.“), und in den letzten Schritten steht der Grund statt einer Watt-Zahl. Lädt dein Auto unter „Sofort“ noch nicht mit voller Leistung, kündigt die Zeile an, was Soalex gleich tut. Am Schalten ändert sich nichts.
- **Bei „Sonne + Netz“ sagt der Satz unter den Tasten, wenn dein Auto gerade auf drei Phasen lädt.** Bisher nannte er nur die kleinste Stufe auf einer Phase, auch wenn die Wallbox auf drei Phasen lief oder dort starten würde. Jetzt steht dort zum Beispiel „Dein Auto lädt immer mit mindestens 6 A, im Moment auf drei Phasen.“
- **Wartet „Günstig“ auf die günstige Zeit, steht in der Geräte-Zeile „wartet“ statt „Akku zuerst“.** Die drei Sätze darunter nannten schon die günstige Zeit, das Wort in der Zeile widersprach ihnen.
- **Marstek Venus: Die Geräte-Obergrenzen mit englischem Namen (`…_max_charge_power`, `…_max_discharge_power`) schlägt die Einrichtung nicht mehr als Stellwert vor.** Bisher kannte Soalex nur die deutschen Namen („Maximale Ladeleistung“, „Maximale Entladeleistung“). War die englische Lade-Obergrenze als Entlade-Stellwert eingetragen, stellte Soalex sie bei jedem Ladebefehl auf 0 W, und dein Akku lud nicht mehr. Die Einrichtung schlägt beide Obergrenzen jetzt in beiden Sprachen nicht mehr vor, weder für Laden noch für Entladen. Ist eine davon bei dir schon eingetragen, steht auf der Gerätekarte unter Einstellungen → Anlage → Anschluss ein Hinweis mit dem Knopf „Anschluss ändern“. Steht deine Lade-Obergrenze dadurch auf 0 W, stell sie in Home Assistant wieder auf ihren alten Wert — das macht Soalex nicht selbst.
- **„Sofort“, „Sonne + Netz“ und „Günstig“ gelten jetzt auch, wenn Soalex einen Messwert nicht lesen kann.** Fehlte der Wert deines Smart Meters oder die Leistung deines Akkus, startete ein Gerät mit dieser Lade-Wahl bisher nicht, und ein laufendes schaltete nach kurzer Zeit aus. Jetzt lädt „Sofort“ voll, „Sonne + Netz“ hält die kleinste Stufe und „Günstig“ lädt in der geplanten Viertelstunde voll, auch beim Start. Lief das Gerät mit Sonne höher, stellt Soalex es nach gut einer Minute ohne Wert auf die Stufe der Lade-Wahl zurück. „Nur Sonne“ wartet wie bisher. Solange ein Gerät so läuft und der Wert fehlt, gibt dein Akku nichts dazu, weil Soalex den Netz-Anteil nicht messen kann. Die Geräte-Zeile sagt jetzt, welcher Wert fehlt: „Dein Smart Meter liefert gerade keinen Wert.“ oder „Soalex kann die Leistung deines Akkus gerade nicht lesen.“
- **Tippst du auf eine andere Lade-Wahl, stehen nicht mehr bis zu einer halben Minute die Sätze der alten Wahl da.** Bis Soalex mit der neuen Wahl entschieden hat (höchstens etwa 30 Sekunden), steht in der Geräte-Zeile „stellt um“ und darunter „Soalex stellt um.“ / „Du hast gerade „Günstig“ gewählt.“ / „Gleich steht hier, was Soalex als Nächstes tut.“ Ist die Steuerung pausiert, die Verbindung zu Home Assistant weg, das Gerät bei „Macht mit“ aus oder fehlt gerade ein Messwert, steht dort kein „stellt um“, sondern wie bisher, was die Zeile zu diesem Zustand sagt. Bei „Günstig“ sind „Fertig bis“ und „Ungefähr laden“ (wie bisher nur ohne gültigen Ladestand deines Autos) sofort mit deinen gespeicherten Werten da; die geplanten Zeiten kommen mit der nächsten Entscheidung. Am Schalten ändert sich nichts.
- **„Deine letzten 24 Stunden“ zählt jetzt alle Akkus.** Bisher standen dort nur die Zahlen des ersten Akkus: Mit zwei Akkus konnte „Fail-Safes: 0“ dastehen, obwohl der zweite in derselben Zeit viele hatte. Anpassungen und Fail-Safes sind jetzt die Summe über alle Akkus.
- **Ein Seitenwechsel beginnt wieder oben.** Ein Tipp auf „Diagnose“ unten auf der Startseite öffnete die Diagnose-Seite mitten im Inhalt, Reiter und Filter waren weggerollt.
- **Die Knöpfe in der Hinweis-Karte der Startseite („Einrichtung prüfen“, „Zur Diagnose“) sind auf dem Telefon groß genug zum Treffen.** Sie waren nur eine Textzeile hoch.
- **Texte berichtigt.** Der Rat zu einer automatischen Pause nannte einen „Resume-Button im Live-Screen“, den es nicht gibt; jetzt steht dort, was du auf der Startseite wirklich tippst. Der Satz zur Verteilung auf mehrere Akkus sagt bei zwei Akkus „hilft der andere“. Ein Akku-Name in den Sätzen der Startseite schließt mit dem richtigen Anführungszeichen.
- **Läuft ein Gerät mit „Sofort“, „Sonne + Netz“ oder „Günstig“, steht auf der Startseite nicht mehr „Dein Akku müsste decken, tut es aber nicht“.** In dieser Zeit gibt dein Akku mit Absicht nichts ab — Soalex hält ihn zurück. Der Satz beschuldigte den Akku für etwas, das Soalex selbst angeordnet hat.
- **„Sofort“: „Die Sonne reicht gerade dafür.“ steht nur noch da, wenn wirklich Sonnenstrom ins Gerät fließt.** Der Satz stand auch nachts da, solange das Auto noch nichts nahm.
- **„Ja, alles löschen“ beim Zurücksetzen ist auf dem Telefon nicht mehr abgeschnitten.**

### Neu

- „Günstig laden“ ohne Solaranlage, Lade-Wahl ohne Messwert, Sätze nach Wahl-Wechsel
- guide system check with real screenshots (website)
- add device compatibility and setup guide (website)

### Behoben

- Funde aus dem UX-Test – Startseite, Sätze, Tippziele (ui)
- Marstek-Obergrenzen nicht mehr als Lade-/Entladeleistung vorschlagen (setup)
- Sätze um Phasen-Wechsel und Lade-Wahl (S2, N1, N3) (epic-17)
- explain charge tests directly in Home Assistant (website)

Frühere Versionen: https://github.com/thealkly/SoalexBeta/blob/main/addon/CHANGELOG.md
