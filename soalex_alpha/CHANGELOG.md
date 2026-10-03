# Changelog — Soalex Add-on

Dieses Changelog betrifft nur das HA-Add-on-Artefakt (Container + Manifest).
Repo-weites Changelog: `/CHANGELOG.md`.

## 0.1.187.142

_Alpha vom 03.10.2026 · 703e4b2 · enthält alles seit Beta 0.1.186_

### Für die nächste Beta beschrieben

#### Behoben

- **Beim Pausieren fuhr Soalex manche Akkus kurz in die Gegenrichtung.** Bei Akkus mit einem einzigen Sollwert, dessen Vorzeichen umgekehrt gezählt wird (z. B. Hoymiles MS-A2), und bei Akkus mit Modus-Umschalter (z. B. SolakonONE) las das Herunterfahren den aktuellen Wert falsch: Ein ladender Akku bekam für eine Sekunde einen Entlade-Befehl, bevor er auf 0 W ging — bei jeder Pause, auch bei der automatischen. Das Herunterfahren liest den Sollwert jetzt für alle Akku-Typen richtig herum und geht nur noch in Richtung 0.
- **Ein falsch gewählter Akku-Sensor löste Pausen am laufenden Band aus.** War als Akku-Leistungssensor in Wahrheit der Stromzähler unter anderem Namen gewählt, sah Soalex beim Laden „der Akku nimmt nichts auf“ und pausierte dreimal in einer halben Stunde. Soalex erkennt jetzt auch einen Sensor, der Wert für Wert die Zählerwerte liefert, und sagt das statt zu pausieren. Außerdem hebt ein einzelner Messausreißer die Erkennung „dieser Sensor sieht nur eine Richtung“ nicht mehr auf.
- **Ein Akku an seiner eigenen Entladegrenze bekam stundenlang Leistung zugeteilt.** Stellt der Akku selbst unterhalb eines Ladestands ab (z. B. Marstek bei 13 %, während in Soalex 10 % eingestellt sind), schickte Soalex ihm bis zu zwölf Stunden lang den Entlade-Befehl, und die übrigen Akkus sprangen nicht ein. Liefert ein Akku nahe seiner Grenze drei Minuten lang nichts, gibt Soalex die Leistung jetzt an die anderen Akkus und probiert ihn später wieder.

- **Nach einem Neustart wusste Soalex nicht mehr, was dein Akku gerade tut.** Wird das Add-on neu gestartet (Update, Home-Assistant-Neustart, Host unter Speicherdruck), hält der Akku seinen letzten Befehl, Soalex ging aber von 0 W aus. Solange der Zähler dadurch ruhig blieb, schrieb Soalex nichts mehr — in einer gemessenen Nacht 2,5 Stunden lang, während der Akku unbemerkt weiter 556 W lieferte; der erste neue Befehl sprang dann vom falschen Nullpunkt aus. Soalex liest den tatsächlichen Sollwert jetzt beim Start von der Hardware zurück (für alle Akku-Typen, bisher nur für Ausgangs-gesteuerte Wechselrichter) und frischt ihn wie gewohnt auf.
- **Akku-Sensor-Warnung „sieht aus wie ein PV-Strang“ traf Anker- und Zendure-Sensoren zu Unrecht.** Ein Sensor wie `solarbank_akkuleistung` wurde wegen des Wortteils „solar“ verdächtigt und aus dem automatischen Vorschlag gestrichen. Produktnamen werden jetzt vor der Prüfung ausgeblendet.
- **Während das Auto lud, hielt Soalex deinen PV-Wechselrichter auf 0 W.** Die Wallbox-Sperre („Akku nicht entladen, solange das Auto lädt“) galt auch für einen reinen PV-Wechselrichter ohne Akku — dessen „Entladen“ ist aber seine Solar-Einspeisung. Genau in der Zeit, in der die Sonne das Auto hätte laden können, blieb sie ungenutzt, und das Auto zog den Strom aus dem Netz. Die Sperre gilt jetzt nur noch für Akkus (auch für einen Akku hinter einem Wechselrichter); dein PV-Wechselrichter speist weiter ein. Die Zeile „Wallbox lädt — dein Akku gibt gerade keinen Strom ab“ erscheint nur noch, wenn wirklich ein Akku zurückgehalten wird.


#### Verbessert — Akku-Sensor richtig wählen

- **Der Funktionstest prüft jetzt auch deinen Akku-Leistungssensor.** Bisher hieß „bestanden“ nur, dass der Akku den Befehl angenommen hat. Jetzt steht für den gewählten Sensor eine eigene Zeile da: folgt er dem Befehl, bewegt er sich gar nicht, misst er nur eine Richtung — oder zeigt er dieselben Werte wie dein Stromzähler. Bei einem Befund führt „Leistungssensor ändern“ direkt zum Feld, und der Akku-Sensor ist als eigene Linie im Test-Diagramm zu sehen.
- **Zuerst der Stromzähler.** Beim ersten Einrichten wählst du den Stromzähler jetzt vor den Akku-Feldern — an ihm prüft Soalex alles andere.
- **Soalex rät keinen Akku-Sensor mehr.** Vorgeschlagen wird nur noch ein Sensor desselben Geräts. Bei Zendure schlägt Soalex keinen Sensor vor, der nur Laden oder nur Entladen zeigt; gibt es keinen gemeinsamen, verweist der Wizard auf die Anleitung, wie du in drei Minuten einen anlegst.
- **Hinweis, wenn der Akku-Sensor wie der Stromzähler aussieht** — schon beim Auswählen, und auf der Startseite führt „Leistungssensor ändern“ jetzt direkt zum Sensor deines Akkus statt zur Diagnose.
- **Als Stellwert tauchen keine Hilfswerte mit fremder Einheit mehr auf** (z. B. ein Strompreis in ct/kWh).

### Neu

- Geräte-Zeile zeigt Sonne und Abgabe ins Hausnetz bei PV-Hybrid-Akkus (live)
- Live-Screen — Geräte-Zeilen, Hero-Sätze, Akku-springt-ein, Heute-Satz, Anlass-Zeile (14.6)
- Sonne vor Akku – WR mit Solar-Prognose liefert zuerst (14.8)
- Zwei-Schritte-Upload „Feedback an Alex" im Diagnose-Export (feedback)
- Solar-Prognose-Sensor pro Wechselrichter — Auswahl, Vorschlag, Abo (14.5b)
- Profi-Einstellungen schon beim Anlegen eines Überschuss-Geräts (14.4)
- Kaskade schaltet N Geräte — Rest-Bilanz, Freigabe, Probe, Autorschaft (14.5)
- Überschuss-Geräte einrichten — Liste, Kacheln, Reihenfolge, Freigabe-Regel (14.4)

### Behoben

- Lade-Serie auch bei unlesbarem Sensor, unterdrückter Bewertung und Modus-Wechsel beenden (controller)
- Lade-Serie endet mit dem Ladebefehl und an jedem Lebenszyklus-Reset (controller)
- Idle-Mode über armierter Number gilt nicht als Ruhewert (pause)
- Einseitigkeit nur per Lade-Serie aufheben + Recovery-Richtung je Gerät (controller)
- Ramp-Down fährt nie in die Gegenrichtung (signed_setpoint invertiert, mode_switch_single) (pause)
- bestätigt stummer Zähler nimmt den Akku auf 0 W zurück (BUG-0156) (regelung)
- VACUUM-Deckel bricht den Export-Snapshot wirklich ab (BUG-0157) (diag)
- Review-Nachtrag + KISS-Rückbau — Deckel/Echo-Fenster/Rücksprung als einfache Regeln, „nur Entladen" nach Neustart und im Funktionstest (welle-2b)
- Geräte-Grenzen — kappen statt ablehnen, Deckel ≠ Fremdsteuerung, gelerntes Echo-Fenster, „nur Entladen", Rücksprung-Erkennung (BUG-0120/0126/0127/0151/0152) (welle-2b)
- Sensor-Wahrheit — E3 nur mit SoC-Beleg, Sensor==Smart Meter, SoC-Trend-Guard, Evidenz restart-fest, Zählerkadenz (BUG-0145/0132/0092/0133/0138) (welle-2c)
- Review 2026-09-30 — Gleichwert-Auffrischung nur bei gleicher Richtung ohne Pre-Flight-Änderung + field_check (welle-2a)
- Review 2026-09-30 — Testsperre bis Restore-Ende, frische 0 als Beleg, Solakon-Timeout nur mit Registry (welle-1)
- Bugfix-Welle 1 (0.1.187) — Solakon, Tests, Live-Texte, Zähler, DB, Betrieb (welle-1)
- Chart-Hinweis sagt beim Laden „nimmt erst … auf“ statt „liefert noch“ (anzeige)
- Halte-Stunden zählen nur abgedeckte Zeit, nicht die Spanne (I5) (anzeige)
- BUG-0104 Entscheidungen 1+3 — Hero bei stummem Akku-Sensor, Audit-Row für eingefrorene Messwerte, Richtungs-Verb im Drill-down (anzeige)
- Gleichwert-Auffrischung gegen ruhigen Sensor gilt als bestaetigt (I4) (readback)
- BUG-0104 — Befehl gilt nicht als Lieferung, wenn der Akku-Sensor keinen Wert liefert (anzeige)
- Dev-Review 2026-09-29 — PV-WR-Schlaf-Grace, passive_soc im Akku-leer-Hero, Stop-Log-Guard, 0-h-Bilanz, Höchst-Ladestand (review)
- „h auf null gehalten" an die beobachtete Spanne binden statt × 24 (anzeige)
- schlafender PV-WR mit unavailable-Sensor bekommt keine Zuteilung (allocator)
- Gegenrichtungs-0 im Pre-Flight nachvollziehbar loggen (executor)
- PV-WR ist kein Akku, leere Akkus auch in MULTI, Ladestand statt SoC (hero)
- PV-WR-Echo-Lag zählt nicht als failed-Write (Liefer-Signal b) (controller)
- Review 2026-09-26 — 12 Befunde aus den review-Stories (Port auf main) (review)
- Wallbox-Entladesperre sperrt nur Akkus, reiner PV-WR speist weiter ein (BUG-0116) (8.25)
- BUG-0115 — Cold-Start-Seed für alle vier Akku-Topologien (controller)
- Zendure acMode statt gridOffMode als Modus-Select vorschlagen (wizard)
- keine Probe im Nur-Zähler-Modus + Story 14.6 ready-for-dev + Livestream-Fragen (14.5)
- Solarbank-/SolarFlow-Sensoren nicht mehr als PV-Strang warnen (BUG-0114) (wizard)

### Verbessert

- Halte-Stunden-Abfrage sortiert nur gewertete Zyklen in Minuten-Buckets (diagnose)

Frühere Versionen: https://github.com/thealkly/SoalexBeta/blob/main/addon/CHANGELOG.md
