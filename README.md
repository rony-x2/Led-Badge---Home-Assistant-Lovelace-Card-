# LED-Badge Dashboard-Karte

Eine Lovelace-Karte zum direkten Eintippen von Text + Icon-Auswahl, ohne dass du jedes Mal den Aktionsaufruf bauen musst.

Voraussetzung ist die Custom Integration [LED Name Badge (LSLED)](https://github.com/rony-x2/Led-Badge-44x11---Home-Assistant), die die Aktion `led_badge.send` bereitstellt, sowie Home Assistant 2024.8 oder neuer.

## Was du bekommst

Eine Karte im Dashboard mit:
- Textfeld für den Inhalt
- Icon-Dropdown (alle 13 Built-in-Icons + "keins")
- Position des Icons: vorne oder hinten am Text
- Modus: scrollen (gut für lange Texte) oder statisch
- Geschwindigkeit (1–8) und Helligkeit (25/50/75/100 %) als Slider
- Blink-Toggle
- "Senden"-Button

Werte bleiben über Neustarts erhalten – du tippst also einmal Name + Icon ein, drückst Knopf, Knopf am Badge, klickst Senden, fertig.

Ist weder Text noch Icon gesetzt, sendet das Skript nichts. Beim allerersten Start stehen Geschwindigkeit und Helligkeit auf dem kleinsten Wert – einmal einstellen, danach merkt sich Home Assistant die Werte.

## Installation

### 1. Packages-Mechanismus aktivieren (einmalig)

Falls in deiner `/config/configuration.yaml` noch nicht vorhanden:

```yaml
homeassistant:
  packages: !include_dir_named packages
```

### 2. Package-Datei ablegen

`led_badge.yaml` nach **`/config/packages/led_badge.yaml`** kopieren. (Verzeichnis ggf. anlegen.)

Diese Datei enthält alle Helper-Variablen + das Send-Skript in einer Datei. Nichts muss in der UI angeklickt werden.

### 3. HA neustarten

Einmal komplett – beim ersten Mal wegen der Packages-Direktive. Spätere Änderungen kannst du mit "YAML neu laden → Eingabe-Helfer" und "→ Skripts" einspielen, ohne Neustart.

### 4. Karte ins Dashboard

Im Dashboard:
- Drei Punkte oben rechts → **Dashboard bearbeiten**
- **Karte hinzufügen** → ganz unten **Manuell**
- Inhalt von `lovelace_card.yaml` einfügen
- **Speichern**

Fertig. Bedienung dann: Werte einstellen → Knopf, Knopf am Badge → Senden klicken.

## Eigene Icons hinzufügen

Wenn du PNGs in `/config/led_badge_icons/` ablegst, sind die zwar in der Integration verfügbar, **erscheinen aber nicht automatisch im Dropdown**. HA kann für `input_select`-Optionen keine Verzeichnisse zur Laufzeit auslesen.

Lösung: in `led_badge.yaml` unter `input_select.led_badge_icon.options` den Namen ergänzen, "YAML neu laden → Eingabe-Helfer", fertig.

## Wenn du mehr Modes willst

Die UI bietet bewusst nur `scrollen` und `statisch`. Falls du auch `up`, `down`, `anim`, `drop`, `curtain`, `laser` brauchst:

In `led_badge.yaml` unter `input_select.led_badge_mode.options` ergänzen, und im Skript-Template `mode_value` die Übersetzung erweitern:

```yaml
mode_value: >-
  {%- if mode_label == 'scrollen' -%}left
  {%- elif mode_label == 'statisch' -%}fixed
  {%- elif mode_label == 'hoch' -%}up
  {%- elif mode_label == 'runter' -%}down
  {%- elif mode_label == 'animation' -%}anim
  {%- elif mode_label == 'drop' -%}drop
  {%- elif mode_label == 'curtain' -%}curtain
  {%- elif mode_label == 'laser' -%}laser
  {%- endif -%}
```

## Mehrere Nachrichten gleichzeitig

Die Karte ist auf eine Nachricht ausgelegt – das deckt die meisten Fälle ab. Wenn du mehrere Slots gleichzeitig nutzen willst (z. B. abwechselnd Name + WLAN), bau dir ein zweites Skript, das fest verdrahtete `messages:` an die Aktion schickt, wie im [README der Integration](https://github.com/rony-x2/Led-Badge-44x11---Home-Assistant#beispiel-name-und-wlan-zugang-anzeigen) beschrieben. Die Karte hier macht keinen Sinn dafür, da würden ihr UI-Elemente wachsen wie ein Tannenbaum.

## Lizenz

GPL-3.0 – siehe [LICENSE](LICENSE). © 2026 Dennis Deutschkämer
