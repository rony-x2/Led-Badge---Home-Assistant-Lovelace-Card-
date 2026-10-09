# Changelog

Alle nennenswerten Änderungen an diesem Projekt. Das Format folgt
[Keep a Changelog](https://keepachangelog.com/de/1.1.0/), die Versionen
[Semantic Versioning](https://semver.org/lang/de/).

## [1.1.0] – 2026-10-09

### Behoben
- Eingaben bleiben jetzt wirklich über Neustarts erhalten: die
  `initial:`-Werte haben die Helfer bei jedem Neustart zurückgesetzt.
- Beim allerersten Start wurde „unknown“ als Text an das Badge geschickt,
  weil der Text-Helfer noch keinen Wert hatte.

### Geändert
- Das Skript sendet nichts, wenn weder Text noch Icon gesetzt ist.
- Aktuelle Schreibweise `action:` statt `service:` (benötigt Home Assistant
  2024.8 oder neuer).
- Der Senden-Button ist jetzt eine Skript-Zeile mit `action_name` statt der
  Sonderzeile `call-service`.
- README: Link zur Integration, Versionshinweis, Lizenzangabe.

### Hinzugefügt
- Lizenz: GPL-3.0 (wie die zugehörige Integration).

## [1.0.0] – 2026-05-04

- Erste Veröffentlichung.

[1.1.0]: https://github.com/rony-x2/Led-Badge---Home-Assistant-Lovelace-Card-/compare/1.0.0...1.1.0
[1.0.0]: https://github.com/rony-x2/Led-Badge---Home-Assistant-Lovelace-Card-/releases/tag/1.0.0
