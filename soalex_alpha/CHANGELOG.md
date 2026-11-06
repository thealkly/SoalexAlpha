# Changelog — Soalex Add-on

Dieses Changelog betrifft nur das HA-Add-on-Artefakt (Container + Manifest).
Repo-weites Changelog: `/CHANGELOG.md`.

## 0.1.189.190

_Alpha vom 06.11.2026 · 40fc49d · enthält alles seit Beta 0.1.188_

### Für die nächste Beta beschrieben

#### Behoben — Einrichtung

- **Findet Soalex kein steuerbares Gerät, sagt die Einrichtung jetzt zuerst, dass der Akku in Home Assistant eingebunden sein muss.** Dazu steht in Zahlen, was Soalex gefunden hat, z. B. „1 Gerät, davon 0 steuerbar (dein Zähler ist dabei)".
- Der Funktionstest bricht nicht mehr nach 60 Sekunden ab, wenn Fernzugriff oder Proxy die Verbindung kappen: Soalex testet im Hintergrund weiter und die Seite holt das Ergebnis ab.

#### Behoben — Verhalten

- **Die Haus-Akku-Sperre endet jetzt nach spätestens 10 Minuten und zeigt sich im Live-Screen.** Hielt Soalex die Entladung oder das Laden wegen deines Haus-Akkus zurück, blieb die Sperre bisher stehen, solange der Haus-Akku immer wieder dazwischenregelte — ein Tester bezog so 24 Minuten 1–2 kW aus dem Netz bei 35–41 % im Akku. Jetzt steht unter dem Hero „Soalex hält die Entladung zurück, weil dein Haus-Akku zuletzt gleichzeitig geladen hat — seit 4 min, höchstens 10 min" samt Hinweis, das Vorzeichen des Haus-Akku-Sensors zu prüfen; nach 10 Minuten gibt Soalex frei und sperrt erst bei neuen Störungen wieder.
- **Quer-Laden gibt die volle Quelle frei, wenn das Haus trotz Sperre deutlich Strom bezieht.** Nach einem Rückschritt durfte die volle Quelle eine Weile nicht mehr abgeben, und diese Pause beendete das Umladen nie — ein Tester bezog 17 Minuten 1,4–2 kW aus dem Netz, während die Quelle bei 400 W stehen blieb. Jetzt steigt Soalex aus, wenn dein Haus während der Umlade-Pause anhaltend mehr als 160 W über deinem Netz-Sollwert aus dem Netz bezieht, und die normale Regelung übernimmt; ein kurzer Bezug nach einer Wolke unterbricht das Umladen nicht.
- **Ein verstummtes Gerät gilt nicht mehr als Fremdsystem, und sein alter Ladestand nicht mehr als gültig.** Lieferte die Integration deines Akkus keine Werte mehr, meldete Soalex „ein anderes System steuert deinen Akku" und fuhr mit dem eingefrorenen Ladestand bis zu 12 Stunden weiter — zwei Nächte ohne Entladung bei einem Tester. Jetzt zählt ein Befehl ohne Antwort als unbestätigt, und meldet sich das Gerät auf keiner Entity mehr als 6 Stunden, obwohl Soalex ihm neue Werte geschickt hat, behandelt Soalex den Ladestand als fehlend und probiert es jede halbe Stunde neu. Sobald das Gerät wieder einen Wert liefert, läuft alles normal weiter.
- **Der Regelungs-Modus-Schalter unter Verhalten → Profi ist weg; Soalex wählt den Modus immer selbst.** Ein gespeicherter manueller Modus wird beim Start entfernt. Mit zwei oder mehr Akkus hatte ein manuell gesetzter Modus den zweiten Akku stillgelegt — er bekam keinen Befehl mehr und der Strom kam aus dem Netz.

#### Behoben — Live-Screen

- **Hört Soalex auf, Überschuss an deine anderen Akkus weiterzugeben, siehst du jetzt warum.** Unter dem Hero steht z. B. „Soalex gibt gerade nichts an deine anderen Akkus weiter: dein Haus hat mehr als 160 W über deinem Netz-Sollwert aus dem Netz bezogen — neuer Versuch in 8 min.", und im Verlauf eine Zeile wie „Weitergabe an anderen Akku beendet — dein Haus bezog 1450 W aus dem Netz".
- **Nimmt dein Akku bei bekanntem Ladestand keinen Ladestrom an, sagt Soalex das jetzt mit Zahl statt „vermutlich voll".** Hero „Dein Akku nimmt gerade keinen Ladestrom an — Ladestand 80 %" mit dem Hinweis auf Kälteschutz, Heizung oder eine Ladegrenze im Gerät. „Vermutlich voll" bleibt nur, wenn der Ladestand nahe der Obergrenze liegt oder Ladestand bzw. Obergrenze unbekannt sind.
- **Meldet dein Akku seit Stunden keinen Ladestand mehr, nennt Soalex die Dauer und bei mehreren Akkus das betroffene Gerät.** Die Diagnose zeigt das Alter des letzten Werts und markiert veraltete Werte sichtbar.
- **Fällt dein Akku ohne Soalex-Entladung unter deine Untergrenze, erklärt die Akku-Zeile die Selbstentladung.** Soalex zeigt dabei deine eingestellte Untergrenze, etwa „Soalex entlädt nicht unter 25 %“.

### Neu

- Umlade-Ausstieg sichtbar — Verlaufs-Zeile und Live-Zeile mit Grund und Rest-Haltezeit (Story 15.23) (live)
- Story 4.30 — Wiederholung als +1 am offenen Fall (fleet)
- Antwort-Entwürfe — Vorlagen je Lage, eindeutiger Empfänger, Gmail-Entwurf per IMAP APPEND, Gesendet-Scan, 90-Tage-Löschung auf der VM (4.25)
- Forensik mit Claude Code auf der Dev-VM — Auftrag, Sandbox + Werkzeug-Wache, Ausgabe-Schranke, Drei-Regeln-Prüfer, Rückweg unter forget-Sperre (4.28)
- Bilanz aus Messwerten — Akku-Strom statt Netz in kWh und Euro (5.30)
- Betrieb — ingest --new, Router + Fall-Status, Tages-Digest, Sofort-Mail, Cron-Kette, forget-Sperrliste (4.24)
- Soalex legt den Akku-Sensor aus zwei einseitigen Werten an (16.15)
- zeigt, wessen Reaktionsstärke bei mehreren Akkus gilt (16.14 G7) (verhalten)
- Fortschritt während des Tests — erledigt / läuft / kommt noch (funktionstest)

### Behoben

- Haus-Akku-Eskalation max. 10 min, Quer-Lade-Ausstieg bei Bezug > Soll + 160 W, stummes Gerät kein Fremdsystem (BUG-0232, BUG-0234, BUG-0235) (regelung)
- verstummtes Gerät mit Stunden im Hero, Alter in der Diagnose, Selbstentladung an der Akku-Kachel (BUG-0235, BUG-0237) (5.33)
- Funktionstest als Hintergrund-Job mit Polling — kein 60-s-Abbruch über Proxy/Fernzugriff mehr (BUG-0230) (16.19)
- BUG-0231 Lade-Hero mit Ladestand statt „vermutlich voll", BUG-0236 als Klasse-A-Folge (Story 5.32) (api)
- Regelungs-Modus-Schalter entfernt, Legacy-Modus beim Start gelöscht (Story 8.28, BUG-0229) (verhalten)
- BUG-0238 — Einrichtung nennt zuerst „Akku gar nicht in Home Assistant" und zählt, was Soalex fand (Story 16.17) (ui)
- Codex R2 — Anhalten folgt dem Zähler (kein Gate-Durchschlupf nach Zähler-Wechsel), Ausfall-Name auch bei einem Akku (16.18)
- Codex R1 — gemessener Widerspruch übersteht Sensor-Tausch, nicht prüfbares Bein folgt dem Solar-Eingang (16.18)
- Alpha-189-Befunde — Prüfpunkte je Punkt (N1), Startseiten-Banner (N2), Akku-Sensor mit unruhigem Bein (N4), Hilfssensor-Texte (N5–N9), Welcome-Card (N10), Website-Szenen (16.18)
- Zahlenprüfung kennt Setup/Konfig-Belege, Vorlage nennt erlaubte Zahlen, TID löst Kontakt-Schranke nicht aus (4.28)
- Kontakt-Prüfung der Paketkopie wertweise statt Rohbytes (Fehlalarm), generierte Spalten, sqlite_stat, Unicode-Schnellpfad (4.28)
- Codex R2 — Wechselrichter-Ausgang getrennt im Ledger (Migration 025), Bilanz zählt nur Akku-Strom (5.30)
- Codex R2 — voller Tag je lokaler Tageslänge, „keine Entladung gemessen“ statt „nichts abgegeben“ mit Abdeckung (5.30)
- Codex R1 — Migration wiederanlauf-fest, Ratgeber-Eintrag, Preis-Stempel schließt jede Transaktion und verliert nichts beim Commit-Fehler, kein veralteter Kurvenpreis, 23-h-Tag reicht, kein Euro ohne Entladung (5.30)
- Codex R2 — Lock des richtigen Paars, abgeschirmtes Flow-Aufräumen, Reparatur ohne Verlauf, Neu suchen am Cache vorbei (16.15)
- Codex R1 — kein zweiter Helfer neben ausgeschaltetem/unlesbarem, nur kanonische Formel ist eigen, Lock je Paar mit Frist, Reparatur-Angebot, Zeilenteil auf der Anlage-Karte (16.15)
- Codex R4 — Umlade-Quelle im Spiegel ausgelassen, PV-Wechselrichter heißen „Geräte“ (16.14 G7)
- svelte-check — Null-Eingrenzung in der Zuletzt-Zeile (16.14)
- Codex R2 — gestauter Ladestand zählt nicht als lebend, Doppel-Guard auf alle Steuer-Entities und den Rebind, Sammelzeile folgt dem Pass (16.14)
- Hauslast nicht mehr als Solar-Eingang der lokalen Anker-Integration (16.14 G4) (profil)
- Akku-Zeilen tragen den HA-Gerätenamen statt wandernder Nummer (16.14 G2) (verhalten)
- „Läuft seit“ zählt ab dem letzten Fortsetzen (16.14 G1) (live)
- Codex R1 — Seriennummer mit HA-Zähler, MS-A2 bleibt steuerbar, Guard in der Transaktion, ehrlicher Nebensatz (16.14)
- Pause-Zeile nennt Gerät und Rolle statt Entity-ID (16.14 M5) (live)
- Pass trägt den Gerätenamen aus HA, nicht „deinem Gerät“ (16.14 G3) (anschluss)
- Start-Hinweis nennt alle Geräte mit offenem Hinweis (16.14 A1) (live)
- nicht erreichbares Gerät sagt es, statt „wartet“ (16.14 M4) (anlage)
- Sensor ohne Vorzeichen heißt nicht mehr „Spiegelbild“ (16.14 M2) (funktionstest)
- Ladestand korrigieren legt das Gerät nicht mehr neu an (16.14 M1) (anschluss)
- dasselbe Gerät über zwei Integrationen nur einmal steuerbar (16.14 H2) (einrichten)
- Ausfall eines Geräts sagt nicht mehr „die Steuerung wartet“ (16.14 H1) (hero)

Frühere Versionen: https://github.com/thealkly/SoalexBeta/blob/main/addon/CHANGELOG.md
