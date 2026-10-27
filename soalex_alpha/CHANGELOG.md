# Changelog — Soalex Add-on

Dieses Changelog betrifft nur das HA-Add-on-Artefakt (Container + Manifest).
Repo-weites Changelog: `/CHANGELOG.md`.

## 0.1.189.186

_Alpha vom 27.10.2026 · 04438e8 · enthält alles seit Beta 0.1.188_

### Neu

- Forensik mit Claude Code auf der Dev-VM — Auftrag, Sandbox + Werkzeug-Wache, Ausgabe-Schranke, Drei-Regeln-Prüfer, Rückweg unter forget-Sperre (4.28)
- Bilanz aus Messwerten — Akku-Strom statt Netz in kWh und Euro (5.30)
- Betrieb — ingest --new, Router + Fall-Status, Tages-Digest, Sofort-Mail, Cron-Kette, forget-Sperrliste (4.24)
- Soalex legt den Akku-Sensor aus zwei einseitigen Werten an (16.15)
- zeigt, wessen Reaktionsstärke bei mehreren Akkus gilt (16.14 G7) (verhalten)
- Fortschritt während des Tests — erledigt / läuft / kommt noch (funktionstest)

### Behoben

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
