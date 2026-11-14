# Changelog — Soalex Add-on

Dieses Changelog betrifft nur das HA-Add-on-Artefakt (Container + Manifest).
Repo-weites Changelog: `/CHANGELOG.md`.

## 0.1.189.203

_Alpha vom 14.11.2026 · 97e15a1 · enthält alles seit Beta 0.1.188_

### Neu

- Dunkler Modus folgt dem Home-Assistant-Theme (Systemfallback), Amendment 2026-11-13 (5.40)
- Manuell anpassen für jede Einheit, ein Wert für beide Richtungen, MS-A2 nach Umbenennen, Kombi abgeschlossen (16.22)
- Akku aus Ladegerät + Wechselrichter, „Manuell einrichten", Rückmeldung per Betrag am Akku-Sensor (16.22)
- unter dem Hero höchstens eine Handlungskarte, Heute mit Uhrzeiten, Anlage entkernt (Story 5.38) (live)
- Sonnenbogen, Marke „ab hier teurer“ und gemeinsamer Ladestand (Story 5.37) (live)
- Bühne mit Horizont, Tagesspur, Akku-Spur und großem Akku (Story 5.36) (live)
- Sprungantwort je Akku im Diagnose-Paket (Story 4.31) (diagnostics)
- Umlade-Ausstieg sichtbar — Verlaufs-Zeile und Live-Zeile mit Grund und Rest-Haltezeit (Story 15.23) (live)
- Story 4.30 — Wiederholung als +1 am offenen Fall (fleet)
- Antwort-Entwürfe — Vorlagen je Lage, eindeutiger Empfänger, Gmail-Entwurf per IMAP APPEND, Gesendet-Scan, 90-Tage-Löschung auf der VM (4.25)
- Startseite zeigt Messung statt Sollwert, nennt das betroffene Gerät, Willkommenskarte nur mit Zahl (5.31)
- Forensik mit Claude Code auf der Dev-VM — Auftrag, Sandbox + Werkzeug-Wache, Ausgabe-Schranke, Drei-Regeln-Prüfer, Rückweg unter forget-Sperre (4.28)
- Bilanz aus Messwerten — Akku-Strom statt Netz in kWh und Euro (5.30)
- Betrieb — ingest --new, Router + Fall-Status, Tages-Digest, Sofort-Mail, Cron-Kette, forget-Sperrliste (4.24)
- Soalex legt den Akku-Sensor aus zwei einseitigen Werten an (16.15)
- zeigt, wessen Reaktionsstärke bei mehreren Akkus gilt (16.14 G7) (verhalten)
- Fortschritt während des Tests — erledigt / läuft / kommt noch (funktionstest)

### Behoben

- Mindest-Abgabe ist Ruhewert reiner Wechselrichter bei Pause, Stopp und Liefersperre (BUG-0168) (3.62)
- Steuerart zurücksetzbar, Akku-Sensor-Pflichtgrund folgt der Marke (einrichten)
- Pause fährt nur eigene Werte herunter, Fremdwert bleibt stehen (BUG-0245) (3.61)
- Funktionstest übergibt die Unit kalt an den Regler (BUG-0244, Story 3.60) (regelung)
- Lesehilfe, Läuft-Chip und Fußleiste bei 360 px mit 200 % Zoom (UI-Nachtest 12.11.) (live)
- Befunde aus dem UI-Test der Bühne (Alpha .195, 11.11.) (live)
- nicht erreichbarer Akku ist im Fach vorausgewählt und markiert (UI-Test 10.11. M8 auf der Bühne) (live)
- Live-Hinweise im each-Block mit Schlüssel (ESLint require-each-key) (5.35)
- Ladestunde nur nach ihren Nicht-Lade-Minuten beurteilen (BUG-0243, Codex R2) (4.32)
- Ladung entschuldigt nur Stunden ohne 20 Stillstandsminuten (BUG-0243, Codex R1) (4.32)
- Fallakte zählt geplantes Günstig laden je Pool, steigender Ladestand ist keine tote Nacht (BUG-0243) (4.32)
- Solakon-Ermittlung nur bei Wechsel und alle 300 s statt alle 10 s (BUG-0124, Codex R1) (5.35)
- BUG-0214 Wallbox-Rohzustände und Reserve bis 89 % absichern (Story 8.29) (settings)
- Vorzeichen-Save am Helfer übernimmt die Rückmeldungs-Bindung, Testdaten ohne Helfer-Stellwert (16.20)
- BUG-0241, BUG-0242, BUG-0067 und BUG-0114 beheben (Story 16.20) (einrichtung)
- Ratgeber-Einträge für die Sprungantwort-Logger-Schlüssel (4.31)
- Fremdwert-Übernahme, Liefersperre je Richtung mit Probe, Mindest-Abgabe, Ladestand-Sprung, Sperrgrund (BUG-0239, BUG-0169, BUG-0205, BUG-0240, BUG-0236) (regler)
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
